#Charges
Charges can be made to cards, stores and banks. Each charge is assigned with an unique identifier in the system.

You can do card charges by using a saved card id, using a token or you can send the card information at the time of invocation.

##With a card id or token

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "source_id" : "kqgykn96i7bcs1wwhvgw",
   "method" : "card",
   "amount" : 100,
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-00051",
   "device_session_id":"kR1MiQhz2otdIuUlQkbEyitIqVMiI16f",
   "customer" : {
   	    "name" : "Juan",
   	    "last_name" : "Vazquez Juarez",
   	    "phone_number" : "4423456723",
   	    "email" : "juan.vazquez@empresa.com.mx"
   }
}' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');
$customer = array(
   	 'name' => 'Juan',
   	 'last_name' => 'Vazquez Juarez',
   	 'phone_number' => '4423456723',
   	 'email' => 'juan.vazquez@empresa.com.mx');

$chargeRequest = array(
    'method' => 'card',
    'source_id' => 'kqgykn96i7bcs1wwhvgw',
    'amount' => 100,
    'description' => 'Cargo inicial a mi merchant',
    'order_id' => 'oid-00051'
    'device_session_id' => 'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f',
    'customer' => $customer);

$charge = $openpay->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateCardChargeParams request = new CreateCardChargeParams();
Customer customer = new Customer();
customer.setName("Juan");
customer.setLastName("Vazquez Juarez");
customer.setPhoneNumber("4423456723");
customer.setEmail("juan.vazquez@empresa.com.mx");

request.cardId("kqgykn96i7bcs1wwhvgw"); // =source_id
request.amount(new BigDecimal("100.00"));
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
customer.PhoneNumber = "4423456723";
customer.Email = "juan.vazquez@empresa.com.mx";

ChargeRequest request = new ChargeRequest();
request.Method = "card";
request.SourceId = "kwkoqpg6fcvfse8k8mg2";
request.Amount = new Decimal(100.00);
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
   'amount' : 100,
   'description' : 'Cargo inicial a mi cuenta',
   'order_id' : 'oid-00051',
   'device_session_id' : 'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f',
   'customer' : {
   	    'name' : 'Juan',
   	    'last_name' : 'Vazquez Juarez',
   	    'phone_number' : '4423456723',
   	    'email' : 'juan.vazquez@empresa.com.mx'
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
    "phone_number" => "4423456723",
    "email" => "juan.vazquez@empresa.com.mx"
}
request_hash={
    "method" => "card",
    "source_id" => "kqgykn96i7bcs1wwhvgw",
    "amount" => 100.00,
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
   "id":"trzjaozcik8msyqshka4",
   "amount":100.00,
   "authorization":"801585",
   "method":"card",
   "operation_type":"in",
   "transaction_type":"charge",
   "card":{
      "id":"kqgykn96i7bcs1wwhvgw",
      "type":"debit",
      "brand":"visa",
      "address":null,
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "allows_charges":true,
      "allows_payouts":true,
      "creation_date":"2014-05-26T11:02:16-05:00",
      "bank_name":"Banamex",
      "bank_code":"002",
      "customer_id":"ag4nktpdzebjiye1tlze"
   },
   "status":"completed",
   "currency":"MXN",
   "creation_date":"2014-05-26T11:02:45-05:00",
   "operation_date":"2014-05-26T11:02:45-05:00",
   "description":"Cargo inicial a mi cuenta",
   "error_message":null,
   "order_id":"oid-00051"
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
cvv2 |***numeric***  (length = 3 or 4) <br/>Security code as it appears on the back of the card. Usually 3 digits.<br/>It's used only charges with [Stored Cards](#create-a-card).
amount | ***numeric*** (required) <br/>Amount to charge. Must be an amount greater than zero, with up to two decimal digits.
description | ***string*** (required, length = 250) <br/>A description associated to the charge.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of charge. Must be unique among all transactions.
device_session_id |  ***string*** (required, length = 255) <br/>Identifier of the device generated by the antifraud tool.
capture | ***boolean*** (optional, default = true) <br/>Indicates whether the charge is made immediately or not , when the value is false the charge is handled as authorized (or pre-authorization) and the amount is only to be confirmed or canceled in a second call.
[customer](#create-a-new-customer)| ***object*** (required) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the merchant level<br/><br/> To create a customer and keep a record of their charges history refer to [create a customer] (#create-a-new-customer) and do the charge at the customer level.
[payment_plan](#objetc-paymentplan)|***object*** (opcional) <br/>Plan data months without interest is desired as use in the charge. Refer to [PaymentPlan Object](#paymentplan-objetc).
metadata |  ***list(key, value)*** (optional) <br/>Field list to send antifraud system, It must be according to [Rules to send custom antifraud fields] (#custom-to-send-antifraud-fields).
use_card_points | ***string*** (optional, default = NONE) <br/> <table><tr><td><strong>ONLY_POINTS</strong></td> <td>Charge only with points (<a href="#consulta-de-puntos">Points card</a>)</td></tr><tr><td><strong>MIXED</strong></td><td>Charge with points and pesos</td></tr><tr><td><strong>NONE</strong></td>        <td>Charge only with pesos</td></tr></table>The values that indicate points must be used only if the points_card property is true, otherwise an error will occur.
send_email | ***boolean*** (optional) <br/>Used in redirect charges. Indicates if is need send a email that redirect to the openpay payment form.
redirect_url | ***string*** (optional) <br/>Used in redirect charges. It indicates the url to which redirect after a successful transaction in the openpay payment form.
use_3d_secure | ***boolean*** (optional) <br/> Used to specify if 3D Secure should be used.

###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

##With virtual terminal

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method" : "card",
   "amount" : 100,
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-00051",
   "customer" : {
        "name" : "Juan",
        "last_name" : "Vazquez Juarez",
        "phone_number" : "4423456723",
        "email" : "juan.vazquez@empresa.com.mx"
   },
   "confirm" : "false",
   "send_email":"false",
   "redirect_url":"http://www.openpay.mx/index.html"
}'
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');
$customer = array(
     'name' => 'Juan',
     'last_name' => 'Vazquez Juarez',
     'phone_number' => '4423456723',
     'email' => 'juan.vazquez@empresa.com.mx');

$chargeRequest = array(
    "method" : "card",
    'amount' => 100,
    'description' => 'Cargo terminal virtual a mi merchant',
    'customer' => $customer,
    'send_email' => false,
    'confirm' => false,
    'redirect_url' => 'http://www.openpay.mx/index.html')
;

$charge = $openpay->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateCardChargeParams request = new CreateCardChargeParams();
Customer customer = new Customer();
customer.setName("Juan");
customer.setLastName("Vazquez Juarez");
customer.setPhoneNumber("4423456723");
customer.setEmail("juan.vazquez@empresa.com.mx");

request.amount(new BigDecimal("100.00"));
request.description("Cargo inicial a mi merchant");
request.orderId("oid-00051");
request.setCustomer(customer);
request.setSendEmail(false);
request.setConfirm(false);
request.setRedirectUrl("http://www.openpay.mx/index.html");

Charge charge = api.charges().create(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ChargeRequest request = new ChargeRequest();
Customer customer = new Customer();
customer.Name = "Juan";
customer.LastName = "Vazquez Juarez";
customer.PhoneNumber = "4423456723";
customer.Email = "juan.vazquez@empresa.com.mx";

request.Method = "card";
request.Amount = new Decimal(100.00);
request.Description = "Cargo inicial a mi merchant";
request.OrderId = "oid-00051";
request.Confirm = false;
request.SendEmail = false;
request.RedirectUrl = "http://www.openpay.mx/index.html";
request.Customer = customer;

Charge charge = api.ChargeService.Create(request);
```

```javascript
var chargeRequest = {
   'method' : 'card',
   'amount' : 100,
   'description' : 'Cargo inicial a mi cuenta',
   'order_id' : 'oid-00051',
   'customer' : {
        'name' : 'Juan',
        'last_name' : 'Vazquez Juarez',
        'phone_number' : '4423456723',
        'email' : 'juan.vazquez@empresa.com.mx'
   },
  'send_email' : false,
  'confirm' : false,
  'redirect_url' : 'http://www.openpay.mx/index.html')
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
    "email" => "juan.vazquez@empresa.com.mx"
}

request_hash={
    "method" => "card",
    "amount" => 100.00,
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
    "customer" => customer_hash,
    "send_email" => false,
    "confirm" => false,
    "redirect_url" => "http://www.openpay.mx/index.html"
}

response_hash=@charges.create(request_hash.to_hash)
```

> Response example

```json

{
  "id": "trq7yrthx5vc4gtjdkwg",
  "authorization": null,
  "method": "card",
  "operation_type": "in",
  "transaction_type": "charge",
  "status": "charge_pending",
  "conciliated": false,
  "creation_date": "2016-09-09T18:52:02-05:00",
  "operation_date": "2016-09-09T18:52:02-05:00",
  "description": "Cargo desde terminal virtual de 111",
  "error_message": null,
  "amount": 100,
  "currency": "MXN",
  "payment_method": {
    "type": "redirect",
    "url": "https://sandbox-api.openpay.mx/v1/mexzhpxok3houd5lbvz1/charges/trq7yrthx5vc4gtjdkwg/card_capture"
  },
  "customer": {
    "name": "Juan",
    "last_name": "Vazquez Juarez",
    "email": "juan.vazquez@empresa.com.mx",
    "phone_number": "4423456723",
    "creation_date": "2016-09-09T18:52:02-05:00",
    "clabe": null,
    "external_id": null
  }
}
```

This type of charge don't requires a saved card or a previously generated token

###Request 

Property | Description
--------- | -----
method|***string*** (required in card) <br/>It must contain the card value in order to specify the charge will be made from card.
amount | ***numeric*** (required) <br/>Amount to charge. Must be an amount greater than zero, with up to two decimal digits.
description | ***string*** (required, length = 250) <br/>A description associated to the charge.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of charge. Must be unique among all transactions.
[customer](#create-a-new-customer)| ***object*** (required) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the merchant level<br/><br/> To create a customer and keep a record of their charges history refer to [create a customer] (#create-a-new-customer) and do the charge at the customer level.
confirm |  ***boolean*** (required in false) <br/>Indicates whether the charge is made immediately or not , when the value is false the charge is handled as authorized (or pre-authorization) and the amount is only to be confirmed or canceled in a second call.
send_email | ***boolean*** (optional) <br/>Indicates if is need send a email that redirect to the openpay payment form.
redirect_url | ***string*** (required) <br/>It indicates the url to which redirect after a successful transaction in the openpay payment form.

###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

##Charge via store

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Merchant
$openpay->charges->create(chargeRequest);

Customer
$customer = $openpay->customers->get(customerId);
$customer->charges->create(chargeRequest;
?>
```

```java
//Customer
openpayAPI.charges().create(String customerId, CreateStoreChargeParams request);

//Merchant
openpayAPI.charges().create(CreateStoreChargeParams request);
```

```csharp
//Customer
openpayAPI.ChargeService.Create(string customer_id, ChargeRequest request);

//Merchant
openpayAPI.ChargeService.Create(ChargeRequest request);
```

```javascript
//Merchant
openpay.charges.create(chargeRequest, callback);

//Customer
openpay.customers.charges.create(customerId, chargeRequest, callback);
```

```ruby
#Customer
@charges=@openpay.create(:charges)
@charges.create(request_hash, customer_id)

#Merchant
@charges=@openpay.create(:charges)
@charges.create(request_hash)
```

> Customer request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method" : "store",
   "amount" : 100,
   "description" : "Cargo con tienda",
   "order_id" : "oid-00053",
   "due_date" : "2014-05-28T13:45:00"
}' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$chargeRequest = array(
    'method' => 'store',
    'amount' => 100,
    'description' => 'Cargo con tienda',
    'order_id' => 'oid-00053',
    'due_date' => '2014-05-28T13:45:00');

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Calendar dueDate = Calendar.getInstance();
dueDate.set(2014, 5, 28, 13, 45, 0);
CreateStoreChargeParams request = new CreateStoreChargeParams();
request.amount(new BigDecimal("100.00"));
request.description("Cargo con tienda");
request.orderId("oid-00053"
request.dueDate(dueDate.getTime());

Charge charge = api.charges().create("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ChargeRequest request = new ChargeRequest();
request.Method = "store";
request.Amount = new Decimal(100.00);
request.Description = "Cargo con tienda";
request.OrderId = "oid-00053";
request.DueDate = new DateTime(2014, 5, 28, 13, 45, 0);

Charge charge = api.ChargeService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var storeChargeRequest = {
   'method' : 'store',
   'amount' : 100,
   'description' : 'Cargo con tienda',
   'order_id' : 'oid-00053',
   'due_date' : '2014-05-28T13:45:00'
};

openpay.customers.charges.create('ag4nktpdzebjiye1tlze', storeChargeRequest, function(error, charge) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)
request_hash={
     "method" => "store",
     "amount" => 100.00,
     "description" => "Cargo con tienda",
     "order_id" => "oid-00053",
     "due_date" => "2014-05-28T13:45:00"
   }

response_hash=@charges.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Response example

```json
{
   "id":"trnirkiyobo5qfex55ef",
   "amount":100.00,
   "authorization":null,
   "method":"store",
   "operation_type":"in",
   "transaction_type":"charge",
   "status":"in_progress",
   "currency":"MXN",
   "creation_date":"2014-05-26T13:48:25-05:00",
   "operation_date":"2014-05-26T13:48:25-05:00",
   "due_date":"2014-05-28T13:45:00-05:00",
   "description":"Cargo con tienda",
   "error_message":null,
   "order_id":"oid-00053",
   "customer_id":"ag4nktpdzebjiye1tlze",
   "payment_method":{
      "type":"store",
      "reference":"000020TRNIRKIYOBO5QFEX55EF0100009",
      "paybin_reference":"0101990000001065",
      "barcode_url":"https://sandbox-api.openpay.mx/barcode/000020TRNIRKIYOBO5QFEX55EF0100009?width=1&height=45&text=false",
      "barcode_paybin_url":"https://sandbox-api.openpay.mx/barcode/0101990000001065?width=1&height=45&text=false"
   }
}
```

For payments at a convenience store you should create a charge type request by indicating **store** as method. This will generate a response with a reference number and a URL with a barcode, which you must use to create a receipt so your customer can make the payment in one of the convenience stores. The barcode is Code 128 type.

###Request 

Property | Description
--------- | -----
method|***string*** (required) <br/>It must constains the **store** value in order to specify you want to pay at store.
amount | ***numeric*** (required) <br/>Amount of charge. Must be an amount greater than zero, with up to two decimal digits.
description | ***string*** (required, length = 250) <br/>A description associated to the charge.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of charge. Must be unique among all transactions.
due_date | ***datetime*** (optional) <br/>Due date for making the payment in the store in  ISO 8601 format. <br/><br/>Example (UTC): 2014-08-01T00:50:00Z <br/>***Note:*** On the server side the date will be changeg to central time<br/><br/>Example (Central Time): 2014-08-01T11:51:23-05:00
[customer](#create-a-new-customer)|***object*** (required) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the Merchant level establishing a level trade <br/><br/> To create a customer and keep a record of their charges history refer to [create a customer] (#create-a-new-customer) and do the charge at the customer level.

###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

##Charge via bank

> Definition

```plaintext--endpoints
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Merchant
$openpay->charges->create(chargeRequest);

Customer
$customer = $openpay->customers->get(customerId);
$customer->charges->create(chargeRequest);
?>
```

```java
//Customer
openpayAPI.charges().create(String customerId, CreateBankChargeParams request);

//Merchant
openpayAPI.charges().create(CreateBankChargeParams request);
```

```csharp
//Customer
openpayAPI.ChargeService.Create(string customer_id, ChargeRequest request);

//Merchant
openpayAPI.ChargeService.Create(ChargeRequest request);
```

```javascript
// Merchant
openpay.charges.create(chargeRequest, callback);

// Customer
openpay.customers.charges.create(customerId, chargeRequest, callback);
```

```ruby
#Customer
@charges=@openpay.create(:charges)
@charges.create(request_hash, customer_id)

#Merchant
@charges=@openpay.create(:charges)
@charges.create(request_hash)
```

> customer request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method" : "bank_account",
   "amount" : 100,
   "description" : "Cargo con banco",
   "order_id" : "oid-00055"
} ' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$chargeRequest = array(
    'method' => 'bank_account',
    'amount' => 100,
    'description' => 'Cargo con banco',
    'order_id' => 'oid-00055');

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateBankChargeParams request = new CreateBankChargeParams();
request.amount(new BigDecimal("100.00"));
request.description("Cargo con banco");
request.orderId("oid-00053");

Charge charge = api.charges().create("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ChargeRequest request = new ChargeRequest();
request.Method = "bank_account";
request.Amount = new Decimal(100.00);
request.Description = "Cargo con banco";
request.OrderId = "oid-00053";

Charge charge = api.ChargeService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var bankChargeRequest = {
   'method' : 'bank_account',
   'amount' : 100,
   'description' : 'Cargo con banco',
   'order_id' : 'oid-00055'
};

openpay.customers.charges.create('ag4nktpdzebjiye1tlze', bankChargeRequest, function(error, charge) {
  // ...
});

```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)
request_hash={
     "method" => "bank_account",
     "amount" => 100.00,
     "description" => "Cargo con banco",
     "order_id" => "oid-00053"
   }

response_hash=@charges.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Response example

```json
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
      "bank":"BBVA Bancomer",
      "clabe":"012914002014112176",
      "name":"11030021342311520255"
   }
}
```
For a charge via bank you must create a charge type request  by indicating ** bank_account** as method. This will 
generate a response with a Bancomer CIE agreement number, a CLABE account number and a reference, you have to indicate 
these data in a receipt so your customer can do the wire transfer via SPEI.

###Request 

Property | Description
--------- | -----
method|***string*** (required) <br/>It must contain the **bank_account** value to specify the pay will be made with bank transfer.
amount | ***numeric*** (required) <br/>Amount of charge. Must be an amount greater than zero, with up to two decimal digits.
description | ***string*** (required, length = 250) <br/>A description associated to the charge.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of charge. Must be unique among all transactions.
due_date | ***datetime*** (optional) <br/>>Due date for making the bank charge in the ISO 8601 format. <br/><br/>Example (UTC): 2014-08-01T00:50:00Z <br/>***Note:*** On the server side the date will be changed to central time<br/><br/>Example (Central Time): 2014-08-01T11:51:23-05:00
[customer](#create-a-new-customer)|***object*** (optional) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the Merchant level establishing a level trade <br/><br/> To create a customer and keep a record of their charges history refer to [create a customer] (#create-a-new-customer) and do the charge at the customer level.

###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

##Confirming a charge

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/capture

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}/capture
```

```php
<?
Merchant
$charge = $openpay->charges->get(transactionId);
$charge->capture(captureData);

Customer
$customer = $openpay->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
$charge->capture(captureData);
?>
```

```java
//Customer
openpayAPI.charges().confirmCapture(String customerId, ConfirmCaptureParams request);

//Merchant
openpayAPI.charges().confirmCapture(ConfirmCaptureParams request);
```

```csharp
//Customer
openpayAPI.ChargeService.Capture(string customer_id, string transaction_id, Decimal? amount);

//Merchant
openpayAPI.ChargeService.Capture(string transaction_id, Decimal? amount);
```

```javascript
// Merchant
openpay.charges.capture(transactionId, captureRequest, callback);

// Customer
openpay.customers.charges.capture(customerId, transactionId, captureRequest, callback);
```

```ruby
#Customer
@charges=@openpay.create(:charges)
@charges.capture(transaction_id, customer_id)

#Merchant
@charges=@openpay.create(:charges)
@charges.capture(transaction_id)
```

> Customer request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges/tryqihxac3msedn4yxed/capture \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
    "amount" : 100.00
} ' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$captureData = array('amount' => 100.00);

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->get('tryqihxac3msedn4yxed');
$charge->capture($captureData);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ConfirmCaptureParams request = new ConfirmCaptureParams();
request.chargeId("tryqihxac3msedn4yxed");
request.amount(new BigDecimal("100.00"));

Charge charge = api.charges().confirmCapture("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.ChargeService.Capture("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", new Decimal(100.00));
```

```javascript
var captureRequest = {
  'amount' : 100.00
};

openpay.customers.charges.capture('ag4nktpdzebjiye1tlze', 'tryqihxac3msedn4yxed', captureRequest, 
    function(error, charge){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)

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
   "description":"Cargo inicial a mi cuenta",
   "error_message":null,
   "order_id":null,
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```
Confirm a charge created with the <code>capture = "false" </code> property, this method is the second part of the [create a charge with a card (id or token)] (#with-a-card-id-or-token) and it can confirm the amount captured on the first call or a lesser amount.

<aside class="notice">
**Note:** You only can confirm charges via card. To cancel the charge created you should make a call to the method [charge refund] (#charge-refund)
</aside>


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
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/refund

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}/refund
```

```php
<?
Merchant
$charge = $openpay->charges->get(transactionId);
$charge->refund(refundData);

Customer
$customer = $openpay->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
$charge->refund(refundData);
?>
```

```java
//Customer
openpayAPI.charges().refund(String customerId, RefundParams request);

//Merchant
openpayAPI.charges().refund(RefundParams request);
```

```csharp
//Customer
openpayAPI.ChargeService.Refund(string customer_id, string transaction_id, string description);

//Merchant
openpayAPI.ChargeService.Refund(string transaction_id, string description);
```

```javascript
// Merchant
openpay.charges.refund(transactionId, refundRequest, callback);

// Customer
openpay.customers.charges.refund(customerId, transactionId, refundRequest, callback);
```

```ruby
#Customer
@charges=@openpay.create(:charges)
@charges.refund(transaction_id, request_hash, customer_id)

#Merchant
@charges=@openpay.create(:charges)
@charges.refund(transaction_id, request_hash)
```

> Customer request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges/tr6cxbcefzatd10guvvw/refund \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "description" : "devolución",
   "amount" : 100.00
} ' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$refundData = array(
    'description' => 'devolución',
    'amount' => 100);

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->get('tr6cxbcefzatd10guvvw');
$charge->refund($refundData);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
RefundParams request = new RefundParams();
request.chargeId("tryqihxac3msedn4yxed");
request.description("Monto de cargo devuelto");
request.amount(new BigDecimal("100.00"));

