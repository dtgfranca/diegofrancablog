---
_advads_ad_settings:
  disable_ads: 0
_b2s_post_meta:
  card_desc: Fala pessoal!!! Venho trabalhando com o PHP e MySql alguns anos e nos últimos meses precisei fazer a conexão com o Oracle. Passei muito tempo pesquisando e ho
  card_image: http://diegofranca.dev/wp-content/uploads/2020/05/Php_Oracle_ImagePost.png
  card_title: Configurando o OCI8 e PDO_OCI no PHP7
  og_desc: Fala pessoal!!! Venho trabalhando com o PHP e MySql alguns anos e nos últimos meses precisei fazer a conexão com o Oracle. Passei muito tempo pesquisando e ho
  og_image: http://diegofranca.dev/wp-content/uploads/2020/05/Php_Oracle_ImagePost.png
  og_image_alt: ""
  og_title: Configurando o OCI8 e PDO_OCI no PHP7
_edit_last: "1"
_thumbnail_id: "220"
_yoast_wpseo_content_score: "60"
author: diego.tg.franca@gmail.com
categories:
  - uncategorized
cover:
  alt: Php_Oracle_ImagePost
  image: /wp-content/uploads/2020/05/Php_Oracle_ImagePost.png
date: "2020-05-07T11:44:48+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=219
parent_post_id: null
post_id: "219"
summary: Fala pessoal!!! Venho trabalhando com o PHP e MySql alguns anos e nos últimos meses precisei fazer a conexão com o Oracle. Passei muito tempo pesquisando e hoje gostaria de criar um tutorial simples para que vocês possam ter uma fonte confiável de como realizar essa instalação. Eu utilizei o Ubuntu 16.04 e o PHP 7.0.
tags:
  - oci8
  - oracle
  - pdo_oci
  - php7
title: Configurando o OCI8 e PDO_OCI no PHP7
url: /2020/05/05/configurando-o-oci8-e-pdo_oci-no-php7/

---
Fala pessoal!!! Venho trabalhando com o PHP e MySql alguns anos e nos últimos meses precisei fazer a conexão com o Oracle. Passei muito tempo pesquisando e hoje gostaria de criar um tutorial simples para que vocês possam ter uma fonte confiável de como realizar essa instalação. Eu utilizei o Ubuntu 16.04 e o PHP 7.0.

**INSTALANDO O OCI8**

Primeiramente devemos fazer o download do INSTANT ORACLE e do SDK ORACLE:  
[http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html](http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html)  
Os arquvios são instantclient-basic-linux.x64-12.2.0.1.0.zip e o instantclient-sdk-linux.x64-12.2.0.1.0.zip

Após o download , vamos criar um diretório para que possamos armazernar os arquivos que fizemos o dowload:  
`mkdir /opt/oracle`

Vamos entrar na pasta que acabamos de criar e extraimos os arquivos:  
`cd /opt/oracle
unzip instantclient-basic-linux.x64-12.2.0.1.0.zip
unzip instantclient-sdk-linux.x64-12.2.0.1.0.zip`

Próximo passo, vamos criar um link simbólico para o Instant Client:  
`ln -s /opt/oracle/instantclient_12_2/libclntsh.so.12.1 /opt/oracle/instantclient_12_2/libclntsh.so`  
`
ln -s /opt/oracle/instantclient_12_2/libocci.so.12.1 /opt/oracle/instantclient_12_2/libocci.so`

Precisamos adicionar a pasta ao nosso ldconfig:  
`echo /opt/oracle/instantclient_12_2 >/etc/ld.so.conf.d/oracle-instantclient`

E por fim, atualizamos o Update the Dynamic Linker Run-Time Bindings   
` ldconfig `

PACOTES ADICIONAIS

Para instalarmos o OCI precisamos de alguns pacotes extras

Primeiro, rode esse comando :  
`apt-get install php-dev php-pear build-essential libaio1`

Uma vez instaldo os pacotes, nós precisamos do arquivo oci8, antes precisamos de atualizar o PECL:  
`pecl channel-update pecl.php.net`

Então execute:  
`pecl install oci8`

Quando o prompt lhe pedir um caminho, digite:  
`instantclient,/opt/oracle/instantclient_12_2`

Nós precisamos dizer ao PHP para carregar o módulo OCI8:   
`echo "extension =oci8.so" >> /etc/php/7.0/fpm/php.ini
echo "extension =oci8.so" >> /etc/php/7.0/cli/php.ini
echo "extension =oci8.so" >> /etc/php/7.0/apache2/php.ini`

Também precisamos adicionar no apache as variáveis de ambiente:  
`echo "export LD_LIBRARY_PATH=/opt/oracle/instantclient_12_2" >> /etc/apache2/envvars
echo "export ORACLE_HOME=/opt/oracle/instantclient_12_2" >> /etc/apache2/envvars
echo "LD_LIBRARY_PATH=/opt/oracle/instantclient_12_2:$LD_LIBRARY_PATH" >> /etc/environment`

Reinicie o seu computador

Para chegar se a extensão foi instalado corretamente, execute:  
`php -m | grep 'oci8'`

Se no seu terminal aparecer oci8, então foi instalado corretamente

Para finalizar a instalação do oci8, basta apensar reiniciar o php-fpm:  
`service php7.0-fpm restart `

**INSTALANDO O PDO\_OCI**

Primeiramente, vamos fazer o download do fonte: [http://us1.php.net/get/php-7.0.27.tar.bz2/from/a/mirror](http://us1.php.net/get/php-7.0.27.tar.bz2/from/a/mirror)

Extraia o fonte:

`tar -jxvf7.0.27.tar.bz2`

Copie o diretório pdo\_oci para a tmp:

`sudo cp -r php-7.0.27/ext/pdo_oci /tmp`

Entre no diretório que acabamos de criar:

`sudo cd /tmp/pdo_oci`

Execute os comandos abaixo em sequência:

`sudo phpize`

`sudo ./configure -with-pdo-oci=instantclient,/opt/oracle/instantclient_12_2,12.2 `

`sudo make`

`sudo make install`

Após executar os comandos acima, crie um link simbólico:

`$ sudo touch /etc/php/7.0/mods-available/pdo_oci.ini`

`$ sudo echo extension=pdo_oci.so' > /etc/php/7.0/mods-available/pdo_oci.ini`

`$ sudo ln -s /etc/php/7.0/mods-available/pdo_oci.ini /etc/php/7.0/apache2/conf.d/20-pdo_oci.ini`

Reinicie o apache e o seu ambiente de desenvolvimento PHP já estará preparado para se conectar com o Oracle
