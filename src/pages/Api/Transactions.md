# Transactions

## Initializing Transactions
```php
<?php

    $data = [
        'amount' => 20000,
        'email' => 'email@example.com',
    ];
    
    $transaction = $paystack->transactions()->initialize($data);
    
    header("location: " . $transaction->initialization_url);
```
## Verifying Transactions
```php
<?php

$transaction = $paystack->transactions()->verify();
// Do something with the Transaction
$amount = $transaction->amount;
```
## Listing Transactions
```php
<?php

$transactions = $paystack->transactions()->list();

$transactionReferences = $transactions->map(function ($transaction) {
    return $transaction->reference;
});
```
## Fetching a Transaction
```php
<?php

$transactions = $paystack->transactions()->fetch('5466721');

$status = $transactions->status;
```
## Charge Authorization
```php
<?php

    $data = [
        'amount' => 20000,
        'email' => 'email@example.com',
        'authorization_code' => 'AUTH_12xed34',
    ];
    
    $transaction = $paystack->transactions()->authorize($data);
    
    if ($transaction->status === "success") {
        // Do Something
    }
```
## Viewing Transaction Timeline
```php
<?php

    $timeline = $paystack->transactions()->timeline('5466721');
    
    $history = $timeline->history;
```
## Transaction Totals
```php
<?php

    $totals = $paystack->transactions()->totals();
    
    $pendingTransfers = $totals->pending_transfers;
```
## Exporting Transactions
```php
<?php

    $data = [
        'from' => '17-12-2011',
        'to' => '17-12-2014',
    ];
    
    $export = $paystack->transactions()->export($data);
    
    // Redirect to download
    header("location: " . $export->path);
```
## Request Re-authorization
```php
<?php

    $data = [
        'amount' => 20000,
        'email' => 'email@example.com',
        'authorization_code' => 'AUTH_12xed34',
    ];
    
    $transaction = $paystack->transactions()->reauthorize($data);
    
    header("location: " . $transaction->reauthorization_url);
```
## Check Authorization
```php
<?php

    $data = [
        'amount' => 20000,
        'email' => 'email@example.com',
        'authorization_code' => 'AUTH_12xed34',
    ];
    
    $transaction = $paystack->transactions()->checkAuthorization($data);
    
    if ($transaction->amount < 1000) {
        // 🔥
    }
```
