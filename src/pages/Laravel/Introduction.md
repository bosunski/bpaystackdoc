# Introduction

In other to make using this package in Laravel framework more sound, we have made a superset package that is designed
for laravel so we can take advantages of some things offered by Laravel for better development.

If you're considering using this package in a Laravel environment, we highly recommend that you use the Laravel package instead as it integrates better. The laravel
package is built upon the `xeviant/paystack` package, hence, it supports all the future it has and even more. Currently, some of the features supported by the laravel package are:
- WebHook integration with Request Validation
- Recording of WebHook Payloads
- Lumen Framework Support
- Integrates [Laravel Events][1]
- Multi-Tenancy Support - Ability to use Multiple Paystack Credentials if need be.
- Multi-Tenancy also grants you the ability to switch between Live and Test Mode at Runtime.
- All features supported by `xeviant/paystack` package.

In subsequent sections, we will try to explain how to use all these features.

## Requirements
- Laravel 5.7 and Above

## Setting up the Laravel Paystack Package
```bash
$ composer require xeviant/laravel-paystack
```
### Publishing Configuration

```bash
$ php artisan vendor:publish --provider="Xeviant\LaravelPaystack\PayStackServiceProvider" --tag=config
```
You will see `paystack.php` inside the `config` directory, you can modify the contents of this file to configure the package. Here is a sample content of the `paystack.php` file:

```php
<?php

declare(strict_types=1);

return [
    /**
     * Paystack WebHook URL
     */
    'webhookUrl' => '/paystack/hook',

    /**
     * Public Key From Paystack Dashboard
     *
     */
    'publicKey' => $publicKey = env('PAYSTACK_PUBLIC_KEY', 'publicKey'),

    /**
     * Secret Key From Paystack Dashboard
     *
     */
    'secretKey' => $secretKey = env('PAYSTACK_SECRET_KEY', 'secretKey'),

    /**
     * Paystack Payment URL
     *
     */
    'paymentUrl' => $paymentUrl = env('PAYSTACK_PAYMENT_URL'),

    /**
     * Optional email address of the merchant
     *
     */
    'merchantEmail' => $merchantEmail = env('MERCHANT_EMAIL'),

    /**
     * Default connection that will be used to connect to the API
     */
    'default' => 'test',

    /**
     * Here you can specify different Paystack connection.
     */
    'connections' => [
        'test' => [
            'publicKey'     => $publicKey,
            'secretKey'     => $secretKey,
            'paymentUrl'    => $paymentUrl,
            'cache'         => false,
        ],
        'live' => [
            'publicKey'     => $publicKey,
            'secretKey'     => $secretKey,
            'paymentUrl'    => $paymentUrl,
            'cache'         => false,
        ],
        // You can add More connection as you want
    ],
];
```

### Publishing Migrations
The Laravel Paystack package uses database to store payloads received by from WebHook calls. By default, the package ships with its own migration to create the table and fields required for it to work. To make changes to the migration you can publish it like so:

```bash
$ php artisan vendor:publish --provider="Xeviant\LaravelPaystack\PayStackServiceProvider" --tag=migration
```

### Register Paystack Facade
Open `config/app.php` and add the line below to the Aliases:

```php
'Paystack' => Unicodeveloper\Paystack\Facades\Paystack::class,
```

### Run Migrations
```bash
$ php artisan migrate
```

[1]: https://laravel.com/5.8/events
