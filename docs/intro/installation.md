# Installation

This package is available on [Packagist] and you can install it using [Composer].

We require at least an implementation for:

* Dependency Injection handling
* Service bus
* HTTP routing

By running the following command you'll have the very minimum setup for Chimera:

```sh
composer require chimera/bus-tactician \
    chimera/di-symfony \
    chimera/routing-mezzio \
    lcobucci/di-builder
```

## Additional packages

You may optionally install the following packages to have some helpful features:

* **`chimera/mapping`**: gives you the possibility of configuring components using annotations
* **`chimera/serialization-jms`**: allows you to use [JMS serializer] to decode requests and encode responses
* **`lcobucci/error-handling-middleware`**: uses [lcobucci/error-handling-middleware] as the default error handler for the application

## PHP configuration

In order to make sure that we're dealing with the correct data, we're using the function `assert()`.

The nice thing about `assert()` is that we can (and should) disable it on production.
That would avoid creating and executing _opcodes_ which are relevant only for development.

Check the documentation for more information: <https://php.net/manual/en/function.assert.php>

### Production mode

We recommend you to set `zend.assertions` to `-1` in your `php.ini`.

### Development

You should leave `zend.assertions` as `1` and set `assert.exception` to `1`, which will make PHP throw an `AssertionError` when things go wrong.

[Packagist]: https://packagist.org/packages/chimera
[Composer]: https://getcomposer.org
[lcobucci/error-handling-middleware]: https://github.com/lcobucci/error-handling-middleware
[JMS serializer]: https://www.jmsyst.com/libs/serializer
