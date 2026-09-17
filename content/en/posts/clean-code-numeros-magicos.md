---
  card_desc: "Sometimes we think that to refactor a code and make it more readable we need to do something complex, but that's not always the case — sometimes"
  card_image: http://diegofranca.dev/wp-content/uploads/2021/01/clean-code-1-728.jpg
  card_title: Clean Code - Magic Numbers
  og_desc: "Sometimes we think that to refactor a code and make it more readable we need to do something complex, but that's not always the case — sometimes"
  og_image: http://diegofranca.dev/wp-content/uploads/2021/01/clean-code-1-728.jpg
  og_image_alt:
  og_title: Clean Code - Magic Numbers
_edit_last: "1"
_thumbnail_id: "345"
author: diego.tg.franca@gmail.com
  - uncategorized
  alt: clean-code-1-728
  image: /wp-content/uploads/2021/01/clean-code-1-728.jpg
date: "2021-01-26T14:23:27+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
  page-builder: {}
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=339
parent_post_id: null
post_id: "339"
summary: "Sometimes we think that to refactor a code and make it more readable we need to do something complex, but that's not always the case — sometimes just renaming a variable to a name that matches what it really does is already a big step."
  - clean-code
  - code-smell
  - php
title: Clean Code - Magic Numbers
  - /2021/01/26/clean-code-numeros-magicos/
---
Sometimes we think that to refactor a code and make it more readable we need to do something complex, but that's not always the case — sometimes just renaming a variable to a name that matches what it really does is already a big step.

Last weekend, I was studying TDD and decided to write a simple login code. In that algorithm there were some HTTP response status codes — 400, 401, 403, 422, and so on — that I had added directly into the code. Then I thought: "Would someone who doesn't know HTTP status codes know what this means?"

With that in mind, I started thinking about how to solve it, and I remembered something I had read in *Clean Code* about eliminating magic numbers. According to Robert Martin, this should be avoided in your code because it leads to bugs and makes the code harder to understand.

For those unfamiliar with the term, a magic number is one of those numbers we put in our code that requires an explanation to understand why it's there.

To fix this code smell, you should use constants to represent those values.

In the first image I show how the code looked with the magic numbers.

{{< figure src="/wp-content/uploads/2021/01/1.jpeg" alt="" caption="" >}}

I created a new class where I defined some constants to represent the response codes:

{{< figure src="/wp-content/uploads/2021/01/2.jpeg" alt="" caption="" >}}

Then I swapped the numbers for the constants, and you can see how much the code's readability improved:

{{< figure src="/wp-content/uploads/2021/01/3-1.jpeg" alt="" caption="" >}}

{{< adsense >}}
