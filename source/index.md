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
---

# Introducción

La API de Openpay está diseña sobre [REST](http://es.wikipedia.org/wiki/Representational_State_Transfer), por lo tanto encontrarás que las URL están orientadas a recursos y se usa códigos de respuesta HTTP para indicar los errores en la API.

Todas las respuestas de la API están en formato [JSON](http://www.json.org/), incluyendo errores.

# API Endpoints

> Recurso disponibles

<br/>
<br/>

> a) Por Comercio

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

> b) Por Cliente

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

La API REST de Openpay tiene un ambiente de pruebas (sandbox) y un ambiente de producción. Usa las credenciales que se generaron al momento de tu registro para realizar la integración de tu sistema con Openpay. Una vez que estes listo para pasar a producción y tu solicitud sea aprobada, se generarán nuevas credenciales para acceder al ambiente de producción.

La siguientes URIs forman la base de los endpoints para los ambientes soportados:

* **Pruebas**, URI base: <br/> `https://sandbox-api.openpay.mx`<br/><br/>
* **Producción**, URI base: <br/>`https://api.openpay.mx`<br/>

Un endpoint completo esta formado por la URI base del ambiente, el identificador del comercio y el recurso. 

Por ejemplo, si queremos crear un nuevo cliente, el endpoint sería:

<code>POST https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers</code>

Para crear una petición completa es necesaria envíar las cabeceras HTTP correctas y la información en formato JSON.

<aside class="notice">
Todos los ejemplos de está documentación están apuntados al ambiente de pruebas.
</aside>

# Autenticación

> Ejemplo de autenticación

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges/ \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:

El parámetro -u se ocupa para realizar la autenticación HTTP Basic (al agregar dos puntos después de la llave privada se previene el uso de contraseña)
```

```php
<? 
//Por default se usa el ambiente de sandbox
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c4875b178ce26348b0fac'); 
?>
```

```java
//Sandbox
final OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "moiep6umtcnanql3jrxp", "sk_3433941e467c4875b178ce26348b0fac");

//Produccion
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

//Produccion
OpenpayAPI openpayAPI = new OpenpayAPI("sk_3433941e467c4875b178ce26348b0fac", "moiep6umtcnanql3jrxp");
openpayAPI.Production = true;
```

```ruby
#Sandbox
openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")

#Produccion
openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac", true)
```

> Producción 

```shell
Solo es necesario usar la URI base https://api.openpay.mx
```

```php
<? 
Openpay::setProductionMode(true); 
?>
```

```java
//Solo es necesario usar la URI base https://api.openpay.mx
```

```csharp
openpayAPI.Production = true;
```

```javascript
openpay.setProductionReady(true);
```

```ruby
#Solo es necesario pasar como tercer argumento un "true" cuando se crea el objeto OpenpayApi
```

Para realizar peticiones a la API de Openpay, es necesario enviar la llave de API (API Key) en todas tus llamadas a nuestros  servidores. ​La llave la puedes obtener desde el [dashboard](https://sandbox-dashboard.openpay.mx).

Existen 2 tipos de llaves de API:

* **Privada.-** 
Para llamadas entre servidores y con acceso total a todas las operaciones de la API (nunca debe ser  compartida).

<aside class="warning">
Manten está llave segura y nunca la compartas con nadie.
</aside>

* **Pública.-**
Sólo se debe utilizar en llamadas desde JavaScript. Esta llave sólo tiene permitido realizar crear tarjetas o crear tokens

<aside class="notice">
Para hacer llamadas con tu llave pública utiliza la librería [Openpay.js](#)
</aside>

Para la autenticación al API debes usar [autenticación de acceso básica](http://es.wikipedia.org/wiki/Autenticación_de_acceso_básica), donde la llave de API es el nombre de usuario. La contraseña no es requerida y debe dejarse en blanco por fines de simplicidad.

<aside class="notice">
Por razones de seguridad todas las peticiones deben ser vía **HTTPS**.
</aside>

#Errores

Openpay regresa objetos de JSON en las respuestas del servicio, incluso en caso de errores por lo que cuando exista un error.

##Objeto Error

> Ejemplo de objeto

```json
{
    "category" : "request",
    "description" : "The customer with id 'm4hqp35pswl02mmc567' does not exist",
    "http_code" : 404,
    "error_code" : 1005,
    "request_id" : "1981cdb8-19cb-4bad-8256-e95d58bc035c"
}
```

```java
//Para el caso de java, toda operación regresara una instancia de la clase "OpenpayServiceException" la cual contendrá esta información del error.
```

```csharp
//Para el caso de C Sharp, toda operación regresara una instancia de la clase "OpenpayException" la cual contendrá esta información del error.
```

```ruby
#Para el caso de Ruby, toda operación puede regresar cualquiera de las siguientes excepciones:

# => OpenpayException: Para errores genericos, como acceso a recursos invalidos, etc.
# => OpenpayConnectionException: Para errores relacionados con problemas en la conexión al servidor.
# => OpenpayTransactionException: Para errores relacionados durante la ejecución de las operaciones.
```

Propiedad | Descripción
--------- | -----
category    |***string*** <br/>**request:** Indica un error causado por datos enviados por el cliente. Por ejemplo, una petición inválida, un intento de una transacción sin fondos, o una transferencia a una cuenta que no existe. <br/><br/>**internal:** Indica un error del lado de Openpay, y ocurrira muy raramente. <br/><br/>**gateway:** Indica un error durante la transacción de los fondos de una tarjeta a la cuenta de Openpay o de la cuenta hacia un banco o tarjeta.
error_code  |***numeric*** <br/>El código del error de Openpay indicando el problema que ocurrió.
description |***string*** <br/>Descripción del error.
http_code   |***string*** <br/>Código de error HTTP de la respuesta.
request_id  |***string*** <br/>Identificador de la petición.

##Códigos de error

###Generales
Código    | Error HTTP  |Causa
--------- | ----------- | --------
1000  |500 Internal Server Error  |Ocurrió un error interno en el servidor de Openpay
1001  |400 Bad Request   |El formato de la petición no es JSON, los campos no tienen el formato correcto, o la petición no tiene campos que son requeridos.
1002  |401 Unauthorized  |La llamada no esta autenticada o la autenticación es incorrecta.
1003  |422 Unprocessable Entity  |La operación no se pudo completar por que el valor de uno o más de los parametros no es correcto.
1004  |503 Service Unavailable |Un servicio necesario para el procesamiento de la transacción no se encuentra disponible.
1005  |404 Not Found | Uno de los recursos requeridos no existe.
1006  |409 Conflict  | Ya existe una transacción con el mismo ID de orden.
1007  |402 Payment Required | La transferencia de fondos entre una cuenta de banco o tarjeta y la cuenta de Openpay no fue aceptada.
1008  |423 Locked | Una de las cuentas requeridas en la petición se encuentra desactivada.
1009  |413 Request Entity too large  | El cuerpo de la petición es demasiado grande.
1010  |403 Forbidden  |Se esta utilizando la llave pública para hacer una llamada que requiere la llave privada, o bien, se esta usando la llave privada desde JavaScript.

###Almacenamiento

Código    | Error HTTP  |Causa
--------- | ----------- | --------
2001  |409 Conflict | La cuenta de banco con esta CLABE ya se encuentra registrada en el cliente.
2002  |409 Conflict | La tarjeta con este número ya se encuentra registrada en el cliente.
2003  |409 Conflict | El cliente con este identificador externo (External ID) ya existe.
2004  |422 Unprocessable Entity | El dígito verificador del número de tarjeta es inválido de acuerdo al algoritmo Luhn.
2005  |400 Bad Request | La fecha de expiración de la tarjeta es anterior a la fecha actual.
2006  |400 Bad Request | El código de seguridad de la tarjeta (CVV2) no fue proporcionado.

###Tarjetas
Código    | Error HTTP  |Causa
--------- | ----------- | --------
3001  |402 Payment Required | La tarjeta fue declinada.
3002  |402 Payment Required | La tarjeta ha expirado.
3003  |402 Payment Required | La tarjeta no tiene fondos suficientes.
3004  |402 Payment Required | La tarjeta ha sido identificada como una tarjeta robada.
3005  |402 Payment Required | La tarjeta ha sido identificada como una tarjeta fraudulenta.

###Cuentas
Código    | Error HTTP  |Causa
--------- | ----------- | --------
4001  |412 Preconditon Failed | La cuenta de Openpay no tiene fondos suficientes.


#Cargos
Los cargos se pueden realizar cargos a tarjetas, tiendas y bancos. A cada cargo se le asigna un identificador único en el sistema.

En cargos a tarjeta puedes hacerlo a una tarjeta guardada usando el id de la tarjeta, usando un token o puedes enviar la información de la tarjeta al momento de la invocación.

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

> Ejemplo de petición con cliente

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "source_id" : "kqgykn96i7bcs1wwhvgw",
   "method" : "card",
   "amount" : 100,
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-00051"
} ' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$chargeRequest = array(
    'method' => 'card',
    'source_id' => 'kqgykn96i7bcs1wwhvgw',
    'amount' => 100,
    'description' => 'Cargo inicial a mi merchant',
    'order_id' => 'oid-00051');

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateCardChargeParams request = new CreateCardChargeParams();
request.cardId("kqgykn96i7bcs1wwhvgw"); // =source_id
request.amount(new BigDecimal("100.00"));
request.description("Cargo inicial a mi merchant");
request.orderId("oid-00051");
request.deviceSessionId("kR1MiQhz2otdIuUlQkbEyitIqVMiI16f");
request.capture(Boolean.TRUE);

Charge charge = api.charges().create("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ChargeRequest request = new ChargeRequest();
request.Method = "card";
request.SourceId = "kwkoqpg6fcvfse8k8mg2";
request.Amount = new Decimal(100.00);
request.Description = "Cargo inicial a mi merchant";
request.OrderId = "oid-00051";
request.DeviceSessionId = "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f";
request.Capture = true;

Charge charge = api.ChargeService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var chargeRequest = {
   'source_id' : 'kqgykn96i7bcs1wwhvgw',
   'method' : 'card',
   'amount' : 100,
   'description' : 'Cargo inicial a mi cuenta',
   'order_id' : 'oid-00051'
}

openpay.customers.charges.create('ag4nktpdzebjiye1tlze', chargeRequest, function(error, charge) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)
request_hash={
    "method" => "card",
    "source_id" => "kqgykn96i7bcs1wwhvgw",
    "amount" => 100.00,
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
    "device_session_id" => "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f"
  }

response_hash=@charges.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Ejemplo de respuesta

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
   "order_id":"oid-00051",
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```

