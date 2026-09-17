---
categories:
  - php
cover:
  alt: social-banner
  image: /wp-content/uploads/2021/03/social-banner.png
date: "2021-03-27T20:03:37+00:00"
title: "Best Practices with PHP (PSR) — Part 1"
aliases:
  - /2021/03/27/boas-praticas-com-php-psr-parte-1/

---
Hey folks, how are you doing? Today I'm bringing you something new for those of you who program in PHP: I'll start a series where I'll show you the best practices in PHP development according to the PSRs. Without further ado, let's begin.

## What is a PSR?

PSR (PHP Standards Recommendation) is the recommendation manual for PHP. The site that defines these recommendations is [PHP-FIG](https://www.php-fig.org/), where we find all the PSRs we'll use throughout this series.

In my opinion, the main PSRs every PHP programmer should know are PSR-1, which deals with basic coding standards; PSR-12, which covers the coding style guide (previously PSR-2); and PSR-4, which deals with how to define autoloads. The other PSR specifications are also important, but they're for more specific topics — for example, PSR-6 deals with caching.

In this series we'll focus on PSR-1, PSR-4, and PSR-12. If you want me to cover the other PSRs, leave a comment!

## PSR-1: Basic Coding Standard

### 1 - Overview

- Files must only use `<?php` or `<?=` to start PHP code.
- Your editor should be configured to use UTF-8 without BOM to encode PHP files.
- Files should not declare classes, functions, constants, etc., or do anything that could cause side effects.
- Namespaces and classes must follow the autoloading described in PSR-4.
- Class names must be declared in [StudlyCaps](https://en.wikipedia.org/wiki/Studly_caps).
- Constants must be declared in uppercase and separated with underscores.
- Method names must be declared in [camelCase](https://en.wikipedia.org/wiki/Camel_case).

### 2 - Files

#### 2.1 - PHP tags

Code written in PHP must use the full `<?php ?>` tag or the short echo tag `<?= ?>`; no other variants should be used.

#### 2.2 - Character encoding

Code written in PHP must use only UTF-8 encoding, without BOM.

#### 2.3 - Side effects

A file SHOULD declare new symbols (classes, functions, constants, etc.) without causing side effects, or it should execute only logic with side effects, but MUST NOT do both.

The expression "side effects" means the execution of logic not directly related to declaring classes, functions, constants, etc., simply by including the file.

"Side effects" include, but are not limited to: generating output, explicit use of `require` or `include`, connecting to external services, modifying `.ini` settings, emitting errors or exceptions, modifying static or global variables, reading and writing to a file, and so on.

Below is an example of a file with declarations and side effects — an example that should be avoided:

{{< figure src="/wp-content/uploads/2021/03/efeito-colateral.png" alt="" caption="" >}}

### 3 - Namespaces and class names

Namespaces and classes MUST follow PSR-4 autoloading, which we'll cover in the next part of this series.

This means each class should be in its own file and in a namespace of at least one level.

Class names must be declared in StudlyCaps.

Code written in PHP 5.3 or later MUST make formal use of namespaces.

Example:

{{< figure src="/wp-content/uploads/2021/03/namespaces.png" alt="" caption="" >}}

### 4 - Class constants, properties, and methods

The term "class" refers to all classes, interfaces, and traits.

#### 4.1 - Constants

Class constants MUST be declared in all uppercase and separated with underscores, as shown in the code below:

{{< figure src="/wp-content/uploads/2021/03/constantes.png" alt="" caption="" >}}

#### 4.2 - Properties

The PSR guide deliberately avoids any recommendation regarding property naming: `$StudlyCaps`, `$camelCase`, or `$under_score`.

Any naming convention SHOULD be used and applied consistently within a given scope.

#### 4.3 - Methods

Method names MUST be declared in camelCase().

{{< adsense >}}
