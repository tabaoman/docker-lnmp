# docker-compose for LNMPR

## Intro
docker-compose
* PHP: 7.4, with most-common extensions
* MySQL: 5.7
* nginx: latest
* redis: 5.1

## Before Installation
**Volumn:** Map the working folder to WEBROOT (See in php service in docker-compose.yml)
**MySQL Users:** Set database, user/password and root password (See in mysql service in docker-compose.yml)
**Redis Password:** Specify in command (See in redis service in docker-compose.yml)

## After Installation
**MySQL**
```shell
$ docker exec -it mysql mysql -uroot -proot123
```
```mysql
USE mysql;
UPDATE `user` SET `host`='%' WHERE `user`='root' AND `host`='"%"';
GRANT ALL PRIVILEGES ON *.* TO 'homestead';
FLUSH PRIVILEGES;
```

## Installation

1.  `git clone https://github.com/tabaoman/docker-compose-lnmp.git lnmp`
2.  `cd lnmp/docker-compose`
3.  `docker-compose build`
4.  `docker-compose up -d`

## Known Issue and Fix
**Error: Sub-process /usr/bin/dpkg returned an error code (1)**
Login the php images with docker. For example:
```shell
docker exec -it ced0a7d1661ac0235717f9995cc91c3e47e7d03912be9ebec13ef0a68e354b4d /bin/sh
```
```shell
cd /etc/apt/sources.list.d 
rm nodesource.list
apt-get --fix-broken install
apt-get update
apt-get remove nodejs
apt-get remove nodejs-doc
curl -fsSL https://deb.nodesource.com/setup_16.x | bash
apt-get install -y nodejs
```
