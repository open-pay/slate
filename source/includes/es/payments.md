#Pagos o retiros
Un pago es la transacción que permite extraer los fondos de una cuenta Openpay y enviarlos a una cuenta bancaria o una tarjeta de débito. Los pagos se pueden realizar desde las cuentas de los clientes o desde tu cuenta de comercio.

<aside class="notice">
**Nota:** Todas las transacciones de pago se regresarán en status **in_progress** lo cual significa que se programó para el día siguiente, cuando se efectúe la operación se cambiará el estado a **completed** y si se tienen webhooks configurados se enviará la notificación.
</aside>

##Pago a id registrado

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts
```

```php
<?
Cliente
$customer = $openpay->customers->get(customerId);
$payout = $customer->payouts->create(payoutRequest);

Comercio
$payout = $openpay->payouts->create(payoutRequest);
?>
```

```java
//Cliente
openpayAPI.payouts().create(String customerId, CreateBankPayoutParams request);

//Comercio
openpayAPI.payouts().create(CreateBankPayoutParams request);
```

```csharp
//Cliente
openpayAPI.PayoutService.Create(string customer_id, PayoutRequest request);

//Comercio
openpayAPI.PayoutService.Create(PayoutRequest request);
```

```javascript
// Comercio
openpay.payouts.create(payoutRequest, callback);

// Cliente
openpay.customers.payouts.create(customerId, payoutRequest, callback);
```

```ruby
#Cliente
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash, customer_id)

#Comercio
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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

