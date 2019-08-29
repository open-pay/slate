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
   "currency":"COP",
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
   "currency":"COP",
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
      "currency":"COP",
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
      "currency":"COP",
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

