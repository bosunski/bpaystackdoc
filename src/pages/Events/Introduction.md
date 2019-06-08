# Introduction

This package provides support for listening to events that occur while interacting with the Paystack API all the events supported by Paystack
are documented in the [Events documentation][1]. Those events' names are described within the `PaystackEventType` interface and are currently supported within the client.
This means that when you interact with any part of the Paystack API that will cause these events to be fired, the Client will examine the response to know if any of those event has occurred and fires such an event. 
This enabled you to react to any of those events or even make your code more decoupled and event driven.
## Listening to Events
Under the hood this client currently uses the `league\event`  [library][2] to handle event listening as well as dispatching. The Client provides a public interface that enables you to get the current Event Handler (as the client is not tightly coupled to any event library).

To listen to an event we will use the public interface provided by the client and then attach a listener to the event we're listening to. This can be achieved like so:

```php
<?php

use League\Event\EventInterface;

$paystack = Paystack::make('pk_test_', 'sk_test_');

$paystack->getEventHandler()->listen('invoice.create', function (EventInterface $event) {
    var_dump($event->getName()); // invoice.create
});
``` 
::: tip
In the above, we're listening to `invoice.create` event. Note that all events that can be listened
to are documented in <a href="https://developers.paystack.co/docs/events#section-types-of-events" target="__blank">here</a>.
:::

To make sure you don't worry about having to know events name word for word, you can reference any event you want to listen to
using the `PaystackEventType` interface which contains constants that represents the event names currently documented on Paystack.
That can be done like this:
 
```php
<?php

use League\Event\EventInterface;
use Xeviant\Paystack\Contract\PaystackEventType;

$paystack = Paystack::make('pk_test_', 'sk_test_');

$paystack->getEventHandler()->listen(PaystackEventType::INVOICE_CREATED, function (EventInterface $event) {
    var_dump($event->getName()); // invoice.create
});
```  

Basically, here is the content of the `PaystackEventType` interface:

```php
<?php

interface PaystackEventType
{
    const INVOICE_UPDATED = 'invoice.update';
    const INVOICE_CREATED = 'invoice.create';
    const CHARGE_SUCCESS = 'charge.success';
    const TRANSFER_SUCCESS = 'transfer.success';
    const BULK_TRANSFER_SUCCESS = 'bulk_transfer.success';
    const BULK_TRANSFER_FAILED = 'bulk_transfer.failed';
    const TRANSFER_FAILED = 'transfer.failed';
    const INVOICE_FAILED = 'invoice.failed';
    const SUBSCRIPTION_ENABLED = 'subscription.enable';
    const SUBSCRIPTION_DISABLED = 'subscription.disable';
    const SUBSCRIPTION_CREATE = 'subscription.create';
}
```
Any event name that is not within this interface(shown above) cannot be listened to.

[1]: https://developers.paystack.co/docs/events#section-types-of-events
[2]: https://event.thephpleague.com/2.0
