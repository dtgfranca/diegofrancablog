---
_b2s_post_meta:
  card_desc: 'A idéia de escrever esse post surgiu após eu fazer uma apresentação sobre testes unitários na empresa que trabalho. Durante a apresentação,  fiz um live '
  card_image: http://diegofranca.dev/wp-content/uploads/2023/02/system-bug.jpg
  card_title: Desbravando testes unitários
  og_desc: 'A idéia de escrever esse post surgiu após eu fazer uma apresentação sobre testes unitários na empresa que trabalho. Durante a apresentação,  fiz um live '
  og_image: http://diegofranca.dev/wp-content/uploads/2023/02/system-bug.jpg
  og_image_alt: ""
  og_title: Desbravando testes unitários
_edit_last: "1"
_thumbnail_id: "479"
author: diego.tg.franca@gmail.com
categories:
  - php
  - teste
cover:
  alt: system-bug
  image: /wp-content/uploads/2023/02/system-bug.jpg
date: "2023-02-17T20:23:38+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=469
parent_post_id: null
post_id: "469"
summary: A idéia de escrever esse post surgiu após eu fazer uma apresentação sobre testes unitários na empresa que trabalho. Durante a apresentação, fiz um live code em que criei um endpoint na qual utilizei os conceitos, que irei abordar, para fazermos a isolação do componente. Gostaria muito de fazer uma aplicação aqui no blog, mas pode ser que fique muito tedioso fazer um passo a passo. Então, decidi fazer um resumo do que foi apresentado, com exemplos de código para melhor entendimento.
tags:
  - engenharia-e-software
  - php
  - teste
  - testes-unitarios
title: Desbravando testes unitários
url: /2023/02/17/desbravando-testes-unitarios/

---
A idéia de escrever esse post surgiu após eu fazer uma apresentação sobre testes unitários na empresa que trabalho. Durante a apresentação, fiz um live code em que criei um endpoint na qual utilizei os conceitos, que irei abordar, para fazermos a isolação do componente. Gostaria muito de fazer uma aplicação aqui no blog, mas pode ser que fique muito tedioso fazer um passo a passo. Então, decidi fazer um resumo do que foi apresentado, com exemplos de código para melhor entendimento.

## **O que é um teste unitário?**

Um teste unitário consiste em testar a menor parte do código que estamos desenvolvendo, que, no nosso caso, seriam os nossos métodos. Ele não é muito confiável, pois testamos somente a nossa lógica e não testamos a integração entre os componentes do sistema.

Algumas dúvidas que vejo sobre testes unitários são: como posso testar apenas uma parte do código quando ele depende de uma interface ou de uma classe específica?

Para atingir esse nível de isolamento, nós temos alguns conceitos que podemos utilizar:

## Stub

Criamos um dublê de teste com os resultados esperados, assim podemos simular nossos casos específicos.

Aqui nesse exemplo eu criei a classe chamada `PessoaFisica`:

