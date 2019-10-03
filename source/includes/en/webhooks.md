#Webhooks
Weebhooks allow to notify a Merchant party when an event has occurred in the platform, so the Merchant can take the corresponding actions.

<aside class="notice">
Openpay requires that the webhook is verified before executing it.
</aside>


##Webhook Object

> Object example

```json
  {
    "id" : "wxvanstudf4ssme8khmc",
    "url" : "http://requestb.in/11vxrsf1",
    "user" : "juanito",
    "password" : "passjuanito",
    "event_types" : [
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "chargeback.accepted"
    ],
    "status":"verified"
}
```

Property | Description
--------- | -----
id            |***string*** <br/>Unique webhook identifier number.
url           |***string*** <br/>Webhook.
user          |***string*** <br/>User name used for webhook's basic authentication.
password      |***string*** <br/>Password for webhook's basic authentication.
event_types   |***array[string]*** <br/>List of events where the webhook will be triggered.
status        |***string*** <br/>Webhook status, it indicates if it's *verified* or not (*unverified*).

<aside class="success">
The supported event type are:
</aside>

Event                      | Category       | Description
-------------------------- | -------------- |------------
charge.refunded            | Charge         | Reports when there is a charge refund.
charge.failed              | Charge         | Reports when a charge failed and it wasn't applied.
charge.cancelled           | Charge         | Reports when a charge is cancelled.
charge.created             | Charge         | Reports when a charge is scheduled.
charge.succeeded           | Charge         | Reports when a charge is applied.
charge.rescored.to.decline | Charge         | Reports when a charge' score is recalculated and is declined.
subscription.charge.failed | Subscription    | Reports when the charge to a subscription fails.
payout.created             | Payout          | Reports when a payout has been scheduled for the next day.
payout.succeeded           | Payout          | Reports when a payout has been applied.
payout.failed              | Payout          | Reports when a payout has failed.
transfer.succeeded         | Transfer | Reports when a transfer has been performed between to Openpay accounts.
fee.succeeded              | Fee     | Reports when a fee is charged successfully to a customer.
fee.refund.succeeded       | Fee     | Reports when a fee has been successfully refunded to a customer.
spei.received              | SPEI           | Reports when a payout has been received by SPEI for adding funds to the account.
chargeback.created         | Chargeback   | Reports when a chargeback of a transaction was receive and a transaction has been initiated.
chargeback.rejected        | Chargeback   | Reports when a chargeback has been rejected.
chargeback.accepted        | Chargeback   | Reports when a chargeback has been accepted.
order.created              | Order          | Reports when an order is created an scheduled.
order.activated            | Order          | Reports when an order is activated.
order.payment.received     | Order          | Reports when an order is received.
order.completed            | Order          | Reports when an order is completed.
order.expired              | Order          | Reports when an order has expired.
order.cancelled            | Order          | Reports when an order is canceled.
order.payment.cancelled    | Order          | Reports when a payment order is canceled.


##Webhook Creation

> Definition

```shell
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/webhooks
```

```php
<?
$webhook = $openpay->webhooks->add(webhook);
?>
```

```java
openpayAPI.webhooks().create(Webhook request);
```

```csharp
openpayAPI.WebhooksService.Create(Webhook request);
```

```javascript
openpay.webhooks.create(webhook, callback);
```

```ruby
@webhooks=@openpay.create(:webhooks)
@webhooks.create(request_hash)
```

> Request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/webhooks \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
    "url" : "http://requestb.in/11vxrsf1",
    "user" : "juanito",
    "password" : "passjuanito",
    "event_types" : [
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "chargeback.accepted"
    ]
}'
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$webhook = array(
    'url' => 'http://requestb.in/11vxrsf1',
    'user' => 'juanito',
    'password' => 'passjuanito',
    'event_types' => array(
      'charge.refunded',
      'charge.failed',
      'charge.cancelled',
      'charge.created',
      'chargeback.accepted'
    )
    );

$webhook = $openpay->webhooks->add($webhook);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Webhook request = new Webhook();
request.url("http://requestb.in/11vxrsf1");
request.user("juanito");
request.password("passjuanito");
request.addEventType("charge.refunded");
request.addEventType("charge.failed");