Charge charge = api.charges().refund("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.ChargeService.Refund("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", "Monto de cargo devuelto", , new Decimal(100.00));
```

```javascript
var refundRequest = {
   'description' : 'devolución',
   'amount' : 100.00
};

openpay.customers.charges.refund('ag4nktpdzebjiye1tlze', 'tryqihxac3msedn4yxed', refundRequest, 
    function(error, charge) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)

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
   "description":"Cargo inicial a mi cuenta",
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
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}

Merchant
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}
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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges/tr6cxbcefzatd10guvvw \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->get('tr6cxbcefzatd10guvvw');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.charges().get("ag4nktpdzebjiye1tlze", "tr6cxbcefzatd10guvvw");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.ChargeService.Get("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed");
```

```javascript
openpay.customers.charges.get('ag4nktpdzebjiye1tlze', 'tr6cxbcefzatd10guvvw', function(error, charge){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)

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
   "description":"Cargo inicial a mi cuenta",
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
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Merchant
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
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
curl -g "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges?creation[gte]=2013-11-01&limit=2" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$searchParams = array(
    'creation[gte]' => '2013-11-01',
    'creation[lte]' => '2014-11-01',
    'offset' => 0,
    'limit' => 2);

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$chargeList = $customer->charges->getList($searchParams);
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
request.amount(new BigDecimal("100.00"));

List<Charge> charges = api.charges().list("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;
request.Amount = new Decimal(100.00);

List<Charge> charges= openpayAPI.ChargeService.List("ag4nktpdzebjiye1tlze", request);
```

```javascript
var searchParams = {
  'creation[gte]' : '2013-11-01',
  'limit' : 2
};

openpay.customers.charges.list('ag4nktpdzebjiye1tlze',searchParams, function(error, chargeList) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)

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
      "description":"Cargo inicial a mi cuenta",
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
         "bank":"BBVA Bancomer",
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
[status](#object-transaction-status) | ***TransactionStatus*** <br/>Estado de la transacción (IN_PROGRESS,COMPLETED,REFUNDED,CHARGEBACK_PENDING,CHARGEBACK_ACCEPTED,CHARGEBACK_ADJUSTMENT,CHARGE_PENDING,CANCELLED,FAILED).

###Response

Returns an array of [transaction objects](#transaction-object) charges in descending order by creation date.

## With Alipay

> Definition

```plaintext--endpoints
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

> Customer request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "description": "Cargo Alipay",
   "amount": "2000.00",
   "method": "alipay",
   "order_id": "oid-00053",
   "redirect_url" : "http://www.example.com/myRedirectUrl"
} '
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$chargeRequest = array(
    'method' => 'alipay',
    'amount' => 100,
    'description' => 'Cargo Alipay',
    'order_id' => 'oid-00055',
    'redirect_url' => 'http://www.example.com/myRedirectUrl');

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "mzdtln0bmtms6o3kck8f");
CreateAlipayChargeParams request = new CreateAlipayChargeParams();
request.amount(new BigDecimal("100.00"));
request.description("Cargo Alipay");
request.orderId("oid-00053");
request.redirectUrl("http://www.example.com/myRedirectUrl")

Charge charge = api.charges().createCharge("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ChargeRequest request = new ChargeRequest();
request.Method = "alipay";
request.Amount = new Decimal(100.00);
request.Description = "Cargo Alipay";
request.OrderId = "oid-00053";
request.RedirectUrl ="http://www.example.com/myRedirectUrl";

Charge charge = api.ChargeService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var alipayChargeRequest = {
   'method' : 'alipay',
   'amount' : 100,
   'description' : 'Cargo Alipay',
   'order_id' : 'oid-00055',
   'redirect_url' : 'http://www.example.com/myRedirectUrl'
};

openpay.customers.charges.create('ag4nktpdzebjiye1tlze', alipayChargeRequest, function(error, charge) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)
request_hash={
     "method" => "alipay",
     "amount" => 100.00,
     "description" => "Cargo Alipay",
     "order_id" => "oid-00053",
     "redirect_url" => "http://www.example.com/myRedirectUrl"
   }

response_hash=@charges.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Response example

```json
{
    "id": "truq1dwjz0kmssvpbrlj",
    "authorization": null,
    "operation_type": "in",
    "method": "alipay",
    "transaction_type": "charge",
    "status": "charge_pending",
    "conciliated": false,
    "creation_date": "2018-06-14T12:42:11-05:00",
    "operation_date": "2018-06-14T12:42:11-05:00",
    "description": "Cargo Alipay",
    "error_message": null,
    "order_id": null,
    "due_date": "2018-06-15T12:42:11-05:00",
    "payment_method": {
        "type": "redirect",
        "url": "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges/truq1dwjo0kmssvqbrlj/redirect/"
    },
    "amount": 2000,
    "currency": "MXN",
    "fee": {
        "amount": 2.00  ,
        "tax": 0,
        "currency": "MXN"
    }
}
```

To start a transaction using Alipay you should create a charge type request by indicating **alipay** as method. 
This will generate a response with an URL which will redirect the customer to the Alipay website
where they can then enter their account details, or scan the QR Code in their mobile app.


### Request 

Property    | Description
----------- | -----
method      | ***string*** (required) <br/>It must constains the **alipat** value in order to specify you want the customer to pay using Alipay.
amount      | ***numeric*** (required) <br/>Amount of charge. Must be an amount greater than zero, with up to two decimal digits.
description | ***string*** (required, length = 250) <br/>A description associated to the charge.
order_id    | ***string*** (optional, length = 100) <br/>Unique identifier of charge. Must be unique among all transactions.
due_date    | ***datetime*** (optional) <br/>Due date for making the payment in Alipay in  ISO 8601 format. The customer may have an additional 15 minutes after this date after they login to their Alipay account to complete payment. <br/><br/>Example (UTC): 2014-08-01T00:50:00Z <br/>***Note:*** On the server side the date will be changeg to central time<br/><br/>Example (Central Time): 2014-08-01T11:51:23-05:00
[customer](#create-a-new-customer)|***object*** (required) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the Merchant level establishing a level trade <br/><br/> To create a customer and keep a record of their charges history refer to [create a customer] (#create-a-new-customer) and do the charge at the customer level.
redirect_url | ***string*** (required) <br/>It indicates the url to which redirect after a successful transaction in the openpay payment form, when a request is receiven in this url, merchant must get id attribute to request for the transaction final result.

### Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).