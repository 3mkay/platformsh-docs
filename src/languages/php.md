# PHP Support

<!-- toc -->

PHP is a popular scripting language designed especially for the web. It currently powers over 80% of websites.

## Supported versions

<div id = "phpSupported"></div>

<script>
makeImagesList("runtimes", "php", "supported", "phpSupported");
</script>

Note that as of PHP 7.1 we use the Zend Thread Safe (ZTS) version of PHP.

To select a PHP version, specify a `type` such as `php:7.3`:

```yaml
# .platform.app.yaml
type: "php:7.3"
```

### Deprecated versions

The following versions are available but are not receiving security updates from upstream, so their use is not recommended. They will be removed at some point in the future.

<div id = "phpDeprecated"></div>

<script>
makeImagesList("runtimes", "php", "deprecated", "phpDeprecated");
</script>

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

<div>
    <table id="phpTemplate" border="1">
    <tbody></tbody>
    </table>
</div>

<script>
makeTemplateTable("php", "phpTemplate");
</script>
