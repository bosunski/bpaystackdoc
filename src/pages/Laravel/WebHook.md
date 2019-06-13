## Introduction

It's no doubt that the WebHooks are very important to guarantee customers get value for what they're paying for. In other to make setting WebHooks up easy within your Laravel app, this package ships with a built in support for handling your hooks. We will go through how to use this feature in this section.

## Prerequisite
You can go ahead to use the WebHook feature if you've:
- Run the migration as explained [here][1]
- Your WebHook URL is set in the `config/paystack.php` file (Of course we put a default there for you).

## Using the WebHook Support
Once this package is installed and setup, everything you need to use the WebHook is ready.

## WebHook Route
Once the Laravel Paystack page is installed it automatically adds the `/paystack/hook` route to your route list. This is the endpoint that you will use to configure your Paystack WebHook on the Paystack Dashboard.

You can change this endpoint by modifying the `webHookUrl` parameter in your `config/paystack.php` file.

```php
<?php
    return [
        'webhookUrl' => '/paystack/hook',
        // ...
    ];
```
Anything you update it to should be used to configure your web hook URL on the paystack dashboard.

## WebHooks and Events
Since calling of WebHooks results from the events emitted from paystack itself, the WebHook feature allows this same event to be emitted within Laravel using Laravel's native event system. With this, you can connfigure Listeners to listen to any of those event within your App. The WebHook emits any of the events referenced in [this][2] part of the documentation. We can attach listeners to the events emitted by webhooks from the `EventServiceProvider` like this:

```php
<?php

namespace App\Providers;

use Illuminate\Support\Facades\Event;
use Illuminate\Foundation\Support\Providers\EventServiceProvider as ServiceProvider;
use Xeviant\Paystack\Contract\PaystackEventType;

class EventServiceProvider extends ServiceProvider
{
    /**
     * The event listener mappings for the application.
     *
     * @var array
     */
    protected $listen = [
        PaystackEventType::CHARGE_SUCCESS => [
            'App\Listeners\FinalizeOrder',
        ],
    ];

    /**
     * Register any events for your application.
     *
     * @return void
     */
    public function boot()
    {
        parent::boot();

        //
    }
}
```
A `payload` data will be available to listeners when the event is emmited. The listener in the above example will access the Payload this way:
```php
<?php

namespace App\Listeners;

use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Support\Facades\Log;
use Xeviant\LaravelPaystack\Model\PaystackEvent;

class FinalizeOrder implements ShouldQueue
{
    /**
     * Handle the event.
     *
     * @param  PaystackEvent  $event
     * @return bool
     */
    public function handle(PaystackEvent $event)
    {
        $payStackPayLoad = $event->payload;
        // Do something
    }
}
```

:::: warning
Make sure long running tasks are not started within the listeners so that the webhook can send response back to the paystack. If you have to do long running tasks in the listener, it's advisable that they are queued.
::::
## Guards
To make sure Developers are not bothered by having to secure the web hook themselves, we have configured the Web hook route only allow Paystack IPs as documented [here][3] as well as Verification of `X-Paystack-Signature` also documented [here][4].

In addition to that, we conditionally include `127.0.0.1` in the allowed IPs if you're in a *local environment* so that you can easily test (or simulate) Payload deliveries when the Web hook is called.

## Testing the WebHook Locally
![5]

Since your local IP `127.0.0.1` will be added to your allowed IPs when inn a local environment, you can test the endpoint by sending some JSON data over **POST** request. Here is a sample JSON payload gotten from [here][6]:

```JSON
{
  "event": "charge.success",
  "data": {
    "id": 84,
    "domain": "test",
    "status": "success",
    "reference": "9cfbae6e-bbf3-5b41-8aef-d72c1a17650g",
    "amount": 50000,
    "message": null,
    "gateway_response": "Approved",
    "paid_at": "2018-12-20T15:00:06.000Z",
    "created_at": "2018-12-20T15:00:05.000Z",
    "channel": "card",
    "currency": "NGN",
    "ip_address": null,
    "metadata": {
      "custome_fields": [
        {
          "display_name": "A sample",
          "variable_name": "a_sample",
          "value": "custom field"
        }
      ]
    },
    "log": null,
    "fees": 750,
    "fees_split": null,
    "authorization": {
      "authorization_code": "AUTH_9246d0h9kl",
      "bin": "408408",
      "last4": "4081",
      "exp_month": "12",
      "exp_year": "2020",
      "channel": "card",
      "card_type": "visa DEBIT",
      "bank": "Test Bank",
      "country_code": "NG",
      "brand": "visa",
      "reusable": true,
      "signature": "SIG_iCw3p0rsG7LUiQwlsR3t"
    },
    "customer": {
      "id": 4670376,
      "first_name": "Asample",
      "last_name": "Personpaying",
      "email": "asam@ple.com",
      "customer_code": "CUS_00w4ath3e2ukno4",
      "phone": "",
      "metadata": null,
      "risk_action": "default"
    },
    "plan": {
      "id": 17,
      "name": "A s(i/a)mple plan",
      "plan_code": "PLN_dbam2fwcqkyyfjc",
      "description": "Sample plan for docs",
      "amount": 50000,
      "interval": "hourly",
      "send_invoices": true,
      "send_sms": true,
      "currency": "NGN"
    },
    "subaccount": {},
    "paidAt": "2018-12-20T15:00:06.000Z"
  }
}
```
You can test the endpoint using a tool like [Postman][7].

[1]: /laravel#run-migrations
[2]: https://developers.paystack.co/docs/events#section-types-of-events
[3]: https://developers.paystack.co/docs/events#section-confirming-events
[4]: https://developers.paystack.co/docs/events#section-confirming-events
[5]: https://res.cloudinary.com/xeviant/image/upload/v1560456632/Screenshot_2019-06-13_at_6.19.18_PM_ve66xc.png
[6]: https://developers.paystack.co/docs/events#section-structure-of-an-event-object
[7]: https://www.getpostman.com/downloads/
