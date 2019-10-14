#Charges
Charges can be made to cards and PSE. Each charge is assigned with an unique identifier in the system.

You can do card charges by using a saved card id, using a token or you can send the card information at the time of invocation.

##With a card id or token

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/charges

Customer
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Merchant
$openpay->charges->create(chargeRequest);

Customer
$customer = $openpay->customers->get($customerId);
$customer->charges->create(chargeRequest);
?>
```

```java
//Customer
openpayAPI.charges().create(String customerId, CreateCardChargeParams request);

//Merchant
openpayAPI.charges().create(CreateCardChargeParams request);
```

```javascript
// Merchant
openpay.charges.create(chargeRequest, callback);

// Customer
openpay.customers.charges.create(customerId, chargeRequest, callback);
```

```csharp
//Customer
openpayAPI.ChargeService.Create(string customer_id, ChargeRequest request);

//Merchant
openpayAPI.ChargeService.Create(ChargeRequest request);
```

```ruby
#Customer
@charges=@openpay.create(:charges)
@charges.create(request_hash, customer_id)

#Merchant
@charges=@openpay.create(:charges)
@charges.create(request_hash)
```

> Merchant request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln3bqtms6o3kck2f/charges \
   -u sk_e562c42a6q384b2ab02cd47d2n301uwk: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "source_id" : "kdx205scoizh93upqbte",
   "method" : "card",
   "amount" : 716,
   "currency" : "COP",
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-12324",
   "device_session_id" : "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f",
   "iva": "10",
   "customer" : {
        "name" : "Cliente Colombia",
        "last_name" : "Vazquez Juarez",
        "phone_number" : "4448936475",
        "email" : "juan.vazquez@empresa.co"
   }
}'
```

```php
<?
$openpay = Openpay::getInstance('mzdtln3bqtms6o3kck2f', 'sk_e562c42a6q384b2ab02cd47d2n301uwk');
$customer = array(
   	 'name' => 'Juan',
   	 'last_name' => 'Vazquez Juarez',
   	 'phone_number' => '571627926831',
   	 'email' => 'juan.vazquez@empresa.co');

$chargeRequest = array(
    'method' => 'card',
    'source_id' => 'kqgykn96i7bcs1wwhvgw',
    'amount' => 716,
    'currency' => 'COP'
    'description' => 'Cargo inicial a mi merchant',
    'order_id' => 'oid-00051',
    'device_session_id' => 'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f',
    'customer' => $customer);

$charge = $openpay->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateCardChargeParams request = new CreateCardChargeParams();
Customer customer = new Customer();
customer.setName("Juan");
customer.setLastName("Vazquez Juarez");
customer.setPhoneNumber("571627926831");
customer.setEmail("juan.vazquez@empresa.co");

request.cardId("kqgykn96i7bcs1wwhvgw"); // =source_id
request.amount(new BigDecimal("716"));
request.currency("COP");
request.description("Cargo inicial a mi merchant");
request.orderId("oid-00051");
request.deviceSessionId("kR1MiQhz2otdIuUlQkbEyitIqVMiI16f");
request.setCustomer(customer);

Charge charge = api.charges().create(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

Customer customer = new Customer();
customer.Name = "Juan";
customer.LastName = "Vazquez Juarez";
customer.PhoneNumber = "571627926831";
customer.Email = "juan.vazquez@empresa.co";

ChargeRequest request = new ChargeRequest();
request.Method = "card";
request.SourceId = "kwkoqpg6fcvfse8k8mg2";
request.Amount = new Decimal(716);
request.Currency = "COP";
request.Description = "Cargo inicial a mi merchant";
request.OrderId = "oid-00051";
request.DeviceSessionId = "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f";
request.Customer = customer;

Charge charge = api.ChargeService.Create(request);
```

```javascript
var chargeRequest = {
   'source_id' : 'kqgykn96i7bcs1wwhvgw',
   'method' : 'card',
   'amount' : 716,
   'currency' : 'COP',
   'description' : 'Cargo inicial a mi cuenta',
   'order_id' : 'oid-00051',
   'device_session_id' : 'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f',
   'customer' : {
   	    'name' : 'Juan',
   	    'last_name' : 'Vazquez Juarez',
   	    'phone_number' : '571627926831',
   	    'email' : 'juan.vazquez@empresa.co'
   }
}

openpay.charges.create(chargeRequest, function(error, charge) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)
customer_hash={
    "name" => "Juan",
    "last_name" => "Vazquez Juarez",
    "phone_number" => "571627926831",
    "email" => "juan.vazquez@empresa.co"
}

request_hash={
    "method" => "card",
    "source_id" => "kqgykn96i7bcs1wwhvgw",
    "amount" => Float(716),
    "currency" => "COP",
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
    "device_session_id" => "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f",
    "customer" => customer_hash
}

response_hash=@charges.create(request_hash.to_hash)
```

> Response example

```json
{
    "id": "trbeuhyvmkr3b9jitajp",
    "authorization": "1128731327",
    "operation_type": "in",
    "method": "card",
    "transaction_type": "charge",
    "card": {
        "id": "kdx205scoizh93upqbte",
        "type": "credit",
        "brand": "diners",
        "address": null,
        "card_number": "367284XXXX3333",
        "holder_name": "DinnersClub",
        "expiration_year": "21",
        "expiration_month": "07",
        "allows_charges": true,
        "allows_payouts": false,
        "creation_date": "2019-08-09T13:35:48-05:00",
        "bank_name": "BANCO DE BOGOTÁ",
        "bank_code": "000"
    },
    "status": "completed",
    "conciliated": true,
    "iva": "10",
    "creation_date": "2019-08-12T12:36:56-05:00",
    "operation_date": "2019-08-12T12:36:56-05:00",
    "description": "Ejemplo cargo",
    "error_message": null,
    "order_id": "oid-12330",
    "currency": "COP",
    "amount": 716,
    "customer": {
        "name": "Cliente Colombia",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.co",
        "phone_number": "4448936475",
        "address": null,
        "creation_date": "2019-08-12T12:36:56-05:00",
        "external_id": null,
        "clabe": null
    },
    "fee": {
        "amount": 21.81,
        "tax": 3.4896,
        "currency": "COP"
    }
}
```

This type of charge requires a saved card or a previously generated token. To save cards read [Create a card] (#create-a-card) and to use tokens visit the [Creation of tokens] (#create-a-new-token) section.

Once you have a saved card or token use the <code>source_id</code> property to send the identifier.

The <code>device_session_id</code> property must be generated using JavaScript API, see [Fraud detection using device data](https://github.com/open-pay/openpay-js#fraud-detection-using-device-data).

<aside class="notice">
You can charge the merchant account or the customer account.
</aside>

***Customized antifraud system***</br>
You can send extra data to Openpay in order to increase number of variables and get better results in antifraud detection for your transactions.

<aside class="notice">
If you want to use this feature you need to send <code>metadata</code> property with all fields you think can help to decide when a transaction is a fraud trying. Call support line to enable this feature</br>
</aside>

###Request

Property | Description
--------- | -----
method|***string*** (required) <br/>It must contain the **card** value in order to specify the charge will be made from card.
source_id | ***string*** (required, length = 45) <br/>Saved ID card or token id created from where the funds are withdrawn.
amount | ***numeric*** (required) <br/>Amount to charge. Must be an amount greater than zero.
currency | ***string*** (optional) <br/>currency for charge. At the moment only 1 type of currency is supported: Colombian Peso (COP).
cvv2 |***numeric***  (length = 3 or 4) <br/>Security code as it appears on the back of the card. Usually 3 digits.<br/>It's used only charges with [Stored Cards](#create-a-card).
description | ***string*** (required, length = 250) <br/>A description associated to the charge.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of charge. Must be unique among all transactions.
device_session_id |  ***string*** (required, length = 255) <br/>Identifier of the device generated by the antifraud tool.
[customer](#create-a-new-customer)| ***object*** (required) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the merchant level<br/><br/> To create a customer and keep a record of their charges history refer to [create a customer] (#create-a-new-customer) and do the charge at the customer level.
[payment_plan](#objetc-paymentplan)|***object*** (opcional) <br/>Plan data months without interest is desired as use in the charge. Refer to [PaymentPlan Object](#paymentplan-objetc).
metadata |  ***list(key, value)*** (optional) <br/>Field list to send antifraud system, It must be according to [Rules to send custom antifraud fields] (#custom-to-send-antifraud-fields).


###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

##With redirect

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/charges

Customer
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Merchant
$openpay->charges->create(chargeRequest);

Customer
$customer = $openpay->customers->get($customerId);
$customer->charges->create(chargeRequest);
?>
```

```java
//Customer
openpayAPI.charges().create(String customerId, CreateCardChargeParams request);

//Merchant
openpayAPI.charges().create(CreateCardChargeParams request);
```

```javascript
// Merchant
openpay.charges.create(chargeRequest, callback);

// Customer
openpay.customers.charges.create(customerId, chargeRequest, callback);
```

```csharp
//Customer
openpayAPI.ChargeService.Create(string customer_id, ChargeRequest request);

//Merchant
openpayAPI.ChargeService.Create(ChargeRequest request);
```

```ruby
#Customer
@charges=@openpay.create(:charges)
@charges.create(request_hash, customer_id)

#Merchant
@charges=@openpay.create(:charges)
@charges.create(request_hash)
```

> Merchant request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln3bqtms6o3kck2f/charges \
   -u sk_e562c42a6q384b2ab02cd47d2n301uwk: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method" : "card",
   "amount" : 716,
   "currency":"COP",
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-11152",
   "customer" : {
        "name" : "Juan",
        "last_name" : "Vazquez Juarez",
        "phone_number" : "4423456723",
        "email" : "juan.vazquez@empresa.co"
   },
   "iva": "10",
   "confirm" : "false",
   "send_email":"false",
   "redirect_url":"http://www.openpay.co/index.html"
}'
```

```php
<?
$openpay = Openpay::getInstance('mzdtln3bqtms6o3kck2f', 'sk_e562c42a6q384b2ab02cd47d2n301uwk');
$customer = array(
     'name' => 'Juan',
     'last_name' => 'Vazquez Juarez',
     'phone_number' => '4423456723',
     'email' => 'juan.vazquez@empresa.co');

$chargeRequest = array(
    "method" : "card",
    'amount' => 716,
    "currency"=> "COP",
    'description' => 'Cargo terminal virtual a mi merchant',
    'customer' => $customer,
    'send_email' => false,
    'confirm' => false,
    'redirect_url' => 'http://www.openpay.co/index.html')
;

$charge = $openpay->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateCardChargeParams request = new CreateCardChargeParams();
Customer customer = new Customer();
customer.setName("Juan");
customer.setLastName("Vazquez Juarez");
customer.setPhoneNumber("4423456723");
customer.setEmail("juan.vazquez@empresa.co");

request.amount(new BigDecimal("716"));
request.description("Cargo inicial a mi merchant");
request.orderId("oid-00051");
request.setCustomer(customer);
request.setSendEmail(false);
request.setConfirm(false);
request.setRedirectUrl("http://www.openpay.co/index.html");

Charge charge = api.charges().create(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ChargeRequest request = new ChargeRequest();
Customer customer = new Customer();
customer.Name = "Juan";
customer.LastName = "Vazquez Juarez";
customer.PhoneNumber = "4423456723";
customer.Email = "juan.vazquez@empresa.co";

request.Method = "card";
request.Amount = new Decimal(716);
request.Description = "Cargo inicial a mi merchant";
request.OrderId = "oid-00051";
request.Confirm = false;
request.SendEmail = false;
request.RedirectUrl = "http://www.openpay.co/index.html";
request.Customer = customer;

Charge charge = api.ChargeService.Create(request);
```

```javascript
var chargeRequest = {
   'method' : 'card',
   'amount' : 716,
   'currency': 'COP',
   'description' : 'Cargo inicial a mi cuenta',
   'order_id' : 'oid-00051',
   'customer' : {
        'name' : 'Juan',
        'last_name' : 'Vazquez Juarez',
        'phone_number' : '4423456723',
        'email' : 'juan.vazquez@empresa.co'
   },
  'send_email' : false,
  'confirm' : false,
  'redirect_url' : 'http://www.openpay.co/index.html')
}

openpay.charges.create(chargeRequest, function(error, charge) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)
customer_hash={
    "name" => "Juan",
    "last_name" => "Vazquez Juarez",
    "phone_number" => "4423456723",
    "email" => "juan.vazquez@empresa.co"
}

request_hash={
    "method" => "card",
    "amount" => Float(716),
    "currency" => "COP",
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
    "customer" => customer_hash,
    "send_email" => false,
    "confirm" => false,
    "redirect_url" => "http://www.openpay.co/index.html"
}

response_hash=@charges.create(request_hash.to_hash)
```

> Response example

```json

{
    "id": "tro1ezxbfn5c8lvzhfcr",
    "authorization": null,
    "operation_type": "in",
    "method": "card",
    "transaction_type": "charge",
    "status": "charge_pending",
    "conciliated": false,
    "iva": "10",
    "creation_date": "2019-08-12T12:47:41-05:00",
    "operation_date": "2019-08-12T12:47:41-05:00",
    "description": "Cargo inicial a mi cuenta",
    "error_message": null,
    "order_id": "oid-11153",
    "payment_method": {
        "type": "redirect",
        "url": "https://sandbox-api.openpay.co/v1/mpixehq7z4xupfwoohrm/charges/tro1ezxbfn5c8lvzhfcr/card_capture"
    },
    "currency": "COP",
    "amount": 716,
    "customer": {
        "name": "Juan",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.co",
        "phone_number": "4423456723",
        "address": null,
        "creation_date": "2019-08-12T12:47:41-05:00",
        "external_id": null,
        "clabe": null
    }
}
```

This type of charge don't requires a saved card or a previously generated token

###Request

Property | Description
--------- | -----
method|***string*** (required in card) <br/>It must contain the card value in order to specify the charge will be made from card.
amount | ***numeric*** (required) <br/>Amount to charge. Must be an amount greater than zero.
currency | ***string*** (optional) <br/>currency for charge. At the moment only 1 type of currency is supported: Colombian Peso (COP).
description | ***string*** (required, length = 250) <br/>A description associated to the charge.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of charge. Must be unique among all transactions.
[customer](#create-a-new-customer)| ***object*** (required) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the merchant level<br/><br/> To create a customer and keep a record of their charges history refer to [create a customer] (#create-a-new-customer) and do the charge at the customer level.
confirm |  ***boolean*** (required in false) <br/>Indicates whether the charge is made immediately or not , when the value is false the charge is handled as authorized (or pre-authorization) and the amount is only to be confirmed or canceled in a second call.
send_email | ***boolean*** (optional) <br/>Indicates if is need send a email that redirect to the openpay payment form.
redirect_url | ***string*** (required) <br/>It indicates the url to which redirect after a successful transaction in the openpay payment form.
currency | ***string*** (required) <br/> Currency used in the operation

###Respuesta
Response an [objeto de transacción](#objeto-transacci-n) with payment info or a [respuesta de error](#objeto-error).



You can use this method if you want to make a charge refund to a card. The amount to be returned will be the total charge or a lower amount. Note that the refund may be delayed in the statement of your customer for 1-3 business days.

<aside class="notice">
**Note:** Only charges via card can be refunded.
</aside>


###Request

Property | Description
--------- | -----
description | ***string*** (optional, length = 250) <br/>Text to describe the refund reason.
amount | ***numeric*** (opcional) <br/>Amount to refund. Must be an amount greater than zero and lesser or equal than the original amount.


###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).


##Get a charge
> Definition

```shell
Merchant
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}

Merchant
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}
```

```php
<?
Merchant
$charge = $openpay->charges->get(transactionId);

Customer
$customer = $openpay->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
?>
```

```java
//Customer
openpayAPI.charges().get(String customerId, String transactionId);

//Merchant
openpayAPI.charges().get(String transactionId);
```

```csharp
//Customer
openpayAPI.ChargeService.Get(string customer_id, string transaction_id);

//Merchant
openpayAPI.ChargeService.Get(string transaction_id);
```

```javascript
// Merchant
openpay.charges.get(transactionId, callback);

// Customer
openpay.customers.charges.get(customerId, transactionId, callback);
```

```ruby
#Customer
@charges=@openpay.create(:charges)
@charges.get(transaction_id, customerId)

#Merchant
@charges=@openpay.create(:charges)
@charges.get(transaction_id)
```

> Customer request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln3bqtms6o3kck2f/customers/ag9nkpvdzebjiye5tlzi/charges/tr6cxbcefzatd10guvvw \
   -u sk_e562c42a6q384b2ab02cd47d2n301uwk:
```

```php
<?
$openpay = Openpay::getInstance('mzdtln3bqtms6o3kck2f', 'sk_e562c42a6q384b2ab02cd47d2n301uwk');

$customer = $openpay->customers->get('ag9nkpvdzebjiye5tlzi');
$charge = $customer->charges->get('tr6cxbcefzatd10guvvw');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.charges().get("ag9nkpvdzebjiye5tlzi", "tr6cxbcefzatd10guvvw");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.ChargeService.Get("ag9nkpvdzebjiye5tlzi", "tryqihxac3msedn4yxed");
```

```javascript
openpay.customers.charges.get('ag9nkpvdzebjiye5tlzi', 'tr6cxbcefzatd10guvvw', function(error, charge){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)

response_hash=@charges.get("tr6cxbcefzatd10guvvw", "ag9nkpvdzebjiye5tlzi")
```

> Response example

```json
{
    "id": "trsc2di0dymydqkm5ieo",
    "authorization": "194883321",
    "operation_type": "in",
    "method": "card",
    "transaction_type": "charge",
    "card": {
        "id": "kdx205scoizh93upqbte",
        "type": "credit",
        "brand": "diners",
        "address": null,
        "card_number": "367284XXXX3333",
        "holder_name": "DinnersClub",
        "expiration_year": "21",
        "expiration_month": "07",
        "allows_charges": true,
        "allows_payouts": false,
        "creation_date": "2019-08-09T13:35:48-05:00",
        "bank_name": "BANCO DE BOGOTÁ",
        "bank_code": "000"
    },
    "status": "completed",
    "conciliated": true,
    "creation_date": "2019-08-12T13:02:18-05:00",
    "operation_date": "2019-08-12T13:02:18-05:00",
    "description": "Ejemplo cargo",
    "error_message": null,
    "order_id": "oid-12331",
    "currency": "COP",
    "amount": 716,
    "customer": {
        "name": "Cliente Colombia",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.co",
        "phone_number": "4448936475",
        "address": null,
        "creation_date": "2019-08-12T13:02:18-05:00",
        "external_id": null,
        "clabe": null
    },
    "fee": {
        "amount": 21.8100,
        "tax": 3.4896,
        "currency": "COP"
    }
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
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/charges

Merchant
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Merchant
$chargeList = $openpay->charges->getList(searchParams);

Customer
$customer = $openpay->customers->get(customerId);
$chargeList = $customer->charges->getList(searchParams);
?>
```

```java
//Customer
openpayAPI.charges().list(String customerId, SearchParams request);

//Merchant
openpayAPI.charges().list(SearchParams request);
```

```csharp
//Customer
openpayAPI.ChargeService.List(string customer_id, SearchParams request = null);

//Merchant
openpayAPI.ChargeService.List(SearchParams request = null);
```

```javascript
// Merchant
openpay.charges.list(callback);
openpay.charges.list(searchParams, callback);

// Customer
openpay.customers.charges.list(customerId, callback);
openpay.customers.charges.list(customerId, searchParams, callback);
```

```ruby
#Customer
@charges=@openpay.create(:charges)
@charges.all(customer_id)

#Merchant
@charges=@openpay.create(:charges)
@charges.all
```

> Customer request example

```shell
curl -g "https://sandbox-api.openpay.co/v1/mzdtln3bqtms6o3kck2f/customers/ag9nkpvdzebjiye5tlzi/charges?creation[gte]=2018-11-01&limit=2" \
   -u sk_e562c42a6q384b2ab02cd47d2n301uwk:  
```

```php
<?
$openpay = Openpay::getInstance('mzdtln3bqtms6o3kck2f', 'sk_e562c42a6q384b2ab02cd47d2n301uwk');

$searchParams = array(
    'creation[gte]' => '2018-11-01',
    'creation[lte]' => '2019-11-01',
    'offset' => 0,
    'limit' => 2);

$customer = $openpay->customers->get('ag9nkpvdzebjiye5tlzi');
$chargeList = $customer->charges->getList($searchParams);
?>
```

```java
final Calendar dateGte = Calendar.getInstance();
final Calendar dateLte = Calendar.getInstance();
dateGte.set(2019, 5, 1, 0, 0, 0);
dateLte.set(2019, 5, 15, 0, 0, 0);

OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.creationGte(dateGte.getTime());
request.creationLte(dateLte.getTime());
request.offset(0);
request.limit(100);
request.amount(new BigDecimal("716"));

List<Charge> charges = api.charges().list("ag9nkpvdzebjiye5tlzi", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2019, 5, 1);
request.CreationLte = new DateTime(2019, 5, 15);
request.Offset = 0;
request.Limit = 100;
request.Amount = new Decimal(716);

List<Charge> charges= openpayAPI.ChargeService.List("ag9nkpvdzebjiye5tlzi", request);
```

```javascript
var searchParams = {
  'creation[gte]' : '2018-11-01',
  'limit' : 2
};

openpay.customers.charges.list('ag9nkpvdzebjiye5tlzi',searchParams, function(error, chargeList) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)

response_hash=@charges.all("ag9nkpvdzebjiye5tlzi")
```

> Response example

```json
[
    {
        "id": "trsc2di0dymydqkm5ieo",
        "authorization": "194883321",
        "operation_type": "in",
        "method": "card",
        "transaction_type": "charge",
        "card": {
            "id": "kdx205scoizh93upqbte",
            "type": "credit",
            "brand": "diners",
            "address": null,
            "card_number": "367284XXXX3333",
            "holder_name": "DinnersClub",
            "expiration_year": "21",
            "expiration_month": "07",
            "allows_charges": true,
            "allows_payouts": false,
            "creation_date": "2019-08-09T13:35:48-05:00",
            "bank_name": "BANCO DE BOGOTÁ",
            "bank_code": "000"
        },
        "status": "completed",
        "conciliated": true,
        "creation_date": "2019-08-12T13:02:18-05:00",
        "operation_date": "2019-08-12T13:02:18-05:00",
        "description": "Ejemplo cargo",
        "error_message": null,
        "order_id": "oid-12331",
        "currency": "COP",
        "amount": 716,
        "customer": {
            "name": "Cliente Colombia",
            "last_name": "Vazquez Juarez",
            "email": "juan.vazquez@empresa.co",
            "phone_number": "4448936475",
            "address": null,
            "creation_date": "2019-08-12T13:02:18-05:00",
            "external_id": null,
            "clabe": null
        },
        "fee": {
          "amount": 21.8100,
          "tax": 3.4896,
          "currency": "COP"
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
[status](#object-transaction-status) | ***TransactionStatus*** <br/>Estado de la transacción (IN_PROGRESS,COMPLETED,REFUNDED,CHARGEBACK_PENDING,CHARGEBACK_ACCEPTED,CHARGEBACK_ADJUSTMENT,CHARGE_PENDING,CANCELLED,FAILED).

###Response

Returns an array of [transaction objects](#transaction-object) charges in descending order by creation date.
