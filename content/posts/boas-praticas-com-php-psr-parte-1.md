---
_b2s_post_meta:
  card_desc: Falaa galera, como vocês estão? Hoje eu venho com uma novidade para vocês que programam em php, vou criar uma série onde eu vou mostrar quais são as melhor
  card_image: http://diegofranca.dev/wp-content/uploads/2021/03/social-banner.png
  card_title: Boas práticas com PHP (PSR) Parte-1
  og_desc: Falaa galera, como vocês estão? Hoje eu venho com uma novidade para vocês que programam em php, vou criar uma série onde eu vou mostrar quais são as melhor
  og_image: http://diegofranca.dev/wp-content/uploads/2021/03/social-banner.png
  og_image_alt: ""
  og_title: Boas práticas com PHP (PSR) Parte-1
_edit_last: "1"
_thumbnail_id: "372"
author: diego.tg.franca@gmail.com
categories:
  - php
cover:
  alt: social-banner
  image: /wp-content/uploads/2021/03/social-banner.png
date: "2021-03-27T20:03:37+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=336
parent_post_id: null
post_id: "336"
summary: Falaa galera, como vocês estão? Hoje eu venho com uma novidade para vocês que programam em php, vou criar uma série onde eu vou mostrar quais são as melhores práticas no densenvolvimento em php de acordo com as PSRs. Sem mais delongas, vamos iniciar.
title: Boas práticas com PHP (PSR) Parte-1
url: /2021/03/27/boas-praticas-com-php-psr-parte-1/

---
Falaa galera, como vocês estão? Hoje eu venho com uma novidade para vocês que programam em php, vou criar uma série onde eu vou mostrar quais são as melhores práticas no densenvolvimento em php de acordo com as PSRs. Sem mais delongas, vamos iniciar.

## O que é PSR ?

PSR(PHP Standards Recomendation) é o manual de recomendações para o PHP, o site que define essas recomendações é o [PHP-FIG](https://www.php-fig.org/), nele encontramos todas as PSRs que iremos utilizar nessa série.

Na minha opinião as principais PSRs que todo programador PHP deve saber é a PSR-1 que trata sobre padrões de códigos , PSR-12 que trata do guia de estilo do código(antes era a PSR-2) e a PSR-4 que trata de como definir os autoloads. As outras especificações da PSR também são importante, mas são para assuntos muito específicos, como por exemplo a PSR -6 que trata de caching .

Nessa série iremos focar na PSR-1, PSR-4 e na PSR-12. Caso vocês queiram que eu aborde as outras PSRs deixe nos comentários

## PSR-1: Padrão de código básico

### 1 - Visão Geral

- Arquivos devem inicar tags somente com o <?php ou <?=.
- O seu editor deve ser configurado para utilizar somente o UTF8 sem bom para codificar em php;
- Arquivos não devem declarar classes, funções, constantes e etc, ou fazer algo que possa gerar efeitos colaterais;
- Namespaces e classes devem seguir um autoloading descrito na PSR4;
- Nome de classes devem ser declaradas no estilo [SutdlyCaps](https://pt.wikipedia.org/wiki/Studly_caps)
- Constantes devem ser declaradas em upper case e separados com undescore
- Nome de metódos devem ser declarados em [camelCase](https://pt.wikipedia.org/wiki/CamelCase#:~:text=CamelCase%20%C3%A9%20a%20denomina%C3%A7%C3%A3o%20em,defini%C3%A7%C3%B5es%20de%20classes%20e%20objetos.)

### 2 - Arquivos

#### 2.1 - PHP tags

O código escrito em php deve-se usar a tag completa <?php ?> ou uma tag curta <?= ?>; não devem usar outras variantes

### 2.2 - Codificação de caracteres

O código escrito em php deve-se usar somente a codificação UTF-8 sem o BOM.

#### 2.3 Efeitos colaterais

Um arquivo DEVE declarar novos símbolos(classes, funções, constantes, etc.) sem causar efeitos colaterais, ou deveria executar apenas a lógica com efeitos colaterais, mas NÃO DEVE fazer ambos.

A expressão "Efeitos colaterais" significa a execução da lógica não diretamente relacionada a declaração de classes, funções, constantes, etc., simplesmente incluindo o arquivo.

"Efeitos colaterais" incluem, mas não estão limitados a: geração de output, uso explícito do " _require_" ou " _include_", conectando à serviços externos, modificando configurações no arquivo .ini, emitindo erros ou exceções, modificando variáveis estáticas ou globais, ler e escrever em um arquivo, e por aí vai.

A seguir exemplo de um arquivo com declarações e efeitos colaterais; um exemplo que deve ser evitado:

{{< figure src="/wp-content/uploads/2021/03/efeito-colateral.png" alt="" caption="" >}}

### 3 - Namespaces e nome de classes

Namespaces e classes DEVEM seguir o "autoloading" PRS-4, iremos abordar em na próxima parte dessa série.

Isso significa que cada classe deve estar em seu próprio arquivo e em um namespace de pelo menos um nível.

Nomes de classes devem ser declaradas em StudyCaps.

Código escrito em php 5.3 ou superior DEVE fazer o uso formal de namespaces.

Exemplo:

{{< figure src="/wp-content/uploads/2021/03/namespaces.png" alt="" caption="" >}}

### 4 - Classes de constantes, Propriedades e Métodos

O termo "classe" refere-se a todas classes, interfaces, e traits.

#### 4.1 - Constantes

Classes de constantes DEVEM ser declaradas todas em upper case e separadas com underscore, como mostra no código abaixo:

{{< figure src="/wp-content/uploads/2021/03/constantes.png" alt="" caption="" >}}

#### 4.2 Propriedades

No guia das PSR's evita-se a recomendação de qualquer uso com relação ao nome de propriedades: $StudlyCaps, $camelCase, $under\_score.

Qualquer convenção de nomenclatura DEVE ser usada e aplicada de forma consistente dentro de um escopo.

#### 4.3 - Metódos

Nomes de métodos DEVEM ser declarados em camelCase().
