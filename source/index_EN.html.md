---
title: API Reference

language_tabs:
  - shell: cURL
  - php: PHP
  - java: JAVA
  - csharp: C#
  - javascript : Node.js
  - ruby: Ruby

toc_footers:
 - <a href='#'>Sign Up for a Developer Key</a>
 - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

lang: EN
---

# Introduction

The Openpay API is designed on [REST](http://es.wikipedia.org/wiki/Representational_State_Transfer),  therefore you'll find that URLs are oriented to resources and that HTTP response codes are used to indicate errors in the API.

All the API responses are in [JSON](http://www.json.org/) format, including the errors.

In the case to use the existents Openpay API clients ([Java](https://github.com/open-pay/openpay-java), [Php](https://github.com/open-pay/openpay-php), [C#](https://github.com/open-pay/openpay-dotnet), [Python](https://github.com/open-pay/openpay-python), [Ruby](https://github.com/open-pay/openpay-ruby), [NodeJS](https://github.com/open-pay/openpay-node)), the responses are specifically of type defined in the clients and their respective languajes.

# API Endpoints

> Available resourcers

<br/>
<br/>

> a) By Merchant

```
/v1/{MERCHANT_ID}/...

/fees
/fees/{FEE_ID}
/charges
/charges/{TRANSACTION_ID}
/payouts
/payouts/{TRANSACTION_ID}
/cards
/cards/{CARD_ID}
/customers
/customers/{CUSTOMER_ID}
/plans
/plans/{PLAN_ID}
​/tokens
/tokens/{TOKEN_ID}
```

> b) By Customer

```
/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/...

/cards
/cards/{CARD_ID}
/bankaccounts
/bankaccounts/{BANKACCOUNT_ID}
/charges
/charges/{TRANSACTION_ID}
/payouts
/payouts/{TRANSACTION_ID}
/transfers
/transfers/{TRANSACTION_ID}
/subscriptions
/subscriptions/{SUBSCRIPTION_ID}
```

The Openpay REST API has a test environment (sandbox) and a production environment. For integrating your system with Openpay, use the credentials that were generated when you signed up. Once you are ready to move to production environment and your request is approved, new credentials will be generated for accessing the production environment.

The following URIs are the basis of the endpoints for the supported environments:

* **Test**, URI base: <br/> `https://sandbox-api.openpay.mx`<br/><br/>
* **Production**, URI base: <br/>`https://api.openpay.mx`<br/>

A complete endpoint consists of the base URI of the environment, the identifier of the Merchant and the resource.

For example, if we want to create a new customer, the endpoint would be::

<code>POST https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers</code>

In order to create a complete request is necessary to send the right HTTP headers and the information in JSON format.

<aside class="notice">
 All the examples of this documentation are based on the testing environment.
</aside>

# Authentication

> Authentication example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:

The -u parameter is responsible for the HTTP basic authentication (adding two points after the private key prevents the use of password)
```

```php
<? 
//Sandbox is used by default 
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c4875b178ce26348b0fac'); 
?>
```

```java
//Sandbox
final OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "moiep6umtcnanql3jrxp", "sk_3433941e467c4875b178ce26348b0fac");

//Production
final OpenpayAPI api = new OpenpayAPI("https://api.openpay.mx", "moiep6umtcnanql3jrxp", "sk_3433941e467c4875b178ce26348b0fac");
```

```javascript
var Openpay = require('openpay');
var openpay = new Openpay('moiep6umtcnanql3jrxp','sk_3433941e467c4875b178ce26348b0fac');
```

```csharp
//Sandbox
OpenpayAPI openpayAPI = new OpenpayAPI("sk_3433941e467c4875b178ce26348b0fac", "moiep6umtcnanql3jrxp");
openpayAPI.Production = false; // Default value = false

//Produtcion
OpenpayAPI openpayAPI = new OpenpayAPI("sk_3433941e467c4875b178ce26348b0fac", "moiep6umtcnanql3jrxp");
openpayAPI.Production = true;
```

```ruby
#Sandbox
openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")

#Production
openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac", true)


#Define the timeout for the requests
#This cllient uses a default 90 secs timeout. In order to configure the timeout used to create request to the openpay services, you need to clearly define the kind of environment, followed by the new timeout value for the request:

#Syntax:
#   openpay_prod=OpenpayApi.new(merchant_id,private_key,isProduction,timeout)
#Example:
#   openpay_prod=OpenpayApi.new(merchant_id,private_key,false,30)
```

> Production 

```shell
You only need to use the URI base https://api.openpay.mx
```

```php
<? 
Openpay::setProductionMode(true); 
?>
```

```java
//You only need to use the URI base https://api.openpay.mx
```

```csharp
openpayAPI.Production = true;
```

```javascript
openpay.setProductionReady(true);
```

```ruby
#You only need to pass a "true" value as the third argument when creating the OpenpayApi object. 
```

To make requests to the Openpay API, is necessary to send the API Key on all your calls to our servers. You can get the key from the [dashboard](https://sandbox-dashboard.openpay.mx).

There are 2 types of API keys:

* **Private.-** 
For calls between servers and full access to all API operations (should never be shared).

<aside class="warning">
Keep this key safe and never share it to anyone.
</aside>

* **Public.-**
should only be used in JavaScript calls. This key is only allowed to create cards or create tokens.

<aside class="notice">
To make calls with your public key use the [Openpay.js] library(#)
</aside>

For API authentication you must use the [basic access authentication]http://es.wikipedia.org/wiki/Autenticación_de_acceso_básica), where the API key is the username. The password is not required and it should be left blank for purposes of simplicity

<aside class="notice">
For security reasons, all requests must be through **HTTPS**.
</aside>

#Errors

Openpay returns JSON objects in the service responses. 

##Error Object

> Object example 

```json
{
    "category" : "request",
    "description" : "The customer with id 'm4hqp35pswl02mmc567' does not exist",
    "http_code" : 404,
    "error_code" : 1005,
    "request_id" : "1981cdb8-19cb-4bad-8256-e95d58bc035c",
    "fraud_rules": [
        "Billing <> BIN Country for VISA/MC"
    ]
}
```

```java
//For Java every operation will return an instance of the "OpenpayServiceException" class which will have the error information. ```

```csharp
//For C Sharp,  every operation will return an instance of the "OpenpayException" class which will have the error information.
```

```ruby
#For Ruby, every operation can return any of the following exceptions:

# => OpenpayException: For generic errors, like invalid resources, etc.
# => OpenpayConnectionException: For errors related with server connection problems.
# => OpenpayTransactionException: For errors during operations implementation.
```

Property | Description
--------- | -----
category    |***string*** <br/>**request:**  Indicates an error caused by data sent by the customer. For example, an invalid request, an attempt at a transaction without funds or a transfer to an account that does not exist. <br/><br/>**internal:** Indicates an error on Openpay side, and will occur very rarely. <br/><br/>**gateway:** Indicates an error during the transaction of funds from one card to the Openpay account or from the account to a bank or card.
error_code  |***numeric*** <br/>Openpay numeric error code indicating a problem happened.
description |***string*** <br/>Error description.
http_code   |***string*** <br/>HTTP error code  of the response.
request_id  |***string*** <br/> Request identifier.
fraud_rules |***array*** <br/> Array with antifraud rules broken according to fraud detection rules.

##Error codes

###General
Code    | HTTP Error |Cause
--------- | ----------- | --------
1000 | 500 Internal Server Error | An internal error occurred on the Openpay server 
1001 | 400 Bad Request | The format of the request is not JSON, the fields do not have the correct format, or the request does not have fields that are required.
1002 | 401 Unauthorized | The call is not authenticated or the authentication is incorrect.
1003 | 422 Unprocessable Entity | The operation could not be completed because the value of one or more of the parameters is incorrect.
1004 | 503 Service Unavailable | A necessary for processing the transaction service is unavailable.
1005 | 404 Not Found | One of the resources requested does not exist.
1006 | 409 Conflict | A transaction with the same order ID already exists.
1007 | 402 Payment Required | The transfer of funds from a bank account or card to the Openpay account was not accepted.
1008 | 423 Locked | One of the accounts required in the request is deactivated.
1009 | 413 Request Entity too large | The request body is too large.
1010 | 403 Forbidden | The public key is used to make a call but it requires the private key, or it ‘s using the private key from JavaScript.

###Storage

Code    | HTTP Error |Cause
--------- | ----------- | --------
2001 | 409 Conflict | The bank account with this CLABE is already registered on the customer.
2002 | 409 Conflict | The card with this number is already registered on the customer.
2003 | 409 Conflict | Customer with this external identifier (External ID) already exists.
2004 | 422 Unprocessable Entity | The check digit card number is invalid according to the Luhn algorithm.
2005 | 400 Bad Request | The expiration date of the card is prior to the current date.
2006 | 400 Bad Request | Security code card (CVV2) was not provided.
2007 | 412 Precondition Failed | The card number is a test number and can only be used in Sandbox.
2008 | 412 Precondition Failed | The consulted card is not valid for points.

###Cards
Code    | HTTP Error |Cause
--------- | ----------- | --------
3001 | 402 percent Required | The card was declined.
3002 | 402 Payment Required | The card has expired.
3003 | 402 Payment Required | The card has insufficient funds.
3004 | 402 Payment Required | The card has been identified as a stolen card.
3005 | 402 Payment Required | The card has been identified as a fraudulent card.
3006 | 412 Precondition Failed | The operation is not allowed for this customer or this transaction.
3008 | 412 Precondition Failed | The card is not supported in online transactions.
3009 | 402 Payment Required | The card was reported missing.
3010 | 402 Payment Required | The bank has restricted the card.
3011 | 402 Payment Required | The bank has requested that the card is retained. Contact the bank.
3012 | 412 Precondition Failed | A bank authorization is required to make this payment.

###Accounts
Code    | HTTP Error |Cause
--------- | ----------- | --------
4001  |412 Preconditon Failed | The Openpay account has not enough funds.


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
      "walmart_reference":"0101990000001065",
      "barcode_url":"https://sandbox-api.openpay.mx/barcode/000020TRNIRKIYOBO5QFEX55EF0100009?width=1&height=45&text=false"
      "barcode_walmart_url":"https://sandbox-api.openpay.mx/barcode/0101990000001065?width=1&height=45&text=false"
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
[customer](#create-a-new-customer)|***object*** (required) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the Merchant level establishing a level trade <br/><br/> To create a customer and keep a record of their charges history refer to [create a customer] (#create-a-new-customer) and do the charge at the customer leve.

###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

##Charge via bank

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
      "bank":"STP",
      "clabe":"646180109400135624",
      "name":"0021589"
   }
}
```
For a charge via bank you must create a charge type request  by indicating ** bank_account** as method. This will generate a response with a CLABE account number and a description, you have to indicate these data in a receipt so your customer can do the wire transfer via SPEI.

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
   "description" : "devolución"
} ' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$refundData = array('description' => 'devolución' );

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

Charge charge = api.charges().refund("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.ChargeService.Refund("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", "Monto de cargo devuelto");
```

```javascript
var refundRequest = {
   'description' : 'devolución'
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
     "description" => "Monto de cargo devuelto"
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
You can use this method f you want to make a charge refund to a card. The amount to be returned will be the total charge. Note that the refund may be delayed in the statement of your customer for 1-3 business days.

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
         "bank":"STP",
         "clabe":"646180109400135624",
         "name":"0021589"
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

###Response

Returns an array of [transaction objects](#transaction-object) charges in descending order by creation date.

#Payouts or withdrawals
A payout is the transaction that allows to extract funds from a Openpay account and send the funds to a bank account or a debit card. Payouts can be made from the accounts of the customers or from the Merchant account.

<aside class="notice">
**Note:**  All payout transactions will be returned in **IN_PROGRESS** status meaning that it is scheduled for the next day when the operation takes place the status will change to **completed** and if there are configured WebHooks, a notification will be sent.
</aside>

##Payout to a registered id

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts
```

```php
<?
Customer
$customer = $openpay->customers->get(customerId);
$payout = $customer->payouts->create(payoutRequest);

Merchant
$payout = $openpay->payouts->create(payoutRequest);
?>
```

```java
//Customer
openpayAPI.payouts().create(String customerId, CreateBankPayoutParams request);

//Merchant
openpayAPI.payouts().create(CreateBankPayoutParams request);
```

```csharp
//Customer
openpayAPI.PayoutService.Create(string customer_id, PayoutRequest request);

//Merchant
openpayAPI.PayoutService.Create(PayoutRequest request);
```

```javascript
// Merchant
openpay.payouts.create(payoutRequest, callback);

// Customer
openpay.customers.payouts.create(customerId, payoutRequest, callback);
```

```ruby
#Customer
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash, customer_id)

#Merchant
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash)
```

