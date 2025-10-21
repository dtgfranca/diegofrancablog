---
title: "10 Modelos De Prompts Para Usar Hoje"
date: 2025-09-26T11:44:56-03:00
draft: true
---

Quando comecei a conhecer o chagpt e vi que ele podia fazer muitas coisas, eu fiquei muito impressionado. Com o passar do tempo
eu fui ficando um pouco desmotivado porque muito do que eu pedia me retornava informações incosistntes, alucionações e resposta ruins, via algumas pessoas
falando sobre prompt e não ligava muito, para mim era hype, mas com o passar do tempo fui vendo que alguns conseguiam fazer sistemas completos utilizando somente
prompts, criar documentações arquiteturais  e eu com dificuldade em receber uma simples respostas que me satisfazesse. Foi então que comecei 
a estudar um pouco mais sobre prompts e vi que tinha um universo de possibilidades, não era só um hype que estava acontecendo mas uma ciência que estava
atrás de escrever prompts.

Comecei a aplicar os prompts em diversas tarefas e vi que o resultado era muito melhor, as vvezes até mais do que esperava. Talvez você que esteja lendo
esse artigo esteja se perguntando: "Como eu posso  melhorar meu resultado com os prompts?", foi pensando nisso  que quero mostrar de forma simples e usual
para que você possa aplicar os prompts no seu cotidiano. Aqui vai exemplos de prompts simples(zero-shot, one-shot/few-shot) até alguns mais complexos(chain of thought, skeleton of thought, tree of thought, self-consistency, directional stimulus, re-acting).

O legal é que, com os prompts mostrados aqui você pode já ir testando nos modelos de IA que você utiliza(chatgpt, claude, entre outros), e ver como eles se comportam.

[//]: # (Com o advento dos LLMs, muitas pessoas começaram a usar modelos de IA para fazer suas tarefas.)

[//]: # (Com isso, surgiram estudos sobre como descrever instruções para o modelo de IA.)

[//]: # ()
[//]: # (Hoje, o mais importante é saber como usar os prompts — mas muitos ainda desconhecem o poder deles.)

[//]: # (Eles podem ser aplicados em diferentes níveis: desde uma tarefa simples, como responder uma pergunta, até uma tarefa complexa, como auxiliar na criação de um aplicativo.)

[//]: # ()
[//]: # (E é justamente nesse ponto que muitas pessoas se perdem: tentam criar seus aplicativos usando modelos de IA e percebem que as respostas podem gerar alucinações e inconsistências.)

[//]: # (Então, buscam soluções mais avançadas, como RAG ou Finetuning — sem perceber que, muitas vezes, um prompt bem estruturado e escrito já é suficiente para obter respostas mais consistentes e interessantes.)

[//]: # ()
[//]: # (Aqui quero mostrar alguns dos prompts mais usados, para que você consiga tirar o máximo proveito deles.)

[//]: # (Então, vamos começar definindo o que é um prompt.)


[//]: # (Se você está sentindo que quando você escreve os seus prompts  e não fica contente com as respostas ou )

[//]: # (o agente de IA gera uma resposta quee você ver que ela está alucinando ou gera inconsistencia nas suas respostas.)

[//]: # (Então é hora de aprender a usar os prompts de forma correta.)

### O   que é  prompt?
Prompt é uma frase ou um texto que o  agente de IA vai usar para responder. Os modelos de IA sao ótimos
para seguir instruções dadas, mas um prompt mal construído pode gerar respostas ruins também.
O mais importante para tirar o máximo de aproveito é saber como fazer um bom prompt. Eu vejo muitas  pessoas
escrevendo prompts ruins e até desistindo de usar o modelo de IA. Para que não aconteça isso eu vou mostar como podemos 
usar os prompts de forma correta.


### Zero-shot
Zero-shot é uma técnica onde o modelo de linguagem recebe somente a tarefa ser feita sem um exemplo de como 
a tarefa deve ser feita.

- Quando usar
 - A tarefa é simples e bem conhecida pelo modelo;
 - Não há tempo ou espaço para adicionar
 - Deseja-se a capacidade de aprender sem um exemplo de como a tarefa deve ser feita.
 - É preciso processar uma grande quantidade de tarefas  e economizar tokens
 - Você não sabe o que deve ser feito;
- Vantagens
 - Simples de usar
 - Pode ser usado para tarefas simples
- Desvantagens
    - Pode gerar respostas incompletas
    - Pode gerar alucinações

- Exemplos:
  Prompt:  Quero fazer uma pizza com queijo e presunto. Pode me ajudar?

### One-shot/Few-shot
- Quando usar
 - Quando você tem uma ou mais tarefas semelhantes.
 - Quando pode fornecer um ou alguns exemplos de como a tarefa deve ser feita.
- Vantagens
    - O modelo “aprende” com os exemplos.
    - Útil para tarefas mais complexas ou que exigem consistência.
  

- Desvantagens
 - Consome mais tokens.
 - prompt pode ficar mais complexo.

   - Exemplos
     Exemplo One-shot
     Prompt:
   - ````
     Seguindo esta forma: Eu gosto de jogar bola → I love to play basketball.
     Traduza para o inglês: Hoje vai chover.
     Exemplo Few-shot
     ````
     Exemplo Few-shot
    ````
       Traduza para o inglês seguindo o formato:

       Exemplo 1:  
       Português: Eu gosto de programar em PHP.  
       Inglês: I like to program in PHP.
    
       Exemplo 2:  
       Português: Hoje está chovendo muito.  
       Inglês: It is raining a lot today.
    
       Agora traduza:  
       Português: Amanhã vou ao mercado.  
       Inglês:
     ````

- 
### Chain of Thought

- Quando usar

- Vantagens

- Desvantagens

- Exemplos

### Skeleton of Thought

- Quando usar

- Vantagens

- Desvantagens

- Exemplos

### Tree of Thought

- Quando usar

- Vantagens

- Desvantagens

- Exemplos
- 
### Self-Consistency

- Quando usar

- Vantagens

- Desvantagens

- Exemplos
### Directional Stimulus

- Quando usar

- Vantagens

- Desvantagens

- Exemplos

### ReActing

- Quando usar

- Vantagens

- Desvantagens

- Exemplos


Experimente hoje: escolha um desses modelos de prompt e teste na sua ferramenta favorita (ChatGPT, Claude, Gemini, etc). Veja qual deles melhora mais o seu resultado.