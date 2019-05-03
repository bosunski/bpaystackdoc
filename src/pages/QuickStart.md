# QuickStart Guide

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
    $paystack = new Paystack('PUBLIC_KEY', 'SECRET_KEY');
    
    // Retrieves Customers
    $customers = $paystack->customers()->list();
```

2. Static instantiation using `::make` method

```php
<?php
    $paystack = Paystack::make('PUBLIC_KEY', 'SECRET_KEY');
    
    // Retrieves Customers
    $customers = $paystack->customers()->list();
```
