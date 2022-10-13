# 2008pedia
2008 Wikipedia Archive

https://2008pedia.xyz

![2008pedia logo](2008pedia.png)

# Setup Instructions
## Install MediaWiki
https://www.linode.com/docs/guides/how-to-install-mediawiki-ubuntu-2004/

#### Install Apache
```
sudo apt-get install -y apache2
```

#### Install PHP
```
sudo apt-get install -y php libapache2-mod-php php-mbstring php-mysql php-xml php-intl
```

#### Setup SQL
```
sudo apt-get install -y mariadb-server
```

```
$ sudo mysql
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 36
Server version: 10.3.34-MariaDB-0ubuntu0.20.04.1 Ubuntu 20.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>  CREATE DATABASE mediawiki;
Query OK, 1 row affected (0.001 sec)

MariaDB [(none)]>  CREATE USER 'wikiuser'@'localhost' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.003 sec)

MariaDB [(none)]>  GRANT ALL PRIVILEGES ON mediawiki.* TO 'wikiuser'@'localhost' WITH GRANT OPTION;
Query OK, 0 rows affected (0.001 sec)

MariaDB [(none)]> exit;
Bye

```

#### Download MediaWiki
```
sudo cd /var/www/html/
sudo wget https://releases.wikimedia.org/mediawiki/1.38/mediawiki-1.38.0.tar.gz
sudo tar xvzf mediawiki-1.38.0.tar.gz
rm index.html mediawiki-1.38.0.tar.gz
mv mediawiki-1.38.0/* .
rmdir mediawiki-1.38.0

```

#### Configure MediaWiki
Go to your domain name or IP address and use the MediaWiki installer. The installer will create a LocalSettings.php file that you should put in /var/www/html.


Use InstantCommons setting in LocalSettings.php to pull images from Wikipedia Commons
```
$wgUseInstantCommons = true;
```


## Download 2008 Wikipedia archive
[Torrent](enwiki-20080103_archive.torrent)
```
cd
sudo apt-get install -y transmission
wget https://github.com/argosopentech/2008pedia/raw/main/enwiki-20080103_archive.torrent
transmission-cli enwiki-20080103_archive.torrent

```

## Import xml into MediaWiki

```
cd ~/Downloads
bzip2 -d enwiki-20080103/enwiki-20080103-pages-articles.xml.bz2
php /var/www/html/maintenance/importDump.php ~/Downloads/enwiki-20080103/enwiki-20080103-pages-articles.xml

```
