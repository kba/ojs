# Install on Ubuntu 16.04

<!-- BEGIN-MARKDOWN-TOC -->
* [Install packages](#install-packages)
	* [Install mariadb](#install-mariadb)
	* [Install PHP 5.6](#install-php-56)
	* [Install PHP libs](#install-php-libs)
	* [Install Node.JS](#install-nodejs)
* [Clone repository](#clone-repository)
* [Install database](#install-database)
* [Start dev server](#start-dev-server)

<!-- END-MARKDOWN-TOC -->

## Install packages

### Install mariadb

MySQL would also work I guess.

```sh
sudo apt install mariadb-client mariadb-server
```

If newly installed, set `root` MariaDB password with

```sh
sudo mysql_secure_installation
````

### Install PHP 5.6

Default in 16.04 is PHP 7.0 which doesn't have `mysql_connect`.

```sh
add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install php5.6
```

### Install PHP libs

```sh
sudo apt install php5.6-mbstring php5.6-mcrypt php5.6-mysql php5.6-xml
```

### Install Node.JS

See [Node.JS install docs](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions)

```sh
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt update
sudo apt install -y nodejs
```

## Clone repository

```sh
git clone --recursive https://github.com/pkp/ojs
```

⛾  Go grab a coffee, this will take a while. ⛾ 

If any submodules fail to load:

```sh
git submodule update --init --recursive
```

If that still doesn't work (non-retrievable tree IDs):

```sh
git submodule foreach git fetch
```

In the repo root:

```zsh
export OJSROOT=$PWD
curl -sS https://getcomposer.org/installer | php
(cd lib/pkg; php $OJSROOT/composer.phar update)
(cd plugins/paymethod/paypal; php $OJSROOT/composer.phar update)
npm install
```


## Install database

Run `mysql -uroot -p`:

```sql
CREATE DATABASE ojs;
CREATE USER 'ojs'@'localhost' IDENTIFIED BY 'ojs';
GRANT ALL ON ojs.* TO 'ojs'@'localhost';
```

## Start dev server

```sh
php -S localhost:8888
```


