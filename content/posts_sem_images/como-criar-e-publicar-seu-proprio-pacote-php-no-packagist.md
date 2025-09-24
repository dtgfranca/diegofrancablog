---
_b2s_post_meta:
  card_desc: 'Olá pessoal! Hoje quero compartilhar com vocês como criar e publicar pacotes PHP no Packagist. Você já criou um código PHP reutilizável e queria instalar '
  card_image: http://diegofranca.dev/wp-content/uploads/2025/06/private-packagist-for-vendors.png
  card_title: Como criar e publicar seu próprio pacote PHP no Packagist
  og_desc: 'Olá pessoal! Hoje quero compartilhar com vocês como criar e publicar pacotes PHP no Packagist. Você já criou um código PHP reutilizável e queria instalar '
  og_image: http://diegofranca.dev/wp-content/uploads/2025/06/private-packagist-for-vendors.png
  og_image_alt: ""
  og_title: Como criar e publicar seu próprio pacote PHP no Packagist
_edit_last: "1"
_thumbnail_id: "631"
_wp_old_date: "2025-06-25"
author: diego.tg.franca@gmail.com
categories:
  - dicas
  - php
cover:
  alt: private-packagist-for-vendors
  image: /wp-content/uploads/2025/06/private-packagist-for-vendors.png
date: "2025-06-26T00:41:10+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=593
parent_post_id: null
pms-content-restrict-custom-non-member-redirect-url: ""
pms-content-restrict-custom-redirect-url: ""
pms-content-restrict-message-logged_out: ""
pms-content-restrict-message-non_members: ""
pms-content-restrict-type: default
post_id: "593"
summary: Olá pessoal! Hoje quero compartilhar com vocês como criar e publicar pacotes PHP no Packagist. Você já criou um código PHP reutilizável e queria instalar em outro projeto sem a necessidade de ficar duplicando código e até compartilhar com a comunidade PHP?
tags:
  - composer
  - engenharia-e-software
  - packagist
  - php
title: Como criar e publicar seu próprio pacote PHP no Packagist
url: /2025/06/26/como-criar-e-publicar-seu-proprio-pacote-php-no-packagist/

---
Olá pessoal! Hoje quero compartilhar com vocês como criar e publicar pacotes PHP no Packagist. Você já criou um código PHP reutilizável e queria instalar em outro projeto sem a necessidade de ficar duplicando código e até compartilhar com a comunidade PHP?

Então, hoje vou criar um simples pacote e ensiná-los como publicar no packagist. O pacote que vou criar vai ser algo bem simples, um pacote que soma dois números e retorna o valor soma.

Neste tutorial, você vai aprender como:

- Criar a estrutura de um pacote PHP.
- Usar o Composer para gerenciar dependências.
- Publicar no [Packagist.org](https://packagist.org/).

## Estrutura inicial do projeto

Crie a estrutura de diretórios do seu pacote. Aqui está um exemplo básico:

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

## Configurando o Composer

Dentro da pasta do projeto, inicialize o `composer.json` com:

```
composer init
```

Esse comando inicia um assistente interativo. Preencha as informações solicitadas, como:

**Nome**: `seunome/pacote-exemplo`

**Descrição**: Uma breve descrição do que o pacote faz.

**Tipo**: Geralmente "library".

**Licença**: Ex: MIT

**Dependências**: Pressione Enter para pular se não tiver dependências ainda.

Ao final, o Composer gerará o `composer.json`, com esse abaixo:

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

## **Escrevendo o código do pacote**

No diretório `src/`, crie a classe principal do seu pacote.

_src/Calculadora.php_

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

## Adicionando testes (opcional, mas recomendado)

Crie testes no diretório `tests/` com o PHPUnit.

_tests/CalculadoraTest.php_

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

Instale o PHPUnit se ainda não tiver:

```
composer require --dev phpunit/phpunit
```

E rode os testes com:

```
vendor/bin/phpunit
```

## Publicando o nosso pacote no packagist

Agora que subimos para o git, vamos acessar o packagist.org. Ao acessar será mostrado a tela:

{{< figure src="/wp-content/uploads/2025/06/image-1-1024x459.png" alt="" caption="" >}}

1. Clique no menu "Submit" localizado na parte superior direita
1. Adicione o link do repositório do pacote criado
1. Clique em "Check"

{{< figure src="/wp-content/uploads/2025/06/image-5-1024x402.png" alt="" caption="" >}}

Clique em "Submit" e seu pacote já se encontra no packagist para instalação:

{{< figure src="/wp-content/uploads/2025/06/image-6-1024x402.png" alt="" caption="" >}}

## Dicas adicionais

- Se o pacote estiver com `"minimum-stability": "dev"`, adicione também `"prefer-stable": true` no `composer.json`.
- Faça **tag (versão)** no GitHub (ex: `v1.0.0`) para que o Packagist reconheça versões estáveis.
- Inclua um `README.md` claro com instruções de uso.
- Adicione uma **licença** (por exemplo, `LICENSE` com conteúdo da MIT).

Link do repositório:

[https://github.com/dtgfranca/package-soma](https://github.com/dtgfranca/package-soma)
