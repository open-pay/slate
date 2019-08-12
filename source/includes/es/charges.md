#Cargos
Los cargos se pueden realizar a tarjetas. A cada cargo se le asigna un identificador único en el sistema.

Los cargos a tarjeta puedes hacerlos a una tarjeta guardada usando el id de la tarjeta, usando un token o puedes enviar la información de la tarjeta al momento de la invocación.

##Con id de tarjeta o token

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "source_id" : "kdx205scoizh93upqbte",
   "method" : "card",
   "amount" : 666,
   "currency" : "COP",
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-12324",
   "device_session_id" : "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f",
   "iva": "10",
   "customer" : {
        "name" : "Cliente Colombia",
        "last_name" : "Vazquez Juarez",
        "phone_number" : "4448936475",
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
   	 'phone_number' => '571627926831',
   	 'email' => 'juan.vazquez@empresa.com.mx');

$chargeRequest = array(
    'method' => 'card',
    'source_id' => 'kqgykn96i7bcs1wwhvgw',
    'amount' => 100,
    'currency' => 'COP'
    'description' => 'Cargo inicial a mi merchant',
    'order_id' => 'oid-00051',
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
customer.setPhoneNumber("571627926831");
customer.setEmail("juan.vazquez@empresa.com.mx");

request.cardId("kqgykn96i7bcs1wwhvgw"); // =source_id
request.amount(new BigDecimal("100.00"));
request.currency("COP");
request.description("Cargo inicial a mi merchant");
request.orderId("oid-00051");
request.deviceSessionId("kR1MiQhz2otdIuUlQkbEyitIqVMiI16f");
request.setCustomer(customer);

Charge charge = api.charges().create(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ChargeRequest request = new ChargeRequest();
Customer customer = new Customer();
customer.Name = "Juan";
customer.LastName = "Vazquez Juarez";
customer.PhoneNumber = "571627926831";
customer.Email = "juan.vazquez@empresa.com.mx";

request.Method = "card";
request.SourceId = "kwkoqpg6fcvfse8k8mg2";
request.Amount = new Decimal(100.00);
request.Currency = "COP";
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
   'currency' : 'COP',
   'description' : 'Cargo inicial a mi cuenta',
   'order_id' : 'oid-00051',
   'device_session_id' : 'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f',
   'customer' : {
   	    'name' : 'Juan',
   	    'last_name' : 'Vazquez Juarez',
   	    'phone_number' : '571627926831',
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
    "phone_number" => "571627926831",
    "email" => "juan.vazquez@empresa.com.mx"
}

request_hash={
    "method" => "card",
    "source_id" => "kqgykn96i7bcs1wwhvgw",
    "amount" => 100.00,
    "currency" => "COP",
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
    "iva": "10",
    "creation_date": "2019-08-12T12:36:56-05:00",
    "operation_date": "2019-08-12T12:36:56-05:00",
    "description": "Ejemplo cargo",
    "error_message": null,
    "order_id": "oid-12330",
    "currency": "COP",
    "amount": 666.00,
    "customer": {
        "name": "Cliente Colombia",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.com.mx",
        "phone_number": "4448936475",
        "address": null,
        "creation_date": "2019-08-12T12:36:56-05:00",
        "external_id": null,
        "clabe": null
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

<aside class="notice">
Para utilizar esta característica es necesario enviar como parte del contenido de la transacción, la propiedad <code>metadata</code>, el cual contendrá un listado de campos personalizados de antrifraude, con la información propia del comercio que se desea tomar en cuenta al momento de validar y aplicar un cargo. Póngase en contacto con el departamento de soporte de Openpay para habilitar esta funcion. </br>
</aside>


###Petición

Propiedad | Descripción
--------- | -----
method|***string*** (requerido) <br/>Debe contener el valor **card** para indicar que el cargo se hará de una tarjeta.
source_id | ***string*** (requerido, longitud = 45) <br/>ID de la tarjeta guardada o el id del token creado de donde se retirarán los fondos.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
cvv2 | ***numeric*** (requerido, longitud = 3-4) <br/>Código de seguridad como aparece en la parte de atrás de la tarjeta. Generalmente 3 dígitos.<br/>Se utiliza solo para cargos con [Tarjetas Guardadas](#crear-una-tarjeta).
currency | ***string*** (opcional) <br/>Tipo de moneda del cargo. Por el momento solo se soportan 1 tipo de moneda: Pesos Colombianos(COP).
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.
device_session_id |  ***string*** (requerido, longitud = 255) <br/>Identificador del dispositivo generado con la herramienta antifraudes
[customer](#crear-un-nuevo-cliente)|***objeto*** (requerido) <br/>Información del cliente al que se le realiza el cargo. Se puede ocupar los mismos parámetros usados en la creación de un cliente pero no se creará una cuenta al cliente. <br/><br/> **Nota:** Este parámetro solo se puede utilizar creando el cargo a nivel comercio<br/><br/>Si desea crear un cliente y llevar un historial de sus cargos consulte como [crear un cliente](#crear-un-nuevo-cliente) y realice el cargo a nivel cliente.
[payment_plan](#objeto-paymentplan)|***objeto*** (opcional) <br/>Datos del plan de meses sin intereses que se desea utilizar en el cargo. Ver [Objeto PaymentPlan](#objeto-paymentplan).
metadata |  ***list(key, value)*** (opcional) <br/>Listado de campos personalizados de antifraude, estos campos deben de apegarse a las [reglas para creación de campos personalizados de antifraude](#reglas-para-creación-de-campos-personalizados-de-antifraude)


###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).

##Con redireccionamiento

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method" : "card",
   "amount" : 100,
   "currency":"COP",
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-11152",
   "customer" : {
        "name" : "Juan",
        "last_name" : "Vazquez Juarez",
        "phone_number" : "4423456723",
        "email" : "juan.vazquez@empresa.com.mx"
   },
   "iva": "10",
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
    "currency"=> "COP",
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
   'currency': 'COP',
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
    "currency" => "COP",
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
    "customer" => customer_hash,
    "send_email" => false,
    "confirm" => false,
    "redirect_url" => "http://www.openpay.mx/index.html"
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
    "iva": "10",
    "creation_date": "2019-08-12T12:47:41-05:00",
    "operation_date": "2019-08-12T12:47:41-05:00",
    "description": "Cargo inicial a mi cuenta",
    "error_message": null,
    "order_id": "oid-11153",
    "payment_method": {
        "type": "redirect",
        "url": "https://sandbox-api.openpay.mx/v1/mpixehq7z4xupfwoohrm/charges/tro1ezxbfn5c8lvzhfcr/card_capture"
    },
    "currency": "COP",
    "amount": 100.00,
    "customer": {
        "name": "Juan",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.com.mx",
        "phone_number": "4423456723",
        "address": null,
        "creation_date": "2019-08-12T12:47:41-05:00",
        "external_id": null,
        "clabe": null
    }
}
```

Este tipo de cargo no requiere una tarjeta guardada o que hayas generado un token.

###Petición

Propiedad | Descripción
--------- | -----
method|***string*** (requerido en card) <br/>Debe contener el valor **card** para indicar que el cargo se hará de una tarjeta.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.
[customer](#crear-un-nuevo-cliente)|***objeto*** (requerido) <br/>Información del cliente al que se le realiza el cargo. Se puede ocupar los mismos parámetros usados en la creación de un cliente pero no se creará una cuenta al cliente. <br/><br/> **Nota:** Este parámetro solo se puede utilizar creando el cargo a nivel comercio<br/><br/>Si desea crear un cliente y llevar un historial de sus cargos consulte como [crear un cliente](#crear-un-nuevo-cliente) y realice el cargo a nivel cliente.
confirm |  ***boolean*** (requerido en false) <br/>El valor `false` indica que se trata de un cargo con terminal virtual.
send_email | ***boolean*** (opcional) <br/>Indica si se desea enviar un email que direccione al formulario de pago de openpay.
redirect_url | ***string*** (requerido) <br/>Indica la url a la que redireccionar despues de una transaccion exitosa en el fomulario de pago de openpay.
currency | ***string*** (requerido) <br/> Moneda usada en la operación

###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).

##Confirmar un cargo

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/capture

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}/capture
```

```php
<?
Comercio
$charge = $openpay->charges->get(transactionId);
$charge->capture(captureData);

Cliente
$customer = $openpay->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
$charge->capture(captureData);
?>
```

```java
//Cliente
openpayAPI.charges().confirmCapture(String customerId, ConfirmCaptureParams request);

//Comercio
openpayAPI.charges().confirmCapture(ConfirmCaptureParams request);
```

```csharp
//Cliente
openpayAPI.ChargeService.Capture(string customer_id, string transaction_id, Decimal? amount);

//Comercio
openpayAPI.ChargeService.Capture(string transaction_id, Decimal? amount);
```

```javascript
// Comercio
openpay.charges.capture(transactionId, captureRequest, callback);

// Cliente
openpay.customers.charges.capture(customerId, transactionId, captureRequest, callback);
```

```ruby
#Cliente
@charges=@openpay.create(:charges)
@charges.capture(transaction_id, customer_id)

#Comercio
@charges=@openpay.create(:charges)
@charges.capture(transaction_id)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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
   "currency":"COP",
   "creation_date":"2014-05-26T14:00:17-05:00",
   "operation_date":"2014-05-26T14:00:17-05:00",
   "description":"Cargo inicial a mi cuenta",
   "error_message":null,
   "order_id":null,
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```
Confirmar un cargo creado con la propieda de <code>capture = "false"</code>,  este método es la segunda parte de la [creación de un cargo con tarjeta (id o token)](#con-id-de-tarjeta-o-token) y puede confirmar el monto capturado en la primera llamada o un monto menor.

<aside class="notice">
**Nota:** Solo se pueden confirmar cargos a tarjeta. Para cancelar el cargo creado se debe hacer una llamada al método <a href="/#devolver-un-cargo">Devolver un cargo</a>
</aside>


###Petición

Propiedad | Descripción
--------- | -----
amount | ***numeric*** (opcional) <br/>Cantidad a confirmar. Puede ser menor o igual al monto capturado hasta dos dígitos decimales.


###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).

##Devolver un cargo

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/refund

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}/refund
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

> Ejemplo de respuesta

```json
{
    "id": "troztz0scxl7berfxju0",
    "authorization": "332225182",
    "operation_type": "in",
    "method": "card",
    "transaction_type": "charge",
    "card": {
        "type": "debit",
        "brand": "visa",
        "address": null,
        "card_number": "457562XXXXXX0326",
        "holder_name": "Jorge Lopez",
        "expiration_year": "19",
        "expiration_month": "12",
        "allows_charges": true,
        "allows_payouts": false,
        "bank_name": "BBVA COLOMBIA",
        "bank_code": "000"
    },
    "status": "completed",
    "conciliated": true,
    "creation_date": "2019-08-12T12:51:56-05:00",
    "operation_date": "2019-08-12T12:51:56-05:00",
    "description": "Cargo inicial a mi cuenta",
    "error_message": null,
    "order_id": "oid-12317",
    "refunds": [
        {
            "operation_date": "2019-08-12T13:00:23-05:00",
            "authorization": "1091286572",
            "amount": 100.00,
            "status": "completed",
            "conciliated": true,
            "id": "tr76epoxpjwsqcdynpmb",
            "description": "Reembolso",
            "currency": "COP"
        }
    ],
    "refund": {
        "operation_date": "2019-08-12T13:00:23-05:00",
        "authorization": "1091286572",
        "amount": 100.00,
        "operation_type": "out",
        "method": "card",
        "transaction_type": "refund",
        "status": "completed",
        "conciliated": true,
        "id": "tr76epoxpjwsqcdynpmb",
        "creation_date": "2019-08-12T13:00:23-05:00",
        "description": "Reembolso",
        "customer": {
            "name": "Cliente Colombia",
            "last_name": "Vazquez Juarez",
            "email": "juan.vazquez@empresa.com.mx",
            "phone_number": "4448936475",
            "address": null,
            "creation_date": "2019-08-12T12:51:56-05:00",
            "external_id": null,
            "clabe": null
        },
        "currency": "COP"
    },
    "currency": "COP",
    "amount": 100.00,
    "customer": {
        "name": "Cliente Colombia",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.com.mx",
        "phone_number": "4448936475",
        "address": null,
        "creation_date": "2019-08-12T12:51:56-05:00",
        "external_id": null,
        "clabe": null
    },
    "fee": {
        "amount": 5.4000,
        "tax": 0.8640,
        "currency": "COP"
    }
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
amount | ***numeric*** (opcional) <br/>Cantidad a reembolsar. Debe ser una cantidad mayor a cero y menor o igual al cargo original, con hasta dos dígitos decimales.


###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).


##Obtener un cargo
> Definición

```shell
Comercio
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}

Comercio
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}
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
    "currency": "COP",
    "amount": 666.00,
    "customer": {
        "name": "Cliente Colombia",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.com.mx",
        "phone_number": "4448936475",
        "address": null,
        "creation_date": "2019-08-12T13:02:18-05:00",
        "external_id": null,
        "clabe": null
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
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Comercio
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
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
        "currency": "COP",
        "amount": 666.00,
        "customer": {
            "name": "Cliente Colombia",
            "last_name": "Vazquez Juarez",
            "email": "juan.vazquez@empresa.com.mx",
            "phone_number": "4448936475",
            "address": null,
            "creation_date": "2019-08-12T13:02:18-05:00",
            "external_id": null,
            "clabe": null
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
