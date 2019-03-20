#Charges
Charges can be made to cards, stores and banks. Each charge is assigned with an unique identifier in the system.

You can do card charges by using a saved card id, using a token or you can send the card information at the time of invocation.

##With token

> Definition

```shell
Merchant
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges

Customer
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Merchant
$bancomer->charges->create(chargeRequest);

Customer
$customer = $bancomer->customers->get($customerId);
$customer->charges->create(chargeRequest);
?>
```

```java
//Customer
bancomerAPI.charges().create(String customerId, List<Parameter> request);

//Merchant
bancomerAPI.charges().create(List<Parameter> request);
```

```csharp
//Customer
bancomerAPI.ChargeService.Create(string customer_id, List<IParameter> request);

//Merchant
bancomerAPI.ChargeService.Create(List<IParameter> request);
```

```ruby
#Customer
@charges=@bancomer.create(:charges)
@charges.create(request_hash, customer_id)

#Merchant
@charges=@bancomer.create(:charges)
@charges.create(request_hash)
```

> Merchant request example 

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "affiliation_bbva" : "720939",
   "amount" : 100,
   "description" : "Cargo inicial a mi cuenta",
   "currency" : "MXN",
   "token" : "krv3y6yucurt47w2sv1d",
   "order_id" : "oid-00051"
}'
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
List<IParameter> tokenRequest = List<IParameter>{
    new SingleParameter("holder_nane", "Juan Perez Ramirez"),
    new SingleParameter("card_number", "4111111111111111"),
    new SingleParameter("cvv2", "022"),
    new SingleParameter("expiration_month", "12"),
    new SingleParameter("expiration_year", "20"),
};

Dictionary<String, Object> tokenDictionary = bancomerAPI.TokenService.Create(tokenRequest);
ParameterContainer token = new ParameterContainer("token", tokenDictionary);

List<IParameter> request = List<IParameter> {
    new SingleParameter("affiliation_bbva", "720931"),
    new SingleParameter("amount", "200.00"),
    new SingleParameter("description", "Test Charge"),
    new SingleParameter("customer_language", "SP"),
    new SingleParameter("capture", "TRUE"),
    new SingleParameter("use_3d_secure", "FALSE"),
    new SingleParameter("use_card_points", "NONE"),
    new SingleParameter("token", token.GetSingleValue("id").ParameterValue),
    new SingleParameter("currency", "MXN"),
    new SingleParameter("order_id", "oid-00051")
};

Dictionary<String, Object> chargeDictionary = bancomerAPI.ChargeService.Create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```java
BancomerAPI api = new BancomerAPI(
        "https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

List<Parameter> tokenRequest = new ArrayList<Parameter>(Arrays.asList(
    new SingleParameter("card_number", "4111111111111111"),
    new SingleParameter("cvv2", "295"),
    new SingleParameter("expiration_month", "12"),
    new SingleParameter("expiration_year", "20"),
    new SingleParameter("holder_name", "Juan Perez Lopez")));

Map tokenAsMap = api.tokens().create(tokenRequest);
ParameterContainer token = new ParameterContainer("token", tokenAsMap);

List<Parameter> request = new ArrayList<Parameter>(Arrays.asList(
    new SingleParameter("affiliation_bbva", "720931"),
    new SingleParameter("amount", "10.00"),
    new SingleParameter("description", "Cargo inicial"),
    new SingleParameter("customer_language", "SP"),
    new SingleParameter("capture", "true"),
    new SingleParameter("use_3d_secure", "false"),
    new SingleParameter("use_card_points", "NONE"),
    new SingleParameter("token", token.getSingleValue("id").getParameterValue()),
    new SingleParameter("currency", "MXN"),
    new SingleParameter("order_id", "oid-00051")

));

Map chargeAsMap = api.charges().create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```php
<?
$bancomer = Bancomer::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');
$tokenRequest = array(
     'card_number' => '4111111111111111',
     'cvv2' => '295',
     'expiration_month' => '11',
     'expiration_year' => '22',
     'holder_name' => 'Juan Perez Lopez');

