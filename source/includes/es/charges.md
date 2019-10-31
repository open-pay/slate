#Cargos
Los cargos se pueden realizar a tarjetas y PSE. A cada cargo se le asigna un identificador único en el sistema.

Los cargos a tarjeta puedes hacerlos a una tarjeta guardada usando el id de la tarjeta, usando un token o puedes enviar la información de la tarjeta al momento de la invocación.

##Con id de tarjeta o token

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/charges

Cliente
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Comercio
$openpay->charges->create(chargeRequest);

Cliente
$customer = $openpay->customers->get($customerId);
$customer->charges->create(chargeRequest);
?>
```

```java
//Cliente
openpayAPI.charges().create(String customerId, CreateCardChargeParams request);

//Comercio
openpayAPI.charges().create(CreateCardChargeParams request);
```

```javascript
// Comercio
openpay.charges.create(chargeRequest, callback);

// Cliente
openpay.customers.charges.create(customerId, chargeRequest, callback);
```

```csharp
//Cliente
openpayAPI.ChargeService.Create(string customer_id, ChargeRequest request);

//Comercio
openpayAPI.ChargeService.Create(ChargeRequest request);
```

```ruby
#Cliente
@charges=@openpay.create(:charges)
@charges.create(request_hash, customer_id)

#Comercio
@charges=@openpay.create(:charges)
@charges.create(request_hash)
```

> Ejemplo de petición con comercio

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln3bqtms6o3kck2f/charges \
   -u sk_e562c42a6q384b2ab02cd47d2n301uwk: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "source_id" : "kdx205scoizh93upqbte",
   "method" : "card",
   "amount" : 716,
   "currency" : "COP",
   "iva" : "10",
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-12324",
   "device_session_id" : "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f",
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
    'currency' => 'COP',
    'iva' => '10',
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
request.iva("10");
request.description("Cargo inicial a mi merchant");
request.orderId("oid-00051");
request.deviceSessionId("kR1MiQhz2otdIuUlQkbEyitIqVMiI16f");
request.setCustomer(customer);

Charge charge = api.charges().create(request);
```

```javascript
var chargeRequest = {
   'source_id' : 'kqgykn96i7bcs1wwhvgw',
   'method' : 'card',
   'amount' : 716,
   'currency' : 'COP',
   'iva' : '10',
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
request.Iva = "10";
request.Description = "Cargo inicial a mi merchant";
request.OrderId = "oid-00051";
request.DeviceSessionId = "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f";
request.Customer = customer;

Charge charge = api.ChargeService.Create(request);
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
    "iva" => "10",
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
    "device_session_id" => "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f",
    "customer" => customer_hash
}

response_hash=@charges.create(request_hash.to_hash)
```

