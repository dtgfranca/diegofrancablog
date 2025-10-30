---
title: "Construindo Rag Com Laravel"
date: 2025-10-29T21:44:10-03:00
draft: true
---

Venho estudando ultimamente sobre IA como fazer prompts mais eficientes, como construir um RAG, como fazer um finetunning de um modelo de IA. 
E para que eu possa fixar mais o meu conhecimento resolvir criar um  projeto com laravel onde eu posso fazer de uma forma prática. Ainda mais 
que hoje em dia está muito falado sobre IA e Machine Learning, mas não vejo muito conteúdo em português falando sobre RAG com php.

Meu objetivo com esse post é criar um RAG bem simples  onde eu possa mostrar detalhe por detalhe todo o processo de criaçao. Seria um post
inicial, mas que vai servir de base para posts futuros, pois esse rag eu quero evoluí-lo e a cada parte da melhoria quero deixar regisrado aqui no blog.

Então sem mais delongas, vamos iniciar!!!

## O que é RAG?
[//]: # (O que é RAG &#40;explicado de forma leve&#41;)
RAG(Retrieval-Augmented Generation), é uma técnica utilizada para poder aumentar a qualidade de um modelo de IA, com essa
técnica você pode deixar seu modelo mais atualizado e mais inteligente. Podemos falar que precisamos de usar um RAG é quando precisamos
de criar  sistemas para dentro de uma empresa e que precise de ler alguma documentação, como por exemplo, um sistema de suporte. Nesse caso se deixarmos que o modelo
acesse a web ele não irá encontrar as respostas corretas e vai gerar alucinações e inconsistências nessas respostas deixando o modelo com respostas que nao 
vai agradar o usuário. 



[//]: # (Por que fazer localmente &#40;privacidade, custo, aprendizado&#41;)
## Preparando o ambiente
[//]: # (Criar o projeto Laravel e instalar o pacote arda/ollama-php)
Para da sequencia ao nosso projeto vamos instalar o laravel e o arda-ollama-php.
````
    composer create-project laravel/laravel rag-laravel
    cd rag-laravel    
````
Depois que fizemos a instalação do laravel, vamos instllar o arda-ollama, esse pacote é uma bibiloteca para quepossamos acessar o ollama

````
composer require ardagnsrn/ollama-php

````
[//]: # (Instalar Ollama e rodar um modelo &#40;qwen2.5:1.5b&#41;)
Já que estamos com o laravel e o pacote devidamente instaladosl, vamos agora instalar o Ollama e rodar um modelo. Para esse 
exemplo eu estou usando  o modelo qwen2.5:1.5b, mais Ubuntu 22.04. Para quem está usando outro sistema operacional, sugiro
entrar no site do Ollama e verificar qual é a forma de instalar(https://ollama.com/download) o Ollama no seu sistema.

Após a instalaçao do ollama, vamos rodar o modelo. E para isso  vamos usar o comando para fazer um pull do modelo:
````
ollama pull qwen2.5:1.5b

````
A escolha desse modelo: qwen2.5:1.5b , foi devido a grande maioria das pessoas terem um computador não muito robusto e com esse modelo
vai rodar melhor em seu computador, mas em consequencia ele pode demorar um pouco mais para responder.

## Indexando os documentos
[//]: # (Lendo .md)
Agora com tudo praticamente configurado é hora de codar. Primeiro vamos ler os documentos que vamos usar no nosso RAG, 
depois iremos  criar embendings para cada um dos documentos e salvar no banco de dados.

Mas antes de  iniciar, vamos entender como funciona os embeddings e o porquê deles.
A tecnica do embedding é para que possamos passar de forma mais precisa dentro do nosso modelo, para que ele possa entender melhor o que 
estamos falando. Se passarmos por exemplo um livro muito grande para ele, pode ser que a informação seja tão grande e o modelo acabe gerando respostas 
diferentes do que era esperdo, então criamos para cada arquivo um embedding(também podemos criar chuncks para melhorar) e passamos esse embedding para o modelo.
Então na hora de trazer uma respostas para o usuario ele vai transformar a pergunta em um embedding e vai fazer um calculo de similaridade com os embeddings
do banco de dados e vai retornar as respostas mais parecidas.

Entre no diretório  do projeto e vamos criar um comando no laravel para poder  fazer o embending.
````
    php artisan create command embeding
````
Antes de começar a criar embending com ferramentas mais avançadas como qwen2.5:1.5b-embedding, é interessante
aprendermos os conceitos  de embending simples.
Para ilustrar isso, podemos criar uma função simples em php
````
    private function gerarEmbeddingSimples(string $texto): array
    {
        // Quebra o texto em palavras únicas e ordenadas
        $palavras = array_unique(str_word_count(strtolower($texto), 1));
        sort($palavras);
    
        // Cria um hash numérico simples (mock de embedding)
        return array_map(fn($p) => crc32($p) % 1000 / 1000, $palavras);
    }
````
### Entendendo passoa a passo
1. Normalização do texto:

 O código transforma tudo em minúsculas e quebra em palavras únicas.
````
$palavras = array_unique(str_word_count(strtolower($texto), 1));

````
Isso garante que “PHP” e “php” sejam tratados como a mesma palavra.

2. Ordenação:

Assim o resultado é previsível — duas frases com as mesmas palavras terão o mesmo “embedding”.
````
sort($palavras);
````
3. Criaçao do vetor numérico:

````
array_map(fn($p) => crc32($p) % 1000 / 1000, $palavras);
````
Cada palavra é transformada em um número usando crc32.
Esse número é reduzido para algo entre 0 e 1 — simulando o comportamento de um embedding real, que também é uma lista de números flutuantes.

4. Resultado:

Com isso, teremos algo parecido com o seguinte:
````
[0.234, 0.678, 0.912]

````
[//]: # (Salvando no MySQL com embeddings simples)

No codigo abaixo, a gente vai passar  onde fica os nossos documentos, e vamos gerar o embedding de cada arquivo e salvar no banco de dados.
````
    public function handle(): void
    {
        $arquivos = glob('/var/www/projeto/ollama-php/docs/*.md');
        foreach ($arquivos as $arquivo) {
            $conteudo = file_get_contents($arquivo);
            $this->info($arquivo);
            $embedding = $this->gerarEmbeddingSimples($conteudo);
            DB::table('documents_embeddings')->insert([
                'filename' => basename($arquivo),
                'content' => $conteudo,
                'embedding' => json_encode($embedding),
            ]);
        }
    }
````

Exemplo completo do comando embeding:
````
<?php

namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Support\Facades\DB;

class embedingsCommand extends Command
{
    protected $signature = 'embedings';

    protected $description = 'Command description';

    public function handle(): void
    {
        $arquivos = glob('/var/www/projeto/ollama-php/docs/*.md');
        foreach ($arquivos as $arquivo) {
            $conteudo = file_get_contents($arquivo);
            $embedding = $this->gerarEmbeddingSimples($conteudo);
            DB::table('documents_embeddings')->insert([
                'filename' => basename($arquivo),
                'content' => $conteudo,
                'embedding' => json_encode($embedding),
            ]);
        }
    }

    private function gerarEmbeddingSimples(string $texto): array
    {
        // Quebra o texto em palavras únicas e ordenadas
        $palavras = array_unique(str_word_count(strtolower($texto), 1));
        sort($palavras);

        // Cria um hash numérico simples (mock de embedding)
        return array_map(fn($p) => crc32($p) % 1000 / 1000, $palavras);
    }
}
````
[//]: # (Explicando “chunking”)

## Buscando o contéudo por similaridade
Agora que temos no nosso banco de dados os documentos embedados agora é hora de fazer a busca. 
Mas primeiro precisamos criar uma função para poder calcular a similaridade entre dois embeddings.

O que é similaridade?
É uma medda que indica o quanto dois textos, frases ou palavras ouvetores são semelhantes. Ela não compara apenas letras ou palavras
idênticas, mas sim o sentido e a estrutura do texto.
Exemplo:
    Texto A:  "O gato está dormindo no sofá"
    Texto B: "Um felino descansa no sofá"
Eles são diferentes em palavras, mas muito semelhantes em significado.
Um modelo de embedding (como o usado em RAG) vai gerar vetores próximos no espaço vetorial, e a similaridade entre eles será alta (por exemplo, 0.92 em uma escala de 0 a 1).
[//]: # (Criando uma função de similaridade)
Nosso trecho de código da função similaridade:
````
  private function similaridade(array $a, array $b): float
    {
        $inter = count(array_intersect(array_keys($a), array_keys($b)));
        return $inter / max(count($a), count($b));
    }
````
### Entendendo passoa a passo
1. Pega a chaves:
   Pegam só as chaves dos dois arrays.
````
array_keys($a) e array_keys($b)
````
2. Interesençao do array:
````
array_intersect(array_keys($a), array_keys($b))
````
3. Conta as palavras:
````
count(array_intersect(array_keys($a), array_keys($b)));
````
4. Faz a proporção de chaves iguais:
````
$inter / max(count($a), count($b));
````
O resultado é um número entre 0 e 1:

1 = arrays totalmente parecidos (todas as chaves iguais)

0 = arrays completamente diferentes

O código completo do nosso chat:
````
<?php

namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Support\Facades\DB;
use function Laravel\Prompts\textarea;
use function Laravel\Prompts\select;

class chatCommand extends Command
{
    protected $signature = 'chat-test';

    protected $description = 'Command description';

    public function handle()
    {


        $client = \ArdaGnsrn\Ollama\Ollama::client();



        $pergunta = textarea('Escreva aqui');
        $embeddingPergunta = $this->gerarEmbeddingSimples($pergunta);

        // Carrega embeddings do banco
        $documentos = DB::table('documents_embeddings')->get();

        $ranked = [];
        foreach ($documentos as $doc) {
            $emb = json_decode($doc->embedding, true);
            $ranked[$doc->id] = $this->similaridade($embeddingPergunta, $emb);
        }
        // Ordena por similaridade
        arsort($ranked);

        // Pega os 3 melhores
        $topDocs = collect(array_keys($ranked))->take(3)
            ->map(fn($id) => $documentos->firstWhere('id', $id))
            ->pluck('content')
            ->implode("\n\n");
        // Monta o prompt com o contexto combinado
        $prompt = "Você é um assistente que responde apenas com base no conteúdo abaixo.
    Se a resposta não estiver presente no conteúdo, diga: 'Desculpe, a resposta para essa pergunta não está disponível neste documento.'.\n\n" .
            "---\n" . $topDocs . "---\n\n" .
            "Pergunta: $pergunta";

        $response = $client->chat()->create([
            'model' => 'qwen2.5:3b',
            'messages' => [

                ['role' => 'user', 'content' => $prompt],

            ],
        ]);

        $resultado = $response->message->content; // 'Ah, taxes... *chew chew* Hmm, not really sure how to help with that.';
        dd($resultado);
    }

    // Calcula similaridade (cosine-like simplificado)
    private function similaridade(array $a, array $b): float
    {
        $inter = count(array_intersect(array_keys($a), array_keys($b)));
        return $inter / max(count($a), count($b));
    }

    private function gerarEmbeddingSimples(string $texto): array
    {
        // Quebra o texto em palavras únicas e ordenadas
        $palavras = array_unique(str_word_count(strtolower($texto), 1));
        sort($palavras);

        // Cria um hash numérico simples (mock de embedding)
        return array_map(fn($p) => crc32($p) % 1000 / 1000, $palavras);
    }
}

````
Como o código acima pode ser um pouco complicado, vou explicar o passo a passo.:
[//]: # (Selecionando os documentos mais parecidos)
## Enviando para o modelo

[//]: # (Montando o prompt final)

[//]: # (Rodando via comando php artisan chat)