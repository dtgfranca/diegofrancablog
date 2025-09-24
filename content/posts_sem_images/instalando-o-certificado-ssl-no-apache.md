---
_b2s_post_meta:
  card_desc: Fala pessoal!! Hoje, vou ensinar como criar certificados apache auto assinado. Isso é muito importante quando estamos criando nossos sistemas web e queremos ad
  card_image: http://diegofranca.dev/wp-content/uploads/2023/05/apache_ssl_featured.jpg
  card_title: Instalando o certificado ssl no apache
  og_desc: Fala pessoal!! Hoje, vou ensinar como criar certificados apache auto assinado. Isso é muito importante quando estamos criando nossos sistemas web e queremos ad
  og_image: http://diegofranca.dev/wp-content/uploads/2023/05/apache_ssl_featured.jpg
  og_image_alt: ""
  og_title: Instalando o certificado ssl no apache
_edit_last: "1"
_thumbnail_id: "509"
author: diego.tg.franca@gmail.com
categories:
  - uncategorized
cover:
  alt: apache_ssl_featured
  image: /wp-content/uploads/2023/05/apache_ssl_featured.jpg
date: "2023-05-05T05:00:00+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=502
parent_post_id: null
post_id: "502"
summary: Fala pessoal!! Hoje, vou ensinar como criar certificados apache auto assinado. Isso é muito importante quando estamos criando nossos sistemas web e queremos adicionar um certificado ssl no nosso servidor web. Nesse tutorial, estou utilizando Ubuntu 22.04.
tags:
  - apache
  - openssl
  - ssl
  - web
title: Instalando o certificado ssl no apache
url: /2023/05/05/instalando-o-certificado-ssl-no-apache/

---
Fala pessoal!! Hoje, vou ensinar como criar certificados apache auto assinado. Isso é muito importante quando estamos criando nossos sistemas web e queremos adicionar um certificado ssl no nosso servidor web. Nesse tutorial, estou utilizando Ubuntu 22.04.

## Criar certificado

No primeiro passo, iremos criar o nosso certficado. Abra o seu terminal e execute o seguinte comando:

```
sudo openssl req -x509  -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/apache-selfsigned.key -out /etc/ssl/apache-selfsigned.crt
```

Após executar o comando acima, algumas informações serão exibidas para que você preencha:

{{< figure src="/wp-content/uploads/2023/05/image.png" alt="" caption="" >}}

Agora, execute o comando abaixo:

```
 sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```

## Configurar o ssl no apache

Para usar o SSL no apache, primeiro vamos editar o arquivo ssl-params.conf, para isso execute o comando:

```
$ nano /etc/apache2/conf-available/ssl-params.conf
```

Agora, adicione o seguinte trecho de código ao arquivo `ssl-params.conf`:

```
#from https://cipherli.st/
#and https://raymii.org/s/tutorials/Strong_SSL_Security_On_Apache2.html
SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH
SSLProtocol All -SSLv2 -SSLv3
SSLHonorCipherOrder On
# Disable preloading HSTS for now. You can use the commented out header line that includes
# the "preload" directive if you understand the implications.

#Header always set Strict-Transport-Security "max-age=63072000; includeSubdomains; preload"
Header always set Strict-Transport-Security "max-age=63072000; includeSubdomains"
Header always set X-Frame-Options DENY
Header always set X-Content-Type-Options nosniff
# Requires Apache >= 2.4
SSLCompression off
SSLSessionTickets Off
SSLUseStapling on
SSLStaplingCache "shmcb:logs/stapling-cache(150000)"
SSLOpenSSLConfCmd DHParameters "/etc/ssl/certs/dhparam.pem"
```

Faça backup do arquivo /etc/apache2/sites-available/default-ssl.conf com o comando:

```
 $ sudo cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf.bak
```

Agora, abra o arquivo:

```
$ sudo nano /etc/apache2/sites-available/default-ssl.conf
```

Altere as informações a seguir:

```
<IfModule mod_ssl.c>
    <VirtualHost _default_:443>
        ServerAdmin your_email@example.com
        ServerName server_domain_or_IP
        DocumentRoot /var/www/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
        SSLEngine on
        SSLCertificateFile /etc/ssl/apache-selfsigned.crt
        SSLCertificateKeyFile  /etc/ssl/apache-selfsigned.key
        <FilesMatch "\.(cgi|shtml|phtml|php)$">
            SSLOptions +StdEnvVars
        </FilesMatch>
        <Directory /usr/lib/cgi-bin>
            SSLOptions +StdEnvVars
        </Directory>
        BrowserMatch "MSIE [2-6]" \
            nokeepalive ssl-unclean-shutdown \
            downgrade-1.0 force-response-1.0
     </VirtualHost
</IfModule>

```

Altere o virtual host para encaminhar para HTTPS automaticamente,com o comando:

```
$ sudo nano /etc/apache2/sites-available/000-default.conf
```

```
<VirtualHost *:80>
    . . .
    Redirect "/" "https://your_domain_or_IP/"
    . . .
</VirtualHost>
```

Aplique as configurações no apache com os comandos:

```
$ sudo a2enmod ssl
$ sudo a2enmod headers
$ sudo a2ensite default-ssl
$ sudo a2enconf ssl-params
$ sudo apache2ctl configtest
```

Se tudo estiver corrreto, vai aparecer essa mensagem:

{{< figure src="/wp-content/uploads/2023/05/image-1-1024x60.png" alt="" caption="" >}}

Agora, basta apenas reiniciar o apache e fazer o teste:

```
$ sudo systemctl restart apache2
```
