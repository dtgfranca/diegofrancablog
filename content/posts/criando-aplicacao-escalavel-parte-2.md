---
_advads_ad_settings:
  disable_ads: 0
_b2s_post_meta:
  card_desc: 'Fala pessoal! Tudo bem com vocês? Seguindo a nossa jornada da criação de uma aplicação escalável, nessa segunda parte venho contar para vocês como foi o '
  card_image: http://diegofranca.dev/wp-content/uploads/2021/07/21184018666362.jpg
  card_title: Criando aplicação escalável — Parte 2
  og_desc: 'Fala pessoal! Tudo bem com vocês? Seguindo a nossa jornada da criação de uma aplicação escalável, nessa segunda parte venho contar para vocês como foi o '
  og_image: http://diegofranca.dev/wp-content/uploads/2021/07/21184018666362.jpg
  og_image_alt: ""
  og_title: Criando aplicação escalável — Parte 2
_edit_last: "1"
_thumbnail_id: "391"
author: diego.tg.franca@gmail.com
categories:
  - uncategorized
cover:
  alt: "21184018666362"
  image: /wp-content/uploads/2021/07/21184018666362.jpg
date: "2021-07-18T13:37:58+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=393
parent_post_id: null
post_id: "393"
summary: Fala pessoal! Tudo bem com vocês? Seguindo a nossa jornada da criação de uma aplicação escalável, nessa segunda parte venho contar para vocês como foi o início dos testes, [para quem não leu a primeira parte clique aqui](https://diegofranca.dev/2021/07/04/criando-aplicacao-escalavel-parte-1/).
tags:
  - escalabilidade
  - heroku
  - k6
  - php
  - teste-de-carga
  - testing
title: Criando aplicação escalável — Parte 2
url: /2021/07/18/criando-aplicacao-escalavel-parte-2/

---
Fala pessoal! Tudo bem com vocês? Seguindo a nossa jornada da criação de uma aplicação escalável, nessa segunda parte venho contar para vocês como foi o início dos testes, [para quem não leu a primeira parte clique aqui](/2021/07/04/criando-aplicacao-escalavel-parte-1/).

No Primeiro momento tentei rodar o ‘software’ de teste de carga [K6](https://k6.io/) com aplicação na minha máquina pessoal, iniciei com 1000 usuários fazendo acessos simultâneos e obtive somente 2% de sucesso, quando tentei rodar com 2000 usuários começou a gerar um erro de **"socket: too many open files"**, para fim de comparação nesse teste vou manter 1000 tanto na minha máquina quanto no servidor do Heroku. Criei uma conta no [Heroku](https://www.heroku.com/), cujas configurações não são robustas, mas com o passar dos testes talvez posso mudar de plano para fazer um teste melhor.

Configurações da máquina no Heroku:

Memória Ram2 GB N. de processadores2

Configurações do computador onde irei rodar o ‘software’ de teste de carga:

Mémoria Ram8 GBSSD480 GBCPU8 núcleosProcesadorCore i5 8GenS.operacionalUbuntu 20.1

## Resultados dos testes efetuados com a aplicação rodando na minha máquina

{{< figure src="/wp-content/uploads/2021/07/WhatsApp-Image-2021-07-18-at-9.25.54-AM.jpeg" alt="" caption="" >}}

Agora vamos analisar o relatório do teste na máquina local:

Criei um assert para verificar a quantidade de requisições que iria retornar com o status 200, nesse caso de 2525 requisições somente 2% retornou com o status de sucesso, tivemos 97% que falharam e a média de requisição por segundo foi de 42,80/s. O k6 iniciou o teste com o mínimo de 154 usuários virtuais e no máximo de 1000.

## Resultados dos testes efetuados com a aplicação rodando no servidor do Heroku

{{< figure src="/wp-content/uploads/2021/07/WhatsApp-Image-2021-07-18-at-9.45.02-AM.jpeg" alt="" caption="" >}}

Analisando os resultados do Heroku:

O teste foi similar ao teste anterior, nesse caso das 2643 requisições que o k6 fez a URL todos retornaram com o status 200, não tivemos falha como aconteceu no meu computador, a média de requisição por segundo foi de 56,69/s já percebemos que tivemos uma melhora, o K6 inciou os testes com um mínimo de 39 usuários virtuais e o máximo de 1000 usuários virtuais.

Tentei aumentar para 2000 usuários virtuais, mas recebi o erro **"failed to load system roots and no roots provided"**, não sei se esse erro é devido ao meu plano que é gratuito, vou tentar verificar para que no próximo teste eu consigo aumentar o número de usuários virtuais

### Finalizando

Já percebemos a diferença entre dois servidores, nessa segunda parte conseguimos fazer nosso primeiro teste do nosso objetivo de 900 requisições por segundo, conseguimos nesse primeiro momento fazer no máximo 56 requisições por segundo.

O próximo passo será estudar sobre a escalabilidade horizontal e vertical, nesse primeiro teste podemos perceber que o nosso servidor ainda é muito fraco talvez seja melhor aumentar a memória para isso terei que mudar o plano do Heroku, tentarei estudar um pouco mais sobre esse serviço, ainda não estou certo que fazer, mas vamos continuando e aprendendo juntos nessa longa jornada…

Caso você ficou curioso em saber sobre as métricas do k6 mais profundamente, segue o link da documentação: https://k6.io/docs/using-k6/metrics/
