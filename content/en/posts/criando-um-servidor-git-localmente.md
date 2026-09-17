---
  card_desc: |-
    Hello everyone!


    Today I'd like to share a quick and useful tip: how to create a local Git server. Imagine this: you and your
  card_image: http://diegofranca.dev/wp-content/uploads/2020/08/q7uy4yxekcljpr70p2xk.png
  card_title: Creating a local Git server
  og_desc: |-
    Hello everyone!


    Today I'd like to share a quick and useful tip: how to create a local Git server. Imagine this: you and your
  og_image: http://diegofranca.dev/wp-content/uploads/2020/08/q7uy4yxekcljpr70p2xk.png
  og_image_alt:
  og_title: Creating a local Git server
_edit_last: "1"
_thumbnail_id: "261"
author: diego.tg.franca@gmail.com
  - tips
  - git
  - servers
  alt: q7uy4yxekcljpr70p2xk
  image: /wp-content/uploads/2020/08/q7uy4yxekcljpr70p2xk.png
date: "2024-03-16T17:15:42+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
  page-builder: {}
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=540
parent_post_id: null
post_id: "540"
summary: |-
  Hello everyone!

  Today I'd like to share a quick and useful tip: how to create a local Git server. Imagine this situation: you and your colleague are working on an important feature in the office and you need to deliver it in just a few days. Suddenly, the internet goes down — and your mobile data isn't working either. You urgently need to send the part you just developed to your colleague. Feeling that cold panic already?

  Did you know that it's possible to have a local Git server where you can clone and push without needing the internet, just using the internal network? That's exactly what I'd like to show today. Let's go!
  - git
  - php
title: Creating a local Git server
translationKey: "local-git-server"
  - /2024/03/16/criando-um-servidor-git-localmente/
---
Hello everyone!

Today I'd like to share a quick and useful tip: how to create a local Git server. Imagine this situation: you and your colleague are working on an important feature in the office and you need to deliver it in just a few days. Suddenly, the internet goes down — and your mobile data isn't working either. You urgently need to send the part you just developed to your colleague. Feeling that cold panic already?

Did you know that it's possible to have a local Git server where you can clone and push without needing the internet, just using the internal network? That's exactly what I'd like to show today. Let's go!

## Creating a bare repository

First, we need to define a repository as "bare". This means it will only contain the Git metadata needed to manage the project's versions. It's like having a central hub to share between several developers.

To do that, run the following command:

`git clone --bare /project-path /project-path-goo/project.git`

Now that the bare repository has been created, let's update the server information so that we can clone and push from our local server. Use the following command:

Now, with the bare repository created, let's update the server information so that we can run `git clone` or `git push` from our local server with this command:

`git --bare update-server-info && mv hooks/post-update.sample hooks/post-update`

**Explaining the commands:**

- `git --bare update-server-info`: Updates the server information in a bare repository. This ensures we're working with a bare repository.
- `mv hooks/post-update.sample hooks/post-update`: Moves the post-update hook sample file to the actual hook location.

Now, to verify that it actually works, just run `git clone`:

`git clone /project-path-goo/project.git`

And that's it! Now you have a local Git server ready to use, even without an internet connection.
{{< adsense >}}
