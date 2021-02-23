# Application bootstrapping

Once you've [installed the packages you wanted](../intro/installation.md), it's time to bootstrap the dependency injection container.
We rely on [lcobucci/di-builder] and [symfony/dependency-injection] for that task.

With [lcobucci/di-builder], we have the possibility of controlling how the container compilation is performing (adding files, compiler passes, using different formats, etc).
Make sure to read the documentation of that library to understand how it works (and how you can better use it).

## Sample configuration

We need an entrypoint for the application, that should:

1. Initialise the dependency injection container
1. Fetch the instance of your web application
1. Run the application

A **very minimalist version** for the `public/index.php`, would look like this:

!!! Important
    You can organise the directory layout of your application the way you prefer.
    These examples illustrate **one possibility**, but you're the one who controls your software.

```php
<?php
declare(strict_types=1);

namespace MyOrg\MyApi;

require __DIR__ . '/../vendor/autoload.php';

use Chimera\DependencyInjection\RegisterApplication;
use Chimera\Routing\Application;
use Lcobucci\DependencyInjection\ContainerBuilder;

use function dirname;

// 1. Initialise the dependency injection container
$root = dirname(__DIR__);

$container = ContainerBuilder::default(__FILE__, __NAMESPACE__)
    ->setDumpDir($root . '/var/tmp')
    ->setParameter('app.basedir', $root . '/')
    ->addFile($root . '/config/container.xml')
    ->addPackage(RegisterApplication::class, ['my-api'])
    ->getContainer();

// 2. Fetch the instance of your web application
$app = $container->get('my-api.http');
assert($app instanceof Application);

// 3. Run the application
$app->run();
```

Where `config/container.xml` looks like:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<container xmlns="http://symfony.com/schema/dic/services"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://symfony.com/schema/dic/services ../vendor/symfony/dependency-injection/Loader/schema/dic/services/services-1.0.xsd">
    <parameters>
        <parameter key="my-api.router_config" type="collection">
            <parameter key="cache_enabled">true</parameter>
            <parameter key="cache_file">%app.basedir%var/cache/my-api_routing.php</parameter>
        </parameter>
    </parameters>

    <services>
        <defaults public="false" autowire="true" autoconfigure="true"/>

        <prototype namespace="MyOrg\MyApi\" resource="../src" />
    </services>
</container>
```

[lcobucci/di-builder]: https://github.com/lcobucci/di-builder
[symfony/dependency-injection]: https://symfony.com/doc/current/components/dependency_injection.html