Este tipo de cargo requiere una tarjeta guardada o que hayas generado un token. Para guardar tarjetas consulta [como crear una tarjeta](#crear-una-tarjeta) y para usar tokens consulta la sección [creación de tokens](#crear-un-nuevo-token). 

Una vez que tengas una tarjeta guardada o un token usa la propiedad <code>source_id</code> para enviar el identificador.

La propiedad <code>device_session_id</code> deberá ser generada desde el API JavaScript, véase [Fraud detection using device data](https://github.com/open-pay/openpay-js#fraud-detection-using-device-data).

<aside class="notice">
Puedes realizar el cargo a la cuenta del comercio o a la cuenta de un cliente.
</aside>

###Petición 

Propiedad | Descripción
--------- | -----
method|***string*** (requerido) <br/>Debe contener el valor **card** para hacer un cargo de una tarjeta registrada.
source_id | ***string*** (requerido, longitud = 45) <br/>ID de la tarjeta guardada o el id del token creado de donde se retirarán los fondos.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.
device_session_id |  ***string*** (opcional, longitud = 255) <br/>Identificador del dispositivo generado con la herramienta anti-fraudes
capture |  ***boolean*** (opcional, default = true) <br/>Indica si el cargo se hace o no inmediatamente, cuando el valor es false el cargo se maneja como una autorización (o pre-autorización) y solo se reserva el monto para ser confirmado o cancelado en una segunda llamada. 

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del cargo o una [respuesta de error](#objeto-error).

##Cargo a nueva tarjeta

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
//Comercio
$openpay->charges->create(chargeRequest);

//Cliente
$customer = $openpay->customers->get(customerId);
$customer->charges->create(chargeRequest);
?>
```

```java
//Cliente
openpayAPI.charges().create(String customerId, CreateCardChargeParams request);

//Comercio
openpayAPI.charges().create(CreateCardChargeParams request);
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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "card": {
      "card_number": "4111111111111111",
      "holder_name": "Juan Perez Ramirez",
      "expiration_year": "20",
      "expiration_month": "12",
      "cvv2": "110"
   },
   "method" : "card",
   "amount" : 100,
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-00052"
} ' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$card = array(
    'card_number' => '4111111111111111',
    'holder_name' => 'Juan Perez Ramirez',
    'expiration_year' => '20',
    'expiration_month' => '12',
    'cvv2' => '110');

$chargeRequest = array(
    'method' => 'card',
    'card' => $card,
    'amount' => 100,
    'description' => 'Cargo inicial a mi cuenta',
    'order_id' => 'oid-00052');

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateCardChargeParams request = new CreateCardChargeParams();
Card card = new Card();
card.holderName("Juan Perez Ramirez");
card.cardNumber("4111111111111111");
card.cvv2("110");
card.expirationMonth(12);
card.expirationYear(20);
request.amount(new BigDecimal("100.00"));
request.description("Cargo inicial a mi cuenta");
request.card(card);
request.orderId("oid-00052");
request.deviceSessionId("kR1MiQhz2otdIuUlQkbEyitIqVMiI16f");
request.capture(Boolean.TRUE);

Charge charge = api.charges().create("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ChargeRequest request = new ChargeRequest();
request.Method = "card";
Card card = new Card();
card.HolderName = "Juan Perez Ramirez";
card.CardNumber = "4111111111111111";
card.Cvv2 = "110";
card.ExpirationMonth = "12";
card.ExpirationYear = "20";
request.Card = card;
request.Amount = new Decimal(9.99);
request.Description = "Cargo inicial a mi cuenta";
request.OrderId = "oid-00052";
request.DeviceSessionId = "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f";
request.Capture = true;

Charge charge = api.ChargeService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var chargeRequest = {
   'card': {
      'card_number': '4111111111111111',
      'holder_name': 'Juan Perez Ramirez',
      'expiration_year': '20',
      'expiration_month': '12',
      'cvv2': '110'
   },
   'method' : 'card',
   'amount' : 100,
   'description' : 'Cargo inicial a mi cuenta',
   'order_id' : 'oid-00052'
};

openpay.customers.charges.create('ag4nktpdzebjiye1tlze', chargeRequest, function(error, charge) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@openpay.create(:charges)
card_hash={
     "holder_name" => "Juan Perez Ramirez",
     "card_number" => "4111111111111111",
     "cvv2" => "110",
     "expiration_month" => "12",
     "expiration_year" => "20"
   }
request_hash={
     "method" => "card",
     "card" => card_hash,   
     "amount" => 100.00,
     "description" => "Cargo inicial a mi cuenta",
     "order_id" => "oid-00052",
     "device_session_id" => "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f"
   }

response_hash=@charges.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Ejemplo de respuesta

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
   "currency":"MXN",
   "creation_date":"2014-05-26T11:56:25-05:00",
   "operation_date":"2014-05-26T11:56:25-05:00",
   "description":"Cargo inicial a mi cuenta",
   "error_message":null,
   "order_id":"oid-00052",
   "customer_id":"ag4nktpdzebjiye1tlze"
}
```

En este tipo de invocación es necesario enviar toda la información de la tarjeta, la cual solo será usada para esta venta y no será almacenada en el sistema. Esto lo puedes usar para realizar ventas directas en donde no requieres la tarjeta para un uso futuro.


La propiedad <code>device_Session_Id</code> deberá ser generada desde el API JavaScript, véase [Fraud detection using device data](https://github.com/open-pay/openpay-js#fraud-detection-using-device-data).

###Petición 

Propiedad | Descripción
--------- | -----
method|***string*** (requerido) <br/>Debe contener el valor **card** para hacer un cargo de una tarjeta registrada.
card | ***objeto*** (requerido) <br/> Datos de la tarjeta de la cual se retirarán los fondos. Ver [objeto tarjeta](#crear-una-tarjeta) 
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.
device_session_id |  ***string*** (opcional, longitud = 255) <br/>Identificador del dispositivo generado con la herramienta anti-fraudes
capture |  ***boolean*** (opcional, default = true) <br/>Indica si el cargo se hace o no inmediatamente, cuando el valor es false el cargo se maneja como una autorización (o pre-autorización) y solo se reserva el monto para ser confirmado o cancelado en una segunda llamada. 

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del cargo o una [respuesta de error](#objeto-error).


##Cargo en tienda

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
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method" : "store",
   "amount" : 100,
   "description" : "Cargo con tienda",
   "order_id" : "oid-00053"
} ' 
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$chargeRequest = array(
    'method' => 'store',
    'amount' => 100,
    'description' => 'Cargo con tienda',
    'order_id' => 'oid-00053');

$customer = $openpay->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
CreateStoreChargeParams request = new CreateStoreChargeParams();
request.amount(new BigDecimal("100.00"));
request.description("Cargo con tienda");
request.orderId("oid-00053");

Charge charge = api.charges().create("ag4nktpdzebjiye1tlze", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ChargeRequest request = new ChargeRequest();
request.Method = "store";
request.Amount = new Decimal(100.00);
request.Description = "Cargo con tienda";
request.OrderId = "oid-00053";

Charge charge = api.ChargeService.Create("ag4nktpdzebjiye1tlze", request);
```

```javascript
var storeChargeRequest = {
   'method' : 'store',
   'amount' : 100,
   'description' : 'Cargo con tienda',
   'order_id' : 'oid-00053'
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
     "order_id" => "oid-00053"
   }

response_hash=@charges.create(request_hash.to_hash, "ag4nktpdzebjiye1tlze")
```

> Ejemplo de respuesta

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
   "description":"Cargo con tienda",
   "error_message":null,
   "order_id":"oid-00053",
   "customer_id":"ag4nktpdzebjiye1tlze",
   "payment_method":{
      "type":"store",
      "reference":"000020TRNIRKIYOBO5QFEX55EF0100009",
      "barcode_url":"https://sandbox-api.openpay.mx/barcode/000020TRNIRKIYOBO5QFEX55EF0100009?width=1&height=45&text=false"
   }
}
```

Para un pago en una tienda de conveniencia se debe crear un petición de tipo cargo indicando como método **store**. Esto generará una respuesta con un número de referencia y una URL a un código de barras, los cuales debes de utilizar para crear un recibo a tu cliente y que con él pueda realizar el pago en una de las tienda de conveniencia aceptadas. El código de barras es de tipo Code 128.

###Petición 

Propiedad | Descripción
--------- | -----
method|***string*** (requerido) <br/>Debe contener el valor **store** para hacer un cargo de una tarjeta registrada.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del cargo o una [respuesta de error](#objeto-error).

##Cargo en banco

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
$customer = $openpay->customers->get(customerId);
$customer->charges->create(chargeRequest);
?>
```

```java
//Cliente
openpayAPI.charges().create(String customerId, CreateBankChargeParams request);

//Comercio
openpayAPI.charges().create(CreateBankChargeParams request);
```

```csharp
//Cliente
openpayAPI.ChargeService.Create(string customer_id, ChargeRequest request);

//Comercio
openpayAPI.ChargeService.Create(ChargeRequest request);
```

```javascript
// Comercio
openpay.charges.create(chargeRequest, callback);

// Cliente
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

> Ejemplo de respuesta

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
Para un cargo a banco se debe crear una petición de tipo cargo indicando como método **bank_account**. Esto te generará una respuesta con un número de CLABE bancaria y una descripción, estos datos los debes de indicar a tu cliente en un recibo para que realice la transferencia vía SPEI. 


###Petición 

Propiedad | Descripción
--------- | -----
method|***string*** (requerido) <br/>Debe contener el valor **bank_account** para hacer un cargo de una tarjeta registrada.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del cargo o una [respuesta de error](#objeto-error).

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
   "currency":"MXN",
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
**Nota:** Solo se pueden confirmar cargos a tarjeta. Para cancelar el cargo creado se debe hacer una llamada al método [Devolver un cargo](#devolver-un-cargo)
</aside>


###Petición 

Propiedad | Descripción
--------- | -----
amount | ***numeric*** (requerido) <br/>Cantidad a confirmar. Puede ser menor o igual al monto capturado hasta dos dígitos decimales.


###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del cargo o una [respuesta de error](#objeto-error).

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
@charges.refund(transaction_id, description, customer_id)

#Comercio
@charges=@openpay.create(:charges)
@charges.refund(transaction_id, description)
```

> Ejemplo de petición con cliente

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

response_hash=@charges.refund("tryqihxac3msedn4yxed", "Monto de cargo devuelto", "ag4nktpdzebjiye1tlze")
```

> Ejemplo de respuesta

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
Si deseas realizar una devolución de un cargo hecho a tarjeta puedes ocupar este método. El monto a devolver será por el total del cargo. Ten en cuenta que la devolución puede tardar en aparecer en el estado de cuenta de tu cliente de 1 a 3 días hábiles

<aside class="notice">
**Nota:** Solo se pueden hacer devoluciones de cargos a tarjeta.
</aside>


###Petición 

Propiedad | Descripción
--------- | -----
description | ***string*** (opcional, longitud = 250) <br/>Texto libre para describir motivo de la devolución.


###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del cargo o una [respuesta de error](#objeto-error).


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

Regresa la información de un cargo generado en cualquier momento solo con conocer el id de cargo.

###Petición

Propiedad | Descripción
--------- | ------
transaction_id| _**string**_ (requerido, longitud = 45)<br/>Identificador del cargo a consultar.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción) con la información del cargo o una [respuesta de error](#objeto-error).

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
Obtiene un listado de los cargos realizados por comercio o cliente.

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

###Respuesta

Regresa un arreglo de [objetos de transacción](#objeto-transacción) de los cargos en orden descendente por fecha de creación.

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
bank_account | ***object*** (requerido) <br/>Datos de la cuenta bancaria a la que se enviarán los fondos. <br/><br/> **clabe**.- Número de cuenta CLABE de la cuenta a la que se enviarán los fondos. <br/>**holder_name**.- Nombre del propietario de la cuenta.
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
card | ***object*** (requerido) <br/>Datos de la tarjeta a la que se enviarán los fondos. <br/><br/> **card_number**.- Número de tarjeta de crédito a la que se enviarán los fondos <br/>**holder_name**.- Nombre del tarjeta habiente propietario de la tarjeta.
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


#Clientes

Los clientes son recursos en Openpay que se manejan dentro de su cuenta de comercio y puede representar usuarios, clientes o socios segun el tipo de negocio. 

A los clientes les puedes agregar tarjetas y cuentas de banco para despues realizar transacciones de Cargo, Transferencia o Pago.

##Objeto Cliente

> Ejemplo de objeto

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
   }
}
```

Propiedad | Descripción
--------- | -----
id            |***string*** <br/>Identificador único del cliente.
creation_date |***datetime*** <br/>Fecha y hora en que se creó el cliente  en formato ISO 8601
name          |***string*** <br/>Nombre del cliente.
last_name     |***string*** <br/>Apellidos del cliente.
email         |***string*** <br/>Cuenta de correo electrónico del cliente.
phone_number  |***numeric*** <br/>Número telefónico del Cliente.
status        |***string*** <br/>Estatus de la cuenta del cliente puede ser active o deleted. Si la cuenta se encuentra en estatus deleted no se permite realizar ninguna transacción.
balance       |***numeric*** <br/>Saldo en la cuenta con dos decimales.
clabe         |***numeric*** <br/>Cuenta CLABE asociada con la que puede recibir fondos realizando una  transferencia desde cualquier banco en México.
[address](#objeto-dirección) |***object*** <br/>Dirección del Cliente. Usada comúnmente como dirección de envío.


##Crear un nuevo cliente

> Definición

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

> Ejemplo de petición 

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
     'requires_account' => true,
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
     "requires_account" => true,
     "phone_number" => "44209087654",
     "address" => address_hash
   }

response_hash=@customers.create(request_hash.to_hash)
```

> Ejemplo de respuesta

```json
{
   "id":"anbnldwgni1way3yp2dw",
   "name":"customer name",
   "last_name":null,
   "email":"customer_email@me.com",
   "phone_number":null,
   "address":null,
   "creation_date":"2014-05-20T16:47:47-05:00",
   "external_id":null
}
```

Crea un objeto cliente.

###Petición

Propiedad | Descripción
--------- | ------
external_id | ***string*** (opcional, longitud = 100)  <br/> Identificador externo único para el cliente asignado por el comercio.
name        | ***string*** (requerido, longitud = 100)<br/>Nombre(s) del cliente.
last_name   | ***string*** (opcional, longitud = 100)<br/>Apellidos del cliente.
email       | ***string*** (requerido, longitud = 100)<br/>Cuenta de correo electrónico del Cliente.
requires_account | ***boolean***  (opcional, default = true) <br/> Enviar con valor **false** si requiere que el cliente se cree sin cuenta para manejo del saldo.
phone_number| ***string*** (opcional, longitud = 100) <br/>Número telefónico del Cliente.
[address](#objeto-dirección) | ***object*** (opcional) <br/>Dirección del Cliente. Usada comúnmente como dirección de envío.

###Respuesta

Un [objeto cliente](#objeto-cliente) en caso que se hayan enviado todos los datos correctamente, o una [respuesta de error](#objeto-error) si ocurrió algun problema en la creación.


##Actualizar un cliente

> Definición

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

> Ejemplo de petición 

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
     "requires_account" => true,
     "phone_number" => "44209087654",
     "address" => address_hash
   }

response_hash=@customers.update(request_hash.to_hash)
```

> Ejemplo de respuesta

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
   "creation_date":"2014-05-20T16:47:47-05:00",
   "external_id":null
}
```

Actualiza uno o más datos del cliente.

###Petición

Propiedad | Descripción
--------- | ------
name| ***string*** (requerido, longitud = 100)<br/>Nombre(s) del cliente.
last_name| ***string*** (opcional, longitud = 100) <br/>Apellidos del cliente.
email| ***string*** (requerido, longitud = 100)<br/>Cuenta de correo electrónico del Cliente.
phone_number| ***string*** (opcional, longitud = 100) <br/>Número telefónico del Cliente.
[address](#objeto-dirección)| ***object*** <br/>Dirección del Cliente. Usada comúnmente como dirección de envío.

###Respuesta

Regresa un [objeto cliente](#objeto-cliente) con la información actualizada, o una [respuesta de error](#objeto-error) si ocurrió algun problema en la actualización.

##Obtener un cliente existente

> Definición

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

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
   "creation_date":"2014-05-20T16:47:47-05:00",
   "external_id":null
}
```