> Ejemplo de respuesta

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
    "creation_date": "2019-08-12T12:36:56-05:00",
    "operation_date": "2019-08-12T12:36:56-05:00",
    "description": "Ejemplo cargo",
    "error_message": null,
    "order_id": "oid-12330",
    "amount": 716,
    "currency": "COP",
    "iva": "10",
    "customer": {
        "name": "Cliente Colombia",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.co",
        "phone_number": "4448936475",
        "address": null,
        "creation_date": "2019-08-12T12:36:56-05:00",
        "external_id": null
    },
    "fee": {
        "amount": 21.81,
        "tax": 3.4896,
        "currency": "COP"
    }
}
```

Este tipo de cargo requiere una tarjeta guardada o que hayas generado un token. Para guardar tarjetas consulta [como crear una tarjeta](#crear-una-tarjeta) y para usar tokens consulta la sección [creación de tokens](#crear-un-nuevo-token).

Una vez que tengas una tarjeta guardada o un token usa la propiedad <code>source_id</code> para enviar el identificador.

La propiedad <code>device_session_id</code> deberá ser generada desde el API JavaScript, véase [Fraud detection using device data](https://github.com/open-pay/openpay-js#fraud-detection-using-device-data).

<aside class="notice">
Puedes realizar el cargo a la cuenta del comercio o a la cuenta de un cliente. </br>
</aside>

***Sistema antifraude personalizado***</br>
Es posible enviar información adicional a la plataforma Openpay para incrementar su base de conocimientos, esto le permitirá aplicar reglas personalizadas de acuerdo al giro del comercio y de manera oportuna, con el propósito de detectar con la mayor efectividad posible los intentos de fraude.



###Petición

Propiedad | Descripción
--------- | -----
method|***string*** (requerido) <br/>Debe contener el valor **card** para indicar que el cargo se hará de una tarjeta.
source_id | ***string*** (requerido, longitud = 45) <br/>ID de la tarjeta guardada o el id del token creado de donde se retirarán los fondos.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero.
currency | ***string*** (requerido) <br/>Tipo de moneda del cargo. Por el momento solo se soportan 1 tipo de moneda: Pesos Colombianos(COP).
iva | ***string*** (requerido) <br/>Debe contener el valor de IVA, es campo solo informativo, no tiene ningún efecto sobre el campo amount.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.
device_session_id |  ***string*** (requerido, longitud = 255) <br/>Identificador del dispositivo generado con la herramienta antifraudes
[customer](#crear-un-nuevo-cliente)|***objeto*** (requerido) <br/>Información del cliente al que se le realiza el cargo. Se puede ocupar los mismos parámetros usados en la creación de un cliente pero no se creará una cuenta al cliente. <br/><br/> **Nota:** Este parámetro solo se puede utilizar creando el cargo a nivel comercio<br/><br/>Si desea crear un cliente y llevar un historial de sus cargos consulte como [crear un cliente](#crear-un-nuevo-cliente) y realice el cargo a nivel cliente.


###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).

##Con redireccionamiento

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/charges

Cliente
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Comercio
$openpay->charges->create(chargeRequest);

Cliente
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
// Comercio
openpay.charges.create(chargeRequest, callback);

// Cliente
openpay.customers.charges.create(customerId, chargeRequest, callback);
```

```csharp
//Cliente
openpayAPI.ChargeService.Create(string customer_id, ChargeRequest request);

//Comercio
openpayAPI.ChargeService.Create(ChargeRequest request);
```

```ruby
#Cliente
@charges=@openpay.create(:charges)
@charges.create(request_hash, customer_id)

#Comercio
@charges=@openpay.create(:charges)
@charges.create(request_hash)
```

> Ejemplo de petición con comercio

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln3bqtms6o3kck2f/charges \
   -u sk_e562c42a6q384b2ab02cd47d2n301uwk: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method" : "card",
   "amount" : 716,
   "currency": "COP",
   "iva" : "28",
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-11152",
   "customer" : {
        "name" : "Juan",
        "last_name" : "Vazquez Juarez",
        "phone_number" : "4423456723",
        "email" : "juan.vazquez@empresa.co"
   },
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
    'method' : 'card',
    'amount' => 716,
    'currency' => 'COP',
    'iva' => '28',
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateCardChargeParams request = new CreateCardChargeParams();
Customer customer = new Customer();
customer.setName("Juan");
customer.setLastName("Vazquez Juarez");
customer.setPhoneNumber("4423456723");
customer.setEmail("juan.vazquez@empresa.co");

request.amount(new BigDecimal("716.00"));
request.currency("COP");
request.iva("16");
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
request.Currency = "COP";
request.Iva = "16";
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
   'currency' : 'COP',
   'iva' : '16',
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
    "iva" => "16",
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
    "customer" => customer_hash,
    "send_email" => false,
    "confirm" => false,
    "redirect_url" => "http://www.openpay.co/index.html"
}

response_hash=@charges.create(request_hash.to_hash)
```

> Ejemplo de respuesta

```json

