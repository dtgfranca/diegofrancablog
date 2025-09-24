---
_b2s_post_meta:
  card_desc: Há algumas semanas tive a necessidade de configurar várias versões do php no servidor da empresa. Depois de muitas pesquisas eis que achei uma solução e ag
  card_image: http://diegofranca.dev/wp-content/uploads/2020/04/0_WnHaHjdJCtEGGTAV.jpg
  card_title: Configurando várias versões do PHP no Centos 7
  og_desc: Há algumas semanas tive a necessidade de configurar várias versões do php no servidor da empresa. Depois de muitas pesquisas eis que achei uma solução e ag
  og_image: http://diegofranca.dev/wp-content/uploads/2020/04/0_WnHaHjdJCtEGGTAV.jpg
  og_image_alt: ""
  og_title: Configurando várias versões do PHP no Centos 7
_edit_last: "1"
_thumbnail_id: "177"
author: diego.tg.franca@gmail.com
categories:
  - servidores
cover:
  alt: 0_WnHaHjdJCtEGGTAV
  image: /wp-content/uploads/2020/04/0_WnHaHjdJCtEGGTAV.jpg
date: "2020-04-21T17:39:30+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=176
parent_post_id: null
post_id: "176"
summary: Há algumas semanas tive a necessidade de configurar várias versões do php no servidor da empresa. Depois de muitas pesquisas eis que achei uma solução e agora vou compartilhar com vocês caso algum dia venham ter necessidade.
tags:
  - centos
  - linux
  - php
title: Configurando várias versões do PHP no Centos 7
url: /2020/04/21/configurando-varias-versoes-do-php-no-centos-7/

---
Há algumas semanas tive a necessidade de configurar várias versões do php no servidor da empresa. Depois de muitas pesquisas eis que achei uma solução e agora vou compartilhar com vocês caso algum dia venham ter necessidade.

## Instalando todos os pacotes e repositórios necessários

Os comandos a seguir irá instalar todos os pacotes necessários para a realização desse procedimento

`# yum install httpd -y
# yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
# yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
# yum install yum-utils -y
# yum install php56 -y
# yum install php72 -y
# yum install php56-php-fpm -y
# yum install php72-php-fpm -y`

## Pare o serviço dos dois servidores FPM, executando o comando a seguir:

`# systemctl stop php56-php-fpm`

`# systemctl stop php72-php-fpm`

## Por padrão os servidores escutam na porta 9000, então vamos fazé-las ouvirem em portas diferentes:

`# sed -i 's/:9000/:9056/' /etc/opt/remi/php56/php-fpm.d/www.conf`

`# sed -i 's/:9000/:9072/' /etc/opt/remi/php72/php-fpm.d/www.conf`

## Agora podemos inicar os servicos do FPM:

`# systemctl start php72-php-fpm
# systemctl start php56-php-fpm`

## Vamos abrir o arquivo /etc/httpd/php.cnf e adicionar o trecho do código abaixo:

`<Directory /var/www/html/teste/php72>
<IfModule mod_proxy_fcgi.c>
<FilesMatch \.php$>
SetHandler "proxy:fcgi://127.0.0.1:9072"
</FilesMatch>
</IfModule>
#DirectoryIndexphp
AllowOverride all
Require all granted
</Directory>`

Reinicie o servidor Apache:

`# systemctl restart httpd`

## Após reiniciar o servidor Apache iremos fazer o teste. Para isso iremos criar um arquivo php:

`mkdir -p /var/www/html/php72`

`echo "<?php phpinfo(); ?>" > /var/www/html/php72/index.php`

Ao abrir [http://127.0.0.1/php72](http://127.0.0.1/php72) você verá que o php7.2 foi instalado com sucesso.

Caso queira colocar os servidores FPM para ser iniciado junto com o boot do sistema, basta apenas executar os comandos abaixo:

`sudo systemctl enable httpd
sudo systemctl enable php56-php-fpm
sudo systemctl enable php72-php-fpm`
