#Charges
Charges can be made to cards, stores and banks. Each charge is assigned with an unique identifier in the system.

In card charges you can do by showing a form for the user to capture the card information.

<br><br>
**¡ IMPORTANT !**

**The handling and sending of data, as well as the capture of responses from each of the transactions is the responsibility of the commerce**

##With VPOS

This type of charge don’t requires a saved card or a previously generated token

> Definition

```shell
Merchant
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges
```

```php
<?
Merchant
$bbva->charges->create(chargeRequest);
?>
```

```java
//Merchant
bbvaAPI.charges().create(List<Parameter> request);
```

```csharp
//Merchant
bbvaAPI.ChargeService.Create(List<IParameter> request);
```

```ruby
#Merchant
@charges=@bbva.create(:charges)
@charges.create(request_hash)
```

> Merchant request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "affiliation_bbva" : "781500",
   "amount" : 100,
   "description" : "Init charge",
   "currency" : "MXN",
   "order_id" : "oid-00051",
   "customer": {
        "name": "Juan",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@example.com.mx",
        "phone_number": "555-444-3322"
   },
   "redirect_url": "https://micomercio.com"
}'
```

```csharp
BbvaAPI api = new BbvaAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");

ParameterContainer customer = new ParameterContainer("customer");
    customer.AddValue("name", "Juan");
    customer.AddValue("last_name", "Vazquez Juarez");
    customer.AddValue("email", "juan.vazquez@example.com.mx");
    customer.AddValue("phone_number", "554-170-3567");

ParameterContainer request = new ParameterContainer("charge");
    request.AddValue("affiliation_bbva", "781500");
    request.AddValue("amount", "100.00");
    request.AddValue("description", "Init charge");
    request.AddValue("currency", "MXN");
    request.AddValue("order_id", "oid-00051");
    request.AddValue("redirect_url", "https://sand-portal.ecommercebbva.com");
    request.AddMultiValue(customer):

Dictionary<String, Object> chargeDictionary = bbvaAPI.ChargeService.Create(request.ParameterValues);
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```java
BbvaAPI api = new BbvaAPI(
        "https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");

ParameterContainer customer = new ParameterContainer("customer");
    customer.addValue("name", "Juan");
    customer.addValue("last_name", "Vazquez Juarez");
    customer.addValue("email", "juan.vazquez@example.com.mx");
    customer.addValue("phone_number", "554-170-3567");

ParameterContainer charge = new ParameterContainer("charge");
    charge.addValue("affiliation_bbva", "781500");
    charge.addValue("amount", "100.00");
    charge.addValue("description", "Init charge");
    charge.addValue("currency", "MXN");
    charge.addValue("order_id", "oid-00051");
    charge.addValue("redirect_url", "https://sand-portal.ecommercebbva.com");
    charge.addMultiValue(customer);

Map chargeAsMap = api.charges().create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```php
<?
$bbva = Bbva::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$chargeRequest = array(
    'affiliation_bbva' => '781500',
    'amount' => 100,
    'description' => 'Init charge',
    'currency' => 'MXN',
    'order_id' => 'oid-00051',
    'redirect_url' => 'https://sand-portal.ecommercebbva.com',
    'customer' => array(
        'name' => 'Juan',
        'last_name' => 'Vazquez Juarez',
        'email' => 'juan.vazquez@example.com.mx',
        'phone_number' => '554-170-3567')
);

$charge = $bbva->charges->create($chargeRequest);
?>
```

```ruby
@bbva=BbvaApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bbva.create(:charges)
customer_hash={
    "name" => "Juan",
    "last_name" => "Vazquez Juarez",
    "phone_number" => "4423456723",
    "email" => "juan.vazquez@example.com.mx"
}

request_hash={
    "affiliation_bbva" => "781500",
    "amount" => 100.00,
    "currency" => "MXN",
    "description" => "Init charge",
    "order_id" => "oid-00051",
    "redirect_url" => "https://sand-portal.ecommercebbva.com",
    "customer" => customer_hash
}

