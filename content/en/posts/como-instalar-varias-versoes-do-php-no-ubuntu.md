---
  card_desc: |-
    Hey folks! Once again with another super quick and practical tutorial on how to set up multiple PHP versions on Ubuntu. Hope you enjoy.


    Sometimes
  card_image: http://diegofranca.dev/wp-content/uploads/2023/05/1_quEn9EdbO3C4IK4n4-bjxg.jpg
  card_title: How to install multiple PHP versions on Ubuntu
  og_desc: |-
    Hey folks! Once again with another super quick and practical tutorial on how to set up multiple PHP versions on Ubuntu. Hope you enjoy.


    Sometimes
  og_image: http://diegofranca.dev/wp-content/uploads/2023/05/1_quEn9EdbO3C4IK4n4-bjxg.jpg
  og_image_alt:
  og_title: How to install multiple PHP versions on Ubuntu
_edit_last: "1"
_thumbnail_id: "515"
author: diego.tg.franca@gmail.com
  - uncategorized
  alt: 1_quEn9EdbO3C4IK4n4-bjxg
  image: /wp-content/uploads/2023/05/1_quEn9EdbO3C4IK4n4-bjxg.jpg
date: "2023-05-05T16:40:00+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
  page-builder: {}
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=310
parent_post_id: null
post_id: "310"
summary: Hey folks! Once again with another super quick and practical tutorial on how to set up multiple PHP versions on Ubuntu. Hope you enjoy.
  - apache
  - php
title: How to install multiple PHP versions on Ubuntu
  - /2023/05/05/como-instalar-varias-versoes-do-php-no-ubuntu/
---
Hey folks! Once again with another super quick and practical tutorial on how to set up multiple PHP versions on Ubuntu. Hope you enjoy.

Sometimes, when we're developing our applications or working on other projects, we may run into different PHP versions than what's installed on our machine. Then we spend hours and hours on the internet looking for a solution that actually works.

This tutorial was tested on my personal machine with the following configurations:

- Ubuntu 22.04;
- 16GB of RAM;

So, without further ado, let's get to it.

Check your PHP version by running the command below:

```
php -v
PHP 7.3.24-3+ubuntu20.04.1+deb.sury.org+1 (cli) (built: Oct 31 2020 17:00:17) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.3.24, Copyright (c) 1998-2018 Zend Technologies
    with Zend OPcache v7.3.24-3+ubuntu20.04.1+deb.sury.org+1, Copyright (c) 1999-2018, by Zend Technologies
    with Xdebug v3.0.1, Copyright (c) 2002-2020, by Derick Rethans

```

The first step is to add the PPA to Ubuntu, which is maintained by Ondrej Surý. Run the following command:

```
sudo add-apt-repository ppa:ondrej/php
```

Let's update the system:

```
sudo apt update && sudo apt dist-upgrade -y
```

Now, with the PPA installed and the system updated, let's install the PHP versions we want:

**PHP 7.2**

```
sudo apt install php7.2
```

**PHP 7.3**

```
sudo apt install php7.3
```

**PHP 7.4**

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

Then, you can select the version using the `update-alternatives` command:

**PHP 7.2**

```
sudo update-alternatives --set php /usr/bin/php7.2
```

**PHP 7.4**

```
sudo update-alternatives --set php /usr/bin/php7.4
```

**PHP 8.0**

```
sudo update-alternatives --set php /usr/bin/php8.0
```

**PHP 8.1**

```
sudo update-alternatives --set php /usr/bin/php8.1
```

To select the PHP version that will work with Apache, first disable the current version with the `a2dismod` command and then enable the version you need with the `a2enmod` command:

Example of disabling PHP 7.4. If you want to disable another version, just replace 7.4 with the version you intend to disable:

```
sudo a2dismod php7.4
```

Enable the desired version:

```
sudo a2enmod php8.0
```

Let's restart Apache:

```
sudo systemctl restart apache2
```

Done — now we see the version we want. If you have any questions, leave them in the comments.

{{< adsense >}}
