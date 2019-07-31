#Subscriptions

Subscriptions allow to associate customers and cards in order to make recurrent payments.

In order to subscribe a customer first is required to [create a plan](#create-a-new-plan).

##Subscription object

> Object example

```json
{
    "status": "trial",
    "card": {
        "type": "debit",
        "brand": "mastercard",
        "card_number": "1111",
        "holder_name": "Juan Perez Ramirez",
        "expiration_year": "20",
        "expiration_month": "12",
        "allows_charges": true,
        "allows_payouts": false,
        "creation_date": "2013-12-13T12:39:46-06:00",
        "bank_name": "DESCONOCIDO",
        "customer_id": null,
        "bank_code": "000"
    },
    "id": "svxdm1suclzipbi4pavm",
    "cancel_at_period_end": false,
    "charge_date": "2014-01-12",
    "creation_date": "2013-12-13T12:39:46-06:00",
    "current_period_number": 0,
    "period_end_date": "2014-01-11",
    "trial_end_date": "2014-01-11",
    "plan_id": "pjl7wfryrrd1tznr0fnl",
    "customer_id": "a2b79p8xmzeyvmolqfja"
}
```

Property | Description
--------- | ------
id | ***string*** <br/> Unique subscription identifier.
creation_date | ***datetime*** <br/> Date and time in which the subscription was created using ISO 8601 format.
cancel_at_period_end  | ***string*** <br/> Indicates if the subscription has been canceled at the end of the period.
charge_date | ***numeric*** <br/> Date in which the subscription will be charged.
current_period_number | ***string*** <br/> Indicates the current period to be charged.
period_end_date | ***numeric*** <br/> Date in which the current period ends, it's one day before the next charge.
trial_end_date | ***string*** <br/> Date in which the trial period ends.  One day after this date the first charge is applied.
plan_id | ***numeric*** <br/>  Plan identifier in which this subscription will be created.
status | ***string*** <br/> Subscription status, it can be *active*, *trial*, *past_due*, *unpaid* or *cancelled*.  If the subscription has a trial period, the trial period is applied, if it doesn't have or when the trial period ends and the first payment is executed it changes to *active*.  When the charge was unable to be completed it changes to *past_due*.  When all the charge tries has been completed according to the plan configuration it can change to *unpaid* or *cancelled*.  When it's marked as *unpaid* and the subscription wants to be reactivated it's required to update the subscription payment method(card).  In any other case, the status is set to *cancelled*.
customer_id | ***string*** <br/> Customer identifier for the subscription owner.
card | ***object*** <br/> Payment method for the subscription.  See [card object](#card-object).


##Create a new Subscription

> Definition

```shell
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions
```

```php
<?
$customer = $openpay->customers->get(customerId);
$subscription = $customer->subscriptions->add(subscriptionDataRequest);
?>
```

```java
openpayAPI.subscriptions().create(String customerId, Subscription request);
```

```csharp
openpayAPI.SubscriptionService.Create(string customer_id, Subscription request);
```

```javascript
openpay.customers.subscriptions.create(customerId, subscriptionRequest, callback);
```

```ruby
#Customer
@subscriptions=@openpay.create(:subscriptions)
@subscriptions.create(request_hash, customer_id)
```

>Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/subscriptions \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "card":{
      "card_number":"4111111111111111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "cvv2":"110",
      "device_session_id":"kR1MiQhz2otdIuUlQkbEyitIqVMiI16f"
   },
   "plan_id":"pbi4kb8hpb64x0uud2eb"
}'
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$subscriptionDataRequest = array(
    'trial_end_date' => '2014-01-01',
    'plan_id' => 'pbi4kb8hpb64x0uud2eb',
    'card' => array(
         'card_number' => '4111111111111111',
         'holder_name' => 'Juan Perez Ramirez',
         'expiration_year' => '20',
         'expiration_month' => '12',
         'cvv2' => '110',
         'device_session_id' => 'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f'));

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$subscription = $customer->subscriptions->add($subscriptionDataRequest);
?>
```

```java
final Calendar trialEndDate = Calendar.getInstance();
trialEndDate.set(2014, 5, 1, 0, 0, 0);

OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Subscription request = new Subscription();
request.planId("pbi4kb8hpb64x0uud2eb");
request.trialEndDate(trialEndDate.getTime());
Card card = new Card();
card.cardNumber("4111111111111111");
card.holderName("Juan Perez Ramirez");
card.cvv2("110");
card.expirationMonth(12);
card.expirationYear(20);
card.deviceSessionId("kR1MiQhz2otdIuUlQkbEyitIqVMiI16f");
request.card(card);

request = api.subscriptions().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Subscription request = new Subscription();
request.PlanId = "idPlan-01001";
request.TrialEndDate = new Datetime(2014, 5, 1);
Card card = new Card();
card.HolderName = "Juan Perez Ramirez";
card.CardNumber = "4111111111111111";
card.Cvv2 = "110";
card.ExpirationMonth = "12";
card.ExpirationYear = "20";
card.DeviceSessionId = "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f";
request.Card = card;

request = api.SubscriptionService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var subscriptionRequest = {
   'card':{
      'card_number':'4111111111111111',
      'holder_name':'Juan Perez Ramirez',
      'expiration_year':'20',
      'expiration_month':'12',
      'cvv2':'110',
      'device_session_id':'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f'
   },
   'plan_id':'pbi4kb8hpb64x0uud2eb'
};

openpay.customers.subscriptions.create(customerId, subscriptionRequest, function(error, subscription){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@subscriptions=@openpay.create(:subscriptions)
card_hash={
     "holder_name" => "Juan Perez Ramirez",
     "card_number" => "4111111111111111",
     "cvv2" => "110",
     "expiration_month" => "12",
     "expiration_year" => "20",
     "device_session_id" => "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f"
   }
request_hash={
     "plan_id" => "pbi4kb8hpb64x0uud2eb",
     "trial_end_date" => "2014-06-20",
     "card" => card_hash
   }

response_hash=@subscriptions.create(request_hash.to_hash, "a9pvykxz4g5rg0fplze0")
```

> Response example

```json
{
   "id":"s0gmyor4yqtyv1miqwr0",
   "status":"trial",
   "card":{
      "type":"debit",
      "brand":"visa",
      "address":null,
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "allows_charges":true,
      "allows_payouts":true,
      "bank_name":"Banamex",
      "bank_code":"002"
   },
   "cancel_at_period_end":false,
   "charge_date":"2014-06-21",
   "creation_date":"2014-05-22T15:56:18-05:00",
   "current_period_number":0,
   "period_end_date":"2014-06-20",
   "trial_end_date":"2014-06-20",
   "plan_id":"pbi4kb8hpb64x0uud2eb",
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```

Create a new subscription for an existing customer.  You can use an existing card or you can send the info of the card where the charges will be made, in these you can include the property <code>device_session_id</code> to use the antifraud tool, see [Fraud detection using device data](https://github.com/open-pay/openpay-js#fraud-detection-using-device-data).


###Request
Property  | Description
--------- | ------
plan_id   | ***string*** (required, length = 45) <br/> Plan identifier in which the subscription will be created.
trial_end_date | ***string*** (optional, length = 10) <br/> Indicates the customer trial end date. If it's not indicated the plan will be used to calculate it.  If the date is in the past it will be interpreted as a subscription with no trial.  Format: yyyy-mm-dd.
source_id | ***string*** (required if the card is not sent, length = 45) <br/> Card token identifier, or the customer registered card which will be used to charge the subscription.
card | ***object*** (required if the source_id is not present) <br/> Payment method which will be used to charge the subscription. See [card object](#card-object).


###Response
Returns the created [subscription object](#subscription-object) or an [error response](#error-object) if an error occurred during the creation.

##Updating a Subscription

> Definition

```shell
PUT https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions/{subscriptionId}
```

```php
<?
$customer = $openpay->customers->get(customerId);
$subscription = $customer->subscriptions->get(subscriptionId);
$subscription->save();
?>
```

```java
openpayAPI.subscriptions().update(Subscription request);
```

```csharp
openpayAPI.SubscriptionService.Update(string customer_id, Subscription subscription);
```

```javascript
openpay.customers.subscriptions.update(customerId, subscriptionId, subscriptionRequest, callback);
```

```ruby
#Customer
@subscriptions=@openpay.create(:subscriptions)
@subscriptions.update(request_hash, customer_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/subscriptions/s0gmyor4yqtyv1miqwr0 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X PUT -d '{
  "trial_end_date": "2016-01-11",
   "card": {
        "card_number": "343434343434343",
        "holder_name": "Juan Perez Ramirez",
        "expiration_year": "20",
        "expiration_month": "12",
        "cvv2":"1234"
    }
}'
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$subscription = $customer->subscriptions->get('s7ri24srbldoqqlfo4vp');
$subscription->trial_end_date = '2014-12-31';
$subscription->save();
?>
```

```java
final Calendar trialEndDate = Calendar.getInstance();
trialEndDate.set(2014, 5, 1, 0, 0, 0);

OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Subscription request = new Subscription();
request.planId("idPlan-01001");
request.trialEndDate(trialEndDate.getTime());
request.sourceId("ktrpvymgatocelsciak7");

request = api.subscriptions().update(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Subscription request = new Subscription();
request.PlanId = "idPlan-01001";
request.TrialEndDate = new Datetime(2014, 5, 1);;
request.CardId = "ktrpvymgatocelsciak7";

request = api.SubscriptionService.Update("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var subscriptionRequest = {
'trial_end_date': '2016-01-11',
  'card': {
    'card_number': '343434343434343',
    'holder_name': 'Juan Perez Ramirez',
    'expiration_year': '20',
    'expiration_month': '12',
    'cvv2':'1234'
  }
};

openpay.customers.subscriptions.update('ag4nktpdzebjiye1tlze', 's0gmyor4yqtyv1miqwr0', subscriptionRequest,
    function(error, subscription){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@subscriptions=@openpay.create(:subscriptions)
request_hash={
     "plan_id" => "pbi4kb8hpb64x0uud2eb",
     "cancel_at_period_end" => true,
     "trial_end_date" => "2014-06-20",
     "source_id" => "ktrpvymgatocelsciak7"
   }

response_hash=@subscriptions.update(request_hash.to_hash, "pbi4kb8hpb64x0uud2eb")
```

> Response example

```json
{
   "id":"s0gmyor4yqtyv1miqwr0",
   "status":"trial",
   "card":{
      "type":"credit",
      "brand":"american_express",
      "address":null,
      "card_number":"343434XXXXX4343",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "allows_charges":true,
      "allows_payouts":false,
      "bank_name":"AMERICAN EXPRESS",
      "bank_code":"103"
   },
   "cancel_at_period_end":false,
   "charge_date":"2016-01-12",
   "creation_date":"2014-05-22T15:56:18-05:00",
   "current_period_number":0,
   "period_end_date":"2016-01-11",
   "trial_end_date":"2016-01-11",
   "plan_id":"pbi4kb8hpb64x0uud2eb",
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```
Updates the information o an active subscription.
Actualiza la informaciÃ³n de una suscripciÃ³n activa.

###Request
Property | Description
--------- | ------
cancel_at_period_end | ***booelan*** (optional) <br/> Indicates if the subscriptions has to be cancelled at the end of the period.
trial_end_date | ***string*** (optional, length = 10) <br/> Trial end date.  If the value is not indicated, the *trial_days* value from the plan will be used to calculate it.  If a date from the past is sent it will be interpreted as a subscription without trial days.  Format: yyyy-mm-dd.
source_id | ***string*** (optional, length = 45) <br/> Card token identifier, or the customer registered card which will be used to charge the subscription.
card | ***object*** (optional) <br/> Payment method that will be used to charge the subscription.  See [card object](#card-object).


###Response
Returns the updated [subscription object](#subscription-object) or an error response if an error occurred during the update.


##Get a Subscription

> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions/{SUBSCRIPTION_ID}
```

```php
<?
$customer = $openpay->customers->get(customerId);
$subscription = $customer->subscriptions->get(subscriptionId);
?>
```

```java
openpayAPI.subscriptions().get(String customerId, String customerId);
```

```csharp
openpayAPI.SubscriptionService.Get(string customer_id, string subscription_id);
```

```javascript
openpay.customers.subscriptions.get(customerId, subscriptionId, callback);
```

```ruby
#Customer
@subscriptions=@openpay.create(:subscriptions)
@subscriptions.get(subscription_id,customer_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/subscriptions/s0gmyor4yqtyv1miqwr0 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$subscription = $customer->subscriptions->get('s7ri24srbldoqqlfo4vp');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Subscription subscription = api.subscriptions().get("a9pvykxz4g5rg0fplze0", "s0gmyor4yqtyv1miqwr0");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Subscription subscription = api.SubscriptionService.Get("a9pvykxz4g5rg0fplze0", "s0gmyor4yqtyv1miqwr0");
```

```javascript
openpay.customers.subscriptions.get('ag4nktpdzebjiye1tlze', 's0gmyor4yqtyv1miqwr0', function(error, subscription){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@subscriptions=@openpay.create(:subscriptions)

response_hash=@subscriptions.get("s0gmyor4yqtyv1miqwr0", "pbi4kb8hpb64x0uud2eb")
```

> Response example

```json
{
   "id":"s0gmyor4yqtyv1miqwr0",
   "status":"trial",
   "card":{
      "type":"credit",
      "brand":"american_express",
      "address":null,
      "card_number":"343434XXXXX4343",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "allows_charges":true,
      "allows_payouts":false,
      "bank_name":"AMERICAN EXPRESS",
      "bank_code":"103"
   },
   "cancel_at_period_end":false,
   "charge_date":"2016-01-12",
   "creation_date":"2014-05-22T15:56:18-05:00",
   "current_period_number":0,
   "period_end_date":"2016-01-11",
   "trial_end_date":"2016-01-11",
   "plan_id":"pbi4kb8hpb64x0uud2eb",
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```

Gets the details of a customer subscription.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Subscription identifier.

###Response
Returns a [subscription object](#subscription-object).


##Cancel a Subscription

> Definition

```shell
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions/{SUBSCRIPTION_ID}
```

```php
<?
$customer = $openpay->customers->get(customerId);
$subscription = $customer->subscriptions->get(subscriptionId);
$subscription->delete();
?>
```

```java
openpayAPI.subscriptions().delete(String customerId, String subscriptionId);
```

```csharp
openpayAPI.SubscriptionService.Delete(string customer_id, string subscription_id);
```

```javascript
openpay.customers.subscriptions.delete(customerId, subscriptionId, callback);
```

```ruby
#Customer
@subscriptions=@openpay.create(:subscriptions)
@subscriptions.delete(subscription_id, customer_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/subscriptions/s0gmyor4yqtyv1miqwr0 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -X DELETE
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$subscription = $customer->subscriptions->get('s7ri24srbldoqqlfo4vp');
$subscription->delete();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.subscriptions().delete("a9pvykxz4g5rg0fplze0", "s0gmyor4yqtyv1miqwr0");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.SubscriptionService.Delete("a9pvykxz4g5rg0fplze0", "s0gmyor4yqtyv1miqwr0");
```

```javascript
openpay.customers.subscriptions.delete('ag4nktpdzebjiye1tlze', 's0gmyor4yqtyv1miqwr0', function(error){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@subscriptions=@openpay.create(:subscriptions)

@subscriptions.detele("s0gmyor4yqtyv1miqwr0", "pbi4kb8hpb64x0uud2eb")
```

Immediately cancels a customer subscription.  No more charges will be made to the card and all pending charges will be cancelled.

###Request
Property  | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Subscription identifier to cancel.

###Response
If the response was successfully cancelled the response will be empty.  Otherwise an [error object](#error-object) will be sent indicating the error reason.

##Subscription list
> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions
```

```php
<?
$customer = $openpay->customers->get(customerId);
$subscriptionList = $customer->subscriptions->getList(findDataRequest);
?>
```

```java
openpayAPI.subscriptions().list(String customerId, SearchParams request);
```

```csharp
openpayAPI.SubscriptionService.List(string customer_id, SearchParams request = null);
```

```javascript
openpay.customers.subscriptions.list(customerId, callback);
openpay.customers.subscriptions.list(customerId, searchParams, callback);
```

```ruby
#Customer
@subscriptions=@openpay.create(:subscriptions)
@subscriptions.all(customer_id)
```

> Request example

```shell
curl -g "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/subscriptions?limit=10" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$findData = array(
    'creation[gte]' => '2013-01-01',
    'creation[lte]' => '2013-12-31',
    'offset' => 0,
    'limit' => 5);

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$subscriptionList = $customer->subscriptions->getList($findData);
?>
```

```java
final Calendar dateGte = Calendar.getInstance();
final Calendar dateLte = Calendar.getInstance();
dateGte.set(2014, 5, 1, 0, 0, 0);
dateLte.set(2014, 5, 15, 0, 0, 0);

OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.creationGte(dateGte.getTime());
request.creationLte(dateLte.getTime());
request.offset(0);
request.limit(100);

List<Subscription> subscriptions = api.subscriptions().list("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;

List<Subscription> subscriptions = api.SubscriptionService.List("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var searchParams = {
  'limit' : 2
};

openpay.customers.subscriptions.list('ag4nktpdzebjiye1tlze', searchParams, function(error, list){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@subscriptions=@openpay.create(:subscriptions)

@subscriptions.all("pbi4kb8hpb64x0uud2eb")
```

> Response example

```json
[
   {
      "id":"s0gmyor4yqtyv1miqwr0",
      "status":"trial",
      "card":{
         "type":"credit",
         "brand":"american_express",
         "address":null,
         "card_number":"343434XXXXX4343",
         "holder_name":"Juan Perez Ramirez",
         "expiration_year":"20",
         "expiration_month":"12",
         "allows_charges":true,
         "allows_payouts":false,
         "bank_name":"AMERICAN EXPRESS",
         "bank_code":"103"
      },
      "cancel_at_period_end":false,
      "charge_date":"2016-01-12",
      "creation_date":"2014-05-22T15:56:18-05:00",
      "current_period_number":0,
      "period_end_date":"2016-01-11",
      "trial_end_date":"2016-01-11",
      "plan_id":"pbi4kb8hpb64x0uud2eb",
      "customer_id":"ag4nktpdzebjiye1tlze"
   }
]
```
Returns all the subscriptions active for an specific customer.

###Request
You can search using the following parameters:

Property  | Descriptions
--------- | ------
creation| ***date*** <br/> Same as creation date:  Format: yyyy-mm-dd.
creation[gte]| ***date*** <br/>After the creation date. Format: yyyy-mm-dd.
creation[lte]| ***date*** <br/>Before the creation date.  Format: yyyy-mm-dd.
offset| ***numeric*** <br/>Number of records to skip from the beggining, by default is 0.
limit| ***numeric*** <br/> Number of records to return, by default is 10.

###Response
A list of [subscription objects](#subscription-object) for a customer. Sort by creation date in descending order.
