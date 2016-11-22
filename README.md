[hub]: https://hub.docker.com/r/faktiva/php-redis-admin

[![SensioLabsInsight](https://insight.sensiolabs.com/projects/8f0587c9-1ed7-44fe-8a36-1bce6b50632b/small.png)](https://insight.sensiolabs.com/projects/8f0587c9-1ed7-44fe-8a36-1bce6b50632b)
[PHP Redis Admin](https://github.com/faktiva/php-redis-admin)
===

[![GitHub release](https://img.shields.io/github/release/faktiva/php-redis-admin.svg?style=flat&label=latest)](https://github.com/faktiva/php-redis-admin/releases/latest)
[![Project Status](http://opensource.box.com/badges/active.svg?style=flat)](http://opensource.box.com/badges)
[![Percentage of issues still open](http://isitmaintained.com/badge/open/faktiva/php-redis-admin.svg?style=flat)](http://isitmaintained.com/project/faktiva/php-redis-admin "Percentage of issues still open")
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/faktiva/php-redis-admin.svg?style=flat)](http://isitmaintained.com/project/faktiva/php-redis-admin "Average time to resolve an issue")
[![composer.lock](https://poser.pugx.org/faktiva/php-redis-admin/composerlock?style=flat)](https://packagist.org/packages/faktiva/php-redis-admin)
[![Dependencies Status](https://img.shields.io/librariesio/github/faktiva/php-redis-admin.svg?maxAge=3600&style=flat)](https://libraries.io/github/faktiva/php-redis-admin)
[![License](https://img.shields.io/packagist/l/faktiva/php-redis-admin.svg?style=flat)](https://tldrlegal.com/license/mit-license)

[![Docker Pulls](https://img.shields.io/docker/pulls/faktiva/php-redis-admin.svg)][hub]
[![Docker Stars](https://img.shields.io/docker/stars/faktiva/php-redis-admin.svg)][hub]
[![Docker Layers](https://images.microbadger.com/badges/image/faktiva/php-redis-admin.svg)](https://microbadger.com/images/faktiva/php-redis-admin)
[![Docker Version](https://images.microbadger.com/badges/version/faktiva/php-redis-admin.svg)](https://microbadger.com/images/faktiva/php-redis-admin)

[![Join the chat at https://gitter.im/faktiva/php-redis-admin](https://img.shields.io/badge/Gitter-CHAT%20NOW-brightgreen.svg?style=flat)](https://gitter.im/faktiva/php-redis-admin)
[![Twitter](https://img.shields.io/twitter/url/https/github.com/faktiva/php-redis-admin.svg?style=social)](https://twitter.com/intent/tweet?text=Look at this: %23Faktiva "PHP Redis Admin"&url=https://github.com/faktiva/php-redis-admin)

____

**A web interface to manage and monitor your Redis server(s).**

>    For production use the **latest stable [release](https://github.com/faktiva/php-redis-admin/releases/latest)**
>
>    This is a maintained fork of [PHPRedMin](https://github.com/sasanrose/phpredmin).
>    We are going to migrate to Symfony shortly.
>
>    _Note:_ PHP Redis Admin is mostly compatible with [phpredis](https://github.com/phpredis/phpredis) redis module for PHP

## Installation

### Docker

You can use **[docker](https://www.docker.com)** to run PHP Redis Admin:

```Bash
docker run -p 8080:80 -d --name php-redis-admin faktiva/php-redis-admin
```
And then you can just easily point your broswer to [http://localhost:8080](http://localhost:8080)

**Note:**
_You can use **ENV variables** to override any configuration directive of PHP Redis Admin._

Moreover, you can just use **docker compose** to also setup a redis container using the provided `docker-compose.yml` as a startpoint:

```Shell
docker-compose up -d
```

### Manual installation

Just drop PHP Redis Admin in your webserver's root directory and point your browser to it (You also need [phpredis](https://github.com/phpredis/phpredis) installed)

## Configuration

**You can copy `app/config/config.dist.php`to `app/config/config.php` and edit as you need. Of course you can also include the original file at the beginning, overriding only the configuration you need and retaining the distribution defaults.**

```php
// app/config/config.php

require_once __DIR__.'/config.dist.php';

$config = array_merge(
    $config,
    array(
		/*
		 * the following are your custom settings ...
		 */
        'debug' => true,
        'auth' => null,
        'log' => array(
            'driver'    => 'file',
            'threshold' => 5, /* 0: Disable Logging, 1: Error, 2: Warning, 3: Notice, 4: Info, 5: Debug */
            'file'      => array('directory' => 'var/logs')
        ),
    )
);

return $config;

```

**Note:**
_If your redis server is on an IP or port other than defaults (`localhost:6379`), you should specify it in your config file._

Apache configuration example (`/etc/httpd/conf.d/phpredmin.conf`):

```ApacheConf
# PHP Redis Admin sample apache configuration
#
# Allows only localhost by default

Alias /phpredmin /var/www/phpredmin/web

<Directory /var/www/phpredmin/>
   AllowOverride All

   <IfModule mod_authz_core.c>
     # Apache 2.4
     <RequireAny>
       Require ip localhost
       Require local
     </RequireAny>
   </IfModule>
   <IfModule !mod_authz_core.c>
     # Apache 2.2
     Order Deny,Allow
     Deny from All
     Allow from 127.0.0.1
     Allow from ::1
   </IfModule>
</Directory>
```

### Basic Authentication

By default, the dashboard is password protected using **Basic Authentication** mechanism, with the default username and password set to `admin`.

You can find the `auth` config section inside the `config.dist.php` file.

**Note:**
You **should** use the `[password_hash()](http://php.net/manual/en/function.password-hash.php)` PHP function with your desired password and store the result in the `password` config key, instead of storing the plaintext password as shown int the distributed config file.


## Features

See [Features.md](Features.md)