{
    "id": "tro1ezxbfn5c8lvzhfcr",
    "authorization": null,
    "operation_type": "in",
    "method": "card",
    "transaction_type": "charge",
    "status": "charge_pending",
    "conciliated": false,
    "creation_date": "2019-08-12T12:47:41-05:00",
    "operation_date": "2019-08-12T12:47:41-05:00",
    "description": "Cargo inicial a mi cuenta",
    "error_message": null,
    "order_id": "oid-11153",
    "payment_method": {
        "type": "redirect",
        "url": "https://sandbox-api.openpay.co/v1/mpixehq7z4xupfwoohrm/charges/tro1ezxbfn5c8lvzhfcr/card_capture"
    },
    "amount": 716,
    "currency": "COP",
    "iva": "10",
    "customer": {
        "name": "Juan",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.co",
        "phone_number": "4423456723",
        "address": null,
        "creation_date": "2019-08-12T12:47:41-05:00",
        "external_id": null
    }
}
```

Este tipo de cargo no requiere una tarjeta guardada o que hayas generado un token.

###Petición

Propiedad | Descripción
--------- | -----
method|***string*** (requerido en card) <br/>Debe contener el valor **card** para indicar que el cargo se hará de una tarjeta.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero.
currency | ***string*** (requerido) <br/>Tipo de moneda del cargo. Por el momento solo se soportan 1 tipo de moneda: Pesos Colombianos(COP).
iva | ***string*** (requerido) <br/>Debe contener el valor de IVA, es campo solo informativo, no tiene ningún efecto sobre el campo amount.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.
[customer](#crear-un-nuevo-cliente)|***objeto*** (requerido) <br/>Información del cliente al que se le realiza el cargo. Se puede ocupar los mismos parámetros usados en la creación de un cliente pero no se creará una cuenta al cliente. <br/><br/> **Nota:** Este parámetro solo se puede utilizar creando el cargo a nivel comercio<br/><br/>Si desea crear un cliente y llevar un historial de sus cargos consulte como [crear un cliente](#crear-un-nuevo-cliente) y realice el cargo a nivel cliente.
confirm |  ***boolean*** (requerido en false) <br/>El valor `false` indica que se trata de un cargo con terminal virtual.
send_email | ***boolean*** (opcional) <br/>Indica si se desea enviar un email que direccione al formulario de pago de openpay.
redirect_url | ***string*** (requerido) <br/>Indica la url a la que redireccionar despues de una transaccion exitosa en el fomulario de pago de openpay.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).

##Cargo en tienda

> Definición

```plaintext
Comercio
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/charges

Cliente
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Comercio
$openpay->charges->create(chargeRequest);

