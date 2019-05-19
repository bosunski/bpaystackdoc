# API Introduction

This package provides a fluent and convenient way to interact with the [Paystack API](https://developers.paystack.co/reference). However, there are some features that 
this package provides that makes some of this interaction easy. Those features will be the subject of this section.

## Listings
All listings i.e `*->list()` methods returns a `Xeviant\Paystack\Collection` instance which extends
the `Illuminate\Support\Collection` class. This adds the power of Laravel's collection out of the box. 
To know more about the features of the `Illuminate\Support\Collection` class, check [Available Methods](https://laravel.com/docs/5.7/collections#available-methods)

```php
<?php

$transactions = $paystack->transactions()->list();

$transactions->map(function ($transaction) {
    return $transaction->reference;
});
```

## Data Validation
One of the techniques introduced in this package to minimize error is that Validation occurs before API calls are 
made to ensure appropriate data and required data are passed to the Paystack API. In most cases, a common validation that occurs is
the validation against a required field - meaning that when you're sending data, for example, to the customer creation endpoint, the package will
verify that all the fields marked `required` in the paystack API reference for that endpoint is present. If it's not, a `Xeviant\Paystack\Exception\MissingArgumentException` is thrown. This ensures that 
unnecessary errors don't get to the API and can be attended to at the point of development, hence, the chances of bugs are minimized.

```php
<?php
    // Amount is Required, but omitted
    $data = [
        'email' => 'email@example.com',
    ];
    
    // Throws MissingArgumentException since amount is required and it's not present in data 
    $transaction = $paystack->transactions()->initialize($data);
    
    header("location: " . $transaction->initialization_url);
```

## Carbon Dates