response_hash=@charges.create(request_hash.to_hash)
```

> Response example

```json
{
    "id": "trz8v1n3g992xtylohts",
    "authorization": null,
    "operation_type": "in",
    "method": "card",
    "transaction_type": "charge",
    "status": "charge_pending",
    "conciliated": false,
    "creation_date": "2019-04-03T03:57:58-06:00",
    "operation_date": "2019-04-03T03:57:58-06:00",
    "description": "Pago",
    "error_message": null,
    "order_id": "oid-00051",
    "payment_method": {
        "type": "redirect",
        "url": "https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/trywj1kyx7vczirifkyw/card_capture"
    },
    "currency": "MXN",
    "amount": 100.00,
    "customer": {
        "name": "Juan",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@example.com.mx",
        "phone_number": "555-444-3322",
        "address": null,
        "creation_date": "2019-04-03T03:57:58-06:00",
        "external_id": null,
        "clabe": null
    }
}
```

###Request
Property | Description
--------- | -----
affiliation_bbva|               ***string*** (required) <br/>It must contain the affiliation number.
amount |                        ***numeric*** (required) <br/>Amount to charge. Must be an amount greater than zero, with up to two decimal digits.
description |                   ***string*** (required, length = 250) <br/>A description associated to the charge.
currency |                      ***string*** (optional) <br/>Charge currency type. Currently you can only use two currency types: Mexican pesos(MXN) y American dollars(USD).
order_id |                      ***string*** (optional, length = 100) <br/>Unique identifier of charge. Must be unique among all transactions.
[customer](##customer-object)|   ***object*** (required) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the merchant level<br/><br/> To create a customer and keep a record of their charges history refer to [Objeto Cliente](#objeto-cliente) (#create-a-new-customer) and do the charge at the customer level.
[payment_plan](#paymentplan-object)|    ***object*** (optional) <br/>Plan data months without interest is desired as use in the charge. Refer to [PaymentPlan Object](#paymentplan-object).
redirect_url |                          ***string*** (required) <br/>Used in redirect charges. It indicates the url to which redirect after a successful transaction in the BBVA payment form.
use_3d_secure |                         ***string*** (optional) <br/>By default the value is TRUE, if the trade has enabled the configuration to not use 3d secure, then you can send the parameter to FALSE.

###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

## With card

> Definition

```shell
Merchant
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges
```

```php
<?
Merchant
$bbva->charges->create(chargeRequest);
?>
```

```java
//Merchant
bbvaAPI.charges().create(List<Parameter> request);
```

```csharp
//Merchant
bbvaAPI.ChargeService.Create(List<IParameter> request);
```

```ruby
#Merchant
@charges=@bbva.create(:charges)
@charges.create(request_hash)
```

> Merchant request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "affiliation_bbva" : "781500",
   "amount" : 100,
   "description" : "Init charge",
   "currency" : "MXN",
   "order_id" : "oid-00051",
   "customer": {
        "name": "Juan",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@example.com.mx",
        "phone_number": "555-444-3322"
   },
   "card" : {
        "holder_name" : "Juan Vazquez",
        "card_number" : "4242424242424242",
        "expiration_month" : "12",
        "expiration_year" : "21",
        "cvv2" : "842"

   }
   "redirect_url": "https://micomercio.com"
}'
```

