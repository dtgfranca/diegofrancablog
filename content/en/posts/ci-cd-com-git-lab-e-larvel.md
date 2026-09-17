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
title: CI/CD with GitLab and Laravel
---
1 - First step: create the Laravel project

2 - Create the Dockerfile with the configurations

3 - Spin up a remote server

4 - Install the GitLab runner

5 - Register the runner token

6 - Push the Docker image to GitLab

7 - Check that the runner is running on GitLab

8 - Generate public and private keys on the dev machine

9 - Add the private key created earlier in Settings > CI/CD > Variables with the name SSH_PRIVATE_KEY — the .gitlab-ci.yml file will read it

10 - Add the public key from the dev machine to the server where the deploy will run

11 - In Settings > Repository > Deploy Keys, add the public key from the deploy server

Steps to create the .gitlab-ci.yml:

1 - Create the .gitlab-ci.yml file

2 - Install the static analysis tool: `composer require --dev vimeo/psalm`

3 - Then generate the Psalm config file: `vendor/bin/psalm --init`

4 - Install the Laravel-only static analysis plugin: `composer require --dev psalm/plugin-laravel`

5 - Enable the plugin: `vendor/bin/psalm-plugin enable psalm/plugin-laravel`

6 - In psalm.xml, set the error level to 7

7 - Scan and show the report: `vendor/bin/psalm --show-info=true`

8 - Slack notification

9 - Creating the .gitlab-ci.yml file

10 - Creating the deploy.php file
