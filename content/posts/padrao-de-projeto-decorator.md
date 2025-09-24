---
_b2s_post_meta:
  card_desc: Alguns dias atrás, eu estava trabalhando em um sistema responsável por sincronizar dados entre dois sistemas. A nova tarefa exigia reutilizar esse mesmo siste
  card_image: http://diegofranca.dev/wp-content/uploads/2025/07/design.png
  card_title: Padrão de projeto Decorator
  og_desc: Alguns dias atrás, eu estava trabalhando em um sistema responsável por sincronizar dados entre dois sistemas. A nova tarefa exigia reutilizar esse mesmo siste
  og_image: http://diegofranca.dev/wp-content/uploads/2025/07/design.png
  og_image_alt: ""
  og_title: Padrão de projeto Decorator
_edit_last: "1"
_encloseme: "1"
_pingme: "1"
_thumbnail_id: "664"
author: diego.tg.franca@gmail.com
categories:
  - design-patterns
  - dicas
  - php
cover:
  alt: design
  image: /wp-content/uploads/2025/07/design.png
date: "2025-07-08T12:59:17+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=595
parent_post_id: null
pms-content-restrict-custom-non-member-redirect-url: ""
pms-content-restrict-custom-redirect-url: ""
pms-content-restrict-message-logged_out: ""
pms-content-restrict-message-non_members: ""
pms-content-restrict-type: default
post_id: "595"
tags:
  - '#designpatterns'
  - architecture
  - engenharia-e-software
  - php
title: Padrão de projeto Decorator
url: /2025/07/08/padrao-de-projeto-decorator/

---
Alguns dias atrás, eu estava trabalhando em um sistema responsável por sincronizar dados entre dois sistemas. A nova tarefa exigia reutilizar esse mesmo sistema para sincronizar com um **terceiro**, mas com alguns extras: eu queria enviar uma notificação no início, outra no fim, adicionar logs e aceitar mais parâmetros.

O problema? Esse método já era usado em vários pontos do sistema. Alterá-lo diretamente tornaria o código frágil e com alto risco de quebrar outras partes.

Foi aí que me lembrei de uma aula sobre Design Patterns, onde o professor explicou o padrão **Decorator**.  
Na hora, tudo fez sentido: eu poderia "decorar" minha função com novos comportamentos — sem tocar no código original!

## O que é o padrão Decorator?

O padrão **Decorator** permite adicionar funcionalidades extras a um objeto de forma dinâmica — sem precisar alterar a estrutura da classe original.

Imagine que você tem uma xícara de café. Às vezes você quer café puro, às vezes com leite, chocolate, chantilly… ou com tudo isso junto!  
Você não precisa criar uma classe para cada combinação possível — basta ir “decorando” a base com os complementos desejados.

Para ilustrar melhor, imagine este diagrama:

{{< figure src="/wp-content/uploads/2025/07/image.png" alt="" caption="" >}}

Ainda parece confuso? Calma, vou usar um exemplo mais simples — e tenho certeza de que você vai sair daqui entendendo tudo!

## Exemplo prático com café

Você começa com um `CafePuro` (que dev que não gosta de uma bom café para programar? :D), e pode adicionar `Leite`, `Açucar`, `Chantilly` e ir, combinando da forma que quiser.

Vamos começar com um `CafePuro`. Depois, podemos adicionar `Leite`, `Açúcar`, `Chantilly`... e ir combinando como quiser.

Vamos criar a interface do nosso componente, chamada `Cafe`.  
Ela define os métodos que retornam a **descrição** e o **preço** do café:

```
interface Cafe
{
    public function getDescricao(): string;
    public function getPreco(): float;
}
```

Agora criamos a classe `CafePuro`, que implementa a interface `Cafe`:

```

class CafePuro implements Cafe
{

    public function getDescricao(): string
    {
        return "Café puro";
    }

    public function getpreco(): float
    {
        return 0.5;
    }
}

```

Em seguida, criamos a classe `CafeDecorator`, que será a **base para todos os nossos decoradores**:

