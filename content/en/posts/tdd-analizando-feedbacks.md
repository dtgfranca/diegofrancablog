---
categories:
  - uncategorized
cover:
  alt: TDD
  image: /wp-content/uploads/2021/03/TDD.jpg
date: "2021-03-25T21:13:14+00:00"
title: "TDD - Analyzing Feedback"
aliases:
  - /2021/03/05/tdd-analizando-feedbacks/

---
Lately I've been studying TDD in depth and how it can help us write good code.

Many developers still haven't adopted this practice — some because they lack knowledge, others because they think they lose productivity when writing tests before development.

In this article I'll base myself on the book written by Mauricio Aniche, [Test-Driven Development: Testing and Design in the Real World with PHP](https://www.casadocodigo.com.br/products/livro-tdd-php), where he exemplifies some of the feedbacks that the practice of TDD can give us to help write good code.

## What is TDD?

The acronym TDD (Test-Driven Development) means test-driven development. It's a development method that is very popular these days.

TDD is based on the principle that tests are written before the implementation, going through a repetition cycle until you arrive at a simple solution.

{{< figure src="/wp-content/uploads/2021/03/img-tdd.png" alt="" caption="" >}}

To start with TDD it's recommended that the programmer pick an automated test suite (PHPUnit, JUnit, etc.). You should create unit tests for each method of a class to test all of its behavior.

Unit tests aim to test a class in isolation, without any interference from other classes.

To write a good unit test, we should follow a standard:

- Create our test data builders
- Create our setup methods so we don't repeat code
- Create tests with meaningful names
- Create good assertions

The practice of TDD has an advantage: it can indicate that the design of our class isn't great. It can point out high coupling and a lack of cohesion in our classes.

For TDD to help us improve our code writing, it's important to emphasize the programmer's experience with object orientation and concepts like SOLID and design patterns.

## TDD and Coupling

Symptoms:

- The abusive use of mock objects created to test a single class indicates that the tested class depends on many other classes and that makes it fragile, showing that the class is highly coupled.
- The creation of mock objects that aren't used in some test methods is another important feedback. This generally happens when the class is highly coupled, and the result of one dependency's action doesn't interfere with another. When this happens, the programmer ends up writing sets of tests where some deal with a subset of the mocks, while other tests deal with another subset. That indicates high coupling in the class, which needs to be refactored.
- When the developer starts the test and realizes that the public interface of the class isn't friendly, it may indicate that the current abstraction isn't clear enough and could be improved.
- The lack of abstraction generally also means that a simple change needs to be made in different places in the code. When a change happens and the programmer is forced to make the same change in different tests, it indicates a lack of proper abstraction to avoid unnecessary code repetition.
- Likewise, the programmer may notice the same thing when starting to create repeated tests for different entities.

## TDD and Encapsulation

Symptoms:

- Tests that deal too much with other objects instead of dealing with the object under test may be warning the developer about encapsulation problems. Not following the Law of Demeter, both in tests and in production code, can also warn about the same problems. This is very common in tests of anemic classes. An anemic model is one where classes contain only attributes or only methods.
- Classes that contain only attributes represent entities, while other classes, which contain only methods, perform actions on them. This kind of design should be avoided as much as possible.

## When not to use TDD

Generally when developers already have a good command of what they're going to implement, or when something is tied to infrastructure, like SQL code, for example. But don't forget — even if you don't write the test before development, you should create tests after the implementation. Another case that doesn't require tests is for getters and setters.

## Bibliography

- Test-Driven Development: By Example — Kent Beck
- Growing Object-Oriented Software, Guided by Tests
- Agile Software Development: Principles, Patterns, and Practices
- Test-Driven Development: Testing and Design in the Real World with PHP