Cliente
$customer = $openpay->customers->get(customerId);
$customer->charges->create(chargeRequest;
?>
```

```java
//Cliente
openpayAPI.charges().create(String customerId, CreateStoreChargeParams request);

//Comercio
openpayAPI.charges().create(CreateStoreChargeParams request);
```

```csharp
//Cliente
openpayAPI.ChargeService.Create(string customer_id, ChargeRequest request);

//Comercio
openpayAPI.ChargeService.Create(ChargeRequest request);
```

```javascript
//Comercio
openpay.charges.create(chargeRequest, callback);

//Cliente
openpay.customers.charges.create(customerId, chargeRequest, callback);
```

```ruby
#Cliente
@charges=@openpay.create(:charges)
@charges.create(request_hash, customer_id)

#Comercio
@charges=@openpay.create(:charges)
@charges.create(request_hash)
```

> Ejemplo de petición con cliente

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method" : "store",
   "amount" : 100,
   "currency" : "COP",
   "iva" : "10",
   "description" : "Cargo con tienda",
   "order_id" : "oid-00053",
   "due_date" : "2018-05-28T13:45:00"
}'
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$chargeRequest = array(
    'method' => 'store',
    'amount' => 100,
    'currency' => 'COP',
    'iva' => '10',
    'description' => 'Cargo con tienda',
    'order_id' => 'oid-00053',
    'due_date' => '2018-05-28T13:45:00');

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Calendar dueDate = Calendar.getInstance();
dueDate.set(2018, 5, 28, 13, 45, 0);
CreateStoreChargeParams request = new CreateStoreChargeParams();
request.amount(new BigDecimal("100.00"));
request.currency("COP");
request.iva("10");
request.description("Cargo con tienda");
request.orderId("oid-00053"
request.dueDate(dueDate.getTime());

Charge charge = api.charges().create("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ChargeRequest request = new ChargeRequest();
request.Method = "store";
request.Amount = new Decimal(100);
request.Currency = "COP";
request.Iva = "10";
request.Description = "Cargo con tienda";
request.OrderId = "oid-00053";
request.DueDate = new DateTime(2018, 5, 28, 13, 45, 0);

Charge charge = api.ChargeService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var storeChargeRequest = {
   'method' : 'store',
   'amount' : 100,
   'currency' : 'COP',
   'iva' : '10',
   'description' : 'Cargo con tienda',
   'order_id' : 'oid-00053',
   'due_date' : '2018-05-28T13:45:00'
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
     "currency" => "COP",
     "iva" => "10",
     "description" => "Cargo con tienda",
     "order_id" => "oid-00053",
     "due_date" => "2018-05-28T13:45:00"
   }

response_hash=@charges.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Ejemplo de respuesta

```json
{
   "id":"trnirkiyobo5qfex55ef",
   "amount":100.00,
   "currency":"COP",
   "iva":"10",
   "authorization":null,
   "method":"store",
   "operation_type":"in",
   "transaction_type":"charge",
   "status":"in_progress",
   "creation_date":"2018-05-26T13:48:25-05:00",
   "operation_date":"2018-05-26T13:48:25-05:00",
   "due_date":"2018-05-28T13:45:00-05:00",
   "description":"Cargo con tienda",
   "error_message":null,
   "order_id":"oid-00053",
   "customer_id":"ag4nktpdzebjiye1tlze",
   "payment_method":{
      "type":"store",
      "reference":"000020TRNIRKIYOBO5QFEX55EF0100009",
      "paybin_reference":"0101990000001065",
      "barcode_url":"https://sandbox-api.openpay.co/barcode/000020TRNIRKIYOBO5QFEX55EF0100009?width=1&height=45&text=false",
      "barcode_paybin_url":"https://sandbox-api.openpay.co/barcode/0101990000001065?width=1&height=45&text=false"
   }
}
```

Para un pago en una tienda de conveniencia se debe crear un petición de tipo cargo indicando como método **store**. Esto generará una respuesta con un número de referencia y una URL a un código de barras, los cuales debes de utilizar para crear un recibo a tu cliente y que con él pueda realizar el pago en una de las tienda de conveniencia aceptadas. El código de barras es de tipo Code 128.

###Petición

Propiedad | Descripción
--------- | -----
method|***string*** (requerido) <br/>Debe contener el valor **store** para indicar que el pago se hará en tienda.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
currency | ***string*** (requerido) <br/>Tipo de moneda del pago. Por el momento solo se soportan 1 tipo de moneda: Pesos Colombianos(COP).
iva | ***string*** (requerido) <br/>Debe contener el valor de IVA, es campo solo informativo, no tiene ningún efecto sobre el campo amount.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.
due_date | ***datetime*** (opcional) <br/>Fecha de vigencia para hacer el pago en la tienda en formato ISO 8601. <br/><br/>Ejemplo (UTC): 2014-08-01T00:50:00Z <br/>***Nota:*** Del lado del servidor se cambiara a hora central<br/><br/>Ejemplo (Central Time): 2014-08-01T11:51:23-05:00
[customer](#crear-un-nuevo-cliente)|***objeto*** (requerido) <br/>Información del cliente al que se le realiza el cargo. Se puede ocupar los mismos parámetros usados en la creación de un cliente pero no se creará una cuenta al cliente. <br/><br/> **Nota:** Este parámetro solo se puede utilizar creando el cargo a nivel comercio<br/><br/>Si desea crear un cliente y llevar un historial de sus cargos consulte como [crear un cliente](#crear-un-nuevo-cliente) y realize el cargo a nivel cliente.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).
currency | ***string*** (requerido) <br/> Moneda usada en la operación

###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).



##Devolver un cargo

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/refund

Cliente
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}/refund
```

```php
<?
Comercio
$charge = $openpay->charges->get(transactionId);
$charge->refund(refundData);

Cliente
$customer = $openpay->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
$charge->refund(refundData);
?>
```

```java
//Cliente
openpayAPI.charges().refund(String customerId, RefundParams request);

//Comercio
openpayAPI.charges().refund(RefundParams request);
```

```csharp
//Cliente
openpayAPI.ChargeService.Refund(string customer_id, string transaction_id, string description);

//Comercio
openpayAPI.ChargeService.Refund(string transaction_id, string description);
```

```javascript
// Comercio
openpay.charges.refund(transactionId, refundRequest, callback);

// Cliente
openpay.customers.charges.refund(customerId, transactionId, refundRequest, callback);
```

```ruby
#Cliente
@charges=@openpay.create(:charges)
@charges.refund(transaction_id, request_hash, customer_id)

#Comercio
@charges=@openpay.create(:charges)
@charges.refund(transaction_id, request_hash)
```

> Ejemplo de petición con cliente

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges/tr6cxbcefzatd10guvvw/refund \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
RefundParams request = new RefundParams();
request.chargeId("tr6cxbcefzatd10guvvw");
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

> Ejemplo de respuesta

```json
{
   "id":"tr6cxbcefzatd10guvvw",
   "amount":100.00,
   "currency":"COP",
   "iva":"10",
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
      "bank_name":"BANCO DE BOGOTÁ",
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
      "currency":"COP",
      "creation_date":"2018-05-26T13:56:21-05:00",
      "operation_date":"2018-05-26T13:56:21-05:00",
      "description":"devolucion",
      "error_message":null,
      "order_id":null,
      "customer_id":"ag4nktpdzebjiye1tlze"
   },
   "creation_date":"2018-05-26T11:56:25-05:00",
   "operation_date":"2018-05-26T11:56:25-05:00",
   "description":"Cargo inicial a mi cuenta",
   "error_message":null,
   "order_id":"oid-00052",
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```
Si deseas realizar una devolución de un cargo hecho a tarjeta puedes ocupar este método. El monto a devolver será por el total del cargo o un monto menor. Ten en cuenta que la devolución puede tardar en aparecer en el estado de cuenta de tu cliente de 1 a 3 días hábiles.

<aside class="notice">
**Nota:** Solo se pueden hacer devoluciones de cargos a tarjeta.
</aside>


###Petición

Propiedad | Descripción
--------- | -----
description | ***string*** (opcional, longitud = 250) <br/>Texto libre para describir motivo de la devolución.
amount | ***numeric*** (opcional) <br/>Cantidad a reembolsar. Debe ser una cantidad mayor a cero y menor o igual al cargo original.


###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).


##Obtener un cargo
> Definición

```shell
Comercio
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}

Comercio
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}
```

```php
<?
Comercio
$charge = $openpay->charges->get(transactionId);

Cliente
$customer = $openpay->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
?>
```

```java
//Cliente
openpayAPI.charges().get(String customerId, String transactionId);

//Comercio
openpayAPI.charges().get(String transactionId);
```

```csharp
//Cliente
openpayAPI.ChargeService.Get(string customer_id, string transaction_id);

//Comercio
openpayAPI.ChargeService.Get(string transaction_id);
```

```javascript
// Comercio
openpay.charges.get(transactionId, callback);

// Cliente
openpay.customers.charges.get(customerId, transactionId, callback);
```

```ruby
#Cliente
@charges=@openpay.create(:charges)
@charges.get(transaction_id, customerId)

#Comercio
@charges=@openpay.create(:charges)
@charges.get(transaction_id)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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
    "amount": 716,
    "currency": "COP",
    "iva": "10",
    "customer": {
        "name": "Cliente Colombia",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.co",
        "phone_number": "4448936475",
        "address": null,
        "creation_date": "2019-08-12T13:02:18-05:00",
        "external_id": null
    },
    "fee": {
        "amount": 21.8100,
        "tax": 3.4896,
        "currency": "COP"
    }
}
```

Regresa la información de un cargo generado en cualquier momento solo con conocer el id de cargo.

###Petición

Propiedad | Descripción
--------- | ------
transaction_id| _**string**_ (requerido, longitud = 45)<br/>Identificador del cargo a consultar.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).

