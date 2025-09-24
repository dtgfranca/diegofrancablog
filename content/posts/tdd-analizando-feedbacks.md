---
_b2s_post_meta:
  card_desc: |-
    Ultimamente venho estudando a fundo sobre o TDD e como ele pode nos auxiliar a escrever um bom código.



    Muitos desenvolvedores ainda não aderiram  a essa pr
  card_image: http://diegofranca.dev/wp-content/uploads/2021/03/TDD.jpg
  card_title: TDD - Analisando FeedBacks
  og_desc: |-
    Ultimamente venho estudando a fundo sobre o TDD e como ele pode nos auxiliar a escrever um bom código.



    Muitos desenvolvedores ainda não aderiram  a essa pr
  og_image: http://diegofranca.dev/wp-content/uploads/2021/03/TDD.jpg
  og_image_alt: ""
  og_title: TDD - Analisando FeedBacks
_edit_last: "1"
_thumbnail_id: "354"
author: diego.tg.franca@gmail.com
categories:
  - uncategorized
cover:
  alt: TDD
  image: /wp-content/uploads/2021/03/TDD.jpg
date: "2021-03-25T21:13:14+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=348
parent_post_id: null
post_id: "348"
summary: |-
  Ultimamente venho estudando a fundo sobre o TDD e como ele pode nos auxiliar a escrever um bom código.

  Muitos desenvolvedores ainda não aderiram a essa prática alguns por falta de conhecimento e outros por acharem que perdem a produtividade ao criar os testes antes do desenvolvimento
title: TDD - Analisando FeedBacks
url: /2021/03/05/tdd-analizando-feedbacks/

---
Ultimamente venho estudando a fundo sobre o TDD e como ele pode nos auxiliar a escrever um bom código.

Muitos desenvolvedores ainda não aderiram a essa prática alguns por falta de conhecimento e outros por acharem que perdem a produtividade ao criar os testes antes do desenvolvimento

Nesse artigo vou me basear no livro escrito pelo Mauricio Aniche, [Test-Driven Development. Teste e Design no Mundo Real com PHP](https://www.casadocodigo.com.br/products/livro-tdd-php), onde ele exemplefica alguns dos feedabacks na qual com a prática do TDD pode nos ajudar a escrever um bom código.

## O que é o TDD

A sigla TDD(Test Domain Drive) significa teste orientado a testes. Este é um método de desenvolvimento que está muito em alta nos dias de hoje.

O TDD ele parte do princípio de que os testes são escritos primeiro que a implemtentação e passando por um ciclo de repetição até que se chega em uma solução simples.

{{< figure src="/wp-content/uploads/2021/03/img-tdd.png" alt="" caption="" >}}

Para iniciar TDD é recomendável que o programador escolha uma suíte de testes automático(PhpUnit, Junit, etc). Deve-se criar testes unitários para cada metódo de uma classe afim de testar todo o seu comportamento.

Os testes unitários tem como objetivo de testar uma classe de maneira isolada, sem qualquer interferência de outras classes.

Para se escrever um bom teste unitário devemos seguir um padãro

- Criar nossos test data builders
- Criar nossos métodos de inicialização afim de não repertir código
- Criar testes com nomes que faz sentido
- Criar boas asserções

A prática do TDD tem uma vantagem que ela pode nos indicar que o desgin da nossa classe não está legal, ela pode indicar o alto acoplamento e a falta de coesão nas nossas classes.

Para que o TDD possa nos ajudar a melhorar à escrita de código é importante ressaltar a experiência do programador com a orientação a objetos e os conceitos como SOLID e design patterns.

## TDD e Acoplamento

Sintomas:

- O uso abusivo de objetos dublês criados para testar uma única classe indica que a classe testada depedente de muitas outras classes e isso o torna uma classe frágil, e isso demonstra que a classe é altamente acoplada
- A criação de objetos dublês que não sao utilizados em alguns métodos de teste é outro feedback importante. Isso geralmente acontece quando a classe é altamente acoplada, e o resultado da ação de uma dependência não interfere na outra. Quando isso acontece, o programador acaba por escrever cojuntos de testes, sendo que alguns deles lidam com um subconjunto dos objetos dublês, enqaunto outros testes lidam com outro subconjunto de objetos dublês. Isso indica alto acoplamento da classe, que precisa ser refatorada.
- Quando o desenvolvedor começa o teste e percebe que a interaface pública da classa não está amigável, pode indicar que a abastração corrente não é clara o suficiente e poderia ser melhorada.
- A falta de abstração geralemente também faz com que uma simples mudança precise ser feita em diferentes pontos do código. Quando uma mudança acontece e o programador é obriagdo a fazer a mesa alteração em diferentes testes, isso indica a falta de abstração correta para evitar a repetição desnecessária de código.
- Analogamente, programador pode perceber a mesma coisa quando ele começa a criar testes repetidos para entidades diferentes.

## TDD e o Encapsulamento

Sintomas:

- Testes que lidam demais com outros objetos ao invés de lidar com o objeto sob teste podem estar avisando o desenvolvedor em relação a problemas de encapsulamento. A própria não utilização da Lei de Demeter, tanto nos teste quanto no código de produção, também pode avisar sobre os mesmos problemas. Isso é muito comum em bateria de teses de classe anêmicas, Um modelo anêmico é aquele em que as classe contêm apenas atributos ou apenas métodos.
- Classes que contêm atributos apenas representam entidades, enquanto outras classes, que contêm apenas métodos, realizam ações sobre eles. Esse tipo de projeto deve ser evitado ao máximo.

## Quando não usar TDD

Geralmente quando os desenvolvedores já tem um certo dominío sobre o que eles vão implementar, ou algo que esteja associado a infra, como exemplo de códigos sql. Mas não se esqueça, apesar de não fazer o teste antes do desenvolvimento, deve se criar testes após a sua implementação. Outro que não necessita criar testes é para os metódos getters e setters

## Referência Bibliográfica

- Test-Driven Developent: By example - Kent Beck
- Growing Object Oriented Software, Guided By Tests
- Agile Software Development, principles, patterns, and practices
- Test-Driven Development. Teste e Design no Mundo Real com PHP
