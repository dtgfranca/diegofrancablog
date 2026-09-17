---
categories:
  - servers
cover:
  alt: 0_WnHaHjdJCtEGGTAV
  image: /wp-content/uploads/2020/04/0_WnHaHjdJCtEGGTAV.jpg
date: "2020-04-21T17:39:30+00:00"
tags:
  - centos
  - linux
  - php
title: "Setting up multiple PHP versions on CentOS 7"
aliases:
  - /2020/04/21/configurando-varias-versoes-do-php-no-centos-7/

---
A few weeks ago I needed to set up multiple PHP versions on the company server. After a lot of research, I found a solution, and now I'll share it with you in case you ever need to do this.

## Installing all required packages and repositories

The commands below will install all the packages needed for this procedure:

```
# yum install httpd -y
# yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
# yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
# yum install yum-utils -y
# yum install php56 -y
# yum install php72 -y
# yum install php56-php-fpm -y
# yum install php72-php-fpm -y
```

## Stop the two FPM servers by running the following commands:

```
# systemctl stop php56-php-fpm
# systemctl stop php72-php-fpm
```

## By default, the servers listen on port 9000, so let's make them listen on different ports:

```
# sed -i 's/:9000/:9056/' /etc/opt/remi/php56/php-fpm.d/www.conf
# sed -i 's/:9000/:9072/' /etc/opt/remi/php72/php-fpm.d/www.conf
```

## Now we can start the FPM services:

```
# systemctl start php72-php-fpm
# systemctl start php56-php-fpm
```

## Let's open the file /etc/httpd/php.conf and add the snippet below:

```
<Directory /var/www/html/teste/php72>
<IfModule mod_proxy_fcgi.c>
<FilesMatch \.php$>
SetHandler "proxy:fcgi://127.0.0.1:9072"
</FilesMatch>
</IfModule>
#DirectoryIndexphp
AllowOverride all
Require all granted
</Directory>
```

Restart the Apache server:

```
# systemctl restart httpd
```

## After restarting Apache, we'll run the test. To do that we'll create a PHP file:

```
mkdir -p /var/www/html/php72
echo "<?php phpinfo(); ?>" > /var/www/html/php72/index.php
```

When you open [http://127.0.0.1/php72](http://127.0.0.1/php72), you'll see that PHP 7.2 was installed successfully.

If you want the FPM servers to start with the system boot, just run the commands below:

```
sudo systemctl enable httpd
sudo systemctl enable php56-php-fpm
sudo systemctl enable php72-php-fpm
```

{{< adsense >}}
