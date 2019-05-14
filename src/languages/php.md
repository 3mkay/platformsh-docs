# PHP Support

<!-- toc -->

PHP is a popular scripting language designed especially for the web. It currently powers over 80% of websites.

<html>
   <head>
      <title>PHP Supported Versions</title>
      <script type = "text/javascript" src = "/scripts/images/helpers.js" ></script>
   </head>
   <body>
   <h2>Supported versions</h2>
   <div id = 'phpSupported'></div>
   <script>
   makeList(json, "runtimes", "php", "supported", "phpSupported");
   </script>
   </body>
</html>


Note that as of PHP 7.1 we use the Zend Thread Safe (ZTS) version of PHP.

To select a PHP version, specify a `type` such as `php:7.3`:

```yaml
# .platform.app.yaml
type: "php:7.3"
```

<html>
   <head>
      <title>PHP Deprecated Versions</title>
      <script type = "text/javascript" src = "/scripts/images/listTest.js" ></script>
   </head>
   <body>
   <h3>Deprecated versions</h3>
   <p>The following versions are available but are not receiving security updates from upstream, so their use is not recommended. They will be removed at some point in the future.</p>
   <div id = 'phpDeprecated'></div>
   <script>
   makeList(json, "services", "php", "deprecated", "phpDeprecated");
   </script>
   </body>
</html>

## Support libraries

While it is possible to read the environment directly from your application, it is generally easier and more robust to use the [`platformsh/config-reader`](https://github.com/platformsh/config-reader-php) Composer library which handles decoding of service credential information for you.

## Alternate start commands

PHP is most commonly run in a CGI mode, using PHP-FPM. That is the default on Platform.sh. However, you can also start alternative processes if desired, such as if you're running an Async PHP daemon, a thread-based worker process, etc. To do so, simply specify an alternative start command in `platform.app.yaml`, similar to the following:

```yaml
web:
    commands:
        start: php run.php
    upstream:
            socket_family: tcp
            protocol: http
```

The above configuration will execute the `run.php` script in the application root when the container starts using the PHP-CLI SAPI, just before the deploy hook runs, but will *not* launch PHP-FPM. It will also tell the front-controller (Nginx) to connect to your application via a TCP socket, which will be specified in the `PORT` environment variable. Note that the start command _must_ run in the foreground.

If not specified, the effective default start command varies by PHP version:

* On PHP 5.x, it's `/usr/sbin/php5-fpm`.
* On PHP 7.0, it's `/usr/sbin/php-fpm7.0`.
* On PHP 7.1, it's `/usr/sbin/php-fpm7.1-zts`.
* On PHP 7.2, it's `/usr/sbin/php-fpm7.2-zts`.
* On PHP 7.3, it's `/usr/sbin/php-fpm7.3-zts`.

While you can call it manually that is generally not necessary. Note that PHP-FPM cannot run simultaneously along with another persistent process (such as ReactPHP or Amp). If you need both they will have to run in separate containers.

## Debug PHP-FPM

If you want to inspect what's going on with PHP-FPM, you can install this [small CLI](https://github.com/wizaplace/php-fpm-status-cli):

```yaml
dependencies:
  php:
    wizaplace/php-fpm-status-cli: "^1.0"
```

Then when you are connected to your project over SSH you can run:

```shell
$ php-fpm-status --socket=unix://$SOCKET --path=/-/status --full
```

## Accessing services

To access various [services](/configuration/services.md) with PHP, see the following examples.  The individual service pages have more information on configuring each service.

{% codetabs name="Elasticsearch", type="js", url="https://examples.docs.platform.sh/php/elasticsearch" -%}

{% language name="Memcached", type="js", url="https://examples.docs.platform.sh/php/memcached" -%}

{% language name="MongoDB", type="js", url="https://examples.docs.platform.sh/php/mongodb" -%}

{% language name="MySQL", type="js", url="https://examples.docs.platform.sh/php/mysql" -%}

{% language name="PostgreSQL", type="js", url="https://examples.docs.platform.sh/php/postgresql" -%}

{% language name="RabbitMQ", type="js", url="https://examples.docs.platform.sh/php/rabbitmq" -%}

{% language name="Redis", type="js", url="https://examples.docs.platform.sh/php/redis" -%}

{% language name="Solr", type="js", url="https://examples.docs.platform.sh/php/solr" -%}

{%- endcodetabs %}

## Project templates

A number of project templates for major PHP applications are available on GitHub. Not all of them are proactively maintained but all can be used as a starting point or reference for building your own website or web application.

### Applications

* [EZ Platform](https://github.com/platformsh/platformsh-example-ezplatform)
* [Drupal 7](https://github.com/platformsh/template-drupal7)
* [Drupal 7 Commerce Kickstart](https://github.com/platformsh/platformsh-example-drupalcommerce7)
* [Drupal 8](https://github.com/platformsh/template-drupal8)
* [Drupal 8 (Multisite variant)](https://github.com/platformsh/platformsh-example-drupal8-multisite)
* [Laravel](https://github.com/platformsh/template-laravel)
* [Moodle](https://github.com/platformsh/platformsh-example-moodle)
* [Magento 1](https://github.com/platformsh/platformsh-example-magento1)
* [Magento 2](https://github.com/platformsh/template-magento2ce)
* [Sculpin](https://github.com/platformsh/platformsh-example-sculpin)
* [TYPO3](https://github.com/platformsh/platformsh-example-typo3)
* [WordPress](https://github.com/platformsh/template-wordpress)
* [GravCMS](https://github.com/platformsh/platformsh-example-gravcms)

### Frameworks

* [Amp/Aerys](https://github.com/platformsh/platformsh-example-amphp)
* [React PHP](https://github.com/platformsh/platformsh-example-reactphp)
* [Symfony 3.x](https://github.com/platformsh/template-symfony3)
* [Symfony 4.x](https://github.com/platformsh/template-symfony4)
