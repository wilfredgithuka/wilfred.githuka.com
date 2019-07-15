---
title: "Serving Your Wordpress Blog on Caddy on Linode Server"
date: 2017-10-16T09:16:15+03:00
subtitle: "Some information of first time users of Caddy+Wordpress+Linode"
tags: [Caddy, Wordpress, Linode, Archlinux]
---
![image](/img/linux/caddy.jpeg)
After fiddling around and some long hours setting up my server, I managed to 
install Wordpress on Caddy.For those who have not used Caddy before, you can 
read more about it on [Caddyserver](https://caddyserver.com). 

Its awesome since it gives you a https (security) for your domain. Caddy is 
praised by industry experts for security defaults and unpararelleld usability.

### Take Note

To make this tutorial easier to follow, I will first point out my biggest 
issues which you need to take care as you go forth:

* File permissions - know who gets what permissions
* Sytemctl - starting and stopping services
* Check /var/log/php5-fpm.log for any errors.
* Add errors visible to your Caddyfile
* Often times, php-fpm doesn't work because of wrong permissions. Check the 
error logs and change the user in /etc/php5/fpm/pool.d/www.conf
* Switching to a Unix socket might help. Change the listen directive in /etc/
php5/fpm/pool.d/www.conf to listen = unix:/var/run/php5-fpm.sock and adjust 
your Caddyfile accordingly.
* If using a unix socket, make sure Caddy has access to the socket file.

###  What is php-fpm

PHP-FPM (FastCGI Process Manager) is an alternative PHP FastCGI implementation with some additional features useful for sites of any size, especially busier sites. It was not designed with virtual hosting in mind (large amounts of pools) however it can be adapted for any usage model.

###  What is fastcgi

FastCGI is a programming interface that can speed up Web applications that use the most popular way to have the Web server call an application.

### Post Installation

After installing Caddy, go to the caddy file and check whats inside:

* sudo nano /etc/caddy/caddy.conf.d

The start the caddy service

* sudo systemctl start caddy

Now to check what permissions you should give your wordpress folder, use the
following command:

* cat /etc/php/php-fpm.d/www.conf |less

Inside this file you should scroll down and see the following:

* user = http
* group = http

sudo systemctl start php-fpm

Retart your machine. After reboot start and check the status of caddy

* sudo systemctl start caddy
* sudo systemctl status caddy


### Caddy File Examples

The following examples are for Wordpress and Hugo. You can adapt them to
the site you are working on:

#### Wordpress

www.ruarakabaptist.org, ruarakabaptist.org 
{
root /srv/http/rbc/public
#fastcgi / /run/php-fpm/php-fpm.sock php
index index.html
#errors /tmp/error.log
}

#### Hugo

www.conac.co.ke, conac.co.ke {
        gzip
        root /srv/http/conac/wordpress
        fastcgi / /run/php-fpm/php-fpm.sock php
        # fastcgi / 127.0.0.1:9000 php
        errors visible
        # log access.log
        # errors error.log
        rewrite {
                if {path} not_match ^\/wp-admin
                to {path} {path}/ /index.php?_url={uri}
    }
}



Your website should be working well now, served on a clean https



