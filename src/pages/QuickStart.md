# QuickStart Guide

## An Example Playground

<iframe scrolling="no" style="width: 100%;height: 300px;" id="ciroueEmbed" sandbox="allow-forms allow-scripts allow-popups allow-same-origin allow-pointer-lock" src="https://www.ciroue.com/e/x/ndzJVN5rPp7ZkY9O"></iframe>

## Requirements
- **PHP**: 7.1 and Up
- Composer

## Installation

```bash
composer require xeviant/paystack
```

## Including the Package
```php
<?php
    require_once "vendor/autoload.php";
```

## Basic Usage
1. Normal Instantiation using `new` keyword

```php
<?php
    use Xeviant\Paystack\Paystack;

    $paystack = new Paystack('YOUR_PUBLIC_KEY', 'YOUR_SECRET_KEY');
    
    // Retrieves Customers
    $customers = $paystack->customers()->list();
```

2. Static instantiation using `::make` method

```php
<?php
    use Xeviant\Paystack\Paystack;

    $paystack = Paystack::make('PUBLIC_KEY', 'SECRET_KEY');
    
    // Retrieves Customers
    $customers = $paystack->customers()->list();
```

::: tip
In the above examples, we call the API method and then the the part of the API you want to access
In this example I am accessing the list feature of the customers API <a href="https://developers.paystack.co/reference">here</a>
:::
