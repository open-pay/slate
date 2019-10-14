#Transferencias

Las transferencias permite transferir fondos entre las cuentas de tus clientes. 

<aside class="notice">
**Nota:** Si desea realizar una transferencia a un banco consulte la [sección de pagos](#pagos-o-retiros).
</aside>

##Transferir entre clientes

> Definición

```shell
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/transfers
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

> Ejemplo de petición 

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/transfers \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{                                            
     "customer_id" : "dvocf97jd20es3tw5laz",
     "amount" : 716,
     "description" : "Transferencia entre cuentas",
     "order_id" : "oid-1245"
}' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$transferDataRequest = array(
    'customer_id' => 'aqedin0owpu0kexr2eor',
    'amount' => 716,
    'description' => 'Cobro de Comisión',
    'order_id' => 'ORDEN-00061');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$transfer = $customer->transfers->create($transferDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateTransferParams request = new CreateTransferParams();
request.toCustomerId("ah1ki9jmb50mvlsf9gqn");
request.amount(new BigDecimal("716"));
request.description("Transferencia del Customer 1 al Customer 2");
request.orderId("idOrdExt-0101");

Transfer transfer = api.transfers().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
TransferRequest request = new TransferRequest();
request.CustomerId = "ah1ki9jmb50mvlsf9gqn";
request.Amount = new Decimal(716);
request.Description = "Transferencia del Customer 1 al Customer 2";
request.OrderId = "idOrdExt-0101";

Transfer transfer = api.TransferService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var transferRequest = {                                          
  'customer_id' : 'dvocf97jd20es3tw5laz',
  'amount' : 716,          
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
     "amount" => 716,
     "description" => "Transferencia entre cuentas",
     "order_id" => "oid-1245"
   }

response_hash=@transfers.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Ejemplo de respuesta

```json
{
   "amount":716,
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
       "barcode_url": "https://sandbox-api.openpay.co/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
   "clabe": "646180109400423323"
}
```

Realiza la transferencia de fondos de una cuenta de cliente a otra. Los fondos serán cargos a una cuenta origen y abonados a la cuenta destino, lo cual generá dos transacciones. 

###Petición

Propiedad | Descripción
--------- | ------
customer_id | ***string*** (requerido, longitud = 45) <br/>El ID de Openpay del cliente al que deseas enviarle los fondos.
amount | ***numeric*** (requerido) <br/>Cantidad a transferir. Debe ser una cantidad mayor a un peso, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada a la transferencia.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único de la transferencia. Será asignado a la transacción de retiro.

###Respuesta
Si la transacción se realiza correctamente, la respuesta contendrá un [objeto de transacción](#objeto-transacci-n). Este objeto representará el retiro de fondos del cliente actual. En caso de error, se regresará el objeto de error.

##Obtener una transferencia

> Definición

```shell
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/transfers/{TRANSACTION_ID}
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

> Ejemplo de petición 

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/transfers/twpmbike2jejex3pahzd \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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

> Ejemplo de respuesta

```json
{
   "amount":716,
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
Con el identificador del cliente y el identificador de la transferencia, se puede obtener el detalle de la transacción. La transacción de salida se encontrará en el cliente desde el cual se realizó la transferencia, y la transacción de entrada en el cliente que recibió el monto.


###Petición
Propiedad | Descripción
--------- | ------
customer_id| ***string*** (requerido, longitud = 45) <br/> Identificador del cliente
transaction_id| ***string*** (requerido, longitud = 45) <br/> Identificador de la transferencia

###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n)

##Listado de transferencias

> Definición

```shell
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/transfers
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

> Ejemplo de petición 

```shell
curl -g "https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/transfers?limit=2" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$findDataRequest = array(
    'creation[gte]' => '2019-01-01',
    'creation[lte]' => '2019-12-31',
    'offset' => 0,
    'limit' => 5);

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$transferList = $customer->transfers->getList($findDataRequest);
?>
```

```java
final Calendar dateGte = Calendar.getInstance();
final Calendar dateLte = Calendar.getInstance();
dateGte.set(2019, 1, 1, 0, 0, 0);
dateLte.set(2019, 12, 31, 0, 0, 0);
        
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
request.CreationGte = new Datetime(2019, 1, 1);
request.CreationLte = new DateTime(2019, 12, 31);
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

> Ejemplo de respuesta

```json
[
   {
      "amount":716,
      "authorization":null,
      "method":"customer",
      "currency":"COP",
      "operation_type":"out",
      "transaction_type":"transfer",
      "status":"completed",
      "id":"a74mbe4e2j5gc6gfahzd",
      "creation_date":"2019-09-18T00:31:19-06:00",
      "description":"Una descripcion",
      "error_message":null,
      "order_id":"20131115103317",
      "customer_id":"afk4csrazjp1udezj1po"
   },
   {
      "amount":715,
      "authorization":null,
      "method":"customer",
      "currency":"COP",
      "operation_type":"in",
      "transaction_type":"transfer",
      "status":"completed",
      "id":"a74mbe4e2j5gc6gfahzd",
      "creation_date":"2019-09-18T00:31:19-06:00",
      "description":"Una descripcion",
      "error_message":null,
      "order_id":null,
      "customer_id":"agdn58ngcnogqmzruz1i"
   }
]
```

Permite consultar las transacciones de entrada y salida de un cliente.

###Petición
Puede realizar una búsqueda utilizando los siguiente parámetros como filtros.

Propiedad | Descripción
--------- | ------
creation| ***date*** <br/>Igual a la fecha de creación. Formato yyyy-mm-dd
creation[gte]| ***date*** <br/>Mayor a la fecha de creación. Formato yyyy-mm-dd
creation[lte]| ***date*** <br/>Menor a la fecha de creación. Formato yyyy-mm-dd
offset| ***numeric*** <br/>Número de registros a omitir al inicio, por defecto 0.
limit| ***numeric*** <br/>Número de registros que se requieren, por defecto 10.

###Respuesta
Listado de [objetos transacción](#objeto-transacci-n) de las transferencias realizadas, cada uno con el identificador del cliente al que se le realizó. Las transacciones serán listadas en orden descendente por fecha de creación.
