#Fees
If the customer accounts were created to handle their own balance, a fee can be charged which will be shown in the Merchant account.

<aside class="notice">
In order to have customer accounts where they handle their balance they should have been created with the property ***requires_account=true***.  See [customer creation](#create-a-new-customer).
</aside>

##Charging a Fee
> Definition

```shell
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/fees
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
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/fees \
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
OpenpayAPI api = new OpenpayAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/fees/{TRANSACTION_ID}/refund
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
#Customer
@fees=@openpay.create(:fees)
@fees.refund(transaction_id, refund_hash)
```

> Request example 

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/fees/trzjaozcik8msyqshka4/refund \
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
OpenpayAPI api = new OpenpayAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/fees
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
curl -g "https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/fees?limit=10" \
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
        
OpenpayAPI api = new OpenpayAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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