```csharp
BbvaAPI api = new BbvaAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");

ParameterContainer customer = new ParameterContainer("customer");
    customer.AddValue("name", "Juan");
    customer.AddValue("last_name", "Vazquez Juarez");
    customer.AddValue("email", "juan.vazquez@example.com.mx");
    customer.AddValue("phone_number", "554-170-3567");

ParameterContainer card = new ParameterContainer("card");
    customer.AddValue("holder_name", "Juan Vazquez Juarez");
    customer.AddValue("card_number", "4242424242424242");
    customer.AddValue("expiration_month", "12");
    customer.AddValue("expiration_year", "21");
    customer.AddValue("cvv2", "842");

ParameterContainer request = new ParameterContainer("charge");
    request.AddValue("affiliation_bbva", "781500");
    request.AddValue("amount", "100.00");
    request.AddValue("description", "Init charge");
    request.AddValue("currency", "MXN");
    request.AddValue("order_id", "oid-00051");
    request.AddValue("redirect_url", "https://sand-portal.ecommercebbva.com");
    request.AddMultiValue(customer);
    request.AddMultiValue(card):

Dictionary<String, Object> chargeDictionary = bbvaAPI.ChargeService.Create(request.ParameterValues);
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```java
BbvaAPI api = new BbvaAPI(
        "https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");

ParameterContainer customer = new ParameterContainer("customer");
    customer.addValue("name", "Juan");
    customer.addValue("last_name", "Vazquez Juarez");
    customer.addValue("email", "juan.vazquez@example.com.mx");
    customer.addValue("phone_number", "554-170-3567");

ParameterContainer card = new ParameterContainer("card");
    card.addValue("card_number", "4242424242424242");
    card.addValue("holder_name", "Juan Vazquez");
    card.addValue("expiration_year", "21");
    card.addValue("expiration_month", "12");
    card.addValue("cvv2", "842");

ParameterContainer charge = new ParameterContainer("charge");
    charge.addValue("affiliation_bbva", "781500");
    charge.addValue("amount", "100.00");
    charge.addValue("description", "Init charge");
    charge.addValue("currency", "MXN");
    charge.addValue("order_id", "oid-00051");
    charge.addValue("redirect_url", "https://sand-portal.ecommercebbva.com");
    charge.addMultiValue(customer);
    charge.addMultiValue(card);

Map chargeAsMap = api.charges().create(charge.getParameterValues());
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```php
<?
$bbva = Bbva::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$chargeRequest = array(
    'affiliation_bbva' => '781500',
    'amount' => 100,
    'description' => 'Init charge',
    'currency' => 'MXN',
    'order_id' => 'oid-00051',
    'redirect_url' => 'https://sand-portal.ecommercebbva.com',
    'card' => array(
            'holder_name' => 'Juan Vazquez',
            'card_number' => '4242424242424242',
            'expiration_month' => '12',
            'expiration_year' => '21'
            'cvv2' => '842'),
    'customer' => array(
        'name' => 'Juan',
        'last_name' => 'Vazquez Juarez',
        'email' => 'juan.vazquez@example.com.mx',
        'phone_number' => '554-170-3567')
);

$charge = $bbva->charges->create($chargeRequest);
?>
```

```ruby
@bbva=BbvaApi.new("mptdggroasfcmqs8plpy","sk_326c6d0443f6457aae29ffbd48f7d1be")
@charges=@bbva.create(:charges)
customer_hash={
    "name" => "Juan",
    "last_name" => "Vazquez Juarez",
    "phone_number" => "4423456723",
    "email" => "juan.vazquez@example.com.mx"
}

card_hash={
    "holder_name" => "Juan Vazquez",
    "card_number" => "4242424242424242",
    "expiration_month" => "12",
    "expiration_year" => "21",
    "cvv2" => "842"
}

request_hash={
    "affiliation_bbva" => "781500",
    "amount" => 100.00,
    "currency" => "MXN",
    "description" => "Init charge",
    "order_id" => "oid-00051",
    "redirect_url" => "https://sand-portal.ecommercebbva.com",
    "customer" => customer_hash,
    "card" => card_hash
}

response_hash=@charges.create(request_hash.to_hash)
```

> Response example

```json
{
    "id": "trocmtrnivm5scpfguvl",
    "authorization": "trocmtrnivm5scpfguvl",
    "operation_type": "in",
    "method": "card",
    "transaction_type": "charge",
    "card": {
        "type": "credit",
        "brand": "visa",
        "address": null,
        "card_number": "424242XXXXXX4242",
        "holder_name": "Juan Vazquez",
        "expiration_year": "21",
        "expiration_month": "12",
        "allows_charges": true,
        "allows_payouts": false,
        "bank_name": "BBVA",
        "points_type": "BBVA",
        "bank_code": "012",
        "points_card": true
    },
    "status": "charge_pending",
    "conciliated": true,
    "creation_date": "2019-04-24T10:43:06-05:00",
    "operation_date": "2019-04-24T10:43:06-05:00",
    "description": "Pago",
    "error_message": null,
    "order_id": "1556120584928",
    "amount": 105.32,
    "customer": {
        "name": "Juan",
        "last_name": "Perez",
        "email": "juanperez@example.com",
        "phone_number": "554-170-3567",
        "address": {
            "line1": "Calle Morelos #12 - 11",
            "line2": "Colonia Centro",
            "line3": "Cuauhtémoc",
            "state": "Queretaro",
            "city": "Queretaro",
            "postal_code": "12345",
            "country_code": "MX"
        },
        "creation_date": "2019-04-24T10:43:06-05:00",
        "external_id": null,
        "clabe": null
    },
    "payment_method": {
        "type": "redirect",
        "url": "https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/trocmtrnivm5scpfguvl/redirect/"
    },
    "currency": "MXN"
}
```