$token = $bancomer->tokens->create($tokenRequest);

$chargeRequest = array(
    'affiliation_bbva' => '720931',
    'amount' => 100,
    'description' => 'Cargo inicial a mi merchant',
    'customer_language' => 'SP',
    'capture' => 'FALSE',
    'use_card_points' => 'FALSE',
    'currency' => 'MXN'
    'order_id' => 'oid-00051'
    'token' => $token['id']);

$charge = $bancomer->charges->create($chargeRequest);
?>
```

```ruby
@bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bancomer.create(:charges)
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
    "currency" => "MXN",
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
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

<aside class="notice">
You can charge the merchant account or the customer account.
</aside>

***Customized antifraud system***</br>
You can send extra data to Bancomer in order to increase number of variables and get better results in antifraud detection for your transactions.

<aside class="notice">
If you want to use this feature you need to send <code>metadata</code> property with all fields you think can help to decide when a transaction is a fraud trying. Call support line to enable this feature</br>
</aside>

###Request 
Property | Description
--------- | -----
affiliation_bbva|               ***string*** (required) <br/>It must contain the affiliation number.
amount |                        ***numeric*** (required) <br/>Amount to charge. Must be an amount greater than zero, with up to two decimal digits.
currency |                      ***string*** (optional) <br/>Charge currency type. Currently you can only use two currency types: Mexican pesos(MXN) y American dollars(USD).
order_id |                      ***string*** (optional, length = 100) <br/>Unique identifier of charge. Must be unique among all transactions.
description |                   ***string*** (required, length = 250) <br/>A description associated to the charge.
[customer](##objeto-cliente)|   ***object*** (required) <br/>Customer information who is charged. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the charge at the merchant level<br/><br/> To create a customer and keep a record of their charges history refer to [Objeto Cliente](#objeto-cliente) (#create-a-new-customer) and do the charge at the customer level.
customer_language |             ***string*** (required, length = 2) <br/>Language to be used in the receipt and the purchase screen, currently two values are accepted SP-Spanish In-English.
[payment_plan](#objetc-paymentplan)|    ***object*** (optional) <br/>Plan data months without interest is desired as use in the charge. Refer to [PaymentPlan Object](#paymentplan-objetc).
redirect_url |                          ***string*** (optional) <br/>Used in redirect charges. It indicates the url to which redirect after a successful transaction in the bancomer payment form.
use_card_points |                       ***string*** (optional, default = NONE) <br/> <table><tr><td><strong>ONLY_POINTS</strong></td> <td>Charge only with points (<a href="#consulta-de-puntos">Points card</a>)</td></tr><tr><td><strong>MIXED</strong></td><td>Charge with points and pesos</td></tr><tr><td><strong>NONE</strong></td>        <td>Charge only with pesos</td></tr></table>The values that indicate points must be used only if the points_card property is true, otherwise an error will occur.
use_3d_secure |                         ***string*** (optional) <br/>By default the value is TRUE, if the trade has enabled the configuration to not use 3d secure, then you can send the parameter to FALSE.
token |                                 ***string*** (required, length = 45) <br/>ID of the saved card or the id of the token created from where the funds will be withdrawn.
metadata |                              ***list(key, value)*** (optional) <br/>Field list to send antifraud system, It must be according to [Rules to send custom antifraud fields] (#custom-to-send-antifraud-fields).
capture |                               ***boolean*** (optional, default = true) <br/>Indicates whether the charge is made immediately or not , when the value is false the charge is handled as authorized (or pre-authorization) and the amount is only to be confirmed or canceled in a second call.
***************

###Response
Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

##Confirming a charge

> Definition

```shell
Merchant
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/capture

Customer
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}/capture
```

```php
<?
Merchant
$charge = $bancomer->charges->get(transactionId);
$charge->capture(captureData);

Customer
$customer = $bancomer->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
$charge->capture(captureData);
?>
```

```java
//Customer
bancomerAPI.charges().confirmCapture(String customerId, ConfirmCaptureParams request);

//Merchant
bancomerAPI.charges().confirmCapture(ConfirmCaptureParams request);
```

```csharp
//Customer
bancomerAPI.ChargeService.Capture(string customer_id, string transaction_id, Decimal? amount);

//Merchant
bancomerAPI.ChargeService.Capture(string transaction_id, Decimal? amount);
```

```javascript
// Merchant
bancomer.charges.capture(transactionId, captureRequest, callback);

// Customer
bancomer.customers.charges.capture(customerId, transactionId, captureRequest, callback);
```

```ruby
#Customer
@charges=@bancomer.create(:charges)
@charges.capture(transaction_id, customer_id)

#Merchant
@charges=@bancomer.create(:charges)
@charges.capture(transaction_id)
```

> Customer request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges/tryqihxac3msedn4yxed/capture \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
    "amount" : 100.00
} ' 
```

```php
<?
$bancomer = Bancomer::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$captureData = array('amount' => 100.00);

$customer = $bancomer->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->get('tryqihxac3msedn4yxed');
$charge->capture($captureData);
?>
```

```java
BancomerAPI api = new BancomerAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ConfirmCaptureParams request = new ConfirmCaptureParams();
request.chargeId("tryqihxac3msedn4yxed");
request.amount(new BigDecimal("100.00"));

Charge charge = api.charges().confirmCapture("ag4nktpdzebjiye1tlze", request);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.ChargeService.Capture("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", new Decimal(100.00));
```

```javascript
var captureRequest = {
  'amount' : 100.00
};

bancomer.customers.charges.capture('ag4nktpdzebjiye1tlze', 'tryqihxac3msedn4yxed', captureRequest, 
    function(error, charge){
  // ...
});
```

```ruby
@bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bancomer.create(:charges)

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
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/refund

Customer
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}/refund
```

```php
<?
Merchant
$charge = $bancomer->charges->get(transactionId);
$charge->refund(refundData);

Customer
$customer = $bancomer->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
$charge->refund(refundData);
?>
```

```java
//Customer
bancomerAPI.charges().refund(String customerId, RefundParams request);

//Merchant
bancomerAPI.charges().refund(RefundParams request);
```

```csharp
//Customer
bancomerAPI.ChargeService.Refund(string customer_id, string transaction_id, string description);

//Merchant
bancomerAPI.ChargeService.Refund(string transaction_id, string description);
```

```javascript
// Merchant
bancomer.charges.refund(transactionId, refundRequest, callback);

// Customer
bancomer.customers.charges.refund(customerId, transactionId, refundRequest, callback);
```

```ruby
#Customer
@charges=@bancomer.create(:charges)
@charges.refund(transaction_id, request_hash, customer_id)

#Merchant
@charges=@bancomer.create(:charges)
@charges.refund(transaction_id, request_hash)
```

> Customer request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges/tr6cxbcefzatd10guvvw/refund \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "description" : "devolución",
   "amount" : 100.00
} ' 
```

```php
<?
$bancomer = Bancomer::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$refundData = array(
    'description' => 'devolución',
    'amount' => 100);

$customer = $bancomer->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->get('tr6cxbcefzatd10guvvw');
$charge->refund($refundData);
?>
```

```java
BancomerAPI api = new BancomerAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
RefundParams request = new RefundParams();
request.chargeId("tryqihxac3msedn4yxed");
request.description("Monto de cargo devuelto");
request.amount(new BigDecimal("100.00"));

Charge charge = api.charges().refund("ag4nktpdzebjiye1tlze", request);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.ChargeService.Refund("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", "Monto de cargo devuelto", , new Decimal(100.00));
```

```javascript
var refundRequest = {
   'description' : 'devolución',
   'amount' : 100.00
};

bancomer.customers.charges.refund('ag4nktpdzebjiye1tlze', 'tryqihxac3msedn4yxed', refundRequest, 
    function(error, charge) {
  // ...
});
```

```ruby
@bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bancomer.create(:charges)

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
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}

Merchant
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}
```

```php
<?
Merchant
$charge = $bancomer->charges->get(transactionId);

Customer
$customer = $bancomer->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
?>
```

```java
//Customer
bancomerAPI.charges().get(String customerId, String transactionId);

//Merchant
bancomerAPI.charges().get(String transactionId);
```

```csharp
//Customer
bancomerAPI.ChargeService.Get(string customer_id, string transaction_id);

//Merchant
bancomerAPI.ChargeService.Get(string transaction_id);
```

```javascript
// Merchant
bancomer.charges.get(transactionId, callback);

// Customer
bancomer.customers.charges.get(customerId, transactionId, callback);
```

```ruby
#Customer
@charges=@bancomer.create(:charges)
@charges.get(transaction_id, customerId)

#Merchant
@charges=@bancomer.create(:charges)
@charges.get(transaction_id)
```

> Customer request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges/tr6cxbcefzatd10guvvw \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```php
<?
$bancomer = Bancomer::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$customer = $bancomer->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->get('tr6cxbcefzatd10guvvw');
?>
```

```java
BancomerAPI api = new BancomerAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.charges().get("ag4nktpdzebjiye1tlze", "tr6cxbcefzatd10guvvw");
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Charge charge = api.ChargeService.Get("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed");
```

```javascript
bancomer.customers.charges.get('ag4nktpdzebjiye1tlze', 'tr6cxbcefzatd10guvvw', function(error, charge){
  // ...
});
```

```ruby
@bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bancomer.create(:charges)

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
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges

Merchant
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Merchant
$chargeList = $bancomer->charges->getList(searchParams);

Customer
$customer = $bancomer->customers->get(customerId);
$chargeList = $customer->charges->getList(searchParams);
?>
```

```java
//Customer
bancomerAPI.charges().list(String customerId, SearchParams request);

//Merchant
bancomerAPI.charges().list(SearchParams request);
```

```csharp
//Customer
bancomerAPI.ChargeService.List(string customer_id, SearchParams request = null);

//Merchant
bancomerAPI.ChargeService.List(SearchParams request = null);
```

```javascript
// Merchant
bancomer.charges.list(callback);
bancomer.charges.list(searchParams, callback);

// Customer
bancomer.customers.charges.list(customerId, callback);
bancomer.customers.charges.list(customerId, searchParams, callback);
```

```ruby
#Customer
@charges=@bancomer.create(:charges)
@charges.all(customer_id)

#Merchant
@charges=@bancomer.create(:charges)
@charges.all
```

> Customer request example

```shell
curl -g "https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges?creation[gte]=2013-11-01&limit=2" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: 
```

```php
<?
$bancomer = Bancomer::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$searchParams = array(
    'creation[gte]' => '2013-11-01',
    'creation[lte]' => '2014-11-01',
    'offset' => 0,
    'limit' => 2);

$customer = $bancomer->customers->get('ag4nktpdzebjiye1tlze');
$chargeList = $customer->charges->getList($searchParams);
?>
```

```java
final Calendar dateGte = Calendar.getInstance();
final Calendar dateLte = Calendar.getInstance();
dateGte.set(2014, 5, 1, 0, 0, 0);
dateLte.set(2014, 5, 15, 0, 0, 0);

BancomerAPI api = new BancomerAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.creationGte(dateGte.getTime());
request.creationLte(dateLte.getTime());
request.offset(0);
request.limit(100);
request.amount(new BigDecimal("100.00"));

List<Charge> charges = api.charges().list("ag4nktpdzebjiye1tlze", request);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;
request.Amount = new Decimal(100.00);

List<Charge> charges= bancomerAPI.ChargeService.List("ag4nktpdzebjiye1tlze", request);
```

```javascript
var searchParams = {
  'creation[gte]' : '2013-11-01',
  'limit' : 2
};

bancomer.customers.charges.list('ag4nktpdzebjiye1tlze',searchParams, function(error, chargeList) {
  // ...
});
```

```ruby
@bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bancomer.create(:charges)

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