Envío un pago a una cuenta bancario o terjeta de débito previamente registrada. Consulte como [crear una cuenta de bancaria](#crear-una-cuenta-bancaria)

###Petición 

Propiedad | Descripción
--------- | -----
method|***string*** (requerido) <br/>Debe contener el valor **card** para realizar un pago a una tarjeta registrado y **bank_account** para realizarlo a una cuenta bancaria registrada.
destination_id | ***string*** (requerido, longitud = 45) <br/>El ID de la cuenta bancaria o tarjeta de débito previamente registrada.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del pago o una [respuesta de error](#objeto-error).

##Pago a cuenta bancaria

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts
```

```php
<?
Cliente
$customer = $openpay->customers->get(customerId);
$payout = $customer->payouts->create(payoutRequest);

Comercio
$payout = $openpay->payouts->create(payoutRequest);
?>
```

```java
//Cliente
openpayAPI.payouts().create(String customerId, CreateBankPayoutParams request);

//Comercio
openpayAPI.payouts().create(CreateBankPayoutParams request);
```

```csharp
//Cliente
openpayAPI.PayoutService.Create(string customer_id, PayoutRequest request);

//Comercio
openpayAPI.PayoutService.Create(PayoutRequest request);
```

```javascript
// Comercio
openpay.payouts.create(payoutRequest, callback);

// Cliente
openpay.customers.payouts.create(customerId, payoutRequest, callback);
```

```ruby
#Cliente
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash, customer_id)

#Comercio
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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

Envía un pago a una cuenta bancaria.

###Petición 

Propiedad | Descripción
--------- | -----
method|***string*** (requerido) <br/>Debe contener el valor **bank_account**.
[bank_account](#objeto-cuenta-bancaria) | ***object*** (requerido) <br/>Datos de la cuenta bancaria a la que se enviarán los fondos. <br/><br/> **clabe**.- Número de cuenta CLABE de la cuenta a la que se enviarán los fondos. <br/>**holder_name**.- Nombre del propietario de la cuenta.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del pago o una [respuesta de error](#objeto-error).

##Pago a tarjeta de débito

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts
```

```php
<?
Cliente
$customer = $openpay->customers->get(customerId);
$payout = $customer->payouts->create(payoutRequest);

Comercio
$payout = $openpay->payouts->create(payoutRequest);
?>
```

```java
//Cliente
openpayAPI.payouts().create(String customerId, CreateCardPayoutParams request);

//Comercio
openpayAPI.payouts().create(CreateCardPayoutParams request);
```

```csharp
//Cliente
openpayAPI.PayoutService.Create(string customer_id, PayoutRequest request);

//Comercio
openpayAPI.PayoutService.Create(PayoutRequest request);
```

```javascript
// Comercio
openpay.payouts.create(payoutRequest, callback);

// Cliente
openpay.customers.payouts.create(customerId, payoutRequest, callback);
```

```ruby
#Cliente
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash, customer_id)

#Comercio
@payouts=@openpay.create(:payouts)
@payouts.create(request_hash)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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

Envío un pago tarjeta de débito. En dado caso que la tarjeta usada no sea débito los fondos se regresarán a la cuenta de donde fueron retirados.

###Petición 

Propiedad | Descripción
--------- | -----
method|***string*** (requerido) <br/>Debe contener el valor **card**.
[card](#objeto-tarjeta) | ***objeto*** (requerido) <br/>Datos de la tarjeta a la que se enviarán los fondos. <br/><br/> **card_number**.- Número de tarjeta de crédito a la que se enviarán los fondos <br/>**holder_name**.- Nombre del tarjeta habiente propietario de la tarjeta.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del pago o una [respuesta de error](#objeto-error).

##Obtener un pago
> Definición

```shell
Comercio
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts/{TRANSACTION_ID}

Comercio
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts/{TRANSACTION_ID}
```

```php
<?
Comercio
$payout = $openpay->payouts->get(transactionId);

Cliente
$customer = $openpay->customers->get(customerId);
$payout = $customer->payouts->get(transactionId);
?>
```

```java
//Cliente
openpayAPI.payouts().get(String customerId, String transactionId);

//Comercio
openpayAPI.payouts().get(String transactionId);
```

```csharp
//Cliente
openpayAPI.PayoutService.Get(string customer_id, string transaction_id);

//Comercio
openpayAPI.PayoutService.Get(string transaction_id);
```

```javascript
// Comercio
openpay.payouts.get(transactionId, callback);

// Cliente
openpay.customers.payouts.get(customerId, transactionId, callback);
```

```ruby
#Cliente
@payouts=@openpay.create(:payouts)
@payouts.get(transaction_id, customer_id)

#Comercio
@payouts=@openpay.create(:payouts)
@payouts.get(transaction_id)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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

Regresa la información de un pago realizado. Es necesario conocer el id del pago.

###Petición

Propiedad | Descripción
--------- | ------
transaction_id| _**string**_ (requerido, longitud = 45)<br/>Identificador del pago a consultar.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del pago o una [respuesta de error](#objeto-error).

##Cancelar un pago
> Definición

```shell
Comercio
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts/{TRANSACTION_ID}

Comercio
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts/{TRANSACTION_ID}
```

```php
<?
Comercio
$payout = $openpay->payouts->delete(transactionId);

Cliente
$customer = $openpay->customers->get(customerId);
$payout = $customer->payouts->delete(transactionId);
?>
```

```java
//Cliente
openpayAPI.payouts().cancel(String customerId, String transactionId);

//Comercio
openpayAPI.payouts().cancel(String transactionId);
```

```csharp
//Cliente
openpayAPI.PayoutService.Cancel(string customer_id, string transaction_id);

//Comercio
openpayAPI.PayoutService.Cancel(string transaction_id);
```

```javascript
// Comercio
openpay.payouts.delete(transactionId, callback);

// Cliente
openpay.customers.payouts.delete(customerId, transactionId, callback);
```

```ruby
#Cliente
@payouts=@openpay.create(:payouts)
@payouts.delete(transaction_id, customer_id)

#Comercio
@payouts=@openpay.create(:payouts)
@payouts.delete(transaction_id)
```

> Ejemplo de petición con cliente

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
openpay.customers.payouts.delete('ag4nktpdzebjiye1tlze', 'trozeipf364jqrsbt3ej', function(error, payout) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@payouts=@openpay.create(:payouts)

response_hash=@payouts.delete("trozeipf364jqrsbt3ej", "asynwirguzkgq2bizogo")
```

> Ejemplo de respuesta

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
   "order_id":"oid-00021",
   "customer_id":"asynwirguzkgq2bizogo"
}
```

Cancela un pago previamente programado en estado in_progress, es decir el pago no debe estar completado. Es necesario conocer el id del pago.

###Petición

Propiedad | Descripción
--------- | ------
transaction_id| _**string**_ (requerido, longitud = 45)<br/>Identificador del pago a cancelar.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del pago cancelado o una [respuesta de error](#objeto-error).

##Listado de pagos

> Definición


```shell
Comercio
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/payouts

Comercio
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/payouts
```

```php
<?
Comercio
$payoutList = $openpay->payouts->getList(searchParams);

Cliente
$customer = $openpay->customers->get(customerId);
$payoutList = $customer->payouts->getList(searchParams);
?>
```

```java
//Cliente
openpayAPI.payouts().list(String customerId, SearchParams request);

//Comercio
openpayAPI.payouts().list(SearchParams request);
```

```csharp
//Cliente
openpayAPI.PayoutService.List(string customer_id, SearchParams request = null);

//Comercio
openpayAPI.PayoutService.List(SearchParams request = null);
```

```javascript
// Comercio
openpay.payouts.list(callback);
openpay.payouts.list(searchParams, callback);

// Cliente
openpay.customers.payouts.list(customerId, callback);
openpay.customers.payouts.list(customerId, searchParams, callback);
```

```ruby
#Cliente
@payouts=@openpay.create(:payouts)
@payouts.all(customer_id)

#Comercio
@payouts=@openpay.create(:payouts)
@payouts.all
```

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
Obtiene un listado de los pagos realizados a nivel comercio o cliente.

###Petición
Puede realizar una búsqueda utilizando los siguiente parámetros como filtros.

Propiedad | Descripción
--------- | ------
creation| ***date*** <br/>Igual a la fecha de creación. Formato yyyy-mm-dd
creation[gte]| ***date*** <br/>Mayor a la fecha de creación. Formato yyyy-mm-dd
creation[lte]| ***date*** <br/>Menor a la fecha de creación. Formato yyyy-mm-dd
offset| ***numeric*** <br/>Número de registros a omitir al inicio, por defecto 0.
limit| ***numeric*** <br/>Número de registros que se requieren, por defecto 10.
amount| ***numeric*** <br/>Igual al monto.
amount[gte] | ***numeric*** <br/>Mayor o igual al monto.
amount[lte] | ***numeric*** <br/>Menor o igual al monto.
payout_type | ***string (opcional, ALL, AUTOMATIC o MANUAL)***  <br/>Tipo de payout usado para filtrar las transacciones

###Respuesta

Regresa un listado de [objetos de transacción](#objeto-transacción) de los pagos en orden descendente por fecha de creación.

##Resumen de Pagos

> Definición

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

> Ejemplo de petición

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

> Ejemplo de respuesta

```json
{
  "in": 2700,
  "out": 2400,
  "charged_adjustments": 0,
  "refunded_adjustments": 0
}
```

Regresa el resumen de un pago realizado. Es necesario conocer el id del pago.

###Petición

Propiedad | Descripción
--------- | ------
transaction_id| _**string**_ (requerido, longitud = 45)<br/>Identificador del pago a consultar.

###Respuesta
Regresa un [objeto de resumen de pagos](#objeto-resumen-de-pagos) con el resumen del pago o una [respuesta de error](#objeto-error).

##Objeto Resumen de Pagos

> Ejemplo de objeto 

```json
{
   "in":2700,
   "out":2400,
   "charged_adjustments":0,
   "refunded_adjustments":0
}
```

Propiedad | Descripción
--------- | ------
in | ***numeric*** <br/> Monto total de entrada, Debe ser una cantidad con hasta 2 dígitos decimales.
out | ***numeric*** <br/> Monto total de salida, Debe ser una cantidad con hasta 2 dígitos decimales.
charged_adjustments | ***numeric*** <br/> Monto total de cargos de ajuste, Debe ser una cantidad con hasta 2 dígitos decimales.
refunded_adjustments | ***numeric*** <br/> Monto total de cargos de devolución, Debe ser una cantidad con hasta 2 dígitos decimales.

##Detalle de Pagos

> Definición

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

> Ejemplo de petición

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

> Ejemplo de respuesta

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

Regresa el listado las transacciones involucradas en un pago realizado. Es necesario conocer el id del pago.

###Petición

Propiedad | Descripción
--------- | ------
transaction_id| _**string**_ (requerido, longitud = 45)<br/>Identificador del pago a consultar.
detail_type| _**string**_ (***IN***, ***OUT***, ***CHARGED_ADJUSTMENTS***, ***REFUNDED_ADJUSTMENTS***) <br/>Tipo de detalle.
offset| _**numeric**_ <br/> Número de registros a omitir al inicio, por defecto 0.
limit| _**numeric**_ <br/> Número de registros que se requieren, por defecto 10.

###Respuesta
Regresa un listado de [objetos transacción](#objeto-transacci-n) o una [respuesta de error](#objeto-error).
