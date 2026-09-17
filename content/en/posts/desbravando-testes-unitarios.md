---
categories:
  - php
  - testing
cover:
  alt: system-bug
  image: /wp-content/uploads/2023/02/system-bug.jpg
date: "2023-02-17T20:23:38+00:00"
tags:
  - software-engineering
  - php
  - testing
  - unit-tests
title: "Demystifying Unit Tests"
aliases:
  - /2023/02/17/desbravando-testes-unitarios/

---
The idea for this post came up after I gave a presentation on unit tests at the company I work for. During the presentation, I did a live code in which I created an endpoint using the concepts I'll cover here, in order to isolate the component. I would love to build an application right here on the blog, but doing a step-by-step might get a bit tedious. So I decided to summarize what was presented, with code examples for better understanding.

## **What is a unit test?**

A unit test consists of testing the smallest part of the code we're developing — in our case, our methods. It's not very reliable on its own, because we only test our logic and don't test the integration between the system's components.

Some questions I see about unit tests are: how can I test only a part of the code when it depends on an interface or a specific class?

To achieve that level of isolation, we have some concepts we can use:

## Stub

We create a test double with the expected results, so we can simulate our specific cases.

In this example I created a class called `PessoaFisica`:

![](https://lh5.googleusercontent.com/uhCC9Orx_rM21Uy7S6Nz6wdukUC2NwWehoptD3NvLr453FcyGZmHx7TGnyEu219czoZWXZTZVZRCMzmvt53xw1xsGAiZyU_W28sctmXEo7QTUqPQRauEkvLMRHeQ0YA6Gk0MnOgsHjzbqF04zX6fKaHMJw=nw)

With the help of Laravel's Mockery library, we create a stub for the `buscaDadosPorCpf` method, with the expected return:

![](https://lh5.googleusercontent.com/LBna4KPerA-DV99AwplJobx-IZCOrS0o1RG7OPCrLEbZdRTaIg7upZJ7AlU7x1xX0N92RHRMlk0OX2bI_QE3aGEyJKU0ZcYNjPVqcQsKuG_W0I--0NAtX_C5phS09gdRxfL85OPOqq6Alw3l01BCFhJC-A=nw)

## Mock

It has the same characteristics as a stub, but we can also make assertions about its behavior, ensuring that a method will or won't be called.

In this example, in addition to defining an output for the method, we also want to know its behavior. In the test below, we pass the method `times(1)`, which tells us the method must be called once:

![](https://lh6.googleusercontent.com/CVG--I8zJDNsxMG1CoOH2QccmNEw89QB5tG2TiXD7mxcGxer_x1mKued6kHYOcq-lxvIaAKVNLnU-ulIF_-4YlaHTIVr0ujGTseOEq6F-QPLAuk5p-z8rVxjXj1XyJNlHkZ468FYeJgnMIkFRwcCLq6ELg=nw)

## Dummies

A dummy is an object we create in the test for which we don't need to define a return or make assertions about behavior — it only serves to satisfy a parameter of a class or method.

In the figure below, we have a dependency on `cep` (zip code) in our `PessoaFisica` class. Even though we don't use it in the method we're going to test, it has an impact when we instantiate the class, because we must satisfy that dependency:

![](https://lh4.googleusercontent.com/bxMrL8wjbvlUTZK59ghLst2bcc5Mp50Js10rY_TY81ucdhfNPWCTW6VUeMIEOGikk_DqOytEV2Ney9gAgOYX3i7_byOW3yWXGSy2sA-9RMOIOGRCqTtqTz7LGk4_WGP6aGGl8_BtcmWvHh8NVE0UNyQ2JA=nw)

So we create the dummy to satisfy what's required in the class's constructor: `$cep = \Mockery::mock(Cep::class)`. With the dummy created, we can simply pass it in the constructor:

![](https://lh4.googleusercontent.com/vurAp1eAv6yf4O6lofqAA_Ssx7Eaa7RMgldWGsgaIkTyEOL8ZsnvX6JBra9024fZNiYjqcuzlN0TVQMkLtmaTyekBV4wJVairYkf2kI1mQi0o5Qjwf4C64s5YK6k-S0w-8yRVwYhgMW6uF8t0FBCyADk_A=nw)

## Spies

The goal of spies is to make assertions about a method call, instead of making assertions about the object's behavior.

To illustrate, I'll create a class called `UsuarioService`:

{{< figure src="/wp-content/uploads/2023/02/spies-class.png" alt="" caption="" >}}

We can create a test to verify whether the `criarUsuario` method is called with the correct arguments:

{{< figure src="/wp-content/uploads/2023/02/teste-criar-usuario.png" alt="" caption="" >}}

With Mockery, we create a spy for the `UsuarioService` class. Then, the `criarUsuario` method is called with the arguments `"Diego França"` and `"diego@example.com"`. Finally, the `shouldHaveReceived` method is used to verify that the `criarUsuario` method was called once with the same arguments.

## Fake

Fakes have the same functionality as a real class, but they're used only in tests. An example of a fake is a database: we can create a method like `salvar` (save), but save only in memory (in an array). This way, we get the functionality of saving, but only at that moment.

To illustrate, I created a `repository` for saving a record to the database, but we don't want our application to actually hit the database.

{{< figure src="/wp-content/uploads/2023/02/repository-t2este-1.png" alt="" caption="" >}}

To build the fake, I'll use an array where the data will be stored in the computer's memory:

{{< figure src="/wp-content/uploads/2023/02/testefake.png" alt="" caption="" >}}

## Conclusion

The first time you write a unit test, you might think that test serves no purpose, since many times we're emulating generated data. But I'd like to share a personal experience: a unit test won't guarantee your application won't break — it only shows that your algorithm has no errors. That's why it's EXTREMELY important to apply other types of tests, like _end to end_ and _exploratory testing_ (not covered in this article), since those actually ensure the system as a whole works correctly.

Another tip for those just starting out and who want to write good tests is to follow this step-by-step that can serve as a baseline:

- Create test data builders (to create input data for our tests).
- Create our setup methods to avoid repeating code (`tearDown` and `setUp`).
- Create tests with meaningful names.
- Create good assertions.

All of these concepts are available in every programming language.

I hope this article can help you in some way. If you have any questions or critiques (always welcome), leave them in the comments.

{{< adsense >}}