Obtiene la información actual de un cliente existente. Solo es necesario especificar el identificador que fue regresado al momento de crear el cliente.

###Petición

Propiedad | Descripción
--------- | ------
id| _**string**_ (requerido, longitud = 45)<br/>Identificador único del cliente que se desea obtener.

###Respuesta

Si el identificador existe regresa un [objeto cliente](#objeto-cliente) con la información del cliente.

##Eliminar un cliente

> Definición

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

> Ejemplo de petición 

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


Elimina un cliente permanentemente. Se cancelarán las suscripciones que tenga. Openpay mantiene los registros de las operaciones.

###Petición

Propiedad | Descripción
--------- | ------
id| _**string**_ (requerido, longitud = 45)<br/> Identificador único del cliente a borrar.

###Respuesta
Si el cliente se borra correctamente la respuesta es vacía, si no se puede borrar se regresa un [objeto error](#objeto-error) indicando el motivo. 

##Listado de clientes

> Definición

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

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
}, {
   "id":"cz4nkhrlcu9k7qd4lwqx",
   "creation_date":"2013-11-07T14:54:46-06:00",
   "name":"Eriberto",
   "last_name":"Rodriguez Lopez",
   "email":"eriberto.rodriguez@payments.com",
   "phone_number":"442",
   "status":"active",
   "balance":103
}]
```
Regresa una lista de los cliente registrados, si desea delimitar el resultado se pueden utilizar los filtros.

###Petición
Puede realizar una búsqueda utilizando los siguiente parámetros como filtros.

Propiedad | Descripción
--------- | ------
creation| ***date*** <br/>Igual a la fecha de creación del cliente. Formato yyyy-mm-dd
creation[gte]| ***date*** <br/>Mayor a la fecha de creación del cliente .Formato yyyy-mm-dd
creation[lte]| ***date*** <br/>Menor a la fecha de creación del cliente .Formato yyyy-mm-dd
offset| ***numeric*** <br/>Número de registros a omitir al inicio, por defecto 0.
limit| ***numeric*** <br/>Número de registros que se requieren, por defecto 10.

###Respuesta

Regresa un arreglo de [objetos cliente](#objeto-cliente).


#Transferencias

Las transferencias permite transferir fondos entre las cuentas de tus clientes. 

<aside class="notice">
**Nota:** Si desea realizar una transferencia a un banco consulte la [sección de pagos](#pagos-o-retiros).
</aside>

##Transferir entre clientes

> Definición

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

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
   "customer_id":"a9pvykxz4g5rg0fplze0"
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
Si la transacción se realiza correctamente, la respuesta contendrá un [objeto de transacción](#objeto-transacción). Este objeto representará el retiro de fondos del cliente actual. En caso de error, se regresará el objeto de error.

##Obtener una transferencia

> Definición

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

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
Con el identificador del cliente y el identificador de la transferencia, se puede obtener el detalle de la transacción. La transacción de salida se encontrará en el cliente desde el cual se realizó la transferencia, y la transacción de entrada en el cliente que recibió el monto.


###Petición
Propiedad | Descripción
--------- | ------
customer_id| ***string*** (requerido, longitud = 45) <br/> Identificador del cliente
transaction_id| ***string*** (requerido, longitud = 45) <br/> Identificador de la transferencia

###Respuesta
Regresa un [objeto de transacción](#objeto-transacción)

##Listado de transferencias

> Definición

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

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
Listado de [objetos transacción](#objeto-transacción) de las transferencias realizadas, cada uno con el identificador del cliente al que se le realizó. Las transacciones serán listadas en orden descendente por fecha de creación.



#Tarjetas
Dentro de la plataforma Openpay podrás agregar tarjetas a la cuenta del cliente, eliminarlas, recuperar alguna en específico y listarlas​.

Se pueden almacenar multiples tarjetas de débito y/o crédito a nivel cliente o a nivel comercio para realizar cargos posteriormente sin la necesidad de introducir nuevamente la información.

##Objeto Tarjeta

> Ejemplo de objeto 

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
   "customer_id":"a2b79p8xmzeyvmolqfja"
}
```