##Listado de cargos

> Definición


```shell
Comercio
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/charges

Comercio
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Comercio
$chargeList = $openpay->charges->getList(searchParams);

Cliente
$customer = $openpay->customers->get(customerId);
$chargeList = $customer->charges->getList(searchParams);
?>
```

```java
//Cliente
openpayAPI.charges().list(String customerId, SearchParams request);

//Comercio
openpayAPI.charges().list(SearchParams request);
```

```csharp
//Cliente
openpayAPI.ChargeService.List(string customer_id, SearchParams request = null);

//Comercio
openpayAPI.ChargeService.List(SearchParams request = null);
```

```javascript
// Comercio
openpay.charges.list(callback);
openpay.charges.list(searchParams, callback);

// Cliente
openpay.customers.charges.list(customerId, callback);
openpay.customers.charges.list(customerId, searchParams, callback);
```

```ruby
#Cliente
@charges=@openpay.create(:charges)
@charges.all(customer_id)

#Comercio
@charges=@openpay.create(:charges)
@charges.all
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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
        "amount": 716,
        "currency": "COP",
        "iva": "10",
        "customer": {
            "name": "Cliente Colombia",
            "last_name": "Vazquez Juarez",
            "email": "juan.vazquez@empresa.co",
            "phone_number": "4448936475",
            "address": null,
            "creation_date": "2019-08-12T13:02:18-05:00",
            "external_id": null
        },
        "fee": {
          "amount": 21.8100,
          "tax": 3.4896,
          "currency": "COP"
        }
    }

]
```
Obtiene un listado de los cargos realizados por comercio o cliente.