###Request
Property | Description
--------- | -----
affiliation_bbva|               ***string*** (required) <br/>It must contain the affiliation number.
amount |                        ***numeric*** (required) <br/>Amount to charge. Must be an amount greater than zero, with up to two decimal digits.
description |                   ***string*** (required, length = 250) <br/>A description associated to the charge.
currency |                      ***string*** (optional) <br/>Charge currency type. Currently you can only use two currency types: Mexican pesos(MXN) y American dollars(USD).
order_id |                      ***string*** (optional, length = 100) <br/>Unique identifier of charge. Must be unique among all transactions.
[customer](#customer-object)|   ***object*** (required) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the merchant level<br/><br/> To create a customer and keep a record of their charges history refer to [Objeto Cliente](#objeto-cliente) (#create-a-new-customer) and do the charge at the customer level.
[card](#card-object)|    ***object*** (required) <br/> Card information where the funds are withdrawn.
redirect_url |                          ***string*** (required) <br/>Used in redirect charges. It indicates the url to which redirect after a successful transaction in the BBVA payment form.
use_3d_secure |                         ***string*** (optional) <br/>By default the value is TRUE, if the trade has enabled the configuration to not use 3d secure, then you can send the parameter to FALSE.

###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

##Confirming a charge

> Definition

```shell
Merchant
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/capture
```

```php
<?
Merchant
$charge = $bbva->charges->get(transactionId);
$charge->capture(captureData);
?>
```

```java
//Merchant
bbvaAPI.charges().confirmCapture(ConfirmCaptureParams request);
```

```csharp
//Merchant
bbvaAPI.ChargeService.Capture(string transaction_id, Decimal? amount);
```

```javascript
// Merchant
bbva.charges.capture(transactionId, captureRequest, callback);
```

```ruby
#Merchant
@charges=@bbva.create(:charges)
@charges.capture(transaction_id)
```

> Merchant request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/tryqihxac3msedn4yxed/capture \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be: \
   -H "Content-type: application/json" \
   -X POST -d '{
    "amount" : 100.00
} '
```

```php
<?
$bbva = Bbva::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$captureData = array('amount' => 100.00);

$charge = $bbva->charges->get('ag4nktpdzebjiye1tlze');
$charge->capture($captureData);
?>
```

```java
BbvaAPI api = new BbvaAPI("https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
ConfirmCaptureParams request = new ConfirmCaptureParams();
request.chargeId("tryqihxac3msedn4yxed");
request.amount(new BigDecimal("100.00"));

Charge charge = api.charges().confirmCapture("ag4nktpdzebjiye1tlze", request);
```

```csharp
BbvaAPI api = new BbvaAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
Charge charge = api.ChargeService.Capture("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", new Decimal(100.00));
```

```ruby
@bbva=BbvaApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bbva.create(:charges)

response_hash=@charges.capture("tryqihxac3msedn4yxed", "ag4nktpdzebjiye1tlze")
```

> Response example

```json
{
   "id":"tryqihxac3msedn4yxed",
   "amount":100.00,
   "authorization":"801585",
   "method":"card",
   "operation_type":"in",
   "transaction_type":"charge",
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
   "status":"completed",
   "currency":"MXN",
   "creation_date":"2014-05-26T14:00:17-05:00",
   "operation_date":"2014-05-26T14:00:17-05:00",
   "description":"Init charge",
   "error_message":null,
   "order_id":null,
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```
Confirm a charge created with the <code>capture = "false" </code> property, this method is the second part of the [create a charge with a card] (#with-a-card-id-or-token) and it can confirm the amount captured on the first call or a lesser amount.


**Note:** You only can confirm charges via card. To cancel the charge created you should make a call to the method [charge refund] (#charge-refund)



###Request

Property | Description
--------- | -----
amount | ***numeric*** (required) <br/>Amount to confirm. It can be less than or equal to the amount given with up to two decimal digits


###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

##Refunding a charge

> Definition

```shell
Merchant
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/refund
```

```php
<?
Merchant
$charge = $bbva->charges->get(transactionId);
$charge->refund(refundData);
?>
```

```java
//Merchant
bbvaAPI.charges().refund(RefundParams request);
```

```csharp
//Merchant
bbvaAPI.ChargeService.Refund(string transaction_id, string description);
```

```ruby
#Merchant
@charges=@bbva.create(:charges)
@charges.refund(transaction_id, request_hash)
```

> Merchant request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/tr6cxbcefzatd10guvvw/refund \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "description" : "devolución",
   "amount" : 100.00
} '
```

```php
<?
$bbva = Bbva::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$refundData = array(
    'description' => 'devolución',
    'amount' => 100);

$charge = $bbva->charges->get('ag4nktpdzebjiye1tlze');
$charge->refund(refundData);
?>
```

```java
BbvaAPI api = new BbvaAPI("https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
RefundParams request = new RefundParams();
request.chargeId("tryqihxac3msedn4yxed");
request.description("Monto de cargo devuelto");
request.amount(new BigDecimal("100.00"));

Charge charge = api.charges().refund("ag4nktpdzebjiye1tlze", request);
```

```csharp
BbvaAPI api = new BbvaAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
Charge charge = api.ChargeService.Refund("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", "Monto de cargo devuelto", , new Decimal(100.00));
```

```ruby
@bbva=BbvaApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bbva.create(:charges)

request_hash={
     "description" => "Monto de cargo devuelto",
     "amount" => 100.00
   }

response_hash=@charges.refund("tryqihxac3msedn4yxed", request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Response example

```json
{
   "id":"tr6cxbcefzatd10guvvw",
   "amount":100.00,
   "authorization":"801585",
   "method":"card",
   "operation_type":"in",
   "transaction_type":"charge",
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
   "status":"completed",
   "refund":{
      "id":"trcbsmjkroqmjobxqhpb",
      "amount":100.00,
      "authorization":"801585",
      "method":"card",
      "operation_type":"out",
      "transaction_type":"refund",
      "status":"completed",
      "currency":"MXN",
      "creation_date":"2014-05-26T13:56:21-05:00",
      "operation_date":"2014-05-26T13:56:21-05:00",
      "description":"devolucion",
      "error_message":null,
      "order_id":null,
      "customer_id":"ag4nktpdzebjiye1tlze"
   },
   "currency":"MXN",
   "creation_date":"2014-05-26T11:56:25-05:00",
   "operation_date":"2014-05-26T11:56:25-05:00",
   "description":"Init charge",
   "error_message":null,
   "order_id":"oid-00052",
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```
You can use this method if you want to make a charge refund to a card. The amount to be returned will be the total charge or a lower amount. Note that the refund may be delayed in the statement of your customer for 1-3 business days.

<aside class="notice">
**Note:** Only charges via card can be refunded.
</aside>


###Request

Property | Description
--------- | -----
description | ***string*** (optional, length = 250) <br/>Text to describe the refund reason.
amount | ***numeric*** (opcional) <br/>Amount to refund. Must be an amount greater than zero and lesser or equal than the original amount, with up to two decimal digits.


###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).


##Get a charge
> Definition

```shell
Merchant
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}
```

```php
<?
Merchant
$charge = $bbva->charges->get(transactionId);
?>
```

```java
//Merchant
bbvaAPI.charges().get(String transactionId);
```

```csharp
//Merchant
bbvaAPI.ChargeService.Get(string transaction_id);
```

```ruby
#Merchant
@charges=@bbva.create(:charges)
@charges.get(transaction_id)
```

> Merchant request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/tr6cxbcefzatd10guvvw \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be:
```

```php
<?
$bbva = Bbva::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$charge = $bbva->charges->get('tr6cxbcefzatd10guvvw');
?>
```

```java
BbvaAPI api = new BbvaAPI("https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
Charge charge = api.charges().get("ag4nktpdzebjiye1tlze", "tr6cxbcefzatd10guvvw");
```

```csharp
BbvaAPI api = new BbvaAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
Charge charge = api.ChargeService.Get("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed");
```

```ruby
@bbva=BbvaApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bbva.create(:charges)

response_hash=@charges.get("tr6cxbcefzatd10guvvw", "ag4nktpdzebjiye1tlze")
```

> Response example

```json
{
   "id":"tr6cxbcefzatd10guvvw",
   "amount":100.00,
   "authorization":"801585",
   "method":"card",
   "operation_type":"in",
   "transaction_type":"charge",
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
   "status":"completed",
   "refund":{
      "id":"trcbsmjkroqmjobxqhpb",
      "amount":100.00,
      "authorization":"801585",
      "method":"card",
      "operation_type":"out",
      "transaction_type":"refund",
      "status":"completed",
      "currency":"MXN",
      "creation_date":"2014-05-26T13:56:21-05:00",
      "operation_date":"2014-05-26T13:56:21-05:00",
      "description":"devolucion",
      "error_message":null,
      "order_id":null,
      "customer_id":"ag4nktpdzebjiye1tlze"
   },
   "currency":"MXN",
   "creation_date":"2014-05-26T11:56:25-05:00",
   "operation_date":"2014-05-26T11:56:25-05:00",
   "description":"Init charge",
   "error_message":null,
   "order_id":"oid-00052",
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```

Returns the information of a charge generated at any moment, only by knowing the charge id.

###Request

Property | Description
--------- | ------
transaction_id| _**string**_ (required, length = 45)<br/>Charge Id.

###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object)..

##List of charges

> Definition


```shell
Merchant
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges
```

```php
<?
Merchant
$chargeList = $bbva->charges->getList(searchParams);
?>
```

```java
//Merchant
bbvaAPI.charges().list(SearchParams request);
```

```csharp
//Merchant
bbvaAPI.ChargeService.List(SearchParams request = null);
```

```javascript
// Customer
bbva.customers.charges.list(customerId, callback);
bbva.customers.charges.list(customerId, searchParams, callback);
```

```ruby
#Merchant
@charges=@bbva.create(:charges)
@charges.all
```

> Merchant request example

```shell
curl -g "https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges?creation[gte]=2013-11-01&limit=2" \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be:
```

```php
<?
$bbva = Bbva::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$searchParams = array(
    'creation[gte]' => '2013-11-01',
    'creation[lte]' => '2014-11-01',
    'offset' => 0,
    'limit' => 2);

$customer = $bbva->customers->get('ag4nktpdzebjiye1tlze');
$chargeList = $customer->charges->getList($searchParams);
?>
```

```java
final Calendar dateGte = Calendar.getInstance();
final Calendar dateLte = Calendar.getInstance();
dateGte.set(2014, 5, 1, 0, 0, 0);
dateLte.set(2014, 5, 15, 0, 0, 0);

BbvaAPI api = new BbvaAPI("https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
SearchParams request = new SearchParams();
request.creationGte(dateGte.getTime());
request.creationLte(dateLte.getTime());
request.offset(0);
request.limit(100);
request.amount(new BigDecimal("100.00"));

List<Charge> charges = api.charges().list("ag4nktpdzebjiye1tlze", request);
```

```csharp
BbvaAPI api = new BbvaAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;
request.Amount = new Decimal(100.00);

List<Charge> charges= bbvaAPI.ChargeService.List("ag4nktpdzebjiye1tlze", request);
```

```javascript
var searchParams = {
  'creation[gte]' : '2013-11-01',
  'limit' : 2
};

bbva.customers.charges.list('ag4nktpdzebjiye1tlze',searchParams, function(error, chargeList) {
  // ...
});
```

```ruby
@bbva=BbvaApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bbva.create(:charges)

response_hash=@charges.all("ag4nktpdzebjiye1tlze")
```

> Response example

```json
[
   {
      "id":"tryqihxac3msedn4yxed",
      "amount":100.00,
      "authorization":"801585",
      "method":"card",
      "operation_type":"in",
      "transaction_type":"charge",
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
      "status":"completed",
      "currency":"MXN",
      "creation_date":"2014-05-26T14:00:17-05:00",
      "operation_date":"2014-05-26T14:00:17-05:00",
      "description":"Init charge",
      "error_message":null,
      "order_id":null,
      "customer_id":"ag4nktpdzebjiye1tlze"
   },
   {
      "id":"trnzf2xjwpupjfryyj23",
      "amount":100.00,
      "authorization":null,
      "method":"bank_account",
      "operation_type":"in",
      "transaction_type":"charge",
      "status":"in_progress",
      "currency":"MXN",
      "creation_date":"2014-05-26T13:51:25-05:00",
      "operation_date":"2014-05-26T13:51:25-05:00",
      "description":"Cargo con banco",
      "error_message":null,
      "order_id":"oid-00055",
      "customer_id":"ag4nktpdzebjiye1tlze",
      "payment_method":{
         "type":"bank_transfer",
         "agreement" : "1411217",
         "bank":"BBVA",
         "clabe":"012914002014112176",
         "name":"11030021342311520255"
      }
   }
]
```
Gets a list of the charges made by Merchant or customer.

###Request
You can search using the following parameters as filters.

Property | Description
--------- | ------
order_id| ***string*** <br/>Unique order id generated by the merchant and associated to the transaction by the order_id field of the charge request.
creation| ***date*** <br/>Same as creation date. Format yyyy-mm-dd
creation[gte]| ***date*** <br/>After the creation date. Format yyyy-mm-dd
creation[lte]| ***date*** <br/>Before the creation date. Format yyyy-mm-dd
offset| ***numeric*** <br/>Number of records to skip at the beginning, default 0.
limit| ***numeric*** <br/>Number of required records, default 10.
amount| ***numeric*** <br/>Same as the amount.
amount[gte] | ***numeric*** <br/>Greater than or equal to the amount.
amount[lte] | ***numeric*** <br/>Less than or equal to the amount.
[status](#object-transaction-status) | ***TransactionStatus*** <br/>Estado de la transacción (IN_PROGRESS,COMPLETED,REFUNDED,CHARGE_PENDING,CANCELLED,FAILED).

###Response

Returns an array of [transaction objects](#transaction-object) charges in descending order by creation date.
