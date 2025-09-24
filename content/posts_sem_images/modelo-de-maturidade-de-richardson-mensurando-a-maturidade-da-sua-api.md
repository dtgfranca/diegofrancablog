---
_advads_ad_settings:
  disable_ads: 0
_b2s_post_meta:
  card_desc: 'Fala,  pessoal! Hoje tenho algo interessante sobre api restful. Quando você está criando uma api restful já parou para pensar se o que estamos desenvolvendo '
  card_image: http://diegofranca.dev/wp-content/uploads/2022/01/44007397-0330098e-9e6b-11e8-91e0-24a2cf5d3b55.png
  card_title: Modelo de maturidade de Richardson - Mensurando a maturidade da sua api
  og_desc: 'Fala,  pessoal! Hoje tenho algo interessante sobre api restful. Quando você está criando uma api restful já parou para pensar se o que estamos desenvolvendo '
  og_image: http://diegofranca.dev/wp-content/uploads/2022/01/44007397-0330098e-9e6b-11e8-91e0-24a2cf5d3b55.png
  og_image_alt: ""
  og_title: Modelo de maturidade de Richardson - Mensurando a maturidade da sua api
_edit_last: "1"
_thumbnail_id: "454"
author: diego.tg.franca@gmail.com
categories:
  - arquitetura
  - uncategorized
cover:
  alt: 44007397-0330098e-9e6b-11e8-91e0-24a2cf5d3b55
  image: /wp-content/uploads/2022/01/44007397-0330098e-9e6b-11e8-91e0-24a2cf5d3b55.png
date: "2022-01-03T12:35:45+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=381
parent_post_id: null
pms-content-restrict-custom-non-member-redirect-url: ""
pms-content-restrict-custom-redirect-url: ""
pms-content-restrict-message-logged_out: ""
pms-content-restrict-message-non_members: ""
pms-content-restrict-type: default
post_id: "381"
summary: Fala, pessoal! Hoje tenho algo interessante sobre api restful. Quando você está criando uma api restful já parou para pensar se o que estamos desenvolvendo está correto e se existe algum padrão a ser seguido ao criar uma api restful?
tags:
  - architecture
  - php
  - rest
  - richardson-maturity
title: Modelo de maturidade de Richardson - Mensurando a maturidade da sua api
url: /2022/01/03/modelo-de-maturidade-de-richardson-mensurando-a-maturidade-da-sua-api/

---
Fala, pessoal! Hoje tenho algo interessante sobre api restful. Quando você está criando uma api restful já parou para pensar se o que estamos desenvolvendo está correto e se existe algum padrão a ser seguido ao criar uma api restful?

Existe sim uma maneira de saber se o que estamos desenvolvendo é uma api restful e o grau da sua maturidade, chama-e [modelo de maturidade de Richardson](https://martinfowler.com/articles/richardsonMaturityModel.html). A primeira vez que ouvi esse termo foi no canal da Michelli Brito, recomendo acompanhar o canal dela. Fiquei motivado em escrever um pouco do meu entendimento acerca do assunto, mas antes de iniciar quero fazer um overview da diferença entre rest e restful, ainda têm muitos devs que confundem esses termos. E sem mais delongas; bora lá.

## Diferença entre Rest e Restful

O [rest](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) ( **Representational State Transfer**) é um padrão arquitetural que define um conjunto de restrições para a criação de web services, já o restful são web services que implementam esse padrão arquitetural.

## O que é o modelo de maturidade de Richardson

Richardson criou 4 pilares que todo web service deve seguir para ser considerada restful. Há algumas controvérsias em relação a isso. Alguns desenvolvedores pragmáticos dizem que se o web service implementa até o nível 2 já pode ser considerado rest, por outro lado, devs que são mais puristas consideram que para um web service ser considerado rest deve implementar os 4 níveis.

## Níveis de maturidade

### Nível 0

Uma api está no nivel 0 quando se utiliza do protocolo http, porém só utiliza um único método http(normalmente post).

Método: **POST**

URL: `http://localhost/api`

Body (JSON):

```
{
  "action": "getUser",
  "userId": 123
}

```

### Nível 1 - Recursos

Uma api está no nível 1 quando se utiliza do protocolo http e têm as uris(recursos) bem definido — como padrão as uris devem ser nomeadas como substantivos e não como verbos —.

Método: **POST**

URL: `http://localhost/api/users/get`

Body (JSON):

```
{
  "id": 123
}

```

### Nível 2 - Verbos HTTPs

Api além de utilizar o protocolo http como comunicação, utiliza-se a semântica corretas dos seus verbos e dos seus códigos de retorno.

### Obter usuário

- Método: **GET**
- URL: `http://localhost/api/users/123`

### Criar usuário

- Método: **POST**
- URL: `http://localhost/api/users`
- Body (JSON):

```
{
  "nome": "Diego",
  "email": "diego@example.com"
}
```

### Atualizar usuário

- Método: **PUT**
- URL: `http://localhost/api/users/123`
- Body (JSON):

```
{
  "nome": "Diego França"
}
```

### Deletar usuário

- Método: **DELETE**
- URL: `http://localhost/api/users/123`

### Nível 3 - Controle de hipermédia

Além de ter implementado os níveis acima, adicionamos o HATEOAS(hipermedias) na nossa api para alcançar o nível 3 de maturidade.

### Obter usuário com links HATEOAS

- Método: **GET**
- URL: `http://localhost/api/users/123`

```
{
  "id": 123,
  "nome": "Diego",
  "email": "diego@example.com",
  "_links": {
    "self": { "href": "/api/users/123" },
    "editar": { "href": "/api/users/123/edit" },
    "deletar": { "href": "/api/users/123" },
    "posts": { "href": "/api/users/123/posts" }
  }
}
```

# Referências

[Richardson's maturity model - Martin Fowler](https://martinfowler.com/articles/richardsonMaturityModel.html)

[O que é uma api Restful na prática? Maturidade de Richardson](https://www.youtube.com/watch?v=P92SBaN42mQ)
