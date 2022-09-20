# This image is being DEPRECATED.

See github.com/devoply/wordpress for a newer image with a proper process manager.

### OLD INFO

Full documentation for this project can be found here: http://www.wordpressdocker.com/

We also have a development container: https://github.com/etopian/alpine-php-wordpress-dev

# Lightweight WordPress PHP7 PHP-FPM7 & Nginx Docker Production Image

Lightweight Docker image for the (latest) PHP-FPM and Nginx to run WordPress based on [AlpineLinux](http://alpinelinux.org)

* Image size only ~131MB !
* Very new packages (alpine:edge) 2016-07-21:
  * [PHP](http://pkgs.alpinelinux.org/package/main/x86/php) 7.0.13
  * [Nginx](http://pkgs.alpinelinux.org/package/main/x86/nginx) nginx/1.10.2
  * Memory usage is around 50mb on a simple install.

## A simple example
### Say you want to run a single site on a VPS with Docker

```bash

mkdir -p /data/sites/etopian.com/htdocs

sudo docker run -e VIRTUAL_HOST=etopian.com,www.etopian.com -v /data/sites/etopian.com:/DATA -p 80:80 etopian/alpine-php-wordpress

```
The following user and group id are used, the files should be set to this:
User ID: 
Group ID: 

```bash
chown -R 100:101 /data/sites/etopian.com/htdocs
```

### Say you want to run a multiple WP sites on a VPS with Docker

```bash

sudo docker run -p 80:80 etopian/nginx-proxy
mkdir -p /data/sites/etopian.com/htdocs

sudo docker run -e VIRTUAL_HOST=etopian.com,www.etopian.com -v /data/sites/etopian.com:/DATA etopian/alpine-php-wordpress

mkdir -p /data/sites/etopian.net/htdocs
sudo docker run -e VIRTUAL_HOST=etopian.net,www.etopian.net -v /data/sites/etopian.net:/DATA etopian/alpine-php-wordpress
```

Populate /data/sites/etopian.com/htdocs and  /data/sites/etopian.net/htdocs with your WP files. See http://www.wordpressdocker.com if you need help on how to configure your database.

The following user and group id are used, the files should be set to this:
User ID: 
Group ID: 

```bash
chown -R 100:101 /data/sites/etopian.com/htdocs
```



### Volume structure

* `htdocs`: Webroot
* `logs`: Nginx/PHP error logs
* 

### WP-CLI

This image now includes [WP-CLI](wp-cli.org) baked in... So you can. Please `su nginx` before executing or else you can potentially compromise your host.

```
docker exec -it <container_name> bash
su nginx
cd /DATA/htdocs
wp-cli cli
```

### Multisite

For each multisite you need to give the domain as the -e VIRTUAL_HOST parameter. For instance VIRTUAL_HOST=site1.com,www.site1.com,site2.com,www.site2.com ... if you wish to add more sites you need to recreate the container.

### Upload limit

The upload limit is 2 gigabyte.

### Change php.ini value
modify files/php-fpm.conf

To modify php.ini variable, simply edit php-fpm.ini and add php_flag[variable] = value.

```
php_flag[display_errors] = on
```

Additional documentation on http://www.wordpressdocker.com

## Questions or Support

https://gitter.im/etopian/devoply

## Docker WordPress Control Panel

DEVOPly is a free hosting control panel which does everything taught in this tutorial automatically and much more, backups, staging/dev/prod, code editor, Github/Bitbucket deployments, DNS, WordPress Management. https://www.devoply.com


