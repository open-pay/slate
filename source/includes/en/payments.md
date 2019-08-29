#Payouts or withdrawals
A payout is the transaction that allows to extract funds from a Openpay account and send the funds to a bank account. Payouts can be made from the accounts of the customers or from the Merchant account.

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
    "method": "bank_account",
    "destination_id": "b3d54sd3mdjf75udjfvoc",
    "amount": 10.50,
    "description": "Retiro de saldo semanal",
    "order_id": "oid-00021"
}' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$payoutRequest = array(
    'method' => 'bank_account',
    'destination_id' => 'b3d54sd3mdjf75udjfvoc',
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
request.bankAccountId("b3d54sd3mdjf75udjfvoc"); // = destination_id
request.amount(new BigDecimal("10.50"));
request.description("Retiro de saldo semanal");
request.orderId("oid-00021");

Payout payout = api.payouts().create("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_e568c42a6c384b7ab02cd47d2e407cab", "mzdtln0bmtms6o3kck8f");
PayoutRequest request = new PayoutRequest();
request.Method = "bank_account";
request.DestinationId = "b3d54sd3mdjf75udjfvoc";
request.Amount = new Decimal(10.50;
request.Description = "Retiro de saldo semanal";
request.OrderId = "oid-00021;

Payout = api.PayoutService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var payoutRequest = {
    'method': 'bank_account',
    'destination_id': 'b3d54sd3mdjf75udjfvoc',
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
     "destination_id" => "b3d54sd3mdjf75udjfvoc",   
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
   "method":"bank_account",
   "currency":"COP",
   "operation_type":"out",
   "transaction_type":"payout",
   "bank_account":{
      "id":"b3d54sd3mdjf75udjfvoc",
      "clabe":"012XXXXXXXXXX24616",
      "bank_code":"012",
      "bank_name":"BANCOMER",
      "alias":null,
      "holder_name":"Mi empresa"
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

Sends a payout to a previously registered bank account. Refer to [create a bank account] (#create-a-bank-account)

###Request 

Property | Description
--------- | -----
method|***string*** (required) <br/>It must contain the value **bank_account**.
destination_id | ***string*** (required, length = 45) <br/>ID of the registered bank account.
amount | ***numeric*** (required) <br/>Amount of payout. Must be an amount greater than zero, with up to two decimal digits.
description | ***string*** (required, length = 250) <br/>A description associated to the payment.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of payout. Must be unique among all transactions.


###Response
Returns a [transaction object](#transaction-object) with the payout information or with an [error response](#error-object).

##Payment to a bank account

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
   "currency":"COP",
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
   "method":"bank_account",
   "operation_type":"out",
   "transaction_type":"payout",
   "bank_account":{
      "clabe":"012XXXXXXXXXX24616",
      "bank_code":"012",
      "bank_name":"BANCOMER",
      "alias":null,
      "holder_name":"Mi empresa"
   },
   "status":"completed",
   "currency":"COP",
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
   "method":"bank_account",
   "operation_type":"out",
   "transaction_type":"payout",
   "bank_account":{
      "clabe":"012XXXXXXXXXX24616",
      "bank_code":"012",
      "bank_name":"BANCOMER",
      "alias":null,
      "holder_name":"Mi empresa"
   },
   "status":"cancelled",
   "currency":"COP",
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
      "currency":"COP",
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
      "method":"bank_account",
      "operation_type":"out",
      "transaction_type":"payout",
      "bank_account":{
         "clabe":"012XXXXXXXXXX24616",
         "bank_code":"012",
         "bank_name":"BANCOMER",
         "alias":null,
         "holder_name":"Mi empresa"
      },
      "status":"completed",
      "currency":"COP",
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
    "currency": "COP"
  },
  {
    "id": "tru6lsl6xpvseqp87vjd",
    "authorization": "FPVYiN4nyw",
    "method": "card",
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
    "currency": "COP"
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

