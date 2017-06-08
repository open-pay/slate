#Comisiones
Si las cuentas de los clientes fueron creadas para que manejarán su propio saldo, se puede realizar el cobro de una comisión el cual se verá reflejado en la cuenta del comercio.

<aside class="notice">
Para que las cuentas de los clientes manejen saldo debieron ser creadas con la propiedad ***requires_account = true***. Ver [creación de un cliente](#crear-un-nuevo-cliente)
</aside>

##Cobrar Comisión
> Definición

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
#Cliente
@fees=@openpay.create(:fees)
@fees.create(request_hash)
```

> Ejemplo de petición 

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/fees \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{                                            
     "customer_id" : "dvocf97jd20es3tw5laz",
     "amount" : 12.50,          
     "description" : "Cobro de Comisión",
     "order_id" : "oid-1245"
}' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$feeDataRequest = array(
    'customer_id' => 'a9ualumwnrcxkl42l6mh',
    'amount' => 12.50,
    'description' => 'Cobro de Comisión',
    'order_id' => 'ORDEN-00063');

$fee = $openpay->fees->create($feeDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateFeeParams request = new CreateFeeParams();
request.customerId("a9pvykxz4g5rg0fplze0");
request.amount(new BigDecimal("100.00"));
request.description("Cobro de comisión");
request.orderId("oid-1245");

Fee fee = api.fees().create(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
FeeRequest request = new FeeRequest();
request.CustomerId = "a9pvykxz4g5rg0fplze0";
request.Amount = new Decimal(100.00);
request.Description = "Cobro de comisión";
request.OrderId = "oid-1245;

Fee fee = api.FeeService.Create(request);
```

```javascript
var feeRequest = {                                            
     'customer_id' : 'dvocf97jd20es3tw5laz',
     'amount' : 12.50,          
     'description' : 'Cobro de Comisión',
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
     "description" => "Cobro de Comisión",
     "order_id" => "oid-1245"
   }

response_hash=@fees.create(request_hash.to_hash)
```

> Ejemplo de respuesta

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
   "description":"Cobro de comisión",
   "error_message":null,
   "order_id":"oid-1245",
   "customer_id":"dvocf97jd20es3tw5laz"
}
```

Cobra una comisión a la cuenta de un cliente.

###Petición

Propiedad | Descripción
--------- | ------
customer_id | ***string*** (requerido, longitud = 45) <br/>El identificador único del cliente al que deseas cobrarle la comisión.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cobro comisión.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único de la comisión. Debe ser único para todas las transacciones.
 
###Regresa
El [objeto de transacción](#objeto-transacción) de la comisión, con su fecha de creación y su id o una [respuesta de error](#objeto-error).


##Devolver Comisión
> Definición

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

> Ejemplo de petición 

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/fees/trzjaozcik8msyqshka4/refund \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{                                            
     "description" : "Devolución de Comisión"
}' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$refundData = array(
    'description' => 'Devolución de Comisión'
    );

$fee = $openpay->fees->get("trzjaozcik8msyqshka4");
$fee->refund($refundData);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
RefundParams request = new RefundParams();
request.description("Devolución de comisión");

Fee fee = api.fees().refund("trzjaozcik8msyqshka4", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
RefundRequest request = new RefundRequest();
request.Description = "Devolución de comisión";

Fee fee = api.FeeService.Refund("trzjaozcik8msyqshka4", request);
```

```javascript
var refundRequest = {                                            
     'description' : 'Devolución de Comisión'
};

openpay.fees.refund("trzjaozcik8msyqshka4", refundRequest, function(error, refund){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@fees=@openpay.create(:fees)
refund_hash={
     "description" => "Devolución de Comisión"
   }

response_hash=@fees.refund("mzdtln0bmtms6o3kck8f", refund_hash.to_hash)
```

> Ejemplo de respuesta

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
  "description": "devolución de comisión merchant03",
  "error_message": null,
  "order_id": null,
  "customer_id": "ar2btmquidjhykdaztp6",
  "amount": 11.11,
  "currency": "MXN"
}
```

Devuelve una comisión a la cuenta de un cliente.

###Petición

Propiedad | Descripción
--------- | ------
description | ***string*** (opcional, longitud = 250) <br/>Una descripción asociada al reembolso de la comisión.
 
###Regresa
El [objeto de transacción](#objeto-transacción) del reembolso, con su fecha de creación y su id o una [respuesta de error](#objeto-error).


##Listado de comisiones
> Definición

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
#Cliente
@fees=@openpay.create(:fees)
@fees.all
```

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
      "description":"Cobro de comisión",
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
      "description":"Cobro de comisión",
      "error_message":null,
      "order_id":"oid-1366",
      "customer_id":"afk4csrazjp1udezj1po"
   }
]
```
Regresa los detalles de todas las comisiones cobradas del comercio.

###Petición
Se puede realizar búsquedas utilizando los siguiente parámetros.

Propiedad | Descripción
--------- | ------
creation| ***date*** <br/>Igual a la fecha de creación. Formato yyyy-mm-dd
creation[gte]| ***date*** <br/>Mayor a la fecha de creación. Formato yyyy-mm-dd
creation[lte]| ***date*** <br/>Menor a la fecha de creación. Formato yyyy-mm-dd
offset| ***numeric*** <br/>Número de registros a omitir al inicio, por defecto 0.
limit| ***numeric*** <br/>Número de registros que se requieren, por defecto 10.

###Respuesta
Regresa un arreglo de [objetos transacción](#objeto-transacción) de las comisiones cobradas en orden descendente por fecha, cada uno con el identificador del cliente al que se le realizó.
