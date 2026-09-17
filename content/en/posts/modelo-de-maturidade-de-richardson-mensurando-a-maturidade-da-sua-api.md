---
  disable_ads: 0
  card_desc: "Hey folks! Today I have something interesting about RESTful APIs. When you're building a RESTful API, have you ever stopped to think if what we're developing"
  card_image: http://diegofranca.dev/wp-content/uploads/2022/01/44007397-0330098e-9e6b-11e8-91e0-24a2cf5d3b55.png
  card_title: Richardson Maturity Model - Measuring the maturity of your API
  og_desc: "Hey folks! Today I have something interesting about RESTful APIs. When you're building a RESTful API, have you ever stopped to think if what we're developing"
  og_image: http://diegofranca.dev/wp-content/uploads/2022/01/44007397-0330098e-9e6b-11e8-91e0-24a2cf5d3b55.png
  og_image_alt:
  og_title: Richardson Maturity Model - Measuring the maturity of your API
_edit_last: "1"
_thumbnail_id: "454"
author: diego.tg.franca@gmail.com
  - architecture
  - uncategorized
  alt: 44007397-0330098e-9e6b-11e8-91e0-24a2cf5d3b55
  image: /wp-content/uploads/2022/01/44007397-0330098e-9e6b-11e8-91e0-24a2cf5d3b55.png
date: "2022-01-03T12:35:45+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
  page-builder: {}
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=381
parent_post_id: null
pms-content-restrict-custom-non-member-redirect-url:
pms-content-restrict-custom-redirect-url:
pms-content-restrict-message-logged_out:
pms-content-restrict-message-non_members:
pms-content-restrict-type: default
post_id: "381"
summary: "Hey folks! Today I have something interesting about RESTful APIs. When you're building a RESTful API, have you ever stopped to think if what we're developing is correct and if there's a standard to follow when creating one?"
  - architecture
  - php
  - rest
  - richardson-maturity
title: Richardson Maturity Model - Measuring the maturity of your API
  - /2022/01/03/modelo-de-maturidade-de-richardson-mensurando-a-maturidade-da-sua-api/
---
Hey folks! Today I have something interesting about RESTful APIs. When you're building a RESTful API, have you ever stopped to think if what we're developing is correct and if there's a standard to follow when creating one?

There is indeed a way to know if what we're developing is a RESTful API and how mature it is — it's called the [Richardson Maturity Model](https://martinfowler.com/articles/richardsonMaturityModel.html). The first time I heard this term was on Michelli Brito's channel — I recommend following her channel. I was motivated to write a bit of my understanding on the subject, but before I begin, let me give an overview of the difference between REST and RESTful, since many devs still confuse the two terms. Without further ado, let's go.

## The difference between REST and RESTful

[REST](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) (Representational State Transfer) is an architectural style that defines a set of constraints for creating web services. RESTful, on the other hand, refers to web services that actually implement that architectural style.

## What is the Richardson Maturity Model?

Richardson created four levels that every web service should follow to be considered RESTful. There are some controversies around this. Some pragmatic developers say that if a web service implements up to level 2 it can already be considered REST; on the other hand, more purist devs say that for a web service to be considered REST, it should implement all four levels.

## Maturity levels

### Level 0

An API is at level 0 when it uses the HTTP protocol, but only uses a single HTTP method (usually POST).

Method: **POST**

URL: `http://localhost/api`

Body (JSON):

```
{
  "action": "getUser",
  "userId": 123
}
```

### Level 1 - Resources

An API is at level 1 when it uses the HTTP protocol and has well-defined URIs (resources) — as a convention, URIs should be named as nouns rather than verbs.

Method: **POST**

URL: `http://localhost/api/users/get`

Body (JSON):

```
{
  "id": 123
}
```

### Level 2 - HTTP Verbs

The API, in addition to using HTTP as the communication protocol, uses the correct semantics of its verbs and its return codes.

#### Get a user

- Method: **GET**
- URL: `http://localhost/api/users/123`

#### Create a user

- Method: **POST**
- URL: `http://localhost/api/users`
- Body (JSON):

```
{
  "name": "Diego",
  "email": "diego@example.com"
}
```

#### Update a user

- Method: **PUT**
- URL: `http://localhost/api/users/123`
- Body (JSON):

```
{
  "name": "Diego França"
}
```

#### Delete a user

- Method: **DELETE**
- URL: `http://localhost/api/users/123`

### Level 3 - Hypermedia Controls

In addition to implementing the levels above, we add HATEOAS (hypermedia) to our API to reach level 3 of maturity.

#### Get a user with HATEOAS links

- Method: **GET**
- URL: `http://localhost/api/users/123`

```
{
  "id": 123,
  "name": "Diego",
  "email": "diego@example.com",
  "_links": {
    "self": { "href": "/api/users/123" },
    "edit": { "href": "/api/users/123/edit" },
    "delete": { "href": "/api/users/123" },
    "posts": { "href": "/api/users/123/posts" }
  }
}
```

# References

[Richardson's maturity model — Martin Fowler](https://martinfowler.com/articles/richardsonMaturityModel.html)

[O que é uma api Restful na prática? Maturidade de Richardson (What is a RESTful API in practice? Richardson Maturity) — Michelli Brito on YouTube](https://www.youtube.com/watch?v=P92SBaN42mQ)

{{< adsense >}}
