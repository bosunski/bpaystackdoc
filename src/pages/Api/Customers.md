# Customers

## Creating Customer
```php
<?php

    $data = [
        'email' => 'email@example.com',
    ];
    
    $customer = $paystack->customers()->create($data);
    
    $code = $customer->customer_code;
```

## Listing Customers
```php
<?php

$transactions = $paystack->customers()->list();

$customerCodes = $transactions->map(function ($customer) {
    return $customer->customer_code;
});
```
## Fetching Customer
```php
<?php

$customer = $paystack->customers()->fetch('CUS_x5466721');

$firstName = $customer->first_name;
```
## Updating Customer

```php
<?php

    $data = [
        'first_name' => 'Bosun',
    ];
    
    $customer = $paystack->customers()->update($data);
    
     var_dump($customer->first_name === $data['first_name']); // TRUE
```

## White-listing Customer

```php
<?php

$whitelisted = $paystack->customers()->whitelist('CUS_x5466721');

if ($whitelisted) {
    // Do Something
}
```

## Black-listing Customer
```php
<?php

$blacklisted = $paystack->customers()->blacklist('CUS_x5466721');

if ($blacklisted) {
    // Do Something
}
```
## Deactivating Authorization

```php
<?php

$deactivated = $paystack->customers()->deactivateAuthorization('AUTH_x5466721');

if ($deactivated) {
    // Do Something
}
```