> Customer request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/payouts \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
    "method": "card",
    "destination_id": "k3d54sd3mdjf75udjfvoc",
    "amount": 10.50,
    "description": "Retiro de saldo semanal",
    "order_id": "oid-00021"
}' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$payoutRequest = array(
    'method' => 'card',
    'destination_id' => 'k3d54sd3mdjf75udjfvoc',
    'amount' => 1000,
    'description' => 'Retiro de saldo semanal',
    'order_id' => 'ORDEN-00021');

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$payout = $customer->payouts->create($payoutRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_e568c42a6c384b7ab02cd47d2e407cab", "mzdtln0bmtms6o3kck8f");
CreateBankPayoutParams request = new CreateBankPayoutParams();
request.bankAccountId("k3d54sd3mdjf75udjfvoc"); // = destination_id
request.amount(new BigDecimal("10.50"));
request.description("Retiro de saldo semanal");
request.orderId("oid-00021");

Payout payout = api.payouts().create("ag4nktpdzebjiye1tlze", request);
// Para crear pagos a tarjetas se deberá usar la clase CreateCardPayoutParams
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_e568c42a6c384b7ab02cd47d2e407cab", "mzdtln0bmtms6o3kck8f");
PayoutRequest request = new PayoutRequest();
request.Method = "bank_account";
request.DestinationId = "k3d54sd3mdjf75udjfvoc";
request.Amount = new Decimal(10.50;
request.Description = "Retiro de saldo semanal";
request.OrderId = "oid-00021;

Payout = api.PayoutService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var payoutRequest = {
    'method': 'card',
    'destination_id': 'k3d54sd3mdjf75udjfvoc',
    'amount': 10.50,
    'description': 'Retiro de saldo semanal',
    'order_id': 'oid-00021'
};

openpay.customers.payouts.create('ag4nktpdzebjiye1tlze', payoutRequest, function(error, payout) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@payouts=@openpay.create(:payouts)
request_hash={
     "method" => "bank_account",
     "destination_id" => "k3d54sd3mdjf75udjfvoc",   
     "amount" => 10.50,
     "description" => "Retiro de saldo semanal",
     "order_id" => "oid-00021"
   }

response_hash=@payouts.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Response example

```json
{
   "amount":10.5,
   "authorization":null,
   "method":"card",
   "currency":"MXN",
   "operation_type":"out",
   "transaction_type":"payout",
   "card":{
      "id":"k3d54sd3mdjf75udjfvoc",
      "type":"debit",
      "brand":"visa",
      "address":null,
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":null,
      "expiration_month":null,
      "allows_payouts":false,
      "allows_charges":true,
      "creation_date":"2013-11-15T13:42:00-06:00",
      "bank_name":"BANCOMER",
      "bank_code":"012"
   },
   "status":"in_progress",
   "id":"tm50pl40gf6awvalw1ei",
   "creation_date":"2013-11-15T13:42:00-06:00",
   "description":"Retiro de saldo semanal",
   "error_message":null,
   "order_id":"oid-00021",
   "customer_id":"aayr5jjb1fln44yautef"
}
```

Sends a payout to a bank account or debit card previously registered. Refer to [create a bank account] (#create-a-bank-account)

###Request 

Property | Description
--------- | -----
method|***string*** (required) <br/>It must contain the **card** value in order to a make payout to a registered card, and the **bank_account** for the payout to a registered bank account.
destination_id | ***string*** (required, length = 45) <br/>ID of the bank account and registered the debit card.
amount | ***numeric*** (required) <br/>Amount of payout. Must be an amount greater than zero, with up to two decimal digits.
description | ***string*** (required, length = 250) <br/>A description associated to the payment.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of payout. Must be unique among all transactions.


###Response
Returns a [transaction object](#transaction-object) with the payout information or with an [error response](#error-object).

##Pament to a bank account

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts
```

```php
<?
Customer
$customer = $openpay->customers->get(customerId);
$payout = $customer->payouts->create(payoutRequest);

Merchant
$payout = $openpay->payouts->create(payoutRequest);
?>
```

```java
//Customere
openpayAPI.payouts().create(String customerId, CreateBankPayoutParams request);

//Comercio
openpayAPI.payouts().create(CreateBankPayoutParams request);
```

```csharp
//Customer
openpayAPI.PayoutService.Create(string customer_id, PayoutRequest request);

//Merchant
openpayAPI.PayoutService.Create(PayoutRequest request);
```

```javascript
// Merchant
openpay.payouts.create(payoutRequest, callback);

// Customer
openpay.customers.payouts.create(customerId, payoutRequest, callback);
```

```ruby
#Customer
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash, customer_id)

#Merchant
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash)
```

> Customer request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/asynwirguzkgq2bizogo/payouts \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method":"bank_account",
   "bank_account":{
      "clabe":"012298026516924616",
      "holder_name":"Mi empresa"
   },
   "amount":100.00,
   "description":"Retiro de saldo semanal",
   "order_id":"oid-1110011"
}' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$payoutRequest = array(
    'method' => 'bank_account',
    'bank_account' => array(
        'clabe' => '012298026516924616',
        'holder_name' => 'Mi empresa'),
    'amount' => 100.00,
    'description' => 'Retiro de saldo semanal',
    'order_id' => 'ORDEN-00021');

$customer = $openpay->customers->get('asynwirguzkgq2bizogo');
$payout = $customer->payouts->create($payoutRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateBankPayoutParams request = new CreateBankPayoutParams();
BankAccount bankAccount = new BankAccount();
bankAccount.holderName("Mi empresa");
bankAccount.alias(null);
bankAccount.clabe("012XXXXXXXXXX24616");
request.bankAccount(bankAccount);
request.amount(new BigDecimal("10.50"));
request.description("Retiro de saldo semanal");
request.orderId("oid-1110011");

Payout payout = api.payouts().create("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
PayoutRequest request = new PayoutRequest();
request.Method = "bank_account";
BankAccount bankAccount = new BankAccount();
bankAccount.HolderName = "Mi empresa";
bankAccount.Alias = null;
bankAccount.CLABE = "012XXXXXXXXXX24616";
request.BankAccount = bankAccount;
request.Amount = new Decimal(10.50);
request.Description = "Retiro de saldo semanal";
request.OrderId = "oid-1110011";

Payout = api.PayoutService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var payoutRequest = {
   'method':'bank_account',
   'bank_account':{
      'clabe':'012298026516924616',
      'holder_name':'Mi empresa'
   },
   'amount':10.50,
   'description':'Retiro de saldo semanal',
   'order_id':'oid-1110011'
};

openpay.customers.payouts.create('ag4nktpdzebjiye1tlze', payoutRequest, function(error, payout) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@payouts=@openpay.create(:payouts)
bank_account_hash={
     "holder_name" => "Mi empresa",
     "alias" => nil,
     "clabe" => "012XXXXXXXXXX24616"
   }
request_hash={
     "method" => "bank_account",
     "bank_account" => bank_account_hash,
     "amount" => 10.50,
     "description" => "Retiro de saldo semanal",
     "order_id" => "oid-1110011"
   }

response_hash=@payouts.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Response example

```json
{
   "id":"tr4f2atubqchinw71vfs",
   "amount":10.50,
   "authorization":null,
   "method":"bank_account",
   "operation_type":"out",
   "transaction_type":"payout",
   "status":"in_progress",
   "currency":"MXN",
   "creation_date":"2014-05-26T17:23:03-05:00",
   "operation_date":"2014-05-26T17:23:03-05:00",
   "description":"Retiro de saldo semanal",
   "error_message":null,
   "order_id":"oid-1110011",
   "bank_account":{
      "clabe":"012XXXXXXXXXX24616",
      "bank_code":"012",
      "bank_name":"BANCOMER",
      "alias":null,
      "holder_name":"Mi empresa"
   },
   "customer_id":"asynwirguzkgq2bizogo"
}
```

Sends a payment to a bank account.

###Request 

Property | Description
--------- | -----
method|***string*** (required) <br/>It must contain the **bank_account** value.
[bank_account](#bank-account-object)  | ***object*** (required) <br/>Data of the bank account where the funds will be sent. <br/><br/> **clabe**.- CLABE account number where the funds will be sent. <br/>**holder_name**.- Name of the account owner .
amount | ***numeric*** (required) <br/>Amount of payout. Must be an amount greater than zero, with up to two decimal digits.
description | ***string*** (required, length = 250) <br/>A description associated to the payment.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of payout. Must be unique among all transactions.

###Response
Returns a [transaction object](#transaction-object) with the payout information or with an [error response](#error-object).

##Payout to a debit card.

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts
```

```php
<?
Customer
$customer = $openpay->customers->get(customerId);
$payout = $customer->payouts->create(payoutRequest);

Merchant
$payout = $openpay->payouts->create(payoutRequest);
?>
```

```java
//Customer
openpayAPI.payouts().create(String customerId, CreateCardPayoutParams request);

//Merchant
openpayAPI.payouts().create(CreateCardPayoutParams request);
```

```csharp
//Customer
openpayAPI.PayoutService.Create(string customer_id, PayoutRequest request);

//Merchant
openpayAPI.PayoutService.Create(PayoutRequest request);
```

```javascript
// Merchant
openpay.payouts.create(payoutRequest, callback);

// Customer
openpay.customers.payouts.create(customerId, payoutRequest, callback);
```

```ruby
#Customer
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash, customer_id)

#Merchant
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash)
```

> Customer request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/asynwirguzkgq2bizogo/payouts \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method": "card",
   "card": {
      "card_number": "4111111111111111",
      "holder_name": "Juan Perez Ramirez"
   },
   "amount" : 100.00,
   "description" : "Retiro de saldo semanal",
   "order_id" : "ORDEN-00021"
} ' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$payoutRequest = array(
    'method' => 'card',
    'card' => array(
        'card_number' => '4111111111111111',
        'holder_name' => 'Juan Perez Ramirez'),
    'amount' => 100.00,
    'description' => 'Retiro de saldo semanal',
    'order_id' => 'ORDEN-00021');

$customer = $openpay->customers->get('asynwirguzkgq2bizogo');
$payout = $customer->payouts->create($payoutRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateCardPayoutParams request = new CreateCardPayoutParams();
Card card = new Card();
card.holderName("Juan Perez Ramirez");
card.cardNumber("4111111111111111");
card.cvv2("110");
card.expirationMonth(12);
card.expirationYear(20);
request.card(card);
request.amount(new BigDecimal("100.00"));
request.description("Pago a cuenta de banco");
request.orderId("ord-103");

Payout payout = api.payouts().create("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
PayoutRequest request = new PayoutRequest();
request.Method = "card";
Card card = new Card();
card.HolderName = "Juan Perez Ramirez";
card.CardNumber = "4111111111111111";
card.Cvv2 = "110";
card.ExpirationMonth = "12";
card.ExpirationYear = "20";
request.Card = card;
request.Amount = new Decimal(100.00);
request.Description = "Pago a cuenta de banco";
request.OrderId = "ord-101";

Payout = api.PayoutService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var payoutRequest = {
   'method': 'card',
   'card': {
      'card_number': '4111111111111111',
      'holder_name': 'Juan Perez Ramirez'
   },
   'amount' : 10.50,
   'description' : 'Retiro de saldo semanal',
   'order_id' : 'oid-00021'
};

openpay.customers.payouts.create('asynwirguzkgq2bizogo', payoutRequest, function(error, payout) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@payouts=@openpay.create(:payouts)
card_hash={
     "holder_name" => "Juan Perez Ramirez",
     "card_number" => "411111XXXXXX1111",
     "cvv2" => "110",
     "expiration_month" => "12",
     "expiration_year" => "20"
   }
request_hash={
     "method" => "card",
     "card" => card_hash,
     "amount" => 10.50,
     "description" => "Retiro de saldo semanal",
     "order_id" => "oid-00021"
   }

response_hash=@payouts.create(request_hash.to_hash, "asynwirguzkgq2bizogo")
```

> Response example

```json
{
   "id":"trwpxhrgfeub9eqdyvqz",
   "amount":10.50,
   "authorization":null,
   "method":"card",
   "operation_type":"out",
   "transaction_type":"payout",
   "card":{
      "type":"debit",
      "brand":"visa",
      "address":null,
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "allows_charges":false,
      "allows_payouts":true,
      "bank_name":"Banamex",
      "bank_code":"002"
   },
   "status":"in_progress",
   "currency":"MXN",
   "creation_date":"2014-05-26T17:04:26-05:00",
   "operation_date":"2014-05-26T17:04:26-05:00",
   "description":"Retiro de saldo semanal",
   "error_message":null,
   "order_id":"oid-00021",
   "customer_id":"asynwirguzkgq2bizogo"
}
```

Sends a payment to a debit card. In  case the used card is not debit, the funds will be returned to the account from which they were withdrawn.

###Request 

Property | Description
--------- | -----
method|***string*** (required) <br/>It must contain the **card** value.
[card](#card-object) | ***object*** (required) <br/>Data of the card where the funds will be sent. <br/><br/> **card_number**.- Card number where the funds will be sent. <br/>**holder_name**.- Name of the card owner (cardholder).
amount | ***numeric*** (required) <br/>Amount of payout. Must be an amount greater than zero, with up to two decimal digits.
description | ***string*** (required, length = 250) <br/>A description associated to the payment.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of payout. Must be unique among all transactions.

###Response
Returns a [transaction object](#transaction-object) with the payout information or with an [error response](#error-object).

##Get a payout
> Definition

```shell
Merchant
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts/{TRANSACTION_ID}

Customer
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts/{TRANSACTION_ID}
```

```php
<?
Merchant
$payout = $openpay->payouts->get(transactionId);

Customer
$customer = $openpay->customers->get(customerId);
$payout = $customer->payouts->get(transactionId);
?>
```

```java
//Customer
openpayAPI.payouts().get(String customerId, String transactionId);

//Merchant
openpayAPI.payouts().get(String transactionId);
```

```csharp
//Customer
openpayAPI.PayoutService.Get(string customer_id, string transaction_id);

//Merchant
openpayAPI.PayoutService.Get(string transaction_id);
```

```javascript
// Merchant
openpay.payouts.get(transactionId, callback);

// Customer
openpay.customers.payouts.get(customerId, transactionId, callback);
```

```ruby
#Customer
@payouts=@openpay.create(:payouts)
@payouts.get(transaction_id, customer_id)

#Merchant
@payouts=@openpay.create(:payouts)
@payouts.get(transaction_id)
```

> Customer request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/asynwirguzkgq2bizogo/payouts/trwpxhrgfeub9eqdyvqz \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$customer = $openpay->customers->get('asynwirguzkgq2bizogo');
$payout = $customer->payouts->get('trwpxhrgfeub9eqdyvqz');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Payout payout = api.payouts().get("ag4nktpdzebjiye1tlze", "tr6cxbcefzatd10guvvw");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Payout = api.PayoutService.Get("ag4nktpdzebjiye1tlze", "tr6cxbcefzatd10guvvw");
```

```javascript
openpay.customers.payouts.get('ag4nktpdzebjiye1tlze', 'tr6cxbcefzatd10guvvw', function(error, payout) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@payouts=@openpay.create(:payouts)

response_hash=@payouts.get("tr6cxbcefzatd10guvvw", "asynwirguzkgq2bizogo")
```

> Response example

```json
{
   "id":"trwpxhrgfeub9eqdyvqz",
   "amount":10.50,
   "authorization":"TRWPXHRGFEUB9EQDYVQZ",
   "method":"card",
   "operation_type":"out",
   "transaction_type":"payout",
   "card":{
      "type":"debit",
      "brand":"visa",
      "address":null,
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":null,
      "expiration_month":null,
      "allows_charges":false,
      "allows_payouts":true,
      "bank_name":"Banamex",
      "bank_code":"002"
   },
   "status":"completed",
   "currency":"MXN",
   "creation_date":"2014-05-26T17:04:26-05:00",
   "operation_date":"2014-05-26T17:06:28-05:00",
   "description":"Retiro de saldo semanal",
   "error_message":null,
   "order_id":"oid-00021",
   "customer_id":"asynwirguzkgq2bizogo"
}
```

Returns de information of the payout. You must know the payout id.

###Request

Property | Description
--------- | ------
transaction_id| _**string**_ (required, length = 45)<br/>Id of the payout you want to get.

###Response
Returns a [transaction object](#transaction-object) with the payout information or with an [error response](#error-object).

##Cancel a payout
> Definition

```shell
Merchant
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts/{TRANSACTION_ID}

Customer
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts/{TRANSACTION_ID}
```

```php
<?
Merchant
$payout = $openpay->payouts->delete(transactionId);

Customer
$customer = $openpay->customers->get(customerId);
$payout = $customer->payouts->delete(transactionId);
?>
```

```java
//Customer
openpayAPI.payouts().cancel(String customerId, String transactionId);

//Merchant
openpayAPI.payouts().cancel(String transactionId);
```

```csharp
//Customer
openpayAPI.PayoutService.Cancel(string customer_id, string transaction_id);

//Merchant
openpayAPI.PayoutService.Cancel(string transaction_id);
```

```javascript
// Merchant
openpay.payouts.delete(transactionId, callback);

// Customer
openpay.customers.payouts.delete(customerId, transactionId, callback);
```

```ruby
#Customer
@payouts=@openpay.create(:payouts)
@payouts.delete(transaction_id, customer_id)

#Merchant
@payouts=@openpay.create(:payouts)
@payouts.delete(transaction_id)
```

> Customer request example

```shell
curl -X DELETE https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/asynwirguzkgq2bizogo/payouts/trozeipf364jqrsbt3ej \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$customer = $openpay->customers->get('asynwirguzkgq2bizogo');
$payout = $customer->payouts->delete('trozeipf364jqrsbt3ej');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Payout payout = api.payouts().cancel("ag4nktpdzebjiye1tlze", "trozeipf364jqrsbt3ej");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Payout = api.PayoutService.Cancel("ag4nktpdzebjiye1tlze", "trozeipf364jqrsbt3ej");
```

```javascript
openpay.customers.payouts.delete('ag4nktpdzebjiye1tlze', 'tr6cxbcefzatd10guvvw', function(error, payout) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@payouts=@openpay.create(:payouts)

response_hash=@payouts.delete("trozeipf364jqrsbt3ej", "asynwirguzkgq2bizogo")
```

> Response example

```json
{
   "id":"trozeipf364jqrsbt3ej",
   "amount":10.50,
   "authorization":"TROZEIPF364JQRSBT3EJ",
   "method":"card",
   "operation_type":"out",
   "transaction_type":"payout",
   "card":{
      "type":"debit",
      "brand":"visa",
      "address":null,
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":null,
      "expiration_month":null,
      "allows_charges":false,
      "allows_payouts":true,
      "bank_name":"Banamex",
      "bank_code":"002"
   },
   "status":"cancelled",
   "currency":"MXN",
   "creation_date":"2014-05-26T17:04:26-05:00",
   "operation_date":"2014-05-26T17:06:28-05:00",
   "description":"Retiro de saldo semanal",
   "error_message":null,
   "order_id":"oid-00025",
   "customer_id":"asynwirguzkgq2bizogo"
}
```

Cancels a payout in in_progress status, it means not yet completed. You must know the payout id.

###Request

Property | Description
--------- | ------
transaction_id| _**string**_ (required, length = 45)<br/>Payout Id you want to cancel.

###Response
Returns a [transaction object](#transaction-object) with the cancelled payout or with an [error response](#error-object).

##List of payouts

> Definition


```shell
Merchant
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts

Customer
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts
```

```php
<?
Merchant
$payoutList = $openpay->payouts->getList(searchParams);

Customer
$customer = $openpay->customers->get(customerId);
$payoutList = $customer->payouts->getList(searchParams);
?>
```

```java
//Customer
openpayAPI.payouts().list(String customerId, SearchParams request);

//Merchant
openpayAPI.payouts().list(SearchParams request);
```

```csharp
//Customer
openpayAPI.PayoutService.List(string customer_id, SearchParams request = null);

//Merchant
openpayAPI.PayoutService.List(SearchParams request = null);
```

```javascript
// Merchant
openpay.payouts.list(callback);
openpay.payouts.list(searchParams, callback);

// Customer
openpay.customers.payouts.list(customerId, callback);
openpay.customers.payouts.list(customerId, searchParams, callback);
```

```ruby
#Customer
@payouts=@openpay.create(:payouts)
@payouts.all(customer_id)

#Merchant
@payouts=@openpay.create(:payouts)
@payouts.all
```

> Request example 

```shell
curl -g "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/asynwirguzkgq2bizogo/payouts?creation[gte]=2013-11-01&limit=2&payout_type=AUTOMATIC" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$searchParams = array(
    'creation[gte]' => '2013-11-01',
    'creation[lte]' => '2017-12-31',
    'payout_type' => 'AUTOMATIC',
    'offset' => 0,
    'limit' => 2);

$customer = $openpay->customers->get('asynwirguzkgq2bizogo');
$payoutList = $customer->payouts->getList($searchParams);
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

List<Payout> payouts = api.payouts().list("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;
request.Amount = new Decimal(100.00);

List<Payout> payouts = api.PayoutService.List("ag4nktpdzebjiye1tlze", request);
```

```javascript
var searchParams = {
  'creation[gte]' : '2013-11-01',
  'payout_type' : 'AUTOMATIC',
  'limit' : 2
};

openpay.customers.payouts.list('asynwirguzkgq2bizogo', searchParams, function(error, list) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@payouts=@openpay.create(:payouts)

response_hash=@payouts.all("asynwirguzkgq2bizogo")
```

> Response example

```json
[
   {
      "id":"tr4f2atubqchinw71vfs",
      "amount":10.50,
      "authorization":"TR4F2ATUBQCHINW71VFS",
      "method":"bank_account",
      "operation_type":"out",
      "transaction_type":"payout",
      "status":"completed",
      "currency":"MXN",
      "creation_date":"2014-05-26T17:23:03-05:00",
      "operation_date":"2014-05-26T17:26:27-05:00",
      "description":"Retiro de saldo semanal",
      "error_message":null,
      "order_id":"oid-1110011",
      "bank_account":{
         "clabe":"012XXXXXXXXXX24616",
         "bank_code":"012",
         "bank_name":"BANCOMER",
         "alias":null,
         "holder_name":"Mi empresa"
      },
      "customer_id":"asynwirguzkgq2bizogo"
   },
   {
      "id":"trwpxhrgfeub9eqdyvqz",
      "amount":10.50,
      "authorization":"TRWPXHRGFEUB9EQDYVQZ",
      "method":"card",
      "operation_type":"out",
      "transaction_type":"payout",
      "card":{
         "type":"debit",
         "brand":"visa",
         "address":null,
         "card_number":"411111XXXXXX1111",
         "holder_name":"Juan Perez Ramirez",
         "expiration_year":null,
         "expiration_month":null,
         "allows_charges":false,
         "allows_payouts":true,
         "bank_name":"Banamex",
         "bank_code":"002"
      },
      "status":"completed",
      "currency":"MXN",
      "creation_date":"2014-05-26T17:04:26-05:00",
      "operation_date":"2014-05-26T17:06:28-05:00",
      "description":"Retiro de saldo semanal",
      "error_message":null,
      "order_id":"oid-00021",
      "customer_id":"asynwirguzkgq2bizogo"
   }
]
```
Gets a list of payouts made at Merchant or customer level.

###Request

You can search using the following parameters as filters.

Property | Description
--------- | ------
creation| ***date*** <br/>Same as creation date. Format yyyy-mm-dd
creation[gte]| ***date*** <br/>After the creation date. Format yyyy-mm-dd
creation[lte]| ***date*** <br/>Before the creation date. Format yyyy-mm-dd
offset| ***numeric*** <br/>Number of records to skip at the beginning, default 0.
limit| ***numeric*** <br/>Number of required records, default 10.
amount| ***numeric*** <br/>Same as the amount.
amount[gte] | ***numeric*** <br/>Greater than or equal to the amount.
amount[lte] | ***numeric*** <br/>Less than or equal to the amount.
payout_type | ***string (opfional, ALL, AUTOMATIC o MANUAL)***  <br/>Payout type used to filter the transactions

###Response

Returns a list of [transaction objects](#transaction-object) payouts in descending order by creation date.

##Summary Payouts

> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/reports/payout/{TRANSACTION_ID}
```

```php
<?
$transactionsPayout = $openpay->transactionsPayout->get(transactionId);
?>
```

```java
openpayAPI.transactionsPayout().getResume(String transactionId);
```

```csharp
openpayAPI.PayoutReportService.Get(string transaction_id);
```

```javascript
openpay.transactionsPayout.get(transactionId, callback);
```

```ruby
@transactionsPayout=@openpay.create(:transactionsPayout)
@transactionsPayout.get(transaction_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/reports/payout/trwpxhrgfeub9eqdyvqz \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$payout = $openpay->transactionsPayout->get('trwpxhrgfeub9eqdyvqz');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

TransactionsPayoutResume payoutResume = transactionsPayout().getResume("tr6cxbcefzatd10guvvw");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

PayoutSummary payoutSummary = api.PayoutReportService.Get("tr6cxbcefzatd10guvvw");
```

```javascript
openpay.transactionsPayout.get('tr6cxbcefzatd10guvvw', function(error, payout) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@transactionsPayout=@openpay.create(:transactionsPayout)

response_hash=@transactionsPayout.get("tr6cxbcefzatd10guvvw")
```

> Response example

```json
{
  "in": 2700,
  "out": 2400,
  "charged_adjustments": 0,
  "refunded_adjustments": 0
}
```
Return the summary of the payout. You must know the payout id.

###Request

Property | Description
--------- | ------
transaction_id| _**string**_ (required, length = 45)<br/>Id of the payout you want to get.

###Response
Returns a [summary payouts object](#summary-payout-object) with the summary of the payout or a [error response](#error-object).

##Summary Payout Object

> Object example

```json
{
   "in":2700,
   "out":2400,
   "charged_adjustments":0,
   "refunded_adjustments":0
}
```

Property | Description
--------- | ------
in | ***numeric*** <br/> Total amount in, Must be an amount with up to two decimal digits.
out | ***numeric*** <br/> Total amount out, Must be an amount with up to two decimal digits.
charged_adjustments | ***numeric*** <br/> Total amount of adjustment charges, Must be an amount with up to two decimal digits.
refunded_adjustments | ***numeric*** <br/> Total amount of refund charges, Must be an amount with up to two decimal digits.

##Payout Detail

> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/reports/payout/{TRANSACTION_ID}/detail
```

```php
<?
$transactionsPayout = $openpay->transactionsPayout->getDetails(transactionId, searchParams);
?>
```

```java
openpayAPI.transactionsPayout().getDetails(String transactionId, TransactionsPayoutType transactionsPayoutType, PaginationParams paginationParams);
```

```csharp
openpayAPI.PayoutReportService.Detail(string transaction_id, PayoutReportDetailSearchParams searchParams);
```

```javascript
openpay.transactionsPayout.getDetails(transactionId, searchParams, callback);
```

```ruby
@transactionsPayout=@openpay.create(:transactionsPayout)
@transactionsPayout.getDetails(transaction_id, searchParams)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/reports/payout/trwpxhrgfeub9eqdyvqz/detail?detail_type=IN \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$searchParams = array(
    'payout_type' => 'IN',
    'offset' => 0,
    'limit' => 100);

$payout = $openpay->transactionsPayout->getDetails('trwpxhrgfeub9eqdyvqz', $searchParams);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

      PaginationParams paginationParams = new PaginationParams();
      paginationParams.offset(0);
      paginationParams.limit(100);

List<GenericTransaction> payoutTransactions = transactionsPayout().getDetails("tr6cxbcefzatd10guvvw", TransactionsPayoutType.IN, paginationParams);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
PayoutReportDetailSearchParams searchParams = new PayoutReportDetailSearchParams();
searchParams.DetailType = "IN";
searchParams.Offset = 0;
searchParams.Limit = 100;

List<Transaction> transactions = api.PayoutReportService.Detail("tr6cxbcefzatd10guvvw", searchParam);
```

```javascript
var searchParams = {
  'detail_type' : 'IN',
  'offset' : 0,
  'limit' : 100
};

openpay.transactionsPayout.get('tr6cxbcefzatd10guvvw', searchParams, function(error, payout) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@transactionsPayout=@openpay.create(:transactionsPayout)

search_params_hash={
     "detail_type" => "IN",
     "offset" => 0,
     "limit" => 100
   }

response_hash=@transactionsPayout.getDetails("tr6cxbcefzatd10guvvw", search_params_hash.to_hash)
```

> Response example

```json
[
  {
    "id": "trqcwapqeilg596zwrvr",
    "authorization": "7BXqDL1fjb",
    "method": "bank_account",
    "operation_type": "in",
    "transaction_type": "charge",
    "status": "completed",
    "conciliated": true,
    "creation_date": "2016-09-13T12:57:34-05:00",
    "operation_date": "2016-09-13T12:57:34-05:00",
    "description": "mexzhpxok3houd5lbvz1",
    "error_message": null,
    "order_id": null,
    "bank_account": {
      "clabe": "113XXXXXXXXXX09568",
      "bank_code": "113",
      "bank_name": "VE POR MAS",
      "rfc": "OPE130906HN4",
      "holder_name": "persona003"
    },
    "amount": 700,
    "currency": "MXN"
  },
  {
    "id": "tru6lsl6xpvseqp87vjd",
    "authorization": "FPVYiN4nyw",
    "method": "bank_account",
    "operation_type": "in",
    "transaction_type": "charge",
    "card": {
      "type": "debit",
      "brand": "mastercard",
      "address": null,
      "card_number": "555555XXXXXX4444",
      "holder_name": "persona003",
      "expiration_year": null,
      "expiration_month": null,
      "allows_charges": false,
      "allows_payouts": false,
      "bank_name": "MASARI",
      "bank_code": "602"
    },
    "status": "completed",
    "conciliated": true,
    "creation_date": "2016-09-13T12:57:16-05:00",
    "operation_date": "2016-09-13T12:57:16-05:00",
    "description": "mexzhpxok3houd5lbvz1",
    "error_message": null,
    "order_id": null,
    "amount": 2000,
    "currency": "MXN"
  }
]
```

Returns a list of the transactions involved in a payout. You must know the payout id.

###Petición

Propiedad | Descripción
--------- | ------
transaction_id| _**string**_ (required, length = 45)<br/>Id of the payout you want to get.
detail_type| _**string**_ (***IN***, ***OUT***, ***CHARGED_ADJUSTMENTS***, ***REFUNDED_ADJUSTMENTS***) <br/>The detail type.
offset| _**numeric**_ <br/> Number of records to skip at the beginning, default 0.
limit| _**numeric**_ <br/> Number of required records, default 10.

###Response
Return a list of [transaction objects](#transaction-object) in descending order by creation date or a [error response](#error-object).


#Customers

Customers are Openpay resources that are handled within the Merchant account and can represent users, customers or partners according to the type of Merchant.

You can add cards and bank accounts  to the customers so you can make transactions like Charges, Transfers or Payouts.

##Customer object

> Object example

```json
{
   "id":"cz4nkhrlcu9k7qd4lwqx",
   "creation_date":"2013-11-08T12:04:46-06:00",
   "name":"Rodrigo",
   "last_name":"Velazco Perez",
   "email":"rodrigo.velazco@payments.com", 
   "phone_number":"4425667045",
   "external_id":"cliente1",
   "status":"active",
   "balance":103,
   "address":{
      "line1":"Av. 5 de febrero No. 1080 int Roble 207",
      "line2":"Carrillo puerto",
      "line3":"Zona industrial carrillo puerto",
      "postal_code":"06500",
      "state":"Querétaro",
      "city":"Querétaro",
      "country_code":"MX"
   },
   "store": {
       "reference": "OPENPAY02DQ35YOY7",
       "barcode_url": "https://sandbox-api.openpay.mx/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
   "clabe": "646180109400423323"
}
```

Property | Description
--------- | -----
id            |***string*** <br/>Customer unique identifier.
creation_date |***datetime*** <br/>Date and time when the customer was created in ISO 8601 format. 
name          |***string*** <br/>Name of the customer.
last_name     |***string*** <br/>Last name of the customer.
email         |***string*** <br/>Email of the customer.
phone_number  |***numeric*** <br/>Telephone number of the customer.
status        |***string*** <br/>Account status of the customer can be active or deleted. If the account is on deleted status, no transaction is allowed.
balance       |***numeric*** <br/>Account balance with two decimal digits.
clabe         |***numeric*** <br/>CLABE account used to receive funds by transfer from any bank in Mexico.
[address](#addres-object) |***object*** <br/>Address of the customer. It is usually used as shipping address.
[store](#store-object) |_*object**_ <br/>Contains reference string to go to Store and make deposits, the url to generate barcode is contained too.

##Create a new customer

> Definition

```shell
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers
```

```php
<?
$customer = $openpay->customers->add(customerData);
?>
```

```java
openpayAPI.customers().create(Customer customer);
```

```csharp
openpayAPI.CustomerService.Create(Customer customer);
```

```javascript
openpay.customers.create(customerRequest, callback);
```

```ruby
@customers=@openpay.create(:customers)
@customers.create(request_hash)
```

> Request example 

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "name": "customer name",
   "email": "customer_email@me.com",
   "requires_account": false 
   }' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$customerData = array(
     'external_id' => '',
     'name' => 'customer name',
     'last_name' => '',
     'email' => 'customer_email@me.com',
     'requires_account' => false,
     'phone_number' => '44209087654',
     'address' => array(
         'line1' => 'Calle 10',
         'line2' => 'col. san pablo',
         'line3' => 'entre la calle 1 y la 2',
         'state' => 'Queretaro',
         'city' => 'Queretaro',
         'postal_code' => '76000',
         'country_code' => 'MX'
      )
   );

$customer = $openpay->customers->add($customerData);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer request = new Customer();
request.externalId("idExterno0101");
request.name("Julian Gerardo");
request.lastName("López Martínez");
request.email("julian.martinez@gmail.com");
request.phoneNumber("4421432915");
request.requiresAccount(false);
Address address = new Address();
address.city("Queretaro");
address.countryCode("MX");
address.state("Queretaro");
address.postalCode("79125");
address.line1("Av. Pie de la cuesta #12");
address.line2("Desarrollo San Pablo");
address.line3("Qro. Qro.");
request.address(address);

request = api.customers().create(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer request = new Customer();
request.ExternalId = "idExterno0101";
request.Name = "Julian Gerardo";
request.LastName = "López Martínez";
request.Email = "julian.martinez@gmail.com";
request.PhoneNumber = "4421432915";
request.RequiresAccount = false;
Address address = new Address();
address.City = "Queretaro";
address.CountryCode = "MX";
address.State = "Queretaro";
address.PostalCode = "79125";
address.Line1 = "Av. Pie de la cuesta #12";
address.Line2 = "Desarrollo San Pablo";
address.Line3 = "Qro. Qro.";
request.Address = address;

request = api.CustomerService.Create(request);
```

```javascript
var customerRequest = {
   'name': 'customer name',
   'email': 'customer_email@me.com',
   'requires_account': false 
   };

openpay.customers.create(customerRequest, function(error, customer) {
  // ... 
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@customers=@openpay.create(:customers)
address_hash={
      "line1" => "Calle 10",
      "line2" => "col. san pablo",
      "line3" => "entre la calle 1 y la 2",
      "state" => "Queretaro",
      "city" => "Queretaro",
      "postal_code" => "76000",
      "country_code" => "MX"
   }
request_hash={
     "external_id" => nil,
     "name" => "customer name",
     "last_name" => nil,
     "email" => "customer_email@me.com",
     "requires_account" => false,
     "phone_number" => "44209087654",
     "address" => address_hash
   }

response_hash=@customers.create(request_hash.to_hash)
```

> Response example

```json
{
   "id":"anbnldwgni1way3yp2dw",
   "name":"customer name",
   "last_name":null,
   "email":"customer_email@me.com",
   "phone_number":null,
   "address":null,
   "creation_date":"2014-05-20T16:47:47-05:00",
   "external_id":null,
   "store": {
       "reference": "OPENPAY02DQ35YOY7",
       "barcode_url": "https://sandbox-api.openpay.mx/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
   "clabe": "646180109400423323"
}
```

Create a customer object.

###Request

Property | Description
--------- | ------
external_id | ***string*** (optional, length = 100)  <br/> Unique external identifier of the customer assigned for the Merchant.
name        | ***string*** (required, length = 100)<br/>Name of the customer.
last_name   | ***string*** (optional, length = 100)<br/>Last name of the customer.
email       | ***string*** (required, length = 100)<br/>Email of the customer.
requires_account | ***boolean***  (optional, default = true) <br/>Send it with **false** value if you need to create the customer without an account to manage the balance.
phone_number| ***string*** (optional, length = 100) <br/>Telephone number of the customer.
[address](#address-object) | ***object*** (optional) <br/>Address of the customer. It is usually used as shipping address.

###Response

Returns a [customer object](#customer-object) when all the data were sent correctly, or returns an [error response](#error-object) if a problem happened.


##Update a customer

> Definition

```shell
PUT https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}
```

```php
<?
$customer = $openpay->customers->get(customerId);
$customer->save();
?>
```

```java
openpayAPI.customers().update(Customer customer);
```

```csharp
openpayAPI.CustomerService.Update(Customer customer);
```

```javascript
openpay.customers.update(customerId, customerRequest, callback);
```

```ruby
@customers=@openpay.create(:customers)
@customers.update(request_hash)
```

> Request example 

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/anbnldwgni1way3yp2dw \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X PUT -d '{
   "name": "customer name",
   "email": "customer_email@me.com",
   "address":{
      "city":"Queretaro",
      "state":"Queretaro",
      "line1":"Calle 10",
      "postal_code":"76000",
      "line2":"col. san pablo",
      "line3":"entre la calle 1 y la 2",
      "country_code":"MX"
   },
   "phone_number":"44209087654"
 }' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$customer->name = 'Juan';
$customer->last_name = 'Godinez';
$customer->save();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer request = new Customer();
request.name("Julian Gerardo");
request.lastName("López Martínez");
request.email("julian.martinez@gmail.com");
request.phoneNumber("4421432915");
Address address = new Address();
address.city("Queretaro");
address.countryCode("10");
address.state("Queretaro");
address.postalCode("79125");
address.line1("Av. Pie de la cuesta #12");
address.line2("Desarrollo San Pablo");
address.line3("Qro. Qro.");
request.address(address);

request = api.customers().update(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer request = new Customer();
request.Name = "Julian Gerardo";
request.LastName = "López Martínez";
request.Email = "julian.martinez@gmail.com";
request.PhoneNumber = "4421432915";
Address address = new Address();
address.City = "Queretaro";
address.CountryCode = "MX";
address.State = "Queretaro";
address.PostalCode = "79125";
address.Line1 = "Av. Pie de la cuesta #12";
address.Line2 = "Desarrollo San Pablo";
address.Line3 = "Qro. Qro.";
request.Address = address;

request = api.CustomerService.Update(request);
```

```javascript
var customerRequest = {
    'name': 'customer name',
    'email': 'customer_email@me.com',
    'address':{
      'city':'Queretaro',
      'state':'Queretaro',
      'line1':'Calle 10',
      'postal_code':'76000',
      'line2':'col. san pablo',
      'line3':'entre la calle 1 y la 2',
      'country_code':'MX'
    }
};

openpay.customers.update('anbnldwgni1way3yp2dw', customerRequest, function(error, customer) {
  // ... 
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@customers=@openpay.create(:customers)
address_hash={
      "line1" => "Calle 10",
      "line2" => "col. san pablo",
      "line3" => "entre la calle 1 y la 2",
      "state" => "Queretaro",
      "city" => "Queretaro",
      "postal_code" => "76000",
      "country_code" => "MX"
   }
request_hash={
     "external_id" => nil,
     "name" => "customer name",
     "last_name" => nil,
     "email" => "customer_email@me.com",
     "phone_number" => "44209087654",
     "address" => address_hash
   }

response_hash=@customers.update(request_hash.to_hash)
```

> Response example

```json
{
   "id":"anbnldwgni1way3yp2dw",
   "name":"customer name",
   "last_name":null,
   "email":"customer_email@me.com",
   "phone_number":"44209087654",
   "address":{
      "line1":"Calle 10",
      "line2":"col. san pablo",
      "line3":"entre la calle 1 y la 2",
      "state":"Queretaro",
      "city":"Queretaro",
      "postal_code":"76000",
      "country_code":"MX"
   },
   "store": {
      "reference": "OPENPAY02DQ35YOY7",
      "barcode_url": "https://sandbox-api.openpay.mx/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
   "clabe": "646180109400423323",
   "creation_date":"2014-05-20T16:47:47-05:00",
   "external_id":null
}
```

Updates one or more data of the customer. 

###Request

Property | Description
--------- | ------
name        | ***string*** (required, length = 100)<br/>Name of the customer.
last_name   | ***string*** (optional, length = 100)<br/>Last name of the customer.
email       | ***string*** (required, length = 100)<br/>Email of the customer.
phone_number| ***string*** (optional, length = 100) <br/>Telephone number of the customer.
[address](#address-object) | ***object*** (optional) <br/>Address of the customer. It is usually used as shipping address.

###Response

Returns a [customer object](#customer-object) with the updated info, or returns an [error response](#error-object) if a problem happened while updating.


##Get an existing customer

> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}
```

```php
<?
$customer = $openpay->customers->get(customerId);
?>
```

```java
openpayAPI.customers().get(String customerId);
```

```csharp
openpayAPI.CustomerService.Update(string customer_id);
```

```javascript
openpay.customers.get(customerId, callback);
```

```ruby
@customers=@openpay.create(:customers)
@customers.get(customer_id)
```

> Request example 

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/anbnldwgni1way3yp2dw \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer customer = api.customers().get("a9pvykxz4g5rg0fplze0");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer customer = api.CustomerService.Update("a9pvykxz4g5rg0fplze0");
```

```javascript
openpay.customers.get('a9pvykxz4g5rg0fplze0', function(error, customer) {
  // ... 
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@customers=@openpay.create(:customers)

response_hash=@customers.get("asynwirguzkgq2bizogo")
```

> Response example

```json
{
   "id":"anbnldwgni1way3yp2dw",
   "name":"customer name",
   "last_name":null,
   "email":"customer_email@me.com",
   "phone_number":"44209087654",
   "address":{
      "line1":"Calle 10",
      "line2":"col. san pablo",
      "line3":"entre la calle 1 y la 2",
      "state":"Queretaro",
      "city":"Queretaro",
      "postal_code":"76000",
      "country_code":"MX"
   },
   "store": {
       "reference": "OPENPAY02DQ35YOY7",
       "barcode_url": "https://sandbox-api.openpay.mx/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
   "clabe": "646180109400423323",
   "creation_date":"2014-05-20T16:47:47-05:00",
   "external_id":null
}
```

Gets the current information of an existing customer. You only need to specify the id returned when creating the customer.

###Request

Property | Description
--------- | ------
id| _**string**_ (required, legth = 45)<br/>Unique identifier of the customer. 

###Response

If the identifier exists, it returns a [customer object](#customer-object) with the customer information.

##Delete a customer

> Definition

```shell
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}
```

```php
<?
$customer = $openpay->customers->get(customerId);
$customer->delete();
?>
```

```java
openpayAPI.customers().delete(String customerId);
```

```csharp
openpayAPI.CustomerService.Delete(string customer_id);
```

```javascript
openpay.customers.delete(customerId, callback);
```

```ruby
@customers=@openpay.create(:customers)
@customers.delete(customer_id)
```

> Request example 

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/anbnldwgni1way3yp2dw \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X DELETE
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$customer->delete();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.customers().delete("a9pvykxz4g5rg0fplze0");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.CustomerService.Delete("a9pvykxz4g5rg0fplze0");
```

```javascript
openpay.customers.delete('a9pvykxz4g5rg0fplze0', function(error) {
  // ... 
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@customers=@openpay.create(:customers)

response_hash=@customers.delete("asynwirguzkgq2bizogo")
```


Deletes a customer permanently. All the related subscriptions will be canceled. Openpay keeps the operations records.

###Request

Property | Description
--------- | ------
id| _**string**_ (required, length = 45)<br/> Unique identifier of the customer you want to delete.

###Response
If the customer is deleted correctly, it returns an empty response, if the customer can not be deleted it returns a [error object](#error-object) explaining the reason.

##List of customers

> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers
```

```php
<?
$customerList = $openpay->customers->getList(findDataRequest);
?>
```

```java
openpayAPI.customers().list(SearchParams request);
```

```csharp
openpayAPI.CustomerService.List(SearchParams request = null);
```

```javascript
openpay.customers.list(callback);
openpay.customers.list(searchParams, callback);
```

```ruby
@customers=@openpay.create(:customers)
@customers.all
```

> Request example 

```shell
curl -g "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers?creation[gte]=2013-11-01&limit=2" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$findDataRequest = array(
    'creation[gte]' => '2013-01-01',
    'creation[lte]' => '2013-12-31',
    'offset' => 0,
    'limit' => 5);

$customerList = $openpay->customers->getList($findDataRequest);
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

List<Customer> customers = api.customers().list(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;

List<Customer> customers = api.CustomerService.List(request);
```

```javascript
var searchParams = {
  'creation[gte]' : '2013-11-01',
  'limit' : 2
};

openpay.customers.list(searchParams, function(error, list) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@customers=@openpay.create(:customers)

response_hash=@customers.all
```

> Response example

```json
[{
   "id":"cpjdhf754ythr65yu9k7q",
   "creation_date":"2013-11-08T12:04:46-06:00",
   "name":"Rodrigo",
   "last_name":"Velazco Perez",
   "email":"rodrigo.velazco@payments.com",
   "phone_number":"4425667045",
   "status":"active",
   "balance":142.5
   "store": {
       "reference": "OPENPAY02DQ35YOY7",
       "barcode_url": "https://sandbox-api.openpay.mx/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
   "clabe": "646180109400423323"
}, {
   "id":"cz4nkhrlcu9k7qd4lwqx",
   "creation_date":"2013-11-07T14:54:46-06:00",
   "name":"Eriberto",
   "last_name":"Rodriguez Lopez",
   "email":"eriberto.rodriguez@payments.com",
   "phone_number":"442",
   "status":"active",
   "balance":103,
   "store": {
       "reference": "OPENPAY02DQ35DRE4",
       "barcode_url": "https://sandbox-api.openpay.mx/barcode/OPENPAY02DQ35DRE4?width=1&height=45&text=false"
  },
  "clabe": "646180109400423323"
}]
```
Returns a list of registered customers, if you want to delimit the result you may use filters.

###Request
You can search using the following parameters as filters.

Property | Description
--------- | ------
external_id| _**string**_ <br/>Unique customer id generated by the merchant and associated to the customer by the external_id field of the create customer request
creation| ***date*** <br/>Same as the customer creation date. Format yyyy-mm-dd
creation[gte]| ***date*** <br/>After the customer creation date .Format yyyy-mm-dd
creation[lte]| ***date*** <br/>Before the customer creation date.Format yyyy-mm-dd
offset| ***numeric*** <br/>Number of records to skip at the beginning, default 0.
limit| ***numeric*** <br/>Number of required records, default 10.

###Response

Returns an array of [customer object](#customer-object).


#Transfers

The transfers allow to send funds between accounts of your customers. 

<aside class="notice">
**Note:** If you want to make a transfer to a bank see the [payouts section](#payouts-or-withdrawals).
</aside>

##Transfers between customers

> Definition

```shell
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/transfers
```

```php
<?
$customer = $openpay->customers->get(customerId);
$transfer = $customer->transfers->create(transferDataRequest);
?>
```

```java
openpayAPI.transfers().create(String customerId, CreateTransferParams request);
```

```csharp
openpayAPI.TransferService.Create(string from_customer_id, TransferRequest request);
```

```javascript
openpay.customers.transfers.create(customerId, transferRequest, callback);
```

```ruby
@transfers=@openpay.create(:transfers)
@transfers.create(request_hash, from_customer_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/transfers \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{                                            
     "customer_id" : "dvocf97jd20es3tw5laz",
     "amount" : 12.50,          
     "description" : "Transferencia entre cuentas",
     "order_id" : "oid-1245"
}' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$transferDataRequest = array(
    'customer_id' => 'aqedin0owpu0kexr2eor',
    'amount' => 12.50,
    'description' => 'Cobro de Comisión',
    'order_id' => 'ORDEN-00061');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$transfer = $customer->transfers->create($transferDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateTransferParams request = new CreateTransferParams();
request.toCustomerId("ah1ki9jmb50mvlsf9gqn");
request.amount(new BigDecimal("100.00"));
request.description("Transferencia del Customer 1 al Customer 2");
request.orderId("idOrdExt-0101");

Transfer transfer = api.transfers().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
TransferRequest request = new TransferRequest();
request.CustomerId = "ah1ki9jmb50mvlsf9gqn";
request.Amount = new Decimal(100.00);
request.Description = "Transferencia del Customer 1 al Customer 2";
request.OrderId = "idOrdExt-0101";

Transfer transfer = api.TransferService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var transferRequest = {                                          
  'customer_id' : 'dvocf97jd20es3tw5laz',
  'amount' : 12.50,          
  'description' : 'Transferencia entre cuentas',
  'order_id' : 'oid-1245'
};

openpay.customers.transfers.create('ag4nktpdzebjiye1tlze', transferRequest, function(error, transfer) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@transfers=@openpay.create(:transfers)
request_hash={
     "customer_id" => "dvocf97jd20es3tw5laz",
     "amount" => 12.50,
     "description" => "Transferencia entre cuentas",
     "order_id" => "oid-1245"
   }

response_hash=@transfers.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Response example

```json
{
   "amount":12.50,
   "authorization":null,
   "method":"customer",
   "operation_type":"out",
   "currency":"MXN",
   "transaction_type":"transfer",
   "status":"completed",
   "id":"twpmbike2jejex3pahzd",
   "creation_date":"2013-11-15T10:33:19-06:00",
   "description":"Transferencia entre cuentas",
   "error_message":null,
   "order_id":"oid-1245",
   "customer_id":"a9pvykxz4g5rg0fplze0",
   "store": {
       "reference": "OPENPAY02DQ35YOY7",
       "barcode_url": "https://sandbox-api.openpay.mx/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
   "clabe": "646180109400423323"
}
```

Makes the transfer of funds from one account of the customer to another. The funds will be charged to an origin account and added to a destination account, which will create two transactions.

###Request

Property | Description
--------- | ------
customer_id | ***string*** (required, length = 45) <br/>The Openpay ID of the customer you want to send the funds.
amount | ***numeric*** (required) <br/>Amount to transfer. It must be an amount greater than one peso with up to two decimal digits. 
description | ***string*** (required, length = 250) <br/>A description associated to the transfer.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of the transfer. It will be assigned to the withdrawal transaction.

###Response
If the transaction is successful, the response will contain a [transaction object] (#transaction-object). This object represents the withdrawal of the account of the current customer. On error, the error object will be returned.

##Get a transfer

> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/transfers/{TRANSACTION_ID}
```

```php
<?
$customer = $openpay->customers->get(customerId);
$transfer = $customer->transfers->get(transactionId);
?>
```

```java
openpayAPI.transfers().get(String customerId, String transactionId);
```

```csharp
openpayAPI.TransferService.Get(string customer_id, string transaction_id);
```

```javascript
openpay.customers.transfers.get(customerId, transactionId, callback);
```

```ruby
@transfers=@openpay.create(:transfers)
@transfers.get(transaction_id, customer_id)
```

> Request example 

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/transfers/twpmbike2jejex3pahzd \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" 
``` 

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$transfer = $customer->transfers->get('tyxesptjtx1bodfdjmlb');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Transfer transfer = api.transfers().get("a9pvykxz4g5rg0fplze0", "tr6cxbcefzatd10guvvw");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Transfer transfer = api.TransferService.Get("a9pvykxz4g5rg0fplze0", "tr6cxbcefzatd10guvvw");
```

```javascript
openpay.customers.transfers.get('ag4nktpdzebjiye1tlze', 'twpmbike2jejex3pahzd', function(error, transfer) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@transfers=@openpay.create(:transfers)

response_hash=@transfers.get("twpmbike2jejex3pahzd", "ag4nktpdzebjiye1tlze")
```

> Response example

```json
{
   "amount":12.50,
   "authorization":null,
   "method":"customer",
   "operation_type":"out",
   "currency":"MXN",
   "transaction_type":"transfer",
   "status":"completed",
   "id":"twpmbike2jejex3pahzd",
   "creation_date":"2013-11-15T10:33:19-06:00",
   "description":"Transferencia entre cuentas",
   "error_message":null,
   "order_id":"oid-1245",
   "customer_id":"dvocf97jd20es3tw5laz"
}
```
With the customer identifier and the transfer identifier, you can get the details of the transaction. The output transaction will be on the customer from which the transfer was made, and the entry transaction will be on the customer that received the amount.


###Request
Property | Description
--------- | ------
customer_id| ***string*** (required, length = 45) <br/> Identifier of the customer.
transaction_id| ***string*** (required, length = 45) <br/> Identifier of the transfer.

###Response
Returns a [transaction object] (#transaction-object)

##List of transfers

> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/transfers
```

```php
<?
$customer = $openpay->customers->get(customerId);
$transferList = $customer->transfers->getList(findDataRequest);
?>
```

```java
openpayAPI.transfers().list(String customerId, SearchParams request);
```

```csharp
openpayAPI.TransferService.List(string customer_id, SearchParams request = null);
```

```javascript
openpay.customers.transfers.list(customerId, callback);
openpay.customers.transfers.list(customerId, searchParams, callback);
```

```ruby
@transfers=@openpay.create(:transfers)
@transfers.all(customer_id)
```

> Request example

```shell
curl -g "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/transfers?limit=2" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$findDataRequest = array(
    'creation[gte]' => '2013-01-01',
    'creation[lte]' => '2013-12-31',
    'offset' => 0,
    'limit' => 5);

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$transferList = $customer->transfers->getList($findDataRequest);
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

List<Transfer> transfers = api.transfers().list("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;

List<Transfer> transfers = api.TransferService.List("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var searchParams = {
  'limit' : 2
};

openpay.customers.transfers.list('ag4nktpdzebjiye1tlze', searchParams, function(error, list) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@transfers=@openpay.create(:transfers)

response_hash=@transfers.all("asynwirguzkgq2bizogo")
```

> Response example

```json
[
   {
      "amount":130.00,
      "authorization":null,
      "method":"customer",
      "currency":"MXN",
      "operation_type":"out",
      "transaction_type":"transfer",
      "status":"completed",
      "id":"a74mbe4e2j5gc6gfahzd",
      "creation_date":"2013-09-18T00:31:19-06:00",
      "description":"Una descripcion",
      "error_message":null,
      "order_id":"20131115103317",
      "customer_id":"afk4csrazjp1udezj1po"
   },
   {
      "amount":130.00,
      "authorization":null,
      "method":"customer",
      "currency":"MXN",
      "operation_type":"in",
      "transaction_type":"transfer",
      "status":"completed",
      "id":"a74mbe4e2j5gc6gfahzd",
      "creation_date":"2013-09-18T00:31:19-06:00",
      "description":"Una descripcion",
      "error_message":null,
      "order_id":null,
      "customer_id":"agdn58ngcnogqmzruz1i"
   }
]
```

It allows to consult the entry and output transactions of a customer.

###Request
You can search using the following parameters as filters.

Property | Description
--------- | ------
creation| ***date*** <br/>Same as creation date. Format yyyy-mm-dd
creation[gte]| ***date*** <br/>After the creation date. Format yyyy-mm-dd
creation[lte]| ***date*** <br/>Before the creation date. Format yyyy-mm-dd
offset| ***numeric*** <br/>Number of records to skip at the beginning, default 0.
limit| ***numeric*** <br/>Number of required records, default 10.

###Response
List of [[transaction objects] (#transaction-object) of the transfers made, each one with the identifier of the customer that made it. The transactions will be listed in descending order by creation date.



#Cards
Within the Openpay platform you can add cards to the customer's account, delete them, recover some in specific and list them.

You can store multiple debit and / or credit cards at Merchant or customer level for making charges later without the need to enter the information again.

##Card Object

> Object example 

```json
{
   "type":"debit",
   "brand":"mastercard",
   "address":{
      "line1":"Av 5 de Febrero",
      "line2":"Roble 207",
      "line3":"col carrillo",
      "state":"Queretaro",
      "city":"Querétaro",
      "postal_code":"76900",
      "country_code":"MX"
   },
   "id":"kgipbqixvjg3gbzowl7l",
   "card_number":"1111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "allows_charges":true,
   "allows_payouts":false,
   "creation_date":"2013-12-12T17:50:00-06:00",
   "bank_name":"DESCONOCIDO",
   "bank_code":"000",
   "customer_id":"a2b79p8xmzeyvmolqfja",
   "points_card":true
}
```

Property | Description
--------- | ------
id            |***string*** <br/>Unique identifier of the card.
creation_date |***datetime*** <br/>Date and time when the card was created in ISO 8601 format.
holder_name |***string***  <br/>Name of the cardholder.
card_number |***numeric***  <br/>Card Number, it can be 16 or 19 digits.
cvv2 |***numeric***  <br/>Security code as it appears on the back of the card. Usually 3 digits..
expiration_month |***numeric***  <br/>Expiration month as it appears on the card.
expiration_year |***numeric***  <br/>Expiration year as it appears on the card.
[address](#address-object) |***object*** <br/>Billing address of cardholder.
allows_charges |***boolean*** <br/>It allows to know if you can make charges to the card.
allows_payouts |***boolean*** <br/>It allows to know if you can send payments to the card. 
brand |***string*** <br/>Card brand: visa, mastercard, carnet or american express.
type |***string*** <br/>Card Type: debit, credit, cash, etc.
bank_name |***string*** <br/>Name of the issuing bank.
bank_code |***string*** <br/>Code of the issuing bank.
customer_id |***string*** <br/>Customer identifier to which the card belongs. If the card is at Merchant level this value is null.
points_card |***boolean*** <br/>Indicates whether the card allows the use of reward points.

##Create a card

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/cards

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->add(cardDataRequest);

//Merchant
$card = $openpay->cards->add(cardDataRequest);
?>
```

```java
//Customer
openpayAPI.cards().create(String customerId, Card request);

//Merchant
openpayAPI.cards().create(Card request);
```

```csharp
//Customer
openpayAPI.CardService.Create(string customer_id, Card card);

//Merchant
openpayAPI.CardService.Create(Card card);
```

```javascript
// Merchant
openpay.cards.create(cardRequest, callback);

// Customer
openpay.customers.cards.create(customerId, cardRequest, callback);
```

```ruby
#Customer
@cards=@openpay.create(:cards)
@cards.create(request_hash, customer_id)

#Merchant
@cards=@openpay.create(:cards)
@cards.create(request_hash)
```

> Customer Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "card_number":"4111111111111111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "cvv2":"110"
 }' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$cardDataRequest = array(
    'holder_name' => 'Teofilo Velazco',
    'card_number' => '4916394462033681',
    'cvv2' => '123',
    'expiration_month' => '12',
    'expiration_year' => '15',
    'address' => array(
            'line1' => 'Privada Rio No. 12',
            'line2' => 'Co. El Tintero',
            'line3' => '',
            'postal_code' => '76920',
            'state' => 'Querétaro',
            'city' => 'Querétaro.',
            'country_code' => 'MX'));

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$card = $customer->cards->add($cardDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card request = new Card();
request.holderName("Juan Perez Ramirez");
request.cardNumber("4111111111111111");
request.cvv2("110");
request.expirationMonth(12);
request.expirationYear(20);
Address address = new Address();
address.city("Queretaro");
address.countryCode("10");
address.state("Queretaro");
address.postalCode("79125");
address.line1("Av. Pie de la cuesta #12");
address.line2("Desarrollo San Pablo");
address.line3("Qro. Qro.");
request.address(address);

request = api.cards().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card request = new Card();
request.HolderName = "Juan Perez Ramirez";
request.CardNumber = "4111111111111111";
request.Cvv2 = "110";
request.ExpirationMonth = "12";
request.ExpirationYear = "20";
Address address = new Address();
address.City = "Queretaro";
address.CountryCode = "MX";
address.State = "Queretaro";
address.PostalCode = "79125";
address.Line1 = "Av. Pie de la cuesta #12";
address.Line2 = "Desarrollo San Pablo";
address.Line3 = "Qro. Qro.";
request.Address = address;

request = api.CardService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var cardRequest = {
   'card_number':'4111111111111111',
   'holder_name':'Juan Perez Ramirez',
   'expiration_year':'20',
   'expiration_month':'12',
   'cvv2':'110'
};

openpay.customers.cards.create('a9pvykxz4g5rg0fplze0', cardRequest, function(error, card)  {
    // ...    
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)
address_hash={
      "line1" => "Calle 10",
      "line2" => "col. san pablo",
      "line3" => "entre la calle 1 y la 2",
      "state" => "Queretaro",
      "city" => "Queretaro",
      "postal_code" => "76000",
      "country_code" => "MX"
   }
request_hash={
     "holder_name" => "Juan Perez Ramirez",
     "card_number" => "411111XXXXXX1111",
     "cvv2" => "110",
     "expiration_month" => "12",
     "expiration_year" => "20",
     "address" => address_hash
   }

response_hash=@cards.create(request_hash.to_hash, "asynwirguzkgq2bizogo")
```

> Response example

```json
{
   "id":"ktrpvymgatocelsciak7",
   "type":"debit",
   "brand":"visa",
   "card_number":"411111XXXXXX1111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "allows_charges":true,
   "allows_payouts":true,
   "creation_date":"2014-05-21T17:31:01-05:00",
   "bank_name":"Banamex",
   "customer_id":"ag4nktpdzebjiye1tlze",
   "bank_code":"002"
}
```
 
When a card is created the customer must be specified, if the customer is not specified the card will be registered for the Merchant account. Once the card is saved, it can not obtain the number and security code.

<aside class = "notice">
**Note:** When stored in Openpay, all cards  are validated by making an authorization for $ 10.00 which is returned at the time.
</aside>

When saving a card, an ID will be created which can be used to make card charges, payouts to a card or just for getting the not sensitive card information.

###Request

Property | Description
--------- | ------
holder_name |***string*** (required, length  = 80) <br/>Name of the cardholder.
card_number |***numeric*** (required) <br/>Card Number, it can be 16 or 19 digits.
cvv2 |***numeric*** (required) <br/>Security code as it appears on the back of the card. Usually 3 digits.
expiration_month |***numeric*** (required) <br/>Expiration month as it appears on the card.
expiration_year |***numeric*** (required) <br/>Expiration year as it appears on the card.
[address](#address-object) |***object*** <br/>Billing address of cardholder.

###Response
Returns a [card object](#card-object) when it is created correctly or returns an [error response](#error-object) if a problem happened during the creation.


##Create a card with token
 
> Definition

```shell
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/cards

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->add(cardDataRequest);

//Merchant
$card = $openpay->cards->add(cardDataRequest);
?>
```

```java
//Customer
openpayAPI.cards().create(String customerId, Card card);

//Merchant
openpayAPI.cards().create(Card card);
```

```csharp
//Customer
openpayAPI.CardService.Create(string customer_id, Card request);

//Merchant
openpayAPI.CardService.Create(Card request);
```

```javascript
// Merchant
openpay.cards.create(cardRequest, callback);

// Customer
openpay.customers.cards.create(customerId, cardRequest, callback);
```

```ruby
#Customer
@cards=@openpay.create(:cards)
@cards.create(request_hash, customer_id)

#Merchant
@cards=@openpay.create(:cards)
@cards.create(request_hash)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
      "token_id":"tokgslwpdcrkhlgxqi9a",
      "device_session_id":"8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o"
   }' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$cardDataRequest = array(
    'token_id' => 'tokgslwpdcrkhlgxqi9a',
    'device_session_id' => '8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o'
    );

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$card = $customer->cards->add($cardDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card request = new Card();
request.tokenId("tokgslwpdcrkhlgxqi9a");
request.deviceSessionId("8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o");

request = api.cards().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card request = new Card();
request.TokenId = "tokgslwpdcrkhlgxqi9a";
request.DeviceSessionId = "8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o";

request = api.CardService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var cardRequest = {
  'token_id' : 'tokgslwpdcrkhlgxqi9a',
  'device_session_id' : '8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o'
}

openpay.customers.cards.create('a9pvykxz4g5rg0fplze0', cardRequest, function(error, card)  {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)
request_hash={
     "token_id" => "tokgslwpdcrkhlgxqi9a",
     "device_session_id" => "8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o"
   }

response_hash=@cards.create(request_hash.to_hash, "asynwirguzkgq2bizogo")
```


> Response example

```json
{
   "type":"credit",
   "brand":"visa",
   "id":"kso4st83wxaibffyt6su",
   "card_number":"4242",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"15",
   "expiration_month":"12",
   "allows_charges":true,
   "allows_payouts":false,
   "creation_date":"2014-02-12T10:57:09-06:00",
   "bank_name":"BANCOMER",
   "bank_code":"012",
   "customer_id":"a2b79p8xmzeyvmolqfja"
}
```

Creates a card from a token obtained from the browser or from the customer’s device. This way prevents the sensitive card information passes through your servers.

###Request
Property | Description
--------- | ------
token_id| ***string*** (required, length = 45) <br/> Token identifier generated in the the browser or in the customer’s device.
device_session_id| ***string*** (required, length = 255) <br/> Identifier of the device generated by the antifraud tool.

###Response
Returns a [card object](#card-object)

##Get a card

> Definition

```shell
Merchant
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/cards/{CARD_ID}

Customer
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}
```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->get(cardId);

//Merchant
$card = $openpay->cards->get(cardId);
?>
```

```java
//Customer
openpayAPI.cards().get(String customerId, String cardId);

//Merchant
openpayAPI.cards().get(String cardId);
```

```csharp
//Customer
openpayAPI.CardService.Get(string customer_id, string card_id);

//Merchant
openpayAPI.CardService.Get(string card_id);
```

```javascript
// Merchant
openpay.cards.get(cardId, callback);

// Customer
openpay.customers.cards.get(customerId, cardId, callback);
```

```ruby
#Customer
@cards=@openpay.create(:cards)
@cards.get(card_id, customer_id)

#Merchant
@cards=@openpay.create(:cards)
@cards.get(card_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards/ktrpvymgatocelsciak7 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" 
``` 

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$card = $customer->cards->get('k9pn8qtsvr7k7gxoq1r5');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card card = api.cards().get("a9pvykxz4g5rg0fplze0", "ktrpvymgatocelsciak7");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card card = api.CardService.Get("a9pvykxz4g5rg0fplze0", "ktrpvymgatocelsciak7");
```

```javascript
openpay.customers.cards.get('a9pvykxz4g5rg0fplze0', 'ktrpvymgatocelsciak7', function(error, card){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)

response_hash=@cards.get("ktrpvymgatocelsciak7", "asynwirguzkgq2bizogo")
```

> Response example

```json
{
   "id":"ktrpvymgatocelsciak7",
   "type":"debit",
   "brand":"visa",
   "card_number":"411111XXXXXX1111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "allows_charges":true,
   "allows_payouts":true,
   "creation_date":"2014-05-21T17:31:01-05:00",
   "bank_name":"Banamex",
   "customer_id":"ag4nktpdzebjiye1tlze",
   "bank_code":"002"
}
```

It obtains the details of the card by using its id.

<aside class="notice">
**Note:** It will never return sensitive data as the code and card number, only the first 6 and last 4 digits will be displayed.
</aside>

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Card unique identifier.

###Response
Returns a [card object](#card-object)


##Card points
> Definition

```shell
Merchant
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/cards/{CARD_ID}/points

Customer
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}/points

Token
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/tokens/{TOKEN_ID}/points

```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$pointsBalance = $customer->cards->get(cardId)->get("points");

//Merchant
$pointsBalance = $openpay->cards->get(cardId)->get("points");

//Token
$pointsBalance = $openpay->get("tokens")->get(tokenId)->get("points");
?>
```

```java
//Customer
openpayAPI.cards().points(String customerId, String cardId);

//Merchant
openpayAPI.cards().points(String cardId);
```

```csharp
//Customer
openpayAPI.CardService.Points(string customer_id, string cardId);

//Merchant
openpayAPI.CardService.Points(string cardId);
```

```javascript
// Merchant
openpay.cards.getPoints(cardId, callback);

// Customer
openpay.cards.getPoints(customerId, cardId, callback);
```

```ruby
// Merchant
@cards=@openpay.create(:cards)
@cards.getPoints(card_id)

// Customer
@cards=@openpay.create(:cards)
@cards.getPoints(card_id, customer_id)
```

> Customer request example

```shell
curl -g "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards/ktrpvymgatocelsciak7/points" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
``` 

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');
$cardId =  'tfghdfghtertdfbsd';
$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$pointsBalance = $customer->cards->get(cardId)->get("points");
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128",
"maonhzpqm8xp2ydssovf");
PointsBalance points = api.cards().points("a9pvykxz4g5rg0fplze0", "knasugabhdgq456wr");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
PointsBalance points = api.CardService.Points("a9pvykxz4g5rg0fplze0", "knasugabhdgq456wr");
```

```javascript
openpay.customers.cards.getPoints('ag4nktpdzebjiye1tlze', 'tnasugabhdgq456wr', function(error, list){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)

response_hash=@cards.getPoints("asynwirguzkgq2bizogo","tnasugabhdgq456wr")
```

> Response example

```json
[
   {
      "points_type": "santander",
      "remaining_points":"300",
      "remaining_mxn":"22.5"
   }
]
```

Returns the card point balance. Is applicable only for Santander, Scotiabank and Bancomer points.

###Request

You can get the card points of a merchant or customer using the card id.

Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Unique identifier card

Also you can get the card points of a merchant using the token.

Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Identifier token


###Response

Property | Description
--------- | ------
points_type|  Points type accepted by the card (Santander, Scotiabank or Bancomer)
remaining_points| Number of remaining points
remaining_mxn| Balance remaining points in pesos

<aside class="notice">
**Note:** If you try to get the points of a card that no allow points you will get the error code [2008](#errors)
</aside>

##Delete a card

> Definition

```shell
Merchant
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/cards/{CARD_ID}

Customer
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}
```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->get(cardId);
$card->delete();

//Merchant
$card = $openpay->cards->get(cardId);
$card->delete();
?>
```

```java
//Customer
openpayAPI.cards().delete(String customerId, String cardId);

//Merchant
openpayAPI.cards().delete(String cardId);
```

```csharp
//Customer
openpayAPI.CardService.Delete(string customer_id, string card_id);

//Merchant
openpayAPI.CardService.Delete(string card_id);
```

```javascript
// Merchant
openpay.cards.delete(cardId, callback);

// Customer
openpay.customers.cards.delete(customerId, cardId, callback);
```

```ruby
#Customer
@cards=@openpay.create(:cards)
@cards.delete(card_id, customer_id)

#Merchant
@cards=@openpay.create(:cards)
@cards.delete(card_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards/ktrpvymgatocelsciak7 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -X DELETE
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$card = $customer->cards->get('k9pn8qtsvr7k7gxoq1r5');
$card->delete();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.cards().delete("a9pvykxz4g5rg0fplze0", "ktrpvymgatocelsciak7");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.CardService.Delete("a9pvykxz4g5rg0fplze0", "ktrpvymgatocelsciak7");
```

```javascript
openpay.customers.cards.delete('a9pvykxz4g5rg0fplze0', 'ktrpvymgatocelsciak7', function(error) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)

response_hash=@cards.delete("ktrpvymgatocelsciak7", "asynwirguzkgq2bizogo")
```


Deletes a card of the customer or Merchant. After deleting it won’t be possible to make movements with that card, however, all records of the transactions you have made will be kept and will be available on the dashboard.

To remove it is only necessary to provide the card identifier.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Card unique identifier.

###Response
If the card is removed correctly the answer is empty, if it can not be deleted a [error object] (#error-object) indicating the reason is returned. 


##List of cards
> Definition

```shell
Merchant
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers

Customer
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$cardList = $customer->cards->getList(findDataRequest);

//Merchant
$cardList = $openpay->cards->getList(findDataRequest);
?>
```

```java
//Customer
openpayAPI.cards().list(String customerId, SearchParams request);

//Merchant
openpayAPI.cards().list(SearchParams request);
```

```csharp
//Customer
openpayAPI.CardService.List(string customer_id, SearchParams request = null);

//Merchant
openpayAPI.CardService.List(SearchParams request = null);
```

```javascript
// Merchant
openpay.cards.list(callback);
openpay.cards.list(searchParams, callback);

// Customer
openpay.cards.list(customerId, callback);
openpay.cards.list(customerId, searchParams, callback);
```

```ruby
#Customer
@cards=@openpay.create(:cards)
@cards.all(customer_id)

#Merchant
@cards=@openpay.create(:cards)
@cards.all
```

> Request example

```shell
curl -g "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards?limit=2" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$findDataRequest = array(
    'creation[gte]' => '2013-01-01',
    'creation[lte]' => '2013-12-31',
    'offset' => 0,
    'limit' => 5);

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$cardList = $customer->cards->getList($findDataRequest);
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
List<Card> cards = api.cards().list("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;

List<Card> cards = api.CardService.List("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var searchParams = {
  'limit' : 2
};

openpay.customers.cards.list('ag4nktpdzebjiye1tlze', searchParams, function(error, list){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)

response_hash=@cards.all("asynwirguzkgq2bizogo")
```

> Response example

```json
[
   {
      "id":"kxq1rpdymlcpxekvjsxm",
      "card_number":"1118",
      "holder_name":"Pedro Paramo",
      "expiration_year":"15",
      "expiration_month":"12",
      "allows_charges":true,
      "allows_payouts":true,
      "creation_date":"2013-11-20T09:22:25-06:00",
      "bank_name":"BBVA BANCOMER",
      "bank_code":"012",
      "type":"debit",
      "brand":"mastercard"
   },
   {
      "id":"kgjy0jiami01kkpdoywr",
      "card_number":"1111",
      "holder_name":"Pedro Paramo",
      "expiration_year":"15",
      "expiration_month":"12",
      "allows_charges":true,
      "allows_payouts":true,
      "creation_date":"2013-11-19T13:26:12-06:00",
      "bank_name":"BBVA BANCOMER",
      "bank_code":"012",
      "type":"debit",
      "brand":"mastercard"
   }
]
```

Returns a list of registered Merchant or customer cards, if you want to narrow the result you can use filters.

### Request
You can search using the following parameters as filters.

Property | Description
--------- | ------
creation| ***date*** <br/>Same as creation date. Format yyyy-mm-dd
creation[gte]| ***date*** <br/>After the creation date. Format yyyy-mm-dd
creation[lte]| ***date*** <br/>Before the creation date. Format yyyy-mm-dd
offset| ***numeric*** <br/>Number of records to skip at the beginning, default 0.
limit| ***numeric*** <br/>Number of required records, default 10.

###Response
List of [card objects] (#card-object) registered according to the parameters provided, sorted by creation date in descending order.

#Bank Accounts

You can store multiple bank accounts by Merchant or customer for withdraw funds later.

##Bank account object

> Object example 

```json
{
   "id":"brppwl9nwmruogk2do0j",
   "clabe":"032180000118359719",
   "bank_code":"032",
   "bank_name":"IXE",
   "alias":null,
   "holder_name":"Juan Hernández Sánchez",
   "creation_date":"2013-11-14T12:29:18-06shell00"
}
```


Property | Description
--------- | ------
id | ***string*** <br/>ID of the bank account.
holder_name | ***string*** <br/>Holder's full name.
alias | ***string*** <br/>Name by which the bank account is identified.
clabe | ***string*** <br/>CLABE number assigned to the account.
bank_name | ***string*** <br/>Abbreviated name of the bank where the account resides, based on the following catalog of [Bank codes](http://es.wikipedia.org/wiki/CLABE#C.C3.B3digo_de_Banco).
bank_code | ***string*** <br/> Bank code where the account resides, based on the following catalog [Bank Codes](http://es.wikipedia.org/wiki/CLABE#C.C3.B3digo_de_Banco).
creation_date | ***datetime*** <br/>Date and time when the bank account was created in ISO 8601 format.


##Create a bank account
 
> Definition

```shell
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/bankaccounts
```

```php
<?
$customer = $openpay->customers->get(customerId);
$bankaccount = $customer->bankaccounts->add(bankDataRequest);
?>
```

```java
//Customer
openpayAPI.bankAccounts().create(String customerId, BankAccount request);
```

```csharp
//Customer
openpayAPI.BankAccountService.Create(string customer_id, BankAccount request);
```

```javascript
openpay.customers.bankaccounts.create(customerId, bankaccountRequest, callback);
```

```ruby
#Customer
@bank_accounts=@openpay.create(:bankaccounts)
@bank_accounts.create(request_hash, customer_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/bankaccounts \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "clabe":"032180000118359719",
   "alias":"Cuenta principal",
   "holder_name":"Juan Hernández Sánchez"
}'
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$bankDataRequest = array(
    'clabe' => '072910007380090615',
    'alias' => 'Cuenta principal',
    'holder_name' => 'Teofilo Velazco');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$bankaccount = $customer->bankaccounts->add($bankDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
BankAccount request = new BankAccount();
request.holderName("Juan Hernández Sánchez");
request.alias("Cuenta principal");
request.clabe("032XXXXXXXXXX59719");

request = api.bankAccounts().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
BankAccount request = new BankAccount();
request.HolderName = "Juan Hernández Sánchez";
request.Alias = "Cuenta principal";
request.CLABE = "032XXXXXXXXXX59719";

request = api.BankAccountService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var bankaccountRequest = {
  'clabe' : '032180000118359719',
  'alias' : 'Cuenta principal',
  'holder_name' : 'Juan Hernández Sánchez'
};

openpay.customers.bankaccounts.create('a9pvykxz4g5rg0fplze0', bankaccountRequest, function(error, bankaccount) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@bank_accounts=@openpay.create(:bankaccounts)
request_hash={
     "holder_name" => "Juan Hernández Sánchez",
     "alias" => "Cuenta principal",
     "clabe" => "032XXXXXXXXXX59719"
   }

response_hash=@bank_accounts.create(request_hash.to_hash, "asynwirguzkgq2bizogo")
```

> Response example

```json
{
   "id":"buyj4apkwilpp2jfxr9r",
   "clabe":"032XXXXXXXXXX59719",
   "bank_code":"032",
   "bank_name":"IXE",
   "alias":"Cuenta principal",
   "holder_name":"Juan Hernández Sánchez",
   "creation_date":"2014-05-22T11:02:10-05:00"
}
```

Creates and assigns a bank account to a specific customer.

###Request


Property | Description
--------- | ------
holder_name | ***string*** (required, length  = 80) <br/>Holder's full name.
alias | ***string*** (optional, length = 45)<br/>Name by which the bank account is identified.
clabe | ***string*** (required, length  = 45) <br/>CLABE number assigned to the account.

###Response
Returns a [bank account object](#bank-account-object) or an error when a there is a problem.

##Get a bank account

> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/bankaccounts/{BANK_ACCOUNT_ID}
```

```php
<?
$customer = $openpay->customers->get(customerId);
$bankaccount = $customer->bankaccounts->get(bankAccountId);
?>
```

```java
//Customer
openpayAPI.bankAccounts().get(String customerId, String bankAccountId);
```

```csharp
//Customer
openpayAPI.BankAccountService.Get(string customer_id, string bank_account_id);
```

```javascript
openpay.customers.bankaccounts.get(customerId, bankaccountId, callback);
```

```ruby
#Customer 
@bank_accounts=@openpay.create(:bankaccounts)
@bank_accounts.get(customer_id, bankaccount_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/bankaccounts/buyj4apkwilpp2jfxr9r \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
``` 

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$bankaccount = $customer->bankaccounts->get('b4vcouaavwuvkpufh0so');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
BankAccount bankAccount = api.bankAccounts().get("a9pvykxz4g5rg0fplze0", "buyj4apkwilpp2jfxr9r");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
BankAccount bankAccount = api.BankAccountService.Get("a9pvykxz4g5rg0fplze0", "buyj4apkwilpp2jfxr9r");
```

```javascript
openpay.customers.bankaccounts.get('a9pvykxz4g5rg0fplze0', 'buyj4apkwilpp2jfxr9r', function(error, bankaccount){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@bank_accounts=@openpay.create(:bankaccounts)

response_hash=@bank_accounts.get("asynwirguzkgq2bizogo", "buyj4apkwilpp2jfxr9r")
```

> Response example

```json
{
   "id":"buyj4apkwilpp2jfxr9r",
   "clabe":"032XXXXXXXXXX59719",
   "bank_code":"032",
   "bank_name":"IXE",
   "alias":"Cuenta principal",
   "holder_name":"Juan Hernández Sánchez",
   "creation_date":"2014-05-22T11:02:10-05:00"
}
```

It obtains the details of the bank account assigned to a customer.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Unique identifier of the bank account.

###Response
Returns a [bank account object](#bank-account-object)

##Delete a bank account

> Definition

```shell
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/bankaccounts/{BANK_ACCOUNT_ID}
```

```php
<?
$customer = $openpay->customers->get(customerId);
$bankaccount = $customer->bankaccounts->get(bankAccountId);
$bankaccount->delete();
?>
```

```java
//Customer
openpayAPI.bankAccounts().delete(String customerId, String bankAccountId);
```

```csharp
//Customer
openpayAPI.BankAccountService.Delete(string customer_id, string bank_account_id);
```

```javascript
openpay.customers.bankaccounts.delete(customerId,bankaccountId, callback);
```

```ruby
#Customer
@bank_accounts=@openpay.create(:bankaccounts)
@bank_accounts.delete(customer_id, bankaccount_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/bankaccounts/buyj4apkwilpp2jfxr9r \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -X DELETE
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$bankaccount = $customer->bankaccounts->get('b4vcouaavwuvkpufh0so');
$bankaccount->delete();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.bankAccounts().delete("a9pvykxz4g5rg0fplze0", "buyj4apkwilpp2jfxr9r");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.BankAccountService.Delete("a9pvykxz4g5rg0fplze0", "buyj4apkwilpp2jfxr9r");
```

```javascript
openpay.customers.bankaccounts.delete('a9pvykxz4g5rg0fplze0','buyj4apkwilpp2jfxr9r', function(error){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@bank_accounts=@openpay.create(:bankaccounts)

response_hash=@bank_accounts.delete("asynwirguzkgq2bizogo", "buyj4apkwilpp2jfxr9r")
```

Deletes the bank account associated with the customer. The transactions that are associated with this account are unchanged and will continue for you to consult them.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length  = 45) <br/> Unique identifier of the bank account.

###Response
If the bank account is removed correctly the answer is empty, if it can not be deleted a [error object](#error-object) indicating the reason is returned.

##List of bank accounts
> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/bankaccounts
```

```php
<?
$customer = $openpay->customers->get(customerId);
$bankaccountList = $customer->bankaccounts->getList(findDataRequest);
?>
```

```java
//Customer
openpayAPI.bankAccounts().list(String customerId, SearchParams request);
```

```csharp
//Customer
openpayAPI.BankAccountService.List(string customer_id, SearchParams request = null);
```

```javascript
openpay.customers.bankaccounts.list(customerId, callback);
openpay.customers.bankaccounts.list(customerId, searchParams, callback);
```

```ruby
#Customer
@bank_accounts=@openpay.create(:bankaccounts)
@bank_accounts.all(customer_id)
```

> Request example

```shell
curl -g "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/bankaccounts?limit=2" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$findDataRequest = array(
    'creation[gte]' => '2013-01-01',
    'creation[lte]' => '2013-12-31',
    'offset' => 0,
    'limit' => 5);

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$bankaccountList = $customer->bankaccounts->getList($findDataRequest);
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
        
List<BankAccount> bankAccounts = api.bankAccounts().list("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;

List<BankAccount> banckAccounts = api.BankAccountService.List("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var searchParams = {
  'limit' : 2
};

openpay.customers.bankaccounts.list('ag4nktpdzebjiye1tlze', searchParams, function(error, list){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@bank_accounts=@openpay.create(:bankaccounts)

response_hash=@bank_accounts.all("asynwirguzkgq2bizogo")
```

> Response Example

```json
[{
   "id":"brppwl9nwmruogk2do0j",
   "clabe":"032180000118359719",
   "bank_code":"032",
   "bank_name":"IXE",
   "alias":null,
   "holder_name":"Juan Hernández Sánchez",
   "creation_date":"2013-11-14T12:29:18-06:00"
},
{
   "id":"bb0zt72rxoyiwz9jzzai",
   "clabe":"012680012426485980",
   "bank_code":"012",
   "bank_name":"BANCOMER",
   "alias":null,
   "holder_name":"Juan Hernández Sánchez",
   "creation_date":"2013-11-14T18:07:45-06:00"
}]
```
Returns the details of all the bank accounts of the customer specified on the request.


###Request
You can search using the following parameters as filters.

Property | Description
--------- | ------
creation| ***date*** <br/>Same as creation date. Format yyyy-mm-dd
creation[gte]| ***date*** <br/>After the creation date. Format yyyy-mm-dd
creation[lte]| ***date*** <br/>Before the creation date. Format yyyy-mm-dd
offset| ***numeric*** <br/>Number of records to skip at the beginning, default 0.
limit| ***numeric*** <br/>Number of required records, default 10.

###Response
List of [bank account objects](#bank-account-object) registered according to the given parameters, sorted by creation date in descending order. 

#Plans

Plans are an Openpay resource that allows create templates for subscriptions.  Using plans you can define the amount and frequency of recurrent charges.


##Plan Object

> Object example

```json
{
    "name": "Curso de ingles",
    "status": "active",
    "amount": 150,
    "currency": "MXN",
    "id": "patpflacwilazguj6bem",
    "creation_date": "2013-12-13T09:43:52-06:00",
    "repeat_every": 1,
    "repeat_unit": "month",
    "retry_times": 2,
    "status_after_retry": "cancelled",
    "trial_days": 30
}
```

Property | Description
--------- | ------
id | ***string*** <br/> Unique plan identifier.
creation_date | ***datetime*** <br/> Date and time in which the plan was created in ISO 8601 format.
name  | ***string*** <br/> Plan name.
amount | ***numeric*** <br/> Amount that will be applied once the subscription is charged.  It has to be more than zero and it can have up to two decimal places.
currency | ***string*** <br/> Currency used in the operation, by default is MXN (Mexican pesos).
repeat_every | ***numeric*** <br/>  Time units in which the subscription will be charged.  For example, repeat_unit=month and repeat_every=2 indicates that it will be charged every 2 months.
repeat_unit | ***string*** <br/> Describes the charge unit frequency.  It can be weekly(week), monthly(month) or yearly (year).
retry_times | ***numeric*** <br/> Number of attempts to try to charge the subscription.  When the attempts have been exhausted, the status field is determined by the field *status_after_retry*.
status | ***string*** <br/> Plan status can be *active* or *deleted*.  If the plan is in *deleted* state it doesn't allow to register new subscriptions under this plan but existing subscriptions will be charged.
status_after_retry | ***string*** <br/> This field indicates the status in which the subscription will be set once all the charge attempts have been exhausted.  It can be *unpaid* or *cancelled*.
trial_days | ***numeric*** <br/> Number of trial days this subscription will have by default.

##Create a new Plan
 
> Definition

```shell
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/plans
```

```php
<?
$plan = $openpay->plans->add(planDataRequest);
?>
```

```java
openpayAPI.plans().create(Plan request);
```

```csharp
openpayAPI.PlanService.Create(Plan plan);
```

```javascript
openpay.plans.create(planRequest, callback);
```

```ruby
#Customere
@plans=@openpay.create(:plans)
@plans.create(request_hash)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/plans \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
  "amount": 150.00,
  "status_after_retry": "cancelled",
  "retry_times": 2,
  "name": "Curso de ingles",
  "repeat_unit": "month",
  "trial_days": "30",
  "repeat_every": "1"
}' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$planDataRequest = array(
    'amount' => 150.00,
    'status_after_retry' => 'cancelled',
    'retry_times' => 2,
    'name' => 'Plan Curso Verano',
    'repeat_unit' => 'month',
    'trial_days' => '30',
    'repeat_every' => '1',
    'currency' => 'MXN');

$plan = $openpay->plans->add($planDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Plan request = new Plan();
request.name("Curso de ingles");
request.amount(new BigDecimal("100.00"));
request.repeatEvery(1, PlanRepeatUnit.WEEK);
request.retryTimes(3);
request.statusAfterRetry(PlanStatusAfterRetry.UNPAID);
request.trialDays(30);

request = api.plans().create(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Plan request = new Plan();
request.Name = "Curso de ingles";
request.Amount = new Decimal(100.00);
request.RepeatEvery = 1;
request.RepeatUnit = "week";
request.RetryTimes = 2;
request.StatusAfterRetry = "unpaid";
request.TrialDays = 30;

request = api.PlanService.Create(request);
```

```javascript
var planRequest = {
  'amount': 150.00,
  'status_after_retry': 'cancelled',
  'retry_times': 2,
  'name': 'Curso de ingles',
  'repeat_unit': 'month',
  'trial_days': '30',
  'repeat_every': '1'
};

openpay.plans.create(planRequest, function(error, plan){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@plans=@openpay.create(:plans)
request_hash={
     "name" => "Curso de ingles",
     "amount" => 150.00,
     "repeat_every" => "1",
     "repeat_unit" => "month",
     "retry_times" => 2,
     "status_after_retry" => "cancelled",
     "trial_days" => "30"
   }

response_hash=@plans.create(request_hash.to_hash)
```

> Response example

```json
{
   "id":"p8e6x3hafqqsbmnoevrt",
   "name":"Curso de ingles",
   "status":"active",
   "amount":150.00,
   "currency":"MXN",
   "creation_date":"2014-05-22T12:29:31-05:00",
   "repeat_every":1,
   "repeat_unit":"month",
   "retry_times":2,
   "status_after_retry":"cancelled",
   "trial_days":30
}
```

Creates a new plan for allowing customers to subscribe.

###Request


Property | Description
--------- | ------
name | ***string*** (required, length = 255) <br/>Plan's name.
amount | ***numeric*** (required) <br/> Amount that will be charged at subscription.  It needs to be more than zero and can have up to two decimal places.
repeat_every | ***numeric*** (required) <br/>Time units in which the subscription will be charged.  For example, repeat_unit=month and repeat_every=2 indicates that it will be charged every 2 months.
repeat_unit | ***numeric*** (required) <br/>Describes the charge unit frequency.  It can be weekly(week), monthly(month) or yearly (year).
retry_times | ***numeric*** (optional) <br/> Number of attempts to try to charge the subscription.  When the attempts have been exhausted, the status field is determined by the field *status_after_retry*.
status_after_retry | ***string*** (required, values = "UNPAID/CANCELLED") <br/>This field indicates the status in which the subscription will be set once all the charge attempts have been exhausted.  It can be *unpaid* or *cancelled*.
trial_days | ***numeric*** (required) <br/> Number of trial days this subscription will have by default.
 

###Response
Returns the created [plan object](#plan-object) or an error in case an issue occurred.


##Update existing plans.

> Definition

```shell
PUT https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/plans/{PLAN_ID}
```

```php
<?
$plan = $openpay->plans->get(planId);
$plan->save();
?>
```

```java
openpayAPI.plans().update(Plan request);
```

```csharp
openpayAPI.PlanService.Update(Plan plan);
```

```javascript
openpay.plans.update(planId, planRequest, callback);
```

```ruby
#Customer
@plans=@openpay.create(:plans)
@plans.update(request_hash, plan_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/plans/p8e6x3hafqqsbmnoevrt \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X PUT -d '{
      "name": "Curso de aleman",
      "trial_days": "60"
   }' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$plan = $openpay->plans->get('pduar9iitv4enjftuwyl');
$plan->name = 'Plan Curso de Verano 2014';
$plan->save();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Plan request = new Plan();
request.setId("p8e6x3hafqqsbmnoevrt");
request.name("Curso de ingles");
request.trialDays(30);

request = api.plans().update(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Plan request = new Plan();
request.Id = "p8e6x3hafqqsbmnoevrt";
request.Name = "Curso de ingles";
request.TrialDays = 30;

request = api.PlanService.Update(request);
```

```javascript
var planRequest = {
  'name': 'Curso de aleman',
  'trial_days': 60
};

openpay.plans.update(planId, planRequest, function(error, plan){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@plans=@openpay.create(:plans)
request_hash={
     "name" => "Curso de ingles",
     "trial_days" => "30"
   }

response_hash=@plans.update(request_hash.to_hash, "p8e6x3hafqqsbmnoevrt")
```

> Response example

```json
{
   "id":"p8e6x3hafqqsbmnoevrt",
   "name":"Curso de aleman",
   "status":"active",
   "amount":150.00,
   "currency":"MXN",
   "creation_date":"2014-05-22T12:29:31-05:00",
   "repeat_every":1,
   "repeat_unit":"month",
   "retry_times":2,
   "status_after_retry":"cancelled",
   "trial_days":60
}
```
 
Updates the plan information.  It requires a plan id and only certain fields can be updated.

###Request
Property | Description
--------- | ------
name | ***string*** (optional, length = 80) <br/>Plan's name.
trial_days | ***numeric*** (optional) <br/> Number of trial days this subscription will have by default.


###Response
Returns a [plan object](#plan-object) with the updated information or an [error response](#error-object) if a problem occurred with the update.

##Get a plan

> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/plans/{PLAN_ID}
```

```php
<?
$plan = $openpay->plans->get(planId);
?>
```

```java
openpayAPI.plans().get(String planId);
```

```csharp
openpayAPI.PlanService.Get(string plan_id);
```

```javascript
openpay.plans.get(planId, callback);
```

```ruby
#Customer
@plans=@openpay.create(:plans)
@plans.get(plan_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/plans/p8e6x3hafqqsbmnoevrt \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
``` 

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$plan = $openpay->plans->get('pduar9iitv4enjftuwyl');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Plan plan = api.plans().get("p8e6x3hafqqsbmnoevrt");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Plan plan = api.PlanService.Get("p8e6x3hafqqsbmnoevrt");
```

```javascript
openpay.plans.get('p8e6x3hafqqsbmnoevrt', function(error, plan){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@plans=@openpay.create(:plans)

response_hash=@plans.get("p8e6x3hafqqsbmnoevrt")
```

> Response example

```json
{
   "id":"p8e6x3hafqqsbmnoevrt",
   "name":"Curso de aleman",
   "status":"active",
   "amount":150.00,
   "currency":"MXN",
   "creation_date":"2014-05-22T12:29:31-05:00",
   "repeat_every":1,
   "repeat_unit":"month",
   "retry_times":2,
   "status_after_retry":"cancelled",
   "trial_days":60
}
```

It gets the plan details.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Plan identifier.

###Response
Returns a [plan object](#plan-object)

##Delete a plan

> Definition

```shell
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/plans/{PLAN_ID}
```

```php
<?
$customer = $openpay->customers->get(customerId);
$plan = $openpay->plans->get(planId);
$plan->delete();
?>
```

```java
openpayAPI.plans().delete(String planId);
```

```csharp
openpayAPI.PlanService.Delete(string plan_id);
```

```javascript
openpay.plans.delete(planId, callback);
```

```ruby
#Customer
@plans=@openpay.create(:plans)
@plans.delete(plan_id)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/plans/p8e6x3hafqqsbmnoevrt \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -X DELETE
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$plan = $openpay->plans->get('pduar9iitv4enjftuwyl');
$plan->delete();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.plans().delete("p8e6x3hafqqsbmnoevrt");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.PlanService.Delete("p8e6x3hafqqsbmnoevrt");
```

```javascript
openpay.plans.delete('p8e6x3hafqqsbmnoevrt', function(error){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@plans=@openpay.create(:plans)

response_hash=@plans.delete("p8e6x3hafqqsbmnoevrt")
```

When a plan is deleted it won't allow to create more subscriptions associated with it, however the subscriptions already associated will continue to be charged.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Identifier of the plan that will be deleted.

###Response
If the plan is deleted correctly the response will be empty, if it cannot be deleted an [error object](#error-object) will be returned indicating the reason.


##Plan list
> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/plans
```

```php
<?
$planList = $openpay->plans->getList(findDataRequest);
?>
```

```java
openpayAPI.plans().list(SearchParams request);
```

```csharp
openpayAPI.PlanService.List(SearchParams request = null);
```

```javascript
openpay.plans.list(callback);
openpay.plans.list(searchParams, callback);
```

```ruby
#Customer
@plans=@openpay.create(:plans)
@plans.all
```

> Request example

```shell
curl -g "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/plans?limit=10" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$findDataRequest = array(
    'creation[gte]' => '2013-01-01',
    'creation[lte]' => '2013-12-31',
    'offset' => 0,
    'limit' => 5);

$planList = $openpay->plans->getList($findDataRequest);
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

List<Plan> plans = api.plans().list(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;

List<Plan> plans = api.PlanService.List(request);
```

```javascript
var searchParams = {
  'limit' : 10
};

openpay.plans.list(searchParams, function(error, list){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@plans=@openpay.create(:plans)

response_hash=@plans.all
```

> Response example

```json
[
    {
        "name": "Curso de aleman",
        "status": "active",
        "amount": 150,
        "currency": "MXN",
        "id": "patpflacwilazguj6bem",
        "creation_date": "2013-12-13T09:43:52-06:00",
        "repeat_every": 1,
        "repeat_unit": "month",
        "retry_times": 2,
        "status_after_retry": "cancelled",
        "trial_days": 60
    },
    {
        "name": "Curso de ingles",
        "status": "active",
        "amount": 150,
        "currency": "MXN",
        "id": "pjl7wfryrrd1tznr0fnl",
        "creation_date": "2013-12-13T11:36:40-06:00",
        "repeat_every": 1,
        "repeat_unit": "month",
        "retry_times": 2,
        "status_after_retry": "cancelled",
        "trial_days": 30
    }
]
```
Returns the details of all active plans.

###Request
You can search using the following parameters:

Property  | Description
--------- | ------
creation| ***date*** <br/> Same as creation date.  Format yyyy-mm-dd.
creation[gte]| ***date*** <br/>After creation date. Format: yyyy-mm-dd.
creation[lte]| ***date*** <br/>Before the creation date. Format: yyyy-mm-dd.
offset| ***numeric*** <br/>Number of records to skip from the beggining, by default is 0.
limit| ***numeric*** <br/>Number of records to return, by default is 10.

###Response
A list of [plan objects](#plan-object) registered according to the given parameters, sort by creation date in descending order.

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
      "cvv2":"110"
   },
   "plan_id":"pbi4kb8hpb64x0uud2eb"
}' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$subscriptionDataRequest = array(
    "trial_end_date" => "2014-01-01", 
    'plan_id' => 'pduar9iitv4enjftuwyl',
    'card_id' => 'konvkvcd5ih8ta65umie');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$subscription = $customer->subscriptions->add($subscriptionDataRequest);
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

request = api.subscriptions().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Subscription request = new Subscription();
request.PlanId = "idPlan-01001";
request.TrialEndDate = new Datetime(2014, 5, 1);;
request.CardId = "ktrpvymgatocelsciak7";

request = api.SubscriptionService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var subscriptionRequest = {
   'card':{
      'card_number':'4111111111111111',
      'holder_name':'Juan Perez Ramirez',
      'expiration_year':'20',
      'expiration_month':'12',
      'cvv2':'110'
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
request_hash={
     "plan_id" => "pbi4kb8hpb64x0uud2eb",
     "trial_end_date" => "2014-06-20",
     "source_id" => "ktrpvymgatocelsciak7"
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
 
Create a new subscription for an existing customer.  You can use an existing card or you can send the info of the card where the charges will be made.


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
PUT https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions
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


#Fees
If the customer accounts were created to handle their own balance, a fee can be charged which will be shown in the Merchant account.

<aside class="notice">
In order to have customer accounts where they handle their balance they should have been created with the property ***requires_account=true***.  See [customer creation](#create-a-new-customer).
</aside>

##Charging a Fee
> Definition

```shell
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/fees
```

```php
<?
$fee = $openpay->fees->create(feeDataRequest);
?>
```

```java
openpayAPI.fees().create(CreateFeeParams request);
```

```csharp
openpayAPI.FeeService.Create(FeeRequest request);
```

```javascript
openpay.fees.create(feeRequest, callback);
```

```ruby
#Customer
@fees=@openpay.create(:fees)
@fees.create(request_hash)
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/fees \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{                                            
     "customer_id" : "dvocf97jd20es3tw5laz",
     "amount" : 12.50,          
     "description" : "Cobro de ComisiÃ³n",
     "order_id" : "oid-1245"
}' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$feeDataRequest = array(
    'customer_id' => 'a9ualumwnrcxkl42l6mh',
    'amount' => 12.50,
    'description' => 'Cobro de ComisiÃ³n',
    'order_id' => 'ORDEN-00063');

$fee = $openpay->fees->create($feeDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateFeeParams request = new CreateFeeParams();
request.customerId("a9pvykxz4g5rg0fplze0");
request.amount(new BigDecimal("100.00"));
request.description("Cobro de comisiÃ³n");
request.orderId("oid-1245");

Fee fee = api.fees().create(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
FeeRequest request = new FeeRequest();
request.CustomerId = "a9pvykxz4g5rg0fplze0";
request.Amount = new Decimal(100.00);
request.Description = "Cobro de comisiÃ³n";
request.OrderId = "oid-1245;

Fee fee = api.FeeService.Create(request);
```

```javascript
var feeRequest = {                                            
     'customer_id' : 'dvocf97jd20es3tw5laz',
     'amount' : 12.50,          
     'description' : 'Cobro de ComisiÃ³n',
     'order_id' : 'oid-1245'
};

openpay.fees.create(feeRequest, function(error, fee){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@fees=@openpay.create(:fees)
request_hash={
     "customer_id" => "dvocf97jd20es3tw5laz",
     "amount" => 12.50,
     "description" => "Cobro de ComisiÃ³n",
     "order_id" => "oid-1245"
   }

response_hash=@fees.create(request_hash.to_hash)
```

> Response example

```json
{
   "amount":12.50,
   "authorization":null,
   "method":"customer",
   "operation_type":"out",
   "currency":"MXN",
   "transaction_type":"fee",
   "status":"completed",
   "id":"th8tafyrkakdbyry3kxi",
   "creation_date":"2013-11-18T10:33:03-06:00",
   "description":"Cobro de comisiÃ³n",
   "error_message":null,
   "order_id":"oid-1245",
   "customer_id":"dvocf97jd20es3tw5laz"
}
```

Charge a fee to the customer account.

###Request

Property | Description
--------- | ------
customer_id | ***string*** (required, length = 45) <br/>The unique identifier of the customer that you want to charge the fee.
amount | ***numeric*** (required) <br/>Charge amount.  It needs to be more than zero, it can have up to two decimal places.
description | ***string*** (required, length = 250) <br/> A description associated with the fee charge.
order_id | ***string*** (optional, length = 100) <br/>Unique fee identifier.  It has to be unique among all the transactions. 

 
###Response
The [transaction object](#transaction-object) of the fee including the creation date and id or an [error response](#error-object).


##Refund Fee
> Definition

```shell
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/fees/{TRANSACTION_ID}/refund
```

```php
<?
$fee = $openpay->fees->get(transactionId);
$fee->refund(refundData);
?>
```

```java
openpayAPI.fees().refund(String transactionId, RefundParams request);
```

```csharp
openpayAPI.FeeService.Refund(string transaction_id, RefundRequest request);
```

```javascript
openpay.fees.refund(transactionId, feeRequest, callback);
```

```ruby
#Cliente
@fees=@openpay.create(:fees)
@fees.refund(transaction_id, refund_hash)
```

> Request example 

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/fees/trzjaozcik8msyqshka4/refund \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{                                            
     "description" : "Fee Refund"
}' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$refundData = array(
    'description' => 'Fee Refund'
    );

$fee = $openpay->fees->get("trzjaozcik8msyqshka4");
$fee->refund($refundData);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
RefundParams request = new RefundParams();
request.description("Fee Refund");

Fee fee = api.fees().refund("trzjaozcik8msyqshka4", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
RefundRequest request = new RefundRequest();
request.Description = "Fee Refund";

Fee fee = api.FeeService.Refund("trzjaozcik8msyqshka4", request);
```

```javascript
var refundRequest = {                                            
     'description' : 'Fee Refund'
};

openpay.fees.refund("trzjaozcik8msyqshka4", refundRequest, function(error, refund){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@fees=@openpay.create(:fees)
refund_hash={
     "description" => "Fee Refund"
   }

response_hash=@fees.refund("mzdtln0bmtms6o3kck8f", refund_hash.to_hash)
```

> Response example

```json
{
  "id": "th8tafyrkakdbyry3kxi",
  "authorization": null,
  "method": "customer",
  "operation_type": "in",
  "transaction_type": "refund",
  "status": "completed",
  "conciliated": true,
  "creation_date": "2016-09-06T11:56:57-05:00",
  "operation_date": "2016-09-06T11:56:57-05:00",
  "description": "fee refund merchant03",
  "error_message": null,
  "order_id": null,
  "customer_id": "ar2btmquidjhykdaztp6",
  "amount": 11.11,
  "currency": "MXN"
}
```

Refund a fee to the customer account.

###Request

Property | Description
--------- | ------
description | ***string*** (optional, length = 250) <br/> A description associated with the fee charge.
 
###Response
The [transaction object](#transaction-object) of the refund including the creation date and id or an [error response](#error-object).


##Fee  list
> Definition

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/fees
```

```php
<?
$feeList = $openpay->fees->getList(findDataRequest);
?>
```

```java
openpayAPI.fees().list(SearchParams request);
```

```csharp
openpayAPI.FeeService.List(SearchParams request = null);
```

```javascript
openpay.fees.list(callback);
openpay.fees.list(searchParams, callback);
```

```ruby
#Customer
@fees=@openpay.create(:fees)
@fees.all
```

> Ejemplo de peticiÃ³n 

```shell
curl -g "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/fees?limit=10" \
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

$feeList = $openpay->fees->getList($findDataRequest);
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

List<Fee> fees = api.fees().list(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;

List<Fee> fees = api.FeeService.List(request);
```

```javascript
var searchParams = {
  'limit' : 10
};

openpay.fees.list(searchParams, function(error, list){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@fees=@openpay.create(:fees)

response_hash=@fees.all
```

> Response example

```json
[
   {
      "amount":30.00,
      "authorization":null,
      "method":"customer",
      "operation_type":"out",
      "currency":"MXN",
      "transaction_type":"fee",
      "status":"completed",
      "id":"th8tafyrkakdbyry3kxi",
      "creation_date":"2013-11-18T10:33:03-06:00",
      "description":"Cobro de comisiÃ³n",
      "error_message":null,
      "order_id":"oid-1367",
      "customer_id":"dvocf97jd20es3tw5laz"
   },
   {
      "amount":12.00,
      "authorization":null,
      "method":"customer",
      "operation_type":"out",
      "currency":"MXN",
      "transaction_type":"fee",
      "status":"completed",
      "id":"tdzottaaohuhosf4cdv9",
      "creation_date":"2013-11-17T05:35:00-06:00",
      "description":"Cobro de comisiÃ³n",
      "error_message":null,
      "order_id":"oid-1366",
      "customer_id":"afk4csrazjp1udezj1po"
   }
]
```



Returns the details of every fee charged by the Merchant.

###Request
It can be done using the following parameters:

Property     | Description
---------    | ------
creation     | ***date*** <br/>Same as creation date. Format: yyyy-mm-dd
creation[gte]| ***date*** <br/>After the creation date. Format: yyyy-mm-dd
creation[lte]| ***date*** <br/>Before the creation date. Format: yyyy-mm-dd
offset| ***numeric*** <br/>Number of records to skip from the beginning, by default is 0.
limit| ***numeric*** <br/>Number of records to return, by default is 10.

###Response
Returns an array of [transaction object](#transaction-object) for the charged fees  in descending order, each one with the identifier of the customer to whom it was made.

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
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/webhooks
```

```php
<?
$webhook = $openpay->webhooks->create(webhook);
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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/webhooks \
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

$webhook = $openpay->webhooks->create($webhook);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/webhooks/{WEBHOOK_ID}
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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/webhooks/wxvanstudf4ssme8khmc \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/webhooks/{WEBHOOK_ID}
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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/webhooks/wxvanstudf4ssme8khmc \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/webhooks
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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/webhooks \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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

#Tokens

The objective is to created tokens from the user browser or device to capture the card information so this doesn't go through your server and you can avoid or reduce the PCI certification process.

To use this API functionality we recommend using our JavaScript library for your Web application and our Android and iOS SDK for mobile apps.

**Features**

* Tokens are created at Merchant level.
* Tokens are not link to any customer.
* After a token has been created it can only be use once to make a charge.

##Token Object

> Object example 

```json
{
    "id":"tokfa4swch8gr4icy2ma",
    "card":{
       "card_number":"1111",
       "holder_name":"Juan Perez Ramirez",
       "expiration_year":"20",
       "expiration_month":"04",
       "address":{
          "line1":"Av 5 de febrero",
          "line2":"Roble 207",
          "line3":"Queretaro",
          "state":"Queretaro",
          "city":"Queretaro",
          "postal_code":"76900",
          "country_code":"MX"
       },
       "creation_date":"2014-01-30T13:53:11-06:00",
       "brand":"visa",
       "points_card":false
    }
}
```

Property | Description
--------- | ------
id | ***string*** <br/>Token identifier.  This is the ID that you should use to perform operations.
card | ***object*** <br/>Card associated with the token.  See [card object](#card-object).


##Create a new token

> Definition

```
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/tokens
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/tokens \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "card_number":"4111111111111111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "cvv2":"110",
   "address":{
      "city":"QuerÃƒÂ©taro",
      "country_code":"MX",
      "postal_code":"76900",
      "line1":"Av 5 de Febrero",
      "line2":"Roble 207",
      "line3":"col carrillo",
      "state":"Queretaro"
   }
}' 
```

> Response example

```json
{
   "id":"k1n0mscnjwhxqia8q7cm",
   "card":{
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "address":{
         "line1":"Av 5 de Febrero",
         "line2":"Roble 207",
         "line3":"col carrillo",
         "state":"Queretaro",
         "city":"QuerÃƒÂ©taro",
         "postal_code":"76900",
         "country_code":"MX"
      },
      "creation_date":null,
      "brand":"visa"
   }
}
```

To create a token using Openpay you need to send the object with the info that will be stored.  Once the token it's stored, you can't get the number and secutirty code because this information is encrypted.

###Request

Property | Description
--------- | ------
holder_name |***string*** (required) <br/>Account holder name.
card_number |***numeric*** (required) <br/>Card number between 16 to 19 digits.
cvv2 |***numeric*** (required) <br/>Security code like it appears in the back of the card.  Generally 3 digits.
expiration_month |***numeric*** (required) <br/>Expiration month, like it appears in the card.
expiration_year |***numeric*** (required) <br/>Expiration year, like it appears in the card.
address |***object*** (optional)<br/>Invoice address of the card owner.

###Response
Returs the created [token object](#token-object) or an [error response](#error-object) if an error ocurred during the creation.

##Get a Token

> Definition

```
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/tokens/{TOKEN_ID}
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/tokens/k1n0mscnjwhxqia8q7cm \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
``` 

> Response example

```json
{
   "id":"k1n0mscnjwhxqia8q7cm",
   "card":{
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "address":{
         "line1":"Av 5 de Febrero",
         "line2":"Roble 207",
         "line3":"col carrillo",
         "state":"Queretaro",
         "city":"QuerÃƒÂ©taro",
         "postal_code":"76900",
         "country_code":"MX"
      },
      "creation_date":null,
      "brand":"visa"
   }
}
```

Gets the token details.  The ID is required.

<aside class="notice">
**Note:** Sensible data like credit card number and security card will never be included in the response.
</aside>

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Token ID

###Response
Returns a [token object](#token-object)

#Merchant
The *merchant* object allows you to query info related to your account using the API,

##Merchant Object

> Object example:

```json
{ 
   "id": "m9lrykwsmljagrfb38rs", 
   "creationDate": "2013-11-13T16:58:40-06:00", 
   "name": "Promociones en linea", 
   "email": "contacto@enlinea.com.mx", 
   "phone": "(321) 222-2222", 
   "status": "active", 
   "balance": 1000, 
   "clabe": "646180109400000542" 
} 
```

Property | Description
--------- | -----------
id|***string*** <br/>Unique identifier assigned on creation.
creation_date|***datetime*** <br/>Transaction creation date in ISO 8601 format.
name|***string*** <br/>Registered merchant name.
email|***string*** <br/>Email account registered for the merchant.
phone|***string*** <br/>Phone number registered for the merchant.
status| ***string*** <br/>Merchant account status, it can be *active* or *deleted*.  If the account is in *deletate* status no transactions are allowed.
balance| ***numeric*** <br/>Balance in the account with two decimal placess.
clabe | ***numeric***   <br/>Linked CLABE account where funds can be received from any bank in Mexico using SPEI.



##Request a Merchant Object

> Definition



```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}
```


```php
<?
// =============================
// Not yet implemented.
// =============================
?>
```


```java
openpayAPI.merchant().get();

```


```csharp
// =============================
// Not yet implemented.
// =============================
```


```javascript
openpay.merchant.get(callback);
```

Ruby


```ruby
# =============================
# Not yet implemented.
# =============================
```



> Request example:

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Merchant merchant = api.merchant().get();
```

```javascript
openpay.merchant.get(function(error, merchant){
  // ...
});
```

> Response example:

```json
{
   "name":"Demo Openpay",
   "email":"demo@openpay.mx",
   "phone":"(442) 258-1039",
   "status":"active",
   "balance":218.73,
   "clabe":"646180109400135624",
   "id":"mzdtln0bmtms6o3kck8f",
   "creation_date":"2014-01-23T10:45:53-06:00"
}
```

Returns the merchant account details.  Only the unique merchant identifier is required.

###Request

Property | Description
--------- | -----------
id | ***string*** (required, longitude = 45) <br>unique merchant identifier.

###Response
If the identifier is correct it will return a merchant object.

#Stores

The object represents a convenience store

##Store object

> Object example:

```json
{
    "id_store": 4913,
    "id": 115,
    "name": "0503 SAN PABLO -QRO",
    "last_update": "2016-02-04T00:52:16-06:00",
    "status": "active",
    "geolocation": {
      "lng": -100.421865,
      "lat": 20.618171,
      "place_id": "ChIJwSN2wpNa04URsDryLW517lg"
    },
    "address": {
      "line1": "AV. 5 DE FEBRERO KM 7.5 NO 1341",
      "line2": "SAN PABLO",
      "line3": null,
      "state": "QUERETARO",
      "city": "QUERETARO",
      "postal_code": "76030",
      "country_code": "MX"
    },
    "paynet_chain": {
      "name": "EXTRA",
      "logo": "http://www.openpay.mx/logotipos/extra.png",
      "thumb": "http://www.openpay.mx/thumb/extra.png",
      "max_amount": 99999.99
    }
  }
```

Property | Description
--------- | -----------
id_store|***string*** <br/>Unique identifier assigned at the time of its creation.
id|***string*** <br/>nique identifier by chain.
name|***datetime*** <br/>Store name.
last_update|***string*** <br/>Last date of update in format ISO 8601.
[geolocation](#objeto-geolocation)| ***oject*** <br/>Store geographical representation by coordinates, latitude and longitude.
[address](#objeto-dirección)|***object*** <br/>Store address.
[paynet_chain](#objeto-paynetchain)|***object*** <br/>Paynet chain to which it belongs.

##Get list of shops by location

> Definition

```shell
GET https://api.openpay.mx/stores?latitud={latitud}&longitud={longitud}&kilometers={radio}&amount={monto}
```

```php
<?
// =============================
// No implemented
// =============================
?>
```

```java
// =============================
// No implemented
// =============================
```

```csharp
// =============================
// No implemented
// =============================
```

```javascript
// =============================
// No implemented
// =============================
```

```ruby
# =============================
# No implemented
# =============================
```

> Request example

```shell
curl https://api.openpay.mx/stores?latitud=20.618975&longitud=-100.422290&kilometers=1.5&amount=4000 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

> Response example

```json
[
  {
    "id_store": 4913,
    "id": 115,
    "name": "0503 SAN PABLO -QRO",
    "last_update": "2016-02-04T00:52:16-06:00",
    "status": "active",
    "geolocation": {
      "lng": -100.421865,
      "lat": 20.618171,
      "place_id": "ChIJwSN2wpNa04URsDryLW517lg"
    },
    "address": {
      "line1": "AV. 5 DE FEBRERO KM 7.5 NO 1341",
      "line2": "SAN PABLO",
      "line3": null,
      "state": "QUERETARO",
      "city": "QUERETARO",
      "postal_code": "76030",
      "country_code": "MX"
    },
    "paynet_chain": {
      "name": "EXTRA",
      "logo": "http://www.openpay.mx/logotipos/extra.png",
      "thumb": "http://www.openpay.mx/thumb/extra.png",
      "max_amount": 99999.99
    }
  },
  {
    "id_store": 4726,
    "id": 68,
    "name": "ASTURIANO TECNOLOGICO",
    "last_update": "2016-02-04T00:52:16-06:00",
    "status": "active",
    "geolocation": {
      "lng": -100.410136,
      "lat": 20.61632,
      "place_id": "EktQcm9sIFRlY25vbMOzZ2ljbyBOdGUgOTk5LCBTYW4gUGFibG8sIFNhbnRpYWdvIGRlIFF1ZXLDqXRhcm8sIFFyby4sIE3DqXhpY28"
    },
    "address": {
      "line1": "PROLONGACION TECNOLOGICO NORTE #999",
      "line2": "SAN PABLO",
      "line3": null,
      "state": "QUERETARO",
      "city": "QUERETARO",
      "postal_code": "76159",
      "country_code": "MX"
    },
    "paynet_chain": {
      "name": "EL ASTURIANO",
      "logo": "http://www.openpay.mx/logotipos/asturiano.png",
      "thumb": "http://www.openpay.mx/thumb/asturiano.png",
      "max_amount": 99999.99
    }
  }
]
```

Gets the trade account details. Only it required to indicate the unique id of trade to be obtained.

###Resquest

Property  | Description
--------- | -----------
latitud | ***numeric*** (required) <br>Latitude of geographical location Store
longitud | ***numeric*** (required) <br>Longitud of geographical location Store
kilometers | ***numeric*** (required) <br>Radius distance in kilometers search
amount | ***numeric*** (required) <br>Purchase amount

###Response
If there are stores close range a settlement with stores found it is returned.

#Common Objects

Information for objects shared in request and response.

##Transaction Object

> Object example:

```json
{
   "id":"trehwr2zarltvae56vxl",
   "authorization":null,
   "transaction_type":"payout",
   "operation_type":"out",
   "currency":"MXN",
   "method":"bank",
   "creation_date":"2013-11-14T18:29:35-06:00",
   "order_id":"000001",
   "status":"in_progress",
   "amount":500,
   "description":"Winning payments",
   "error_message":null,
   "customer_id":"afk4csrazjp1udezj1po",
   "bank_account":{
      "rfc":ONE316015PM1,
      "mobile":null,
      "alias":null,
      "bank_name":"BANCOMER",
      "creation_date":"2013-11-14T18:29:34-06:00",
      "clabe":"012XXXXXXXXXX24616",
      "holder_name":"Juan Tapia Trejo",
      "bank_code":"012"
   }
}
```

Property | Description
--------- | -----------
id | _**string**_ <br/> Unique identifier assigned by Openpay at the moment of creation.
authorization | ***string*** <br/>Authorization number created by the processor entity.
transaction_type| ***string*** <br/>Transaction type: fee, charge, payout, transfer.
operation_type| ***string*** <br/>Operation type in the account: in, out.
method| ***string*** <br/>Transaction method type: card, bank o customer.
creation_date| ***datetime***  <br/>Transaction creation date in ISO 8601 format.
order_id| ***string*** <br/>Unique transaction and reference number.
status| ***string*** <br/>Current transaction status.  Possible values: completed, in_progress, failed.
amount| ***numeric*** <br/>Transaction full amount, including two decimal places.
description|***string*** <br/>Transaction description.
error_message| ***string*** <br/>If the transaction is in *failed* status, this field will include the error message.
customer_id| ***string*** <br/>Unique identifier for the customer who this transaction belongs.  If the value is null the transaction belongs to Merchant account.
currency| ***string*** <br/>Currency used in the operation by default is MXN (Mexican pesos).
bank_account| ***object*** <br/>Bank account data used for the transaction.  See the *BankAccount* object.
card| ***object*** <br/>Credit card data used in the transaction.  See the *Card* object.
card_points| ***object*** <br/>Contains information about the reward points used for payment, if they were used. See the [CardPoints object](#cardpoints-object) 

## Address Object

> Object example:

```json
{
   "line1":"Av 5 de Febrero",
   "line2":"Roble 207",
   "line3":"col carrillo",
   "state":"Queretaro",
   "city":"QuerÃ©taro",
   "postal_code":"76900",
   "country_code":"MX" 
}
```

Property | Description
--------- | -----------
line1 | ***string*** (required) <br/>The first line is the card owner address. It's commonly used to indicate street address and number.
line2 | ***string*** <br/>Second addres line, commonly use to indicate interior number, suite number  or county.
line3 | ***string*** <br/>Third address line, commonly use to to indicate the neighborhood.
postal_code | ***string*** (required) <br/>Zip code
state | ***string*** (required) <br/>State
city | ***string*** (required) <br/>City
country_code | ***string*** (required) <br/>Country code, in the two character format: ISO_3166-1.

## Store object

> Object example:

```json
{
   "reference":"OPENPAY02DQ35YOY7",
   "barcode_url":"https://sandbox-api.openpay.mx/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
}
```

Property | Description
--------- | -----------
reference | ***string*** <br/>Payment reference to go stores and make deposits to Openpay account
barcode_url | ***string*** <br/>It is the url that generates the bar code of reference.

##PaymentPlan Object

> Object example:

```json
{
   "payments":"6"
}
```

Property | Description
--------- | -----------
payments | ***numeric*** <br/> Plan data months without interest is desired as use in the charge (3, 6, 9, 12, 18).

##Cardpoints Object

> Object example:

```json
{
    "used": 134,
    "remaining": 300,
    "caption": "TRANSACCION APROBADA. ME OBLIGO EN LOS TERMINOS Y CONDICIONES DEL PROGRAMA RECOMPENSAS SANTANDER. PARA CUALQUIER DUDA O ACLARACION LLAME AL 01800 RECOMPE (73-266-73).",
    "amount": 10
}
```

Property | Description
--------- | -----------
used | ***numeric*** <br/> Amount of points used in the payment.
remaining | ***numeric*** <br/> Amount of points remaining in the card after the payment.
amount | ***numeric*** <br/>Transaction amount paid using points.
caption | ***string*** (opcional) <br/> A message to be shown to the customer in their ticket or receipt.

##Object Geolocation

> Object example:

```json
{
  "lng": -100.421865,
  "lat": 20.618171,
  "place_id": "ChIJwSN2wpNa04URsDryLW517lg"
}
```

Property | Description
--------- | -----------
lng | ***numeric*** <br/> Longitud, geographical coordinate.
lat | ***numeric*** <br/> Latitud, geographical coordinate.
place_id | ***string*** <br/>Unique identifier of google maps

##Object PaynetChain

> Object example:

```json
{
      "name": "EXTRA",
      "logo": "http://www.openpay.mx/logotipos/extra.png",
      "thumb": "http://www.openpay.mx/thumb/extra.png",
      "max_amount": 99999.99
}
```

Property | Description
--------- | -----------
name | ***string*** <br/> Chain name.
logo | ***string*** <br/> URL logo image chain.
thumb | ***string*** <br/> URL thumbnail image chain.
max_amount | ***numeric*** <br/>Maximum payment amount that accept chain stores