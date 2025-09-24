---
_b2s_post_meta:
  card_desc: As vezes pensamos que para refatorar um código e torná-lo mais legível precisamos de fazer algo complexo, mas nem sempre isso é necessário, as vezes trocar
  card_image: http://diegofranca.dev/wp-content/uploads/2021/01/clean-code-1-728.jpg
  card_title: Clean Code - Números mágicos
  og_desc: As vezes pensamos que para refatorar um código e torná-lo mais legível precisamos de fazer algo complexo, mas nem sempre isso é necessário, as vezes trocar
  og_image: http://diegofranca.dev/wp-content/uploads/2021/01/clean-code-1-728.jpg
  og_image_alt: ""
  og_title: Clean Code - Números mágicos
_edit_last: "1"
_thumbnail_id: "345"
author: diego.tg.franca@gmail.com
categories:
  - uncategorized
cover:
  alt: clean-code-1-728
  image: /wp-content/uploads/2021/01/clean-code-1-728.jpg
date: "2021-01-26T14:23:27+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=339
parent_post_id: null
post_id: "339"
summary: As vezes pensamos que para refatorar um código e torná-lo mais legível precisamos de fazer algo complexo, mas nem sempre isso é necessário, as vezes trocar um nome de uma variável para um nome que condiz com o que ela realmente faz, já é um grande passo.
tags:
  - clean-code
  - code-smell
  - php
title: Clean Code - Números mágicos
url: /2021/01/26/clean-code-numeros-magicos/

---
As vezes pensamos que para refatorar um código e torná-lo mais legível precisamos de fazer algo complexo, mas nem sempre isso é necessário, as vezes trocar um nome de uma variável para um nome que condiz com o que ela realmente faz, já é um grande passo.

No último final de semana, estava estudando sobre TDD e resolvi desenvolver um código simples de login , nesse algoritmo tinha alguns códigos de status de resposta como 400, 401, 403, 422 e etc, que eu tinha adicionado diretamente no código. Logo pensei: "Será se alguém que não tenha conhecimento de códigos de status de resposta saberia o que isso significa?"

Com isso na cabeça foi então que comecei a pensar em como resolver e me lembrei de algo que tinha lido no Clean Code sobre eliminar números mágicos e segundo Robert Martin isso deve-se ser evitado no seu código, pois provoca bugs e dificuldades no entendimento do código.

Para quem não conhece esse termo, o número mágico são aqueles númerso que colocamos no nosso código e precisa de uma explicação para entender o porquê deles estarem ali.

Para resolver esse code smells deve-se utillizar constantes para representar esses valores.

Nessa primeira imagem eu mostro como o código estava com os números mágicos.

{{< figure src="/wp-content/uploads/2021/01/1.jpeg" alt="" caption="" >}}

Criei uma nova classe onde defini algumas constantes para representar os códigos de resposta:

{{< figure src="/wp-content/uploads/2021/01/2.jpeg" alt="" caption="" >}}

Depois troquei os números pelas constantes e pode-se ver o quanto melhorou o entendimento do código:

{{< figure src="/wp-content/uploads/2021/01/3-1.jpeg" alt="" caption="" >}}