Webhook webhook = api.webhooks().create(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Webhook request = new Webhook();
request.Url = "http://requestb.in/11vxrsf1";
request.User = "juanito";
request.Password = "passjuanito";
request.AddEventType("charge.refunded");
request.AddEventType("charge.failed");

Webhook webhook = api.WebhookService.Create(request);
```

```javascript
var webhook_params = {                                            
    'url' : 'http://requestb.in/11vxrsf1',
    'user' : 'juanito',
    'password' : 'passjuanito',
    'event_types' : [
      'charge.refunded',
      'charge.failed',
      'charge.cancelled',
      'charge.created',
      'chargeback.accepted'
    ]
};

openpay.webhooks.create(webhook_params, function(error, webhook){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@webhooks=@openpay.create(:webhooks)
request_hash={
    "url" => "http://requestb.in/11vxrsf1",
    "user" => "juanito",
    "password" => "passjuanito",
    "event_types" => [
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "chargeback.accepted"
    ]
   }

response_hash=@webhooks.create(request_hash.to_hash)
```

> Response example

```json
{
  "id" : "wkn0t30zfxpmhr5usgfa",
  "url" : "http://requestb.in/qt3bq0qt",
  "user" : "juanito",
  "event_types" : [
    "charge.succeeded",
    "charge.created",
    "charge.cancelled",
    "charge.failed"
  ],
  "status" : "verified"
}
```

When you save webhooks an ID will be generated that can be used to eliminate it or simply get not sensitive webhook information.


###Request

Request   | Description
--------- | -----
url           |***string*** <br/>Webhook URL
user          |***string*** <br/>Username for basic webhook authentication.
password      |***string*** <br/>Password for basic webhook authentication.
event_types   |***array[string]*** <br/>List of events where the webhook will be triggered.

###Response
Returns a [webhook object](#webhook-object) when it was successfully created or an error response if there was an error on creation.



##Get a Webhook

> Definition

```shell
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/webhooks/{WEBHOOK_ID}
```

```php
<?
$webhook = $openpay->webhooks->get(webhookId);
?>
```

```java
openpayAPI.webhooks().get(String webhookId);
```

```csharp
openpayAPI.WebhooksService.Get(string webhookId);
```

```javascript
openpay.webhooks.get(webhookId, callback);
```

```ruby
@webhooks=@openpay.create(:webhooks)
@webhooks.get(webhookId)
```

> Request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/webhooks/wxvanstudf4ssme8khmc \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json"
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$webhook = $openpay->webhooks->get('wxvanstudf4ssme8khmc');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Webhook webhook = api.webhooks().get("wxvanstudf4ssme8khmc");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Webhook webhook = api.WebhooksService.Get("wxvanstudf4ssme8khmc");
```

```javascript
openpay.webhooks.get('wxvanstudf4ssme8khmc', function(error, webhook){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@webhooks=@openpay.create(:webhooks)

response_hash=@webhooks.get("wxvanstudf4ssme8khmc")
```

> Response example

```json
  {
    "id" : "wxvanstudf4ssme8khmc",
    "url" : "http://requestb.in/11vxrsf1",
    "user" : "juanito",
    "event_types" : [
      "verification",
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "charge.succeeded",
      "subscription.charge.failed",
      "payout.created",
      "payout.succeeded",
      "payout.failed",
      "transfer.succeeded",
      "fee.succeeded",
      "spei.received",
      "chargeback.created",
      "chargeback.rejected",
      "chargeback.accepted"
    ],
    "status" : "verified"
  }
```

Get a list of the webhook details by ID.

<aside class="notice">
**Note:** Sensitive data like the password will never be included in the response.
</aside>


###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Unique webhook identifier

###Response
Returns a [webhook object](#webhook-object)


##Delete a Webhook

> Definition

```shell
DELETE https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/webhooks/{WEBHOOK_ID}
```

```php
<?
$webhook = $openpay->webhooks->get(webhookId);
$webhook->delete();
?>
```

```java
openpayAPI.webhooks().delete(String webhookId);
```

```csharp
openpayAPI.WebhooksService.Delete(string webhook_id);
```

```javascript
openpay.webhooks.delete(webhookId, callback);
```

```ruby
@webhooks=@openpay.create(:webhooks)
@webhooks.delete(webhook_id)
```

> Customer request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/webhooks/wxvanstudf4ssme8khmc \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -X DELETE
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$webhook = $openpay->webhooks->get('wxvanstudf4ssme8khmc');
$webhook->delete();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.webhooks().delete("wxvanstudf4ssme8khmc");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.WebhooksService.Delete("wxvanstudf4ssme8khmc");
```

```javascript
openpay.webhooks.delete('wxvanstudf4ssme8khmc', function(error) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@webhooks=@openpay.create(:webhooks)

response_hash=@webhooks.delete("wxvanstudf4ssme8khmc")
```

Delete a webhook from the merchant.

To delete a webhook you only need to provide the ID.


###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Webhook unique identifier.

###Response
If the webhook was deleted correctly the response will be empty, if the webhook cannot be deleted an [error object](#error-object) will be returned including the error message.


##Webhook list

> Definition

```shell
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/webhooks
```

```php
<?
$webhookList = $openpay->webhooks->getList();
?>
```

```java
openpayAPI.webhooks().list();
```

```csharp
openpayAPI.WebhooksService.List();
```

```javascript
openpay.webhooks.list(callback);
```

```ruby
@webhooks=@openpay.create(:webhooks)
@webhooks.all
```

> Request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/webhooks \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json"
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$webhookList = $openpay->webhooks->getList();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
List<Webhook> webhooks = api.webhooks().list();
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
List<Webhook> webhooks = api.WebhooksService.List();
```

```javascript
openpay.webhooks.list(function(error, list){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@webhooks=@openpay.create(:webhooks)

response_hash=@webhooks.all
```

> Response example

```json
[
  {
    "id" : "wDashboard185",
    "event_types" : [
      "verification",
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "charge.succeeded",
      "subscription.charge.failed",
      "payout.created",
      "payout.succeeded",
      "payout.failed",
      "transfer.succeeded",
      "fee.succeeded",
      "spei.received",
      "chargeback.created",
      "chargeback.rejected",
      "chargeback.accepted"
    ],
    "url" : "http://requestb.in/11vxrsf1",
    "status" : "verified"
  },
  {
    "id" : "wDashboard186",
    "event_types" : [
      "verification",
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "charge.succeeded",
      "subscription.charge.failed"
    ],
    "url" : "http://requestb.in/1fhpiog1",
    "status" : "verified"
  }
]
```

Returns a list registered by the merchant.

<aside class="notice">
**Nota:** Never return sensitive data like the webhook password access.
</aside>


###Request

###Response
The list of [webhook objects](#webhook-objects) registered according to the given parameters.
