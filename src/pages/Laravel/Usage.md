# Introduction

The usage of the Laravel Paystack package is not different from the use of the base `xeviant/paystack` package as it sits in the core of the Laravel Paystack package itself.

## Basic instantiation Techniques
Since we're in a Laravel context, we don't need to `new` the Paystack package as we did in the use of the `xeviant/paytsack` as all the building blocks have been baked into Laravel's IoC container 😎. You can do the instantiation in any of the following ways:
### Using the IoC container
```php
<?php
    use Illuminate\Support\Facades\App;

    $paystack = App::make('paystack');
```

### Using the Facade
```php
<?php
    use Paystack;

    $customers = Paystack::customers()->list();
```
For this part make sure you have added the `Paystack` alias to your aliases inside the `config/app.php`. Check out the Introduction to this chapter.

## Connections
This package comes with the ability that allows you to switch between different connections at runtime.
```php
<?php
    use Paystack;

    $testCustomers = Paystack::connection('test')->customers()->list();
    $liveCustomers = Paystack::connection('live')->customers()->list();

    //
    $allCustomers = $testCustomers->merge($liveCustomers);
```

The above example retrieves both the customers in the Live mode and the Test mode. It's assumed that you've configured the the `connections` section inside the `config/paystack.php` configuration file. An example of this is:

```php
<?php
// ...
'connections' => [
    'test' => [
        'publicKey'     => 'pk_test_x123',
        'secretKey'     => 'sk_test_x123',
        'paymentUrl'    => $paymentUrl,
        'cache'         => false,
    ],
    'live' => [
        'publicKey'     => 'pk_live_x123',
        'secretKey'     => 'sk_live_x123',
        'paymentUrl'    => $paymentUrl,
        'cache'         => false,
    ],
    // You can add More connection as you want
],
// ...
```

You can specify connections as you like and call the connection using the `connection('CONNECTION_NAME')` method like it's done in the last example.

[1]: https://laravel.com/5.8/events
