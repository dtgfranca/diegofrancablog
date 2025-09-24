---
_b2s_post_meta:
  card_desc: Venho compartilhar com vocês uma dica rápida sobre o Laravel. Vejo muitas pessoas enfrentando problemas ao tentar acessar variáveis de ambiente dentro da apl
  card_image: http://diegofranca.dev/wp-content/uploads/2025/06/laravel.png
  card_title: Pare de usar env() dentro da sua aplicação Laravel (fora da config)
  og_desc: Venho compartilhar com vocês uma dica rápida sobre o Laravel. Vejo muitas pessoas enfrentando problemas ao tentar acessar variáveis de ambiente dentro da apl
  og_image: http://diegofranca.dev/wp-content/uploads/2025/06/laravel.png
  og_image_alt: ""
  og_title: Pare de usar env() dentro da sua aplicação Laravel (fora da config)
_edit_last: "1"
_thumbnail_id: "601"
author: diego.tg.franca@gmail.com
categories:
  - frameworks
  - php
cover:
  alt: laravel
  image: /wp-content/uploads/2025/06/laravel.png
date: "2025-06-18T18:13:36+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=598
parent_post_id: null
pms-content-restrict-custom-non-member-redirect-url: ""
pms-content-restrict-custom-redirect-url: ""
pms-content-restrict-message-logged_out: ""
pms-content-restrict-message-non_members: ""
pms-content-restrict-type: default
post_id: "598"
summary: Venho compartilhar com vocês uma dica rápida sobre o Laravel. Vejo muitas pessoas enfrentando problemas ao tentar acessar variáveis de ambiente dentro da aplicação. O erro mais comum acontece quando os desenvolvedores utilizam a função `env()` diretamente em suas classes ou serviços, para ler configurações do arquivo `.env`, e depois não entendem por que, em alguns momentos, essa função retorna `null`.
tags:
  - laravel
  - php
title: Pare de usar env() dentro da sua aplicação Laravel (fora da config)
url: /2025/06/18/pare-de-usar-env-dentro-da-sua-aplicacao-laravel-fora-da-config/

---
Venho compartilhar com vocês uma dica rápida sobre o Laravel. Vejo muitas pessoas enfrentando problemas ao tentar acessar variáveis de ambiente dentro da aplicação. O erro mais comum acontece quando os desenvolvedores utilizam a função `env()` diretamente em suas classes ou serviços, para ler configurações do arquivo `.env`, e depois não entendem por que, em alguns momentos, essa função retorna `null`.

A explicação é simples: isso acontece por causa do fluxo de inicialização do Laravel. Para ajudar a visualizar, criei um diagrama que explica como esse processo funciona:


{{< gallery cols="1" >}}  
{{< figure src="/wp-content/uploads/2025/06/ChatGPT-Image-18-de-jun.-de-2025-14%5F31%5F46-683x1024.png" alt="" caption="" >}}  
{{< /gallery >}}  

Como podemos ver na imagem acima, quando o Laravel recebe uma request (ou executa um comando, job, etc.), ele inicia pelo arquivo `index.php`, que chama o `bootstrap/app.php`. Nesse momento, o Laravel carrega as variáveis do arquivo `.env` e, logo em seguida, lê os arquivos de configuração presentes no diretório `config/`. Essas configurações são então armazenadas em cache (caso você utilize o comando `php artisan config:cache`).

Após esse ponto, os Service Providers são registrados e o Kernel da aplicação assume o controle da execução. Por isso, **não é recomendado utilizar `env()` para acessar configurações após essa etapa**, pois o Laravel já não dependerá mais do `.env` diretamente durante o ciclo de vida da aplicação.

**Errado (não recomendado fora da config/):**

```
env('CHAVE')
```

**Certo:**

```
config('configuracao.chave')

```

Seguindo esse padrão, você evita problemas com `null` e garante que sua aplicação seja compatível com o cache de configuração.
