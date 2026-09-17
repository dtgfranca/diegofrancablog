---
categories:
  - uncategorized
cover:
  alt: "21184018666362"
  image: /wp-content/uploads/2021/07/21184018666362.jpg
date: "2021-07-18T13:37:58+00:00"
tags:
  - scalability
  - heroku
  - k6
  - php
  - load-testing
  - testing
title: "Building a scalable application — Part 2"
aliases:
  - /2021/07/18/criando-aplicacao-escalavel-parte-2/

---
Hey folks! How's it going? Continuing our journey of building a scalable application, in this second part I'll tell you how the beginning of the tests went, [if you haven't read the first part, click here](/2021/07/04/criando-aplicacao-escalavel-parte-1/).

At first I tried to run the load-testing tool [K6](https://k6.io/) against the application running on my personal machine. I started with 1000 users hitting it simultaneously and got only 2% success. When I tried with 2000 users, I started getting a **"socket: too many open files"** error. For comparison purposes in this test I'll stick with 1000 both on my machine and on the Heroku server. I created an account on [Heroku](https://www.heroku.com/), whose configurations aren't very robust, but as the tests progress I might switch plans to do a better test.

Heroku machine configurations:

RAM: 2 GB | CPUs: 2

Configurations of the machine where I'll run the load-testing tool:

RAM: 8 GB | SSD: 480 GB | CPU: 8 cores | Processor: Core i5 8th Gen | OS: Ubuntu 20.1

## Test results with the application running on my machine

{{< figure src="/wp-content/uploads/2021/07/WhatsApp-Image-2021-07-18-at-9.25.54-AM.jpeg" alt="" caption="" >}}

Now let's analyze the local test report:

I created an assertion to check how many requests would return with a 200 status. In this case, out of 2525 requests, only 2% returned with success status; we had 97% failures and the average requests per second was 42.80/s. K6 started the test with a minimum of 154 virtual users and a maximum of 1000.

## Test results with the application running on the Heroku server

{{< figure src="/wp-content/uploads/2021/07/WhatsApp-Image-2021-07-18-at-9.45.02-AM.jpeg" alt="" caption="" >}}

Analyzing the Heroku results:

The test was similar to the previous one. In this case, out of the 2643 requests K6 made to the URL, all returned with status 200 — no failures like we had on my machine. The average requests per second was 56.69/s, so we already noticed an improvement. K6 started the tests with a minimum of 39 virtual users and a maximum of 1000 virtual users.

I tried to bump it up to 2000 virtual users, but I got the error **"failed to load system roots and no roots provided"**. I'm not sure if that error is due to my free plan — I'll try to verify so that in the next test I can increase the number of virtual users.

### Wrapping up

We already noticed the difference between the two servers. In this second part we managed to do our first test against our goal of 900 requests per second — for now, we maxed out at 56 requests per second.

The next step will be to study horizontal and vertical scalability. In this first test we could see that our server is still very weak; maybe it's best to increase the memory, which will require upgrading the Heroku plan. I'll try to study a bit more about this service. I'm not yet sure what to do, but let's keep going and learning together on this long journey…

If you're curious to know more about K6 metrics in depth, here's the link to the documentation: https://k6.io/docs/using-k6/metrics/

{{< adsense >}}