![](https://lh5.googleusercontent.com/uhCC9Orx_rM21Uy7S6Nz6wdukUC2NwWehoptD3NvLr453FcyGZmHx7TGnyEu219czoZWXZTZVZRCMzmvt53xw1xsGAiZyU_W28sctmXEo7QTUqPQRauEkvLMRHeQ0YA6Gk0MnOgsHjzbqF04zX6fKaHMJw=nw)

Com a ajuda da biblioteca Mockery do Laravel criamos um stub para o método buscaDadosPorCpf, com o retorno que esperamos:

![](https://lh5.googleusercontent.com/LBna4KPerA-DV99AwplJobx-IZCOrS0o1RG7OPCrLEbZdRTaIg7upZJ7AlU7x1xX0N92RHRMlk0OX2bI_QE3aGEyJKU0ZcYNjPVqcQsKuG_W0I--0NAtX_C5phS09gdRxfL85OPOqq6Alw3l01BCFhJC-A=nw)

## Mock

Tem as mesmas características do stub, mas podemos fazer asserções sobre seu comportamento, garantindo que um método será ou não chamado.

Nesse exemplo, queremos além de definir uma saída para o metodo, queremos também saber o seu comportamento. No teste abaixo, passamos o metodo `time(1)` que nos diz que o método tem que ser chamado uma vez:

![](https://lh6.googleusercontent.com/CVG--I8zJDNsxMG1CoOH2QccmNEw89QB5tG2TiXD7mxcGxer_x1mKued6kHYOcq-lxvIaAKVNLnU-ulIF_-4YlaHTIVr0ujGTseOEq6F-QPLAuk5p-z8rVxjXj1XyJNlHkZ468FYeJgnMIkFRwcCLq6ELg=nw)

## Dummies

Dummie é um objeto que criamos no teste que não precisamos indicar um retorno ou fazer asserções sobre o comportamento, ele serve apenas para satisfazer um parâmetro de uma classe ou de um método.

Na figura abaixo, temos uma dependência com o cep na nossa classe `PessoaFisica`. Apesar de não usarmos no metódo que vamos testar, isso impacta na hora que formos instanciar a classe, pois devemos satisfazer essa depêdencia:

![](https://lh4.googleusercontent.com/bxMrL8wjbvlUTZK59ghLst2bcc5Mp50Js10rY_TY81ucdhfNPWCTW6VUeMIEOGikk_DqOytEV2Ney9gAgOYX3i7_byOW3yWXGSy2sA-9RMOIOGRCqTtqTz7LGk4_WGP6aGGl8_BtcmWvHh8NVE0UNyQ2JA=nw)

Então criamos o Dummie para satisfazer o que se pede no construtor da classe , `$cep = \Mockery::mock(Cep::class)`. Com dummie criado, podemos apenas passá-lo no construtor:

![](https://lh4.googleusercontent.com/vurAp1eAv6yf4O6lofqAA_Ssx7Eaa7RMgldWGsgaIkTyEOL8ZsnvX6JBra9024fZNiYjqcuzlN0TVQMkLtmaTyekBV4wJVairYkf2kI1mQi0o5Qjwf4C64s5YK6k-S0w-8yRVwYhgMW6uF8t0FBCyADk_A=nw)

## Spies

O objetivo dos spies é fazer asserções sobre uma chamada de um método, em vez de fazer a asserção sobre o comportamento do objeto.

Para exemplificar, vou criar uma classe chamada "UsuarioService":

{{< figure src="/wp-content/uploads/2023/02/spies-class.png" alt="" caption="" >}}

Nós podemos criar um teste para verficar se o método "criarUsuario" é chamado com os argumentos corretos:

{{< figure src="/wp-content/uploads/2023/02/teste-criar-usuario.png" alt="" caption="" >}}

Com o Mockery criamos um spy para a classe UsuarioService. Em seguida, o método criarUsuario é chamado com os argumentos "Diego França" e "diego@example.com". Finalmente, o método shouldHaveReceived é usado para verificar se o método criarUsuario foi chamado com os mesmos argumentos uma única vez.

## Fake

Os fakes têm a mesma funcionalidade de uma classe real, mas são usados apenas em testes. Um exemplo de fake é o banco de dados, no qual podemos criar um método como "salvar", mas salvar apenas em memória(array). Dessa forma, temos a funcionalidade de um salvamento, mas somente naquele momento.

Para exemplificar, criei um "repository" para salvar um cadastro no banco de dados, mas nós não queremos que a nossa aplicação utilize o banco.

{{< figure src="/wp-content/uploads/2023/02/repository-t2este-1.png" alt="" caption="" >}}

Para construir o fake, irei utilizar um array onde os dados serão armazenados na memória do computador:

{{< figure src="/wp-content/uploads/2023/02/testefake.png" alt="" caption="" >}}

## Conclusão

Na primeira vez que você for fazer um teste unitário, pode passar na sua cabeça que esse teste não tem função alguma, já que muitas vezes emulamos os dados gerados. Mas gostaria de deixar uma experiência pessoal: o teste unitário ele não vai garantir que sua aplicação não irá quebrar, ele somente lhe mostra que seu algoritmo não tem erro. Por isso, é de EXTREMA importância aplicar os outro tipos de testes, como o _end to end_ e o t _este de exploração(_ não abordado neste artigo), pois eles sim garantem o funcionamento correto do sistema em geral.

Outra dica para quem está começando agora e quer escrever bons testes, é seguir este passo a passo que pode servir como base para você:

- Criar test data builders(Criação dados de entrada para nossos testes.);
- Criar nossos métodos de inicialização afim de não repertir código(tearDown e setUp);
- Criar testes com nomes que faz sentido;
- Criar boas asserções;

Todos esses conceitos que abordei estão disponíveis em todas as linguagens de programação.

Espero que este artigo possa ajudá-lo de alguma forma. Caso tenha alguma duvida crítica (sempre são muito bem vindas), deixe nos comentários.
