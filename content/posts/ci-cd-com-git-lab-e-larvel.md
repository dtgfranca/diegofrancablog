---
_edit_last: "1"
author: diego.tg.franca@gmail.com
categories:
  - uncategorized
date: "2020-12-26T19:50:40+00:00"
draft: "true"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=332
parent_post_id: null
post_id: "332"
title: CI/CD com git lab e larvel
url: /

---
1 - passo criar o projeto laravle

2 - criar o docker file com as configuraçãoes

3 - levantar um servior remoto

4 instalar o gilab runner

5 registrar o runner token

6 fazer o docker push para gitlabhub

7 verificar se está rodando o runner no gitlab

8 - criar chaves publica e privada no computador de dev

9 - adicionar a chave pivada criada anterior em settings/cidcd/variables com o nome de SSH\_PRIVATE\_KEY o arqivo gitlab.yaml irá ler

10 - Adicionar a chave publica do pc de desenvolvimento no servidor onde será feito o deploy

11 - em settings-repostiroy - deploy key, adicionar a chave pública do servidor de deploy

Passos para criar o gitlab-cy.yml

1 -Criar o arquivo .gitlab-yaml

2 instalar o sistema para analise estatica composer require --dev vimeo/psalm

3 depois gerar um arquivo do psalm : vendor/bin/psalm --init

4 instalar plugin somente para fazer analise estática laravel: composer require --dev psalm/plugin-laravel

5 - habilitar o plugin vendor/bin/psalm-plugin enable psal/plugin-laravel

6 - no psalm.xml adicionar o leve erro 7

7 - scanear e mosrar relatório: vendor/bin/psalm --show-info=true

8 noitificaao no slack

9 criando o arquito gitla-ci.yaml

10 criar o arquivo deploy.php
