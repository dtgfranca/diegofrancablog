---
_b2s_post_meta:
  card_desc: |-
    Falaaa Galera! Novamente com mais um tutorial super rápido e prático de como configurar  várias versões do PHP no Ubuntu. Esperem que gostem.







    Às vez
  card_image: http://diegofranca.dev/wp-content/uploads/2023/05/1_quEn9EdbO3C4IK4n4-bjxg.jpg
  card_title: Como instalar várias versões do PHP no ubuntu
  og_desc: |-
    Falaaa Galera! Novamente com mais um tutorial super rápido e prático de como configurar  várias versões do PHP no Ubuntu. Esperem que gostem.







    Às vez
  og_image: http://diegofranca.dev/wp-content/uploads/2023/05/1_quEn9EdbO3C4IK4n4-bjxg.jpg
  og_image_alt: ""
  og_title: Como instalar várias versões do PHP no ubuntu
_edit_last: "1"
_thumbnail_id: "515"
author: diego.tg.franca@gmail.com
categories:
  - uncategorized
cover:
  alt: 1_quEn9EdbO3C4IK4n4-bjxg
  image: /wp-content/uploads/2023/05/1_quEn9EdbO3C4IK4n4-bjxg.jpg
date: "2023-05-05T16:40:00+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=310
parent_post_id: null
post_id: "310"
summary: Falaaa Galera! Novamente com mais um tutorial super rápido e prático de como configurar várias versões do PHP no Ubuntu. Esperem que gostem.
tags:
  - apache
  - php
title: Como instalar várias versões do PHP no ubuntu
url: /2023/05/05/como-instalar-varias-versoes-do-php-no-ubuntu/

---
Falaaa Galera! Novamente com mais um tutorial super rápido e prático de como configurar várias versões do PHP no Ubuntu. Esperem que gostem.

Às vezes, quando estamos desenvolvendo nossas aplicações ou trabalhando em outros projetos, podemos nos deparar com versões diferentes do PHP que está instalado na nossa máquina. Então, passamos horas e horas na internet em busca de alguma solução que realmente funcione.

Esse tutorial foi testado na minha máquina pessoal com as seguintes configurações:

- Ubuntu 22.04;
- 16GB de memória ram;

Então, sem mais delongas bora para a prática.

Verifique a sua versão do php, execute o comando abaixo:

```
php -v
PHP 7.3.24-3+ubuntu20.04.1+deb.sury.org+1 (cli) (built: Oct 31 2020 17:00:17) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.3.24, Copyright (c) 1998-2018 Zend Technologies
    with Zend OPcache v7.3.24-3+ubuntu20.04.1+deb.sury.org+1, Copyright (c) 1999-2018, by Zend Technologies
    with Xdebug v3.0.1, Copyright (c) 2002-2020, by Derick Rethans

```

O primeiro passo é adicionar o PPA no Ubuntu que é mantido pelo Ondrej Surý . Execute o seguinte comando:

```
sudo add-apt-repository ppa:ondrej/php
```

Vamos atualizar o sistema:

```
sudo apt update && sudo apt dist-upgrade -y
```

Agora, com o ppa instalado e o sistema atualizado, vamos instalar as versões do php que desejamos:

**PHP 7.2**

```
sudo apt install php7.2
```

**PHP 7.3**

```
sudo apt install php7.3
```

**PHP** **7.4**

```
sudo apt install php7.4
```

**PHP 8.0**

```
sudo apt install php8.0
```

**PHP 8.1**

```
sudo apt install php8.1
```

Então, você pode selecionar a versão através do comando ` update-alternatives`:

**PHP 7.2**

```
sudo update-alternatives –set php /usr/bin/php7.2
```

**PHP 7.4**

```
sudo update-alternatives –set php /usr/bin/php7.4
```

**PHP 8.0**

```
sudo update-alternatives –set php /usr/bin/php8.0
```

**PHP 8.1**

```
sudo update-alternatives –set php /usr/bin/php8.1
```

Para selecionar a versão do PHP que irá trabalhar com o Apache, primeiro desabilite a versão atual com o comando `a2dismod` e depois habilite a versão que precisa com o comando `a2enmod`:

Exemplo de como desabilitar o php 7.4. Caso queira desabilitar outra versão é so subistituir o 7.4 pela versão que pretende desabilitar:

```
sudo a2dismod php7.4
```

Habilitar a versão desejada:

```
sudo a2enmod php8.0
```

Vamos reiniciar o apache:

```
sudo systemctl restart apache2
```

Pronto, agora vemos a versão que desejamos. Caso tenha alguma dúvida deixe nos comentários.
