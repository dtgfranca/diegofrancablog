---
  card_desc: "Hey folks!! Today I'll show you how to create self-signed Apache certificates. This is very important when we're setting up our web systems and we"
  card_image: http://diegofranca.dev/wp-content/uploads/2023/05/apache_ssl_featured.jpg
  card_title: Installing an SSL certificate on Apache
  og_desc: "Hey folks!! Today I'll show you how to create self-signed Apache certificates. This is very important when we're setting up our web systems and we"
  og_image: http://diegofranca.dev/wp-content/uploads/2023/05/apache_ssl_featured.jpg
  og_image_alt:
  og_title: Installing an SSL certificate on Apache
_edit_last: "1"
_thumbnail_id: "509"
author: diego.tg.franca@gmail.com
  - uncategorized
  alt: apache_ssl_featured
  image: /wp-content/uploads/2023/05/apache_ssl_featured.jpg
date: "2023-05-05T05:00:00+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
  page-builder: {}
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=502
parent_post_id: null
post_id: "502"
summary: "Hey folks!! Today I'll show you how to create self-signed Apache certificates. This is very important when we're setting up our web systems and want to add an SSL certificate to our web server. In this tutorial, I'm using Ubuntu 22.04."
  - apache
  - openssl
  - ssl
  - web
title: Installing an SSL certificate on Apache
  - /2023/05/05/instalando-o-certificado-ssl-no-apache/
---
Hey folks!! Today I'll show you how to create self-signed Apache certificates. This is very important when we're setting up our web systems and want to add an SSL certificate to our web server. In this tutorial, I'm using Ubuntu 22.04.

## Creating the certificate

In the first step, we'll create our certificate. Open your terminal and run the following command:

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/apache-selfsigned.key -out /etc/ssl/apache-selfsigned.crt
```

After running the command above, some information will be displayed for you to fill in:

{{< figure src="/wp-content/uploads/2023/05/image.png" alt="" caption="" >}}

Now, run the command below:

```
sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```

## Configuring SSL on Apache

To use SSL on Apache, first let's edit the `ssl-params.conf` file. To do that, run:

```
$ sudo nano /etc/apache2/conf-available/ssl-params.conf
```

Now, add the following snippet to the `ssl-params.conf` file:

```
# from https://cipherli.st/
# and https://raymii.org/s/tutorials/Strong_SSL_Security_On_Apache2.html
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

Back up the file `/etc/apache2/sites-available/default-ssl.conf` with the command:

```
$ sudo cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf.bak
```

Now, open the file:

```
$ sudo nano /etc/apache2/sites-available/default-ssl.conf
```

Change the following information:

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
     </VirtualHost>
</IfModule>
```

Change the virtual host to redirect to HTTPS automatically, with the command:

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

Apply the Apache configurations with the commands:

```
$ sudo a2enmod ssl
$ sudo a2enmod headers
$ sudo a2ensite default-ssl
$ sudo a2enconf ssl-params
$ sudo apache2ctl configtest
```

If everything is correct, this message will appear:

{{< figure src="/wp-content/uploads/2023/05/image-1.png" alt="" caption="" >}}

Now just restart Apache and run the test:

```
$ sudo systemctl restart apache2
```

{{< adsense >}}