Propiedad | Descripción
--------- | ------
id            |***string*** <br/>Identificador único de la tarjeta.
creation_date |***datetime*** <br/>Fecha y hora en que se creó la tarjeta en formato ISO 8601
holder_name |***string***  <br/>Nombre del tarjeta habiente.
card_number |***numeric***  <br/>Numero de tarjeta puede ser de 16 o 19 dígitos.
cvv2 |***numeric***  <br/>Código de seguridad como aparece en la parte de atrás de la tarjeta. Generalmente 3 dígitos.
expiration_month |***numeric***  <br/>Mes de expiración tal como aparece en la tarjeta.
expiration_year |***numeric***  <br/>Año de expiración tal como aparece en la tarjeta.
[address](#objeto-dirección) |***object*** <br/>Dirección de facturación del tarjeta habiente.
allows_charges |***boolean*** <br/>Permite conocer si se pueden realizar cargos a la tarjeta.
allows_payouts |***boolean*** <br/>Permite conocer si se pueden realizar envío de pagos a la tarjeta. 
brand |***string*** <br/>Marca de la tarjeta: visa, mastercard, carnet o american express.
type |***string*** <br/>Tipo de la tarjeta: debit, credit, cash, etc.
bank_name |***string*** <br/>Nombre del banco emisor.
bank_code |***string*** <br/>Código del banco emisor.
customer_id |***string*** <br/>Identificador del cliente al que pertenece la tarjeta. Si la tarjeta es a nivel comercio este valor será null.

##Crear una tarjeta

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/cards

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Cliente
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->add(cardDataRequest);

//Comercio
$card = $openpay->cards->add(cardDataRequest);
?>
```

```java
//Cliente
openpayAPI.cards().create(String customerId, Card request);

//Comercio
openpayAPI.cards().create(Card request);
```

```csharp
//Cliente
openpayAPI.CardService.Create(string customer_id, Card card);

//Comercio
openpayAPI.CardService.Create(Card card);
```

```javascript
// Comercio
openpay.cards.create(cardRequest, callback);

// Cliente
openpay.customers.cards.create(customerId, cardRequest, callback);
```

```ruby
#Cliente
@cards=@openpay.create(:cards)
@cards.create(request_hash, customer_id)

#Comercio
@cards=@openpay.create(:cards)
@cards.create(request_hash)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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
 
Cuando se crea una tarjeta debe especificarse cliente, si no se especifica el cliente la tarjeta quedará registrada para la cuenta del comercio. Una vez guardada la tarjeta no se puede obtener el número y código de seguridad.

<aside class="notice">
**Nota:** Todas las tarjetas al momento de guardarse en Openpay son validadas haciendo un autorización por $10.00 los cuales son devueltos en el momento.
</aside>

Al momento de guardar la tarjeta se generará un id que podrá ser usado para hacer cargos a la tarjeta, envíos a una tarjeta o simplemente obtener la información no sensible de la tarjeta.

###Petición

Propiedad | Descripción
--------- | ------
holder_name |***string*** (requerido, longitud = 80) <br/>Nombre del tarjeta habiente.
card_number |***numeric*** (requerido) <br/>Numero de tarjeta puede ser de 16 o 19 dígitos.
cvv2 |***numeric*** (requerido) <br/>Código de seguridad como aparece en la parte de atrás de la tarjeta. Generalmente 3 dígitos.
expiration_month |***numeric*** (requerido) <br/>Mes de expiración tal como aparece en la tarjeta.
expiration_year |***numeric*** (requerido) <br/>Año de expiración tal como aparece en la tarjeta.
[address](#objeto-dirección) |***object*** <br/>Dirección de facturación del tarjeta habiente.

###Respuesta
Regresa un [objeto tarjeta](#objeto-tarjeta) cuando se creó correctamente o una [respuesta de error](#objeto-error) si ocurrió algún problema en la creación.


##Crear una tarjeta con token
 
> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/cards

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Cliente
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->add(cardDataRequest);

//Comercio
$card = $openpay->cards->add(cardDataRequest);
?>
```

```java
//Cliente
openpayAPI.cards().create(String customerId, Card card);

//Comercio
openpayAPI.cards().create(Card card);
```

```csharp
//Cliente
openpayAPI.CardService.Create(string customer_id, Card request);

//Comercio
openpayAPI.CardService.Create(Card request);
```

```javascript
// Comercio
openpay.cards.create(cardRequest, callback);

// Cliente
openpay.customers.cards.create(customerId, cardRequest, callback);
```

```ruby
#Cliente
@cards=@openpay.create(:cards)
@cards.create(request_hash, customer_id)

#Comercio
@cards=@openpay.create(:cards)
@cards.create(request_hash)
```

> Ejemplo de petición con cliente

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
      "token_id":"tokgslwpdcrkhlgxqi9a"
   }' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$cardDataRequest = array(
    'token_id' => 'tokgslwpdcrkhlgxqi9a'
    );

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$card = $customer->cards->add($cardDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card request = new Card();
request.tokenId("tokgslwpdcrkhlgxqi9a");

request = api.cards().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card request = new Card();
request.TokenId = "tokgslwpdcrkhlgxqi9a";

request = api.CardService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var cardRequest = {
  'token_id' : 'tokgslwpdcrkhlgxqi9a'
}

openpay.customers.cards.create('a9pvykxz4g5rg0fplze0', cardRequest, function(error, card)  {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)
request_hash={
     "token_id" => "tokgslwpdcrkhlgxqi9a"
   }

response_hash=@cards.create(request_hash.to_hash, "asynwirguzkgq2bizogo")
```


> Ejemplo de respuesta

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

Crea una tarjeta a partir de un token obtenido desde el navegador o dispositivo del cliente. Esta forma evita que la información sensible de la tarjeta pase por tus servidores.

###Petición
Propiedad | Descripción
--------- | ------
token_id| ***string*** (requerido, longitud = 45) <br/> Identificador del token generado en el navegador o dispositivo del cliente.

###Respuesta
Regresa un [objeto tarjeta](#objeto-tarjeta)

##Obtener una tarjeta

> Definición

```shell
Comercio
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/cards/{CARD_ID}

Cliente
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}
```

```php
<?
//Cliente
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->get(cardId);

//Comercio
$card = $openpay->cards->get(cardId);
?>
```

```java
//Cliente
openpayAPI.cards().get(String customerId, String cardId);

//Comercio
openpayAPI.cards().get(String cardId);
```

```csharp
//Cliente
openpayAPI.CardService.Get(string customer_id, string card_id);

//Comercio
openpayAPI.CardService.Get(string card_id);
```

```javascript
// Comercio
openpay.cards.get(cardId, callback);

// Cliente
openpay.customers.cards.get(customerId, cardId, callback);
```

```ruby
#Cliente
@cards=@openpay.create(:cards)
@cards.get(card_id, customer_id)

#Comercio
@cards=@openpay.create(:cards)
@cards.get(card_id)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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

Obtiene los detalles de una tarjeta solicitándola con su id. 

<aside class="notice">
**Nota:** Nunca se regresarán datos sensibles como son el código de seguridad y del número de tarjeta sólo se mostraran los primeros 6 y los últimos 4 dígitos.
</aside>

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador único de la tarjeta

###Respuesta
Regresa un [objeto tarjeta](#objeto-tarjeta)

##Eliminar una tarjeta

> Definición

```shell
Comercio
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/cards/{CARD_ID}

Cliente
DELETE https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}
```

```php
<?
//Cliente
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->get(cardId);
$card->delete();

//Comercio
$card = $openpay->cards->get(cardId);
$card->delete();
?>
```

```java
//Cliente
openpayAPI.cards().delete(String customerId, String cardId);

//Comercio
openpayAPI.cards().delete(String cardId);
```

```csharp
//Cliente
openpayAPI.CardService.Delete(string customer_id, string card_id);

//Comercio
openpayAPI.CardService.Delete(string card_id);
```

```javascript
// Comercio
openpay.cards.delete(cardId, callback);

// Cliente
openpay.customers.cards.delete(customerId, cardId, callback);
```

```ruby
#Cliente
@cards=@openpay.create(:cards)
@cards.delete(card_id, customer_id)

#Comercio
@cards=@openpay.create(:cards)
@cards.delete(card_id)
```

> Ejemplo de petición con cliente

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

Elimina una tarjeta del cliente o comercio. Una vez eliminada no se permitirá hacer movimientos, sin embargo, se mantendrán todos los registros de operaciones que haya realizado y se podrán consultar en el dashboard.

Para eliminarla sólo es necesario proporcionar el identificador de la tarjeta.

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador único de la tarjeta

###Respuesta
Si la tarjeta se borra correctamente la respuesta es vacía, si no se puede borrar se regresa un [objeto error](#objeto-error) indicando el motivo. 


##Listado de tarjetas
> Definición

```shell
Comercio
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers

Cliente
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Clientes
$customer = $openpay->customers->get(customerId);
$cardList = $customer->cards->getList(findDataRequest);

//Comercio
$cardList = $openpay->cards->getList(findDataRequest);
?>
```

```java
//Cliente
openpayAPI.cards().list(String customerId, SearchParams request);

//Comercio
openpayAPI.cards().list(SearchParams request);
```

```csharp
//Cliente
openpayAPI.CardService.List(string customer_id, SearchParams request = null);

//Comercio
openpayAPI.CardService.List(SearchParams request = null);
```

```javascript
// Comercio
openpay.cards.list(callback);
openpay.cards.list(searchParams, callback);

// Cliente
openpay.cards.list(customerId, callback);
openpay.cards.list(customerId, searchParams, callback);
```

```ruby
#Cliente
@cards=@openpay.create(:cards)
@cards.all(customer_id)

#Comercio
@cards=@openpay.create(:cards)
@cards.all
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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

Regresa una lista de las tarjetas registrados por comercio o cliente, si desea delimitar el resultado se pueden utilizar los filtros. 

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
Listado de [objetos tarjeta](#objeto-tarjeta) registrados de acuerdo a los parámetros proporcionados, ordenadas por fecha de creación en orden descendente.

#Cuentas Bancarias

Se pueden almacenar múltiples cuentas bancarias por cliente o por comercio para posteriormente retirar fondos. 

##Objeto Cuenta Bancaria

> Ejemplo de objeto 

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


Propiedad | Descripción
--------- | ------
id | ***string*** <br/>ID de la cuenta bancaria.
holder_name | ***string*** <br/>Nombre completo del titular.
alias | ***string*** <br/>Nombre por el cual el se identifica a la cuenta bancaria.
clabe | ***string*** <br/>Número CLABE asignado a la cuenta bancaria.
bank_name | ***string*** <br/>Nombre abreviado del banco donde radica la cuenta, en base al siguiente catálogo de [Códigos de Banco](http://es.wikipedia.org/wiki/CLABE#C.C3.B3digo_de_Banco).
bank_code | ***string*** <br/>Código del banco donde radica la cuenta bancaria, en base al siguiente catálogo de [Códigos de Banco](http://es.wikipedia.org/wiki/CLABE#C.C3.B3digo_de_Banco).
creation_date | ***datetime*** <br/>Fecha y hora en que se creó la cuenta bancaria en formato ISO 8601.


##Crear una cuenta bancaria
 
> Definición

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
//Cliente
openpayAPI.bankAccounts().create(String customerId, BankAccount request);
```

```csharp
//Cliente
openpayAPI.BankAccountService.Create(string customer_id, BankAccount request);
```

```javascript
openpay.customers.bankaccounts.create(customerId, bankaccountRequest, callback);
```

```ruby
#Cliente
@bank_accounts=@openpay.create(:bankaccounts)
@bank_accounts.create(request_hash, customer_id)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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

Crea y asigna una cuenta bancaria al cliente espeficado.

###Petición


Propiedad | Descripción
--------- | ------
holder_name | ***string*** (requerido, longitud = 80) <br/>Nombre completo del titular.
alias | ***string*** (opcional, longitud = 45)<br/>Nombre por el cual el se identifica a la cuenta bancaria.
clabe | ***string*** (requerido, longitud = 45) <br/>Número CLABE asignado a la cuenta bancaria.

###Respuesta
Regresa un [objeto cuenta bancaria](#objeto-cuenta-bancaria) creado o un error en caso de ocurrir algún problema.

##Obtener una cuenta bancaria

> Definición

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
//Cliente
openpayAPI.bankAccounts().get(String customerId, String bankAccountId);
```

```csharp
//Cliente
openpayAPI.BankAccountService.Get(string customer_id, string bank_account_id);
```

```javascript
openpay.customers.bankaccounts.get(customerId, bankaccountId, callback);
```

```ruby
#Cliente 
@bank_accounts=@openpay.create(:bankaccounts)
@bank_accounts.get(customer_id, bankaccount_id)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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

Obtiene los detalles de una cuenta bancaria asignada a un cliente. 

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador único de la cuenta bancaria

###Respuesta
Regresa un [objeto cuenta bancaria](#objeto-cuenta-bancaria)

##Eliminar una cuenta bancaria

> Definición

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
//Cliente
openpayAPI.bankAccounts().delete(String customerId, String bankAccountId);
```

```csharp
//Cliente
openpayAPI.BankAccountService.Delete(string customer_id, string bank_account_id);
```

```javascript
openpay.customers.bankaccounts.delete(customerId,bankaccountId, callback);
```

```ruby
#Cliente
@bank_accounts=@openpay.create(:bankaccounts)
@bank_accounts.delete(customer_id, bankaccount_id)
```

> Ejemplo de petición con cliente

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

Elimina la cuenta bancaria asociada al cliente. Las transacciones que se encuentran asociadas a esta cuenta no sufren cambios y se podrán seguir consultando.

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador único de la cuenta bancaria.

###Respuesta
Si la cuenta bancaria se borra correctamente la respuesta es vacía, si no se puede borrar se regresa un [objeto error](#objeto-error) indicando el motivo. 

##Listado de cuentas bancarias
> Definición

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
//Cliente
openpayAPI.bankAccounts().list(String customerId, SearchParams request);
```

```csharp
//Cliente
openpayAPI.BankAccountService.List(string customer_id, SearchParams request = null);
```

```javascript
openpay.customers.bankaccounts.list(customerId, callback);
openpay.customers.bankaccounts.list(customerId, searchParams, callback);
```

```ruby
#Cliente
@bank_accounts=@openpay.create(:bankaccounts)
@bank_accounts.all(customer_id)
```

> Ejemplo de petición con cliente

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

> Ejemplo de respuesta

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
Regresa los detalles de todas las cuentas bancarias del cliente especificado en la petición. 

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
Listado de [objetos cuenta bancaria](#objeto-cuenta-bancaria) registrados de acuerdo a los parámetros proporcionados, ordenadas por fecha de creación en orden descendente.

#Planes

Los planes son recursos en Openpay que permiten crear plantillas para las suscripciones. Con ellos podrás definir la cantidad y frecuencia con la que se realizarán los cargos recurrentes. 

##Objeto Plan

> Ejemplo de objeto 

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

Propiedad | Descripción
--------- | ------
id | ***string*** <br/> Identificador único del Plan.
creation_date | ***datetime*** <br/> Fecha y hora en que se creó el Plan  en formato ISO 8601
name  | ***string*** <br/> Nombre del Plan.
amount | ***numeric*** <br/> Monto que se aplicara cada vez que se cobre la suscripción. Debe ser una cantidad mayor a cero, con hasta 2 dígitos decimales.
currency | ***string*** <br/> Moneda usada en la operación, por default es MXN
repeat_every | ***numeric*** <br/> Número de unidades tiempo entre los que se cobrara la suscripción. Por ejemplo, repeat_unit=month y repeat_every=2 indica que se cobrara cada 2 meses.
repeat_unit | ***string*** <br/> Especifica la frecuencia de cobro. Puede ser semanal(week), mensual(month) o anual(year).
retry_times | ***numeric*** <br/>  Numero de reintentos de cobro de la suscripción. Cuando se agotan los intentos se pone en el estatus determinado por el campo status_after_retry.
status | ***string*** <br/> Estatus del Plan puede ser active o deleted. Si el plan se encuentra en estado deleted no se permite registrar nuevas suscripciones, pero las que ya están registradas, se siguen cobrando.
status_after_retry | ***string*** <br/> Este campo especifica el status en el que se pondrá la suscripción una vez que se agotaron los intentos. Puede ser: unpaid o cancelled
trial_days | ***numeric*** <br/> Numero de días de prueba por defecto que tendrá la suscripción.

##Crear un nuevo plan
 
> Definición

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
#Cliente
@plans=@openpay.create(:plans)
@plans.create(request_hash)
```

> Ejemplo de petición 

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

> Ejemplo de respuesta

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

Crea un nuevo plan al se podrán suscribir uno o varios clientes.

###Petición


Propiedad | Descripción
--------- | ------
name | ***string*** (requerido, longitud = 255) <br/>Nombre del Plan.
amount | ***numeric*** (requerido) <br/>Monto que se aplicara cada vez que se cobre la suscripción. Debe ser una cantidad mayor a cero, con hasta 2 dígitos decimales.
repeat_every | ***numeric*** (requerido) <br/>Número de unidades tiempo entre los que se cobrara la suscripción. Por ejemplo, repeat_unit=month y repeat_every=2 indica que se cobrara cada 2 meses.
repeat_unit | ***numeric*** (requerido) <br/>Especifica la frecuencia de cobro. Puede ser semanal(week), mensual(month) o anual(year).
retry_times | ***numeric*** (opcional) <br/> Numero de reintentos de cobro de la suscripción. Cuando se agotan los intentos se pone en el estado determinado por el campo status_after_retry.
status_after_retry | ***string*** (requerido, valores = "UNPAID/CANCELLED") <br/>Este campo especifica el status en el que se pondrá la suscripción una vez que se agotaron los intentos. Puede ser: unpaid o cancelled
trial_days | ***numeric*** (requerido) <br/>Numero de días de prueba por defecto que tendrán las suscripciones que se creen a partir del plan creado.
 

###Respuesta
Regresa un [objeto plan](#objeto-plan) creado o un error en caso de ocurrir algún problema.


##Actualizar un plan existente

> Definición

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
#Cliente
@plans=@openpay.create(:plans)
@plans.update(request_hash, plan_id)
```

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
 
Actualiza la información de un plan. Se requiere tener el id del plan y solo se puede actualizar cierta información.

###Petición
Propiedad | Descripción
--------- | ------
name | ***string*** (opcional, longitud = 80) <br/>Nombre del Plan.
trial_days | ***numeric*** (opcional) <br/>Numero de días de prueba por defecto que tendrán las suscripciones que se creen a partir del plan creado.

###Respuesta
Regresa un [objeto plan](#objeto-plan) con la información actualizada o una [respuesta de error](#objeto-error) si ocurrió algún problema en la actualización.

##Obtener un plan

> Definición

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
#Cliente
@plans=@openpay.create(:plans)
@plans.get(plan_id)
```

> Ejemplo de petición 

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

> Ejemplo de respuesta

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

Obtiene los detalles de un plan.

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador del plan.

###Respuesta
Regresa un [objeto plan](#objeto-plan)

##Eliminar un plan

> Definición

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
#Cliente
@plans=@openpay.create(:plans)
@plans.delete(plan_id)
```

> Ejemplo de petición 

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

Al eliminar un plan no se permitirán crear mas suscripciones asociadas a él, sin embargo las suscripciones ya asociadas se mantienen y se continuan cobrando.

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador del plan a eliminar

###Respuesta
Si el plan se borra correctamente la respuesta es vacía, si no se puede borrar se regresa un [objeto error](#objeto-error) indicando el motivo. 

##Listado de planes
> Definición

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
#Cliente
@plans=@openpay.create(:plans)
@plans.all
```

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
Regresa los detalles de todos los planes que están activos.

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
Listado de [objetos plan](#objeto-plan) registrados de acuerdo a los parámetros proporcionados, ordenadas por fecha de creación en orden descendente.


#Suscripciones

Las suscripciones permiten asociar un cliente y una tarjeta para que se pueden realizar cargos recurrentes.

Para poder suscribir algún cliente es necesario primero [crear un plan](#crear-una-nuevo-plan).

##Objeto Suscripción

> Ejemplo de objeto 

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

Propiedad | Descripción
--------- | ------
id | ***string*** <br/> Identificador único del Plan.
creation_date | ***datetime*** <br/> Fecha y hora en que se creó la suscripción  en formato ISO 8601
cancel_at_period_end  | ***string*** <br/> Indica si se cancela la suscripción al terminar el periodo.
charge_date | ***numeric*** <br/> Fecha en la que se cobrar la suscripción.
current_period_number | ***string*** <br/> Indica el periodo actual a cobrar.
period_end_date | ***numeric*** <br/> Fecha en la que se termina el periodo actual, un día antes del siguiente cobro.
trial_end_date | ***string*** <br/> Fecha en la que termina el periodo de prueba. Un día después de esta fecha, se realiza el primer cargo.
plan_id | ***numeric*** <br/>  Identificador del plan sobre el que se crea la suscripción.
status | ***string*** <br/> Estado de la suscripción puede ser active, "trial", "past_due", "unpaid", o "cancelled". Si la suscripción tiene periodo de prueba, se pone en status "trial", si no tiene periodo de prueba, o cuando termino el periodo de prueba y se logro efectuar el primer pago, se pone en "active", cuando el cobro no logro efectuarse, se coloca en "past_due", y cuando se agotan los intentos de cobro, se coloca de acuerdo a la configuración del plan, en "unpaid" o en "cancelled". Cuando se coloca en "unpaid", y se quiere reactivar la suscripción, es necesario actualizar el medio de pago (tarjeta) de la suscripción. En cualquier otro caso, el status se establece como "cancelled".
customer_id | ***string*** <br/> Identificador del customer al que pertenece la suscripción.
card | ***object*** <br/> Medio de pago con el cual se cobrará la suscripción. Ver [objeto tarjeta](#objeto-tarjeta)


##Crear una nueva suscripción

> Definición

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
#Cliente
@subscriptions=@openpay.create(:subscriptions)
@subscriptions.create(request_hash, customer_id)
```

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
 
Crea una suscripción para un cliente existente. Se puede ocupar una tarjeta previamente creada o se pueden enviar los datos de la tarjeta en donde se realizarán los cargos.

###Petición
Propiedad | Descripción
--------- | ------
plan_id | ***string*** (requerido, longitud = 45) <br/> Identificador del plan sobre el que se crea la suscripción.
trial_end_date | ***string*** (opcional, longitud = 10) <br/> Último día de prueba del cliente. Si no se indica se utilizará el valor de trial_days del plan para calcularlo. Si se indica una fecha anterior al día de hoy, se interpretará como una suscripción sin días de prueba. (Con formato yyy-mm-dd)
source_id | ***string*** (requerido si no se envía card, longitud = 45) <br/> Identificador del token o la tarjeta previamente registrada al cliente con la que se cobrará la suscripción. 
card | ***object*** (requerido si no se envía source_id) <br/> Medio de pago con el cual se cobrará la suscripción. Ver [objeto tarjeta](#objeto-tarjeta)

###Respuesta
Regresa el [objeto suscripción](#objeto-suscripción) creado o una [respuesta de error](#objeto-error) si ocurrió algún problema en la creación.

##Actualizar una suscripción

> Definición

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
#Cliente
@subscriptions=@openpay.create(:subscriptions)
@subscriptions.update(request_hash, customer_id)
```

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
Actualiza la información de una suscripción activa.

###Petición
Propiedad | Descripción
--------- | ------
cancel_at_period_end | ***booelan*** (opcional) <br/> Indica si se cancela la suscripción al terminar el periodo.
trial_end_date | ***string*** (opcional, longitud = 10) <br/> Último día de prueba del cliente. Si no se indica se utilizará el valor de trial_days del plan para calcularlo. Si se indica una fecha anterior al día de hoy, se interpretará como una suscripción sin días de prueba. (Con formato yyy-mm-dd)
source_id | ***string*** (opcional, longitud = 45) <br/> Identificador del token o la tarjeta previamente registrada al cliente con la que se cobrará la suscripción. 
card | ***object*** (opcional) <br/> Medio de pago con el cual se cobrará la suscripción. Ver [objeto tarjeta](#objeto-tarjeta)

###Respuesta
Regresa el [objeto suscripción](#objeto-suscripción) actualizado o una [respuesta de error](#objeto-error) si ocurrió algún problema en la actualización.

##Obtener un suscripción

> Definición

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
#Cliente
@subscriptions=@openpay.create(:subscriptions)
@subscriptions.get(subscription_id,customer_id)
```

> Ejemplo de petición 

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

> Ejemplo de respuesta

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

Obtiene los detalles de la suscripción de un cliente.

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador de la suscripción

###Respuesta
Regresa un [objeto suscripción](#objeto-suscripción)


##Cancelar suscripción

> Definición

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
#Cliente
@subscriptions=@openpay.create(:subscriptions)
@subscriptions.delete(subscription_id, customer_id)
```

> Ejemplo de petición 

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

Cancela inmediatamente la suscrupción del cliente. Ya no se realizarán mas cargos a la tarjeta y todos cargos pendientes se cancelarán.

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador del plan a eliminar

###Respuesta
Si la suscripción se cancelo correctamente la respuesta es vacía, si no se regresa un [objeto error](#objeto-error) indicando el motivo. 

##Listado de suscripciones
> Definición

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
#Cliente
@subscriptions=@openpay.create(:subscriptions)
@subscriptions.all(customer_id)
```

> Ejemplo de petición 

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

> Ejemplo de respuesta

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
Regresa los detalles de todas las suscripciones activas para un cliente en específico.

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
Listado de [objetos suscripción](#objeto-suscripción) que tiene el cliente. Ordenados por fecha de creación en orden descendente.


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

#Tokens

El objetivo de generar tokens es que se capture la información de la tarjeta desde el navegador o dispositivo del usuario final para que dicha información no viaje a través de tu servidor y así puede evitar o reducir certificaciones PCI.

Para usar esta funcionalidad de la API, te recomendamos usar nuestra librería en JavaScript para cuando tu aplicación este en Web y nuestros SDK's de Android o iOS para cuando este en móvil.

**Características**

* Se crean a nivel comercio
* No se ligan a ningún cliente
* Después de crearse solo se puede usar una sola vez, para hacer un cargo con token

##Objeto Token

> Ejemplo de objeto 

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
         "brand":"visa"
      }
   }
```

Propiedad | Descripción
--------- | ------
id | ***string*** <br/>Identificador del token. Esté es el que deberás usar para posteriormente hacer un cargo.
card | ***object*** <br/>Datos de la tarjeta asociada al token. Ver [objeto tarjeta](#objeto-tarjeta)


##Crear un nuevo token

> Definición

```
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/tokens
```

> Ejemplo de petición 

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
      "city":"Querétaro",
      "country_code":"MX",
      "postal_code":"76900",
      "line1":"Av 5 de Febrero",
      "line2":"Roble 207",
      "line3":"col carrillo",
      "state":"Queretaro"
   }
}' 
```

> Ejemplo de respuesta

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
         "city":"Querétaro",
         "postal_code":"76900",
         "country_code":"MX"
      },
      "creation_date":null,
      "brand":"visa"
   }
}
```

Para la creación de un token en Openpay es necesario enviar el objeto con la información a registrar. Una vez guardado el token no se puede obtener el número y código de seguridad ya que esta información es encriptada.

###Petición

Propiedad | Descripción
--------- | ------
holder_name |***string*** (requerido) <br/>Nombre del tarjeta habiente.
card_number |***numeric*** (requerido) <br/>Numero de tarjeta puede ser de 16 o 19 dígitos.
cvv2 |***numeric*** (requerido) <br/>Código de seguridad como aparece en la parte de atrás de la tarjeta. Generalmente 3 dígitos.
expiration_month |***numeric*** (requerido) <br/>Mes de expiración tal como aparece en la tarjeta.
expiration_year |***numeric*** (requerido) <br/>Año de expiración tal como aparece en la tarjeta.
address |***object*** (opcional)<br/>Dirección de facturación del tarjeta habiente.

###Repuesta
Regresa el [objeto token](#objeto-token) creado o una [respuesta de error](#objeto-error) si ocurrió algún problema en la creación.


##Obtener un token

> Definición

```
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/tokens/{TOKEN_ID}
```

> Ejemplo de petición 

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/tokens/k1n0mscnjwhxqia8q7cm \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
``` 

> Ejemplo de respuesta

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
         "city":"Querétaro",
         "postal_code":"76900",
         "country_code":"MX"
      },
      "creation_date":null,
      "brand":"visa"
   }
}
```

Obtiene los detalles de un token. Es necesario tener el id. 

<aside class="notice">
**Nota:** Nunca se regresarán datos sensibles como son el código de seguridad y del número de tarjeta.
</aside>

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador de token.

###Respuesta
Regresa un [objeto token](#objeto-token)


#Comercio

El objeto comercio permite consultar la información de tu cuenta a través de la API.

##Objeto Comercio

> Ejemplo de Objeto:

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

Propiedad | Descripción
--------- | -----------
id|***string*** <br/>Identificador único asignado al momento de su creación.
creation_date|***datetime*** <br/>Fecha de creación de la transacción en formato ISO 8601.
name|***string*** <br/>Nombre del comercio con el que se registró el comercio.
email|***string*** <br/>Cuenta de correo electrónico registrada para el comercio.
phone|***string*** <br/>Número teléfonico registrado del comercio.
status| ***string*** <br/>Estatus de la cuenta del Comercio puede ser active o deleted. Si la cuenta se encuentra en estatus deleted no se permite realizar ninguna transacción.
balance| ***numeric*** <br/>Saldo en la cuenta con dos decimales.
clabe | ***numeric***   <br/>Cuenta CLABE asociada con la que puede recibir fondos realizando una transferencia desde cualquier banco en México vía SPEI.

##Obtener un comercio

> Definición

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}
```

```php
<?
// =============================
// Funcionalidad no implementada
// =============================
?>
```

```java
openpayAPI.merchant().get();
```

```csharp
// =============================
// Funcionalidad no implementada
// =============================
```

```javascript
openpay.merchant.get(callback);
```

```ruby
# =============================
# Funcionalidad no implementada
# =============================
```

> Ejemplo de petición

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

> Ejemplo de respuesta

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

Obtiene los detalles la cuenta del comercio. Solo se requiere indicar el id unico del comercio que se quiere obtener.

###Petición

Propiedad     | Descripción
--------- | -----------
id | ***string*** (requerido, longitud = 45) <br>identificador único del comercio.

###Respuesta
Si el identificador es correcto regresa un objeto comercio. 

#Comisiones de Openpay

El reporte de comisiones cobradas al comercio permite ver un resumen de las comisiones que Openpay te ha cobrado o reembolsado, 
así como un detalle de las transacciones que generaron estas comisiones.

##Objeto Resumen de Comisiones de Openpay

> Ejemplo de Objeto:

```json
{
   "charged": 223.28,
   "charged_tax": 35.70,
   "charged_adjustments": 30.14,
   "charged_adjustments_tax": 4.80,
   "refunded": 5.57,
   "refunded_tax": 0.89,
   "refunded_adjustments": 0.00,
   "refunded_adjustments_tax": 0.00,
   "total": 287.46
}
```

Propiedad | Descripción
--------- | -----------
charged|***numeric*** <br/>Total de comisiones generadas por transacciones del comercio en el periodo.
charged_tax|***numeric*** <br/>IVA de las comisiones generadas en el periodo.
charged_adjustments|***numeric*** <br/>Total de comisiones generadas por circunstancias extraordinarias.
charged_adjustments_tax|***numeric*** <br/>IVA de las comisiones generadas por circunstancias extraordinarias.
refunded|***numeric*** <br/>Total de comisiones devueltas por transacciones reembolsadas del comercio en el periodo.
refunded_tax|***numeric*** <br/>IVA de las comisiones reembolsadas en el periodo.
refunded_adjustments|***numeric*** <br/>Total de comisiones reembolsadas por circunstancias extraordinarias.
refunded_adjustments_tax|***numeric*** <br/>IVA de las comisiones reembolsadas por circunstancias extraordinarias.
charged|***numeric*** <br/>Suma de las comisiones generadas menos la suma de las comisiones reembolsadas en el periodo.

##Obtener resumen

> Definición

```
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/reports/fees?year={YEAR}&month={MONTH}
```

> Ejemplo de petición

```shell
curl -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
  "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/reports/fees?year=2014&month=06"
   
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", 
                      "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
OpenpayFeesSummary = api.openpayFees().getSummary(2014, 06);
```

> Ejemplo de respuesta

```json
{
   "charged": 230.34,
   "charged_tax": 36.85,
   "charged_adjustments": 0.00,
   "charged_adjustments_tax": 0.00,
   "refunded": 16.00,
   "refunded_tax": 2.56,
   "refunded_adjustments": 0.00,
   "refunded_adjustments_tax": 0.00,
   "total": 248.63
}
```

Obtiene el resumen de las comisiones cobradas y reembolsadas en el mes por Openpay. Se debe indicar el periodo que se quiere obtener:

###Petición

Propiedad     | Descripción
--------- | -----------
year | ***numeric*** (requerido) <br>Año del periodo a buscar
month| ***numeric*** (requerido) <br>Mes del periodo a buscar

###Respuesta
Regresa un objeto de resumen de comisiones de Openpay 

##Obtener detalle

> Definición

```
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/reports/fees/detail?year={YEAR}&month={MONTH}&fee_type={FEE_TYPE}
```

> Ejemplo de petición

```shell
curl -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
 "https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/reports/fees/detail?year=2014&month=07&fee_type=charged" 
   
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", 
                      "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
OpenpayFeesSummary = api.openpayFees().getDetails(2014, 07, FeeDetailsType.CHARGED);
```

> Ejemplo de respuesta

```json
[
  {
    "id": "tr8pxmww5pqwbatjimli",
    "amount": 100.00,
    "authorization": "801585",
    "method": "card",
    "operation_type": "in",
    "transaction_type": "charge",
    "card": {
      "id": "kv8xrqnef2o8xmtruhez",
      "type": "debit",
      "brand": "mastercard",
      "address": null,
      "card_number": "555555XXXXXX4444",
      "holder_name": "Juan Pérez Nuñez",
      "expiration_year": "14",
      "expiration_month": "09",
      "allows_charges": true,
      "allows_payouts": false,
      "creation_date": "2014-02-21T11:35:31-06:00",
      "bank_name": "BANCO SANTANDER SERFIN",
      "customer_id": "an8x3tmhl9hwnnl8ppc0",
      "bank_code": "000"
    },
    "status": "completed",
    "currency": "MXN",
    "creation_date": "2014-07-13T12:00:01-05:00",
    "operation_date": "2014-07-13T12:00:06-05:00",
    "description": "Cargo de tarjeta",
    "error_message": null,
    "order_id": null,
    "fee": {
      "amount": 4.9000,
      "tax": 0.78
    },
    "subscription_id": "sxyrqjudamef8zqrkge1"
  },
  {
    "id": "tr9idi4vwc4iliwwbpar",
    "amount": 100.00,
    "authorization": "801585",
    "method": "card",
    "operation_type": "in",
    "transaction_type": "charge",
    "card": {
      "type": "credit",
      "brand": "visa",
      "address": null,
      "card_number": "424242XXXXXX4242",
      "holder_name": "Usuario 6 Tarjeta",
      "expiration_year": "15",
      "expiration_month": "12",
      "allows_charges": true,
      "allows_payouts": false,
      "bank_name": "BANCOMER",
      "bank_code": "012"
    },
    "status": "completed",
    "currency": "MXN",
    "creation_date": "2014-07-11T12:00:17-05:00",
    "operation_date": "2014-07-11T12:00:18-05:00",
    "description": "Cargo de tarjeta",
    "error_message": null,
    "order_id": null,
    "customer_id": "a0zvgga50evtlvcpok8i",
    "fee": {
      "amount": 4.9000,
      "tax": 0.78
    },
    "subscription_id": "svquljrfcwwh9g0ggejk"
  }
]
```

Obtiene el resumen de las comisiones cobradas y reembolsadas en el mes por Openpay. Se debe indicar el periodo que se quiere obtener
y el tipo de fees que se quiere ver a detalle:

###Petición

Propiedad     | Descripción
--------- | -----------
year | ***numeric*** (requerido) <br>Año del periodo a buscar
month| ***numeric*** (requerido) <br>Mes del periodo a buscar
fee_type| ***string*** (requerido) <br>Tipo de detalle a ver. Los valores permitidos son "charged", "refunded", "charged_adjustments" y "refunded_adjustments".

###Respuesta
Regresa una lista de transacciones que afectaron los fees. 

En el caso de los detalles de tipo "charged" y "refunded", las transacciones tendrán un objeto fee, dentro del cual contienen el monto de la comisión y su IVA. 

En el caso de "charged_adjustments" y "refunded_adjustments", las comisiones cobradas se encuentran en su propiedad amount.

#Objetos Comunes

Información de objetos compartidos en peticiones y respuestas.

##Objeto Transacción

> Ejemplo de Objeto:

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
   "description":"Pago de ganancias",
   "error_message":null,
   "customer_id":"afk4csrazjp1udezj1po",
   "bank_account":{
      "alias":null,
      "bank_name":"BANCOMER",
      "creation_date":"2013-11-14T18:29:34-06:00",
      "clabe":"012298026516924616",
      "holder_name":"Juan Tapia Trejo",
      "bank_code":"012"
   }
}
```

Propiedad | Descripción
--------- | -----------
id | _**string**_ <br/> Identificador único asignado por Openpay al momento de su creación.
authorization | ***string*** <br/>Número de autorización generado por el procesador.
transaction_type| ***string*** <br/>Tipo de transacción que fue creada: fee, charge, payout, transfer.
operation_type| ***string*** <br/>Tipo de afectación en la cuenta: in, out. 
method| ***string*** <br/>Tipo de método usado en la transacción: card, bank o customer.
creation_date| ***datetime***  <br/>Fecha de creación de la transacción en formato ISO 8601.
order_id| ***string*** <br/>Referencia única o número de orden/transacción.
status| ***string*** <br/>Estatus actual de la transacción. Posibles valores: completed, in_progress, failed.
amount| ***numeric*** <br/>Cantidad de la transacción a dos decimales.
description|***string*** <br/>Descripción de la transacción.
error_message| ***string*** <br/>Si la transacción está en status: failed, en este campo se mostrará la razón del fallo.
customer_id| ***string*** <br/>Identificar único del cliente al cual pertence la transacción. Si es valor es nulo, la transacción pertenece a la cuenta del comercio.
currency| ***string*** <br/>Moneda usada en la operación, por default es MXN. 
bank_account| ***objeto*** <br/>Datos de la cuenta bancaria usada en la transacción. Ver objeto BankAccoount
card| ***objeto*** <br/>Datos de la tarjeta usada en la transacción. Ver objeto Card

##Objeto Dirección

> Ejemplo de Objeto:

```json
{
   "line1":"Av 5 de Febrero",
   "line2":"Roble 207",
   "line3":"col carrillo",
   "state":"Queretaro",
   "city":"Querétaro",
   "postal_code":"76900",
   "country_code":"MX" 
}
```

Propiedad | Descripción
--------- | -----------
line1 | ***string*** (requerido) <br/>Primera línea de dirección del tarjeta habiente. Usada comúnmente para indicar la calle y número exterior e interior.
line2 | ***string*** <br/>Segunda línea de la dirección del tarjeta habiente. Usada comúnmente para indicar condominio, suite o delegación.
line3 | ***string*** <br/>Tercer línea de la dirección del tarjeta habiente. Usada comúnmente para indicar la colonia.
postal_code | ***string*** (requerido) <br/>Código postal del tarjeta habiente
state | ***string*** (requerido) <br/>Estado del tarjeta habiente
city | ***string*** (requerido) <br/>Ciudad del tarjeta habiente
country_code | ***string*** (requerido) <br/>Código del país del tarjeta habiente a dos caracteres en formato ISO_3166-1