###Petición
Puede realizar una búsqueda utilizando los siguiente parámetros como filtros.

Propiedad | Descripción
--------- | ------
order_id| ***string*** <br/>Identificador único de la orden generado por el comercio y asociado a la transaccion mediante el campo order_id de la petición del cargo.
creation| ***date*** <br/>Igual a la fecha de creación. Formato yyyy-mm-dd
creation[gte]| ***date*** <br/>Mayor a la fecha de creación. Formato yyyy-mm-dd
creation[lte]| ***date*** <br/>Menor a la fecha de creación. Formato yyyy-mm-dd
offset| ***numeric*** <br/>Número de registros a omitir al inicio, por defecto 0.
limit| ***numeric*** <br/>Número de registros que se requieren, por defecto 10.
amount| ***numeric*** <br/>Igual al monto.
amount[gte] | ***numeric*** <br/>Mayor o igual al monto.
amount[lte] | ***numeric*** <br/>Menor o igual al monto.
[status](#objeto-transaction-status) | ***TransactionStatus*** <br/>Estado de la transacción (IN_PROGRESS,COMPLETED,REFUNDED,CHARGEBACK_PENDING,CHARGEBACK_ACCEPTED,CHARGEBACK_ADJUSTMENT,CHARGE_PENDING,CANCELLED,FAILED).

###Respuesta

Regresa un arreglo de [objetos de transacción](#objeto-transacci-n) de los cargos en orden descendente por fecha de creación.
