---
_b2s_post_meta:
  card_desc: |-
    Olá pessoal!



    Hoje gostaria de compartilhar uma dica rápida e útil: como criar um servidor Git localmente. Imagine a seguinte situação: você e seu coleg
  card_image: http://diegofranca.dev/wp-content/uploads/2020/08/q7uy4yxekcljpr70p2xk.png
  card_title: Criando um servidor Git localmente
  og_desc: |-
    Olá pessoal!



    Hoje gostaria de compartilhar uma dica rápida e útil: como criar um servidor Git localmente. Imagine a seguinte situação: você e seu coleg
  og_image: http://diegofranca.dev/wp-content/uploads/2020/08/q7uy4yxekcljpr70p2xk.png
  og_image_alt: ""
  og_title: Criando um servidor Git localmente
_edit_last: "1"
_thumbnail_id: "261"
author: diego.tg.franca@gmail.com
categories:
  - dicas
  - git
  - servidores
cover:
  alt: q7uy4yxekcljpr70p2xk
  image: /wp-content/uploads/2020/08/q7uy4yxekcljpr70p2xk.png
date: "2024-03-16T17:15:42+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=540
parent_post_id: null
post_id: "540"
summary: |-
  Olá pessoal!

  Hoje gostaria de compartilhar uma dica rápida e útil: como criar um servidor Git localmente. Imagine a seguinte situação: você e seu colega estão desenvolvendo uma feature importante no escritório e precisam entregá-la em poucos dias. De repente, a internet cai e seus dados móveis não funcionam. Você precisa urgentemente enviar para seu colega a parte que acabou de desenvolver. Conseguem sentir o frio na barriga?

  Sabiam que é possível ter um servidor Git local onde você pode clonar e fazer push sem precisar de internet, apenas usando a rede interna? É exatamente isso que gostaria de mostrar hoje. Vamos lá!
tags:
  - git
  - php
title: Criando um servidor Git localmente
url: /2024/03/16/criando-um-servidor-git-localmente/

---
Olá pessoal!

Hoje gostaria de compartilhar uma dica rápida e útil: como criar um servidor Git localmente. Imagine a seguinte situação: você e seu colega estão desenvolvendo uma feature importante no escritório e precisam entregá-la em poucos dias. De repente, a internet cai e seus dados móveis não funcionam. Você precisa urgentemente enviar para seu colega a parte que acabou de desenvolver. Conseguem sentir o frio na barriga?

Sabiam que é possível ter um servidor Git local onde você pode clonar e fazer push sem precisar de internet, apenas usando a rede interna? É exatamente isso que gostaria de mostrar hoje. Vamos lá!

## Criando um repósitorio bare

Primeiro, precisamos definir um repositório como "bare". Isso significa que ele conterá apenas os metadados do Git necessários para gerenciar as versões do projeto. É como ter um hub central para compartilhar entre vários desenvolvedores.

Para isso, execute o seguinte comando:

` git clone --bare /caminho-do-projeto /caminho-projetoo/projeto.git`

Agora que o repositório bare foi criado, vamos atualizar as informações do servidor para permitir que possamos clonar e fazer push a partir do nosso servidor local. Use o seguinte comando:

Agora, com o repositório bare criado, vamos atualizar as informações do servidor para que possamos executar o git clone ou git push do nosso servidor local, com este comando:

`git --bare update-server-info && mv hooks/post-update.sample hooks/post-update`

**Explicando os comandos:**

- `git --bare update-server-info`: Atualiza as informações do servidor em um repositório bare. Isso garante que estejamos trabalhando em um repositório bare.
- `mv hooks/post-update.sample hooks/post-update`: Move o arquivo de amostra do hook post-update para o local real do hook.

Agora, para ver se de fato funcionou, basta executar o git clone:

`git clone /caminho-projetoo/projeto.git`

E é isso! Agora você tem um servidor Git local pronto para ser usado, mesmo sem conexão com a internet.