```
class CafeDecorator implements Cafe
{
    public  function __construct(private readonly Cafe $cafe)
    {

    }

    public function getDescricao(): string
    {
        return $this->cafe->getdescricao();
    }

    public function getPreco(): float
    {
        return $this->cafe->getPreco();
    }
}
```

Agora, os nossos decoradores ( `Leite`, `Açucar`, `Chantilly`) vão estender `CafeDecorator` e sobrescrever os métodos:

**Classe Leite:  
**

```
class Leite extends CafeDecorator
{
    public function __construct(private Cafe $decorator)
    {
    }
    #[Override]
    public function getDescricao(): string
    {
        return $this->decorator->getDescricao() .' + Leite';
    }

    #[Override]
    public function getPreco(): float
    {
        return $this->decorator->getPreco() + 1.30;
    }
}
```

**Classe Chantillty:**

```
class Chantily extends CafeDecorator
{
    public function __construct(private Cafe $decorator)
    {

    }
    #[Override]
    public function getDescricao(): string
    {
        return $this->decorator->getDescricao() .' + Chantily';
    }

    #[Override]
    public function getPreco(): float
    {
        return $this->decorator->getPreco() + 1.00;
    }
}

```

**Classe Açucar**

```
class Acucar extends CafeDecorator
{
    public function __construct(private Cafe $decorator)
    {
    }
    #[Override]
    public function getDescricao(): string
    {
        return $this->decorator->getDescricao() .' + Açucar';
    }

    #[Override]
    public function getPreco(): float
    {
        return $this->decorator->getPreco() + 2.00;
    }
}
```

Com as classes prontas, vamos ao **código cliente** — ou seja, como usamos esses decorators na prática.

Começamos com um café puro:

Para ficar mais didático, primeiro vamos "fazer" o café puro:

```
$cafe = new CafePuro();

echo $cafe->getDescricao(). "\n"; //Café Puro
echo $cafe->getPreco(). "\n"; //0.5

```

Agora queremos adicionar leite ao café. Para isso, basta **passar a instância anterior** para o construtor da classe `Leite`:

```
$cafe = new \Dtgfranca\Decorator\Leite($cafe);
echo $cafe->getDescricao(). "\n"; //Saída: Café Puro + Leite
echo $cafe->getPreco(). "\n"; //Saída: 1.8
```

Em seguida, adicionamos **açúcar**:

```
//Adiciona o açucar
$cafe = new \Dtgfranca\Decorator\Acucar($cafe);

echo $cafe->getDescricao(). "\n";//Saída: Café Puro + Leite + Açucar
echo $cafe->getPreco(). "\n"; //Saída: 3.8

```

E por fim, o **chantilly**:

```
//Adiciona o chantily
$cafe = new \Dtgfranca\Decorator\Chantily($cafe);
echo $cafe->getDescricao(). "\n"; //Saída: Café Puro + Leite + Açucar + Chanitly
echo $cafe->getPreco(). "\n";//Saída: 3.8
```

Repare que conseguimos **adicionar novos comportamentos sem modificar a classe original** ( `CafePuro`). Esse é exatamente o espírito do **princípio Open/Closed** do SOLID:

"Aberto para extensão, fechado para modificação."

Quando queremos adicionar algo novo, não alteramos o que já existe — apenas **estendemos** com um decorator.

Outro princípio aplicado aqui é o **Single Responsibility (SRP)**. Cada classe tem um único motivo para mudar. Por exemplo: `CafePuro` só mudaria se o preço do café ou sua descrição mudassem. O comportamento extra (leite, açúcar, etc.) está isolado nos decoradores.

Essa abordagem pode parecer simples, mas é **muito poderosa**.  
Em projetos legados, onde mexer em código antigo pode gerar bugs inesperados, usar o padrão **Decorator** é uma maneira elegante e segura de adicionar comportamentos extras.

O código completo está disponível no GitHub, caso queira testar e brincar com outras combinações:

[https://github.dev/dtgfranca/design-pattern-decorator](https://github.dev/dtgfranca/design-pattern-decorator)
