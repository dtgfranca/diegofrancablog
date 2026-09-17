---
  disable_ads: 0
  card_desc: "Hey folks! Today I want to start my journey learning how to build scalable applications. I've always been curious about how these big companies work"
  card_image: http://diegofranca.dev/wp-content/uploads/2021/07/21184018666362.jpg
  card_title: Building a scalable application — Part 1
  og_desc: "Hey folks! Today I want to start my journey learning how to build scalable applications. I've always been curious about how these big companies work"
  og_image: http://diegofranca.dev/wp-content/uploads/2021/07/21184018666362.jpg
  og_image_alt:
  og_title: Building a scalable application — Part 1
_edit_last: "1"
_thumbnail_id: "391"
author: diego.tg.franca@gmail.com
  - uncategorized
  alt: "21184018666362"
  image: /wp-content/uploads/2021/07/21184018666362.jpg
date: "2021-07-18T13:38:10+00:00"
enclosure: |-
  https://diegofranca.dev/wp-content/uploads/2021/07/encurtador-link-convert-video-online.com_.mp4
  1062260
  video/mp4
fw:opt:ext:pb:page-builder:json: '[]'
  page-builder: {}
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=384
parent_post_id: null
post_id: "384"
summary: "Hey folks! Today I want to start my journey learning how to build scalable applications. I've always been curious about how these big companies handle thousands of simultaneous accesses while keeping their services online, and what it would be like to work with scalability in applications. Thinking about that, I created a URL shortener and my goal is to learn more about scalability and to run load tests on applications."
  - scalability
  - k6
  - testing
  - load-testing
title: Building a scalable application — Part 1
  - /2021/07/04/criando-aplicacao-escalavel-parte-1/
---
Hey folks! Today I want to start my journey learning how to build scalable applications. I've always been curious about how these big companies handle thousands of simultaneous accesses while keeping their services online, and what it would be like to work with scalability in applications. Thinking about that, I created a URL shortener and my goal is to learn more about scalability and to run load tests on applications.

My first goal is to handle at least 900 requests per second, and to do that I'll use [https://k6.io](https://k6.io/) to run the tests, and Heroku (free plan) as the server. Once I reach that number of requests, I'll double it. I want to log each experiment here on the blog, as it might be useful for someone out there.

Feel free to share ideas or tool suggestions for running the load tests.

## Demo video of the application

## Code repository

[https://github.com/dtgfranca/encurtador-link](https://github.com/dtgfranca/encurtador-link)

{{< adsense >}}
