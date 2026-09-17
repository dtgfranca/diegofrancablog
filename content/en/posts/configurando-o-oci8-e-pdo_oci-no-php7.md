---
categories:
  - uncategorized
cover:
  alt: Php_Oracle_ImagePost
  image: /wp-content/uploads/2020/05/Php_Oracle_ImagePost.png
date: "2020-05-07T11:44:48+00:00"
tags:
  - oci8
  - oracle
  - pdo_oci
  - php7
title: "Configuring OCI8 and PDO_OCI on PHP 7"
aliases:
  - /2020/05/05/configurando-o-oci8-e-pdo_oci-no-php7/

---
Hey folks!!! I've been working with PHP and MySQL for some years now, and in the last few months I needed to connect to Oracle. I spent a lot of time researching, and today I'd like to put together a simple tutorial so you can have a reliable source on how to do this installation. I used Ubuntu 16.04 and PHP 7.0.

**INSTALLING OCI8**

First we need to download INSTANT ORACLE and the ORACLE SDK:
[http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html](http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html)
The files are `instantclient-basic-linux.x64-12.2.0.1.0.zip` and `instantclient-sdk-linux.x64-12.2.0.1.0.zip`.

After downloading, let's create a directory to store the files we just downloaded:

`mkdir /opt/oracle`

Let's go into the folder we just created and extract the files:

```
cd /opt/oracle
unzip instantclient-basic-linux.x64-12.2.0.1.0.zip
unzip instantclient-sdk-linux.x64-12.2.0.1.0.zip
```

Next, let's create a symbolic link for the Instant Client:

```
ln -s /opt/oracle/instantclient_12_2/libclntsh.so.12.1 /opt/oracle/instantclient_12_2/libclntsh.so
ln -s /opt/oracle/instantclient_12_2/libocci.so.12.1 /opt/oracle/instantclient_12_2/libocci.so
```

We need to add the folder to our `ldconfig`:

`echo /opt/oracle/instantclient_12_2 >/etc/ld.so.conf.d/oracle-instantclient`

And finally, update the Dynamic Linker Run-Time Bindings:

`ldconfig`

ADDITIONAL PACKAGES

To install OCI we need some extra packages.

First, run this command:

`apt-get install php-dev php-pear build-essential libaio1`

Once these packages are installed, we need the oci8 file. First, update PECL:

`pecl channel-update pecl.php.net`

Then run:

`pecl install oci8`

When the prompt asks for a path, type:

`instantclient,/opt/oracle/instantclient_12_2`

We need to tell PHP to load the OCI8 module:

```
echo "extension =oci8.so" >> /etc/php/7.0/fpm/php.ini
echo "extension =oci8.so" >> /etc/php/7.0/cli/php.ini
echo "extension =oci8.so" >> /etc/php/7.0/apache2/php.ini
```

We also need to add the environment variables to Apache:

```
echo "export LD_LIBRARY_PATH=/opt/oracle/instantclient_12_2" >> /etc/apache2/envvars
echo "export ORACLE_HOME=/opt/oracle/instantclient_12_2" >> /etc/apache2/envvars
echo "LD_LIBRARY_PATH=/opt/oracle/instantclient_12_2:$LD_LIBRARY_PATH" >> /etc/environment
```

Restart your computer.

To check that the extension was installed correctly, run:

`php -m | grep 'oci8'`

If `oci8` shows up in your terminal, it was installed correctly.

To finish the OCI8 installation, just restart php-fpm:

`service php7.0-fpm restart`

**INSTALLING PDO_OCI**

First, download the source: [http://us1.php.net/get/php-7.0.27.tar.bz2/from/a/mirror](http://us1.php.net/get/php-7.0.27.tar.bz2/from/a/mirror)

Extract the source:

`tar -jxvf 7.0.27.tar.bz2`

Copy the `pdo_oci` directory to `/tmp`:

`sudo cp -r php-7.0.27/ext/pdo_oci /tmp`

Enter the directory we just created:

`cd /tmp/pdo_oci`

Run the following commands in sequence:

```
sudo phpize
sudo ./configure --with-pdo-oci=instantclient,/opt/oracle/instantclient_12_2,12.2
sudo make
sudo make install
```

After running the commands above, create a symbolic link:

```
$ sudo touch /etc/php/7.0/mods-available/pdo_oci.ini
$ sudo echo extension=pdo_oci.so > /etc/php/7.0/mods-available/pdo_oci.ini
$ sudo ln -s /etc/php/7.0/mods-available/pdo_oci.ini /etc/php/7.0/apache2/conf.d/20-pdo_oci.ini
```

Restart Apache and your PHP development environment will be ready to connect to Oracle.

{{< adsense >}}
