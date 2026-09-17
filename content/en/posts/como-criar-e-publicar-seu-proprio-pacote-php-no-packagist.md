---
categories:
  - tips
  - php
cover:
  alt: private-packagist-for-vendors
  image: /wp-content/uploads/2025/06/private-packagist-for-vendors.png
date: "2025-06-26T00:41:10+00:00"
tags:
  - composer
  - software-engineering
  - packagist
  - php
title: "How to create and publish your own PHP package on Packagist"
aliases:
  - /2025/06/26/como-criar-e-publicar-seu-proprio-pacote-php-no-packagist/

---
Hello everyone! Today I want to share with you how to create and publish PHP packages on Packagist. Have you ever written reusable PHP code and wanted to install it in another project without duplicating it — and even share it with the PHP community?

So today I'll create a simple package and show you how to publish it on Packagist. The package I'll create will be something very simple — a package that adds two numbers and returns the sum.

In this tutorial, you'll learn how to:

- Create the structure of a PHP package.
- Use Composer to manage dependencies.
- Publish on [Packagist.org](https://packagist.org/).

## Initial project structure

Create your package's directory structure. Here's a basic example:

```
package-soma/
├── src/
│   └── Calculadora.php
├── tests/
│   └── CalculadoraTest.php
├── composer.json
├── composer.lock
└── phpunit.xml

```

## Configuring Composer

Inside the project folder, initialize `composer.json` with:

```
composer init
```

This command starts an interactive wizard. Fill in the requested information, such as:

**Name**: `yourname/example-package`

**Description**: A short description of what the package does.

**Type**: Usually "library".

**License**: E.g. MIT

**Dependencies**: Press Enter to skip if you don't have any dependencies yet.

At the end, Composer will generate a `composer.json` like the one below:

```
{
    "name": "dtgfranca/package-soma",
    "require": {
        "phpunit/phpunit": "^12.2"
    },
    "autoload": {
        "psr-4": {
            "Dtgfranca\\PackageSoma\\": "src/"
        }
    },
    "authors": [
        {
            "name": "Diego França",
            "email": "diego.tg.franca@gmail.com"
        }
    ]
}
```

## **Writing the package code**

In the `src/` directory, create the main class of your package.

`src/Calculadora.php`

```
<?php

namespace DtfFranca\PackageSoma;

class Calculadora
{
    public function somar(int $a, int $b): int
    {
        return $a + $b;
    }
}

```

## Adding tests (optional but recommended)

Create tests in the `tests/` directory with PHPUnit.

`tests/CalculadoraTest.php`

```
<?php

use PHPUnit\Framework\TestCase;
use DtfFranca\PackageSoma\Calculadora;

class CalculadoraTest extends TestCase
{
    public function testSomar()
    {
        $calc = new Calculadora();
        $this->assertEquals(4, $calc->somar(2, 2));
    }
}
```

Install PHPUnit if you don't have it yet:

```
composer require --dev phpunit/phpunit
```

And run the tests with:

```
vendor/bin/phpunit
```

## Publishing our package on Packagist

Now that we've pushed to git, let's go to packagist.org. When you access it, you'll see this screen:

{{< figure src="/wp-content/uploads/2025/06/image-1.png" alt="" caption="" >}}

1. Click on the "Submit" menu in the top-right corner.
2. Add the link to your package's repository.
3. Click "Check".

{{< figure src="/wp-content/uploads/2025/06/image-5.png" alt="" caption="" >}}

Click "Submit" and your package will be available on Packagist for installation:

{{< figure src="/wp-content/uploads/2025/06/image-6.png" alt="" caption="" >}}

## Additional tips

- If the package has `"minimum-stability": "dev"`, also add `"prefer-stable": true` to `composer.json`.
- **Tag a version** on GitHub (e.g. `v1.0.0`) so Packagist recognizes stable versions.
- Include a clear `README.md` with usage instructions.
- Add a **license** (for example, a `LICENSE` file with the MIT contents).

Repository link:

[https://github.com/dtgfranca/package-soma](https://github.com/dtgfranca/package-soma)

{{< adsense >}}
