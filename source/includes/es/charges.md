#Cargos
Los cargos se pueden realizar a tarjetas de crédito o debito. A cada cargo se le asigna un identificador único en el sistema.

En cargos a tarjeta puedes hacerlo usando un token o desplegando un formulario para que el usuario capture los datos de la tarjeta.

##Con tarjeta

> Definición

```shell
Comercio
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges

Cliente
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

```php
<?
Comercio
$bancomer->charges->create(chargeRequest);

Cliente
$customer = $bancomer->customers->get($customerId);
$customer->charges->create(chargeRequest);
?>
```

```java
//Cliente
bancomerAPI.charges().create(String customerId, List<Parameter> request);

//Comercio
bancomerAPI.charges().create(List<Parameter> request);
```

```csharp
//Cliente
bancomerAPI.ChargeService.Create(string customer_id, List<IParameter> request);

//Comercio
bancomerAPI.ChargeService.Create(List<IParameter> request);
```

```ruby
#Cliente
@charges=@bancomer.create(:charges)
@charges.create(request_hash, customer_id)

#Comercio
@charges=@bancomer.create(:charges)
@charges.create(request_hash)
```

> Ejemplo de petición con comercio

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "affiliation_bbva" : "720939",
   "amount" : 100,
   "description" : "Cargo inicial a mi cuenta",
   "currency" : "MXN",
   "order_id" : "oid-00051"
}'
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

List<IParameter> request = List<IParameter> {
    new SingleParameter("affiliation_bbva", "720931"),
    new SingleParameter("amount", "200.00"),
    new SingleParameter("description", "Test Charge"),
    new SingleParameter("customer_language", "SP"),
    new SingleParameter("use_card_points", "NONE"),
    new SingleParameter("currency", "MXN"),
    new SingleParameter("order_id", "oid-00051"),
    new SingleParameter("redirect_url", "https://sand-portal.ecommercebbva.com")
};

Dictionary<String, Object> chargeDictionary = bancomerAPI.ChargeService.Create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```java
BancomerAPI api = new BancomerAPI(
        "https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

List<Parameter> request = new ArrayList<Parameter>(Arrays.asList(
    new SingleParameter("affiliation_bbva", "720931"),
    new SingleParameter("amount", "10.00"),
    new SingleParameter("description", "Cargo inicial"),
    new SingleParameter("customer_language", "SP"),
    new SingleParameter("use_card_points", "NONE"),
    new SingleParameter("currency", "MXN"),
    new SingleParameter("order_id", "oid-00051"),
    new SingleParameter("redirect_url", "https://sand-portal.ecommercebbva.com")
));

Map chargeAsMap = api.charges().create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```php
<?
$bancomer = Bancomer::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$chargeRequest = array(
    'affiliation_bbva' => '720931',
    'amount' => 100,
    'description' => 'Cargo inicial a mi merchant',
    'customer_language' => 'SP',
    'use_card_points' => 'FALSE',
    'currency' => 'MXN'
    'order_id' => 'oid-00051'
    'redirect_url' => 'https://sand-portal.ecommercebbva.com');

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
      "bank_code":"002"
   },
   "status":"completed",
   "currency":"USD",
   "exchange_rate" : {
      "from" : "USD",
      "date" : "2014-11-21",
      "value" : 13.61,
      "to" : "MXN"
   },
   "creation_date":"2014-05-26T11:02:45-05:00",
   "operation_date":"2014-05-26T11:02:45-05:00",
   "description":"Cargo inicial a mi cuenta",
   "error_message":null,
   "order_id":"oid-00051"
}
```

<aside class="notice">
Puedes realizar el cargo a la cuenta del comercio. </br>
</aside>

***Sistema antifraude personalizado***</br>
Es posible enviar información adicional a la plataforma para incrementar su base de conocimientos, esto le permitirá aplicar reglas personalizadas de acuerdo al giro del comercio y de manera oportuna, con el propósito de detectar con la mayor efectividad posible los intentos de fraude.

<aside class="notice">
Para utilizar esta característica es necesario enviar como parte del contenido de la transacción, la propiedad <code>metadata</code>, el cual contendrá un listado de campos personalizados de antrifraude, con la información propia del comercio que se desea tomar en cuenta al momento de validar y aplicar un cargo. Póngase en contacto con el departamento de soporte para habilitar esta funcion. </br>
</aside>


###Petición

Propiedad | Descripción
--------- | -----
affiliation_bbva|***string*** (requerido) <br/>Debe contener el número de afiliación.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
currency | ***string*** (opcional) <br/>Tipo de moneda del cargo. Por el momento solo se soportan 2 tipos de monedas: Pesos Mexicanos(MXN) y Dólares Americanos(USD).
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
[customer](#objeto-cliente)|***objeto*** (requerido) <br/>Información del cliente al que se le realiza el cargo. Se puede ocupar los mismos parámetros usados en la creación de un cliente pero no se creará una cuenta al cliente. <br/><br/> **Nota:** Este parámetro solo se puede utilizar creando el cargo a nivel comercio<br/><br/>Si desea crear un cliente y llevar un historial de sus cargos consulte como [Objeto Cliente](#objeto-cliente) y realice el cargo a nivel cliente.
customer_language | ***string*** (requerido, longitud = 2) <br/>Idioma a usarse en el recibo y la pantalla de compra, actualmente se aceptan dos valores SP-Español En-Inglés.
[payment_plan](#objeto-paymentplan)|***objeto*** (opcional) <br/>Datos del plan de meses sin intereses que se desea utilizar en el cargo. Ver [Objeto PaymentPlan](#objeto-paymentplan).
redirect_url | ***string*** (requerido) <br/>Usado para cargos de tipo redirect. Indica la url a la que redireccionar despues de una transaccion exitosa en el fomulario de pago de bancomer.
use_card_points | ***string*** (opcional, default = NONE) <br/> <table><tr><td><strong>ONLY_POINTS</strong></td> <td>Cargo solo con puntos (<a href="#consulta-de-puntos">Consulta de puntos</a>)</td></tr><tr><td><strong>MIXED</strong></td>       <td>Cargo con pesos y puntos</td></tr><tr><td><strong>NONE</strong></td>        <td>Cargo solo con pesos</td></tr></table>Los valores que indican puntos solo se deben usarse si la propiedad points_card de la tarjeta es true, de otra forma ocurrirá un error.
use_3d_secure | ***string*** (opcional) <br/>Por defecto el valor es TRUE, si el comercio tiene habilitada la configuración para no utilizar 3d secure, entonces podrá enviar el parámetro en FALSE.
metadata |  ***list(key, value)*** (opcional) <br/>Listado de campos personalizados de antifraude, estos campos deben de apegarse a las [reglas para creación de campos personalizados de antifraude](#reglas-para-creación-de-campos-personalizados-de-antifraude)
capture |  ***boolean*** (opcional, default = true) <br/>Indica si el cargo se hace o no inmediatamente, cuando el valor es false el cargo se maneja como una autorización (o preautorización) y solo se reserva el monto para ser confirmado o cancelado en una segunda llamada.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).


##Confirmar un cargo

> Definición

```shell
Comercio
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/capture

Cliente
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}/capture
```

```php
<?
Comercio
$charge = $bancomer->charges->get(transactionId);
$charge->capture(captureData);

Cliente
$customer = $bancomer->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
$charge->capture(captureData);
?>
```

```java
//Cliente
bancomerAPI.charges().confirmCapture(String customerId, ConfirmCaptureParams request);

//Comercio
bancomerAPI.charges().confirmCapture(ConfirmCaptureParams request);
```

```csharp
//Cliente
bancomerAPI.ChargeService.Capture(string customer_id, string transaction_id, Decimal? amount);

//Comercio
bancomerAPI.ChargeService.Capture(string transaction_id, Decimal? amount);
```

```ruby
#Cliente
@charges=@bancomer.create(:charges)
@charges.capture(transaction_id, customer_id)

#Comercio
@charges=@bancomer.create(:charges)
@charges.capture(transaction_id)
```

> Ejemplo de petición con cliente

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
BancomerAPI api = new BancomerAPI(
        "https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
ConfirmCaptureParams request = new ConfirmCaptureParams();
request.chargeId("tryqihxac3msedn4yxed");
request.amount(new BigDecimal("100.00"));

Map chargeAsMap = api.charges().confirmCapture("ag4nktpdzebjiye1tlze", request);
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Dictionary<String, Object> chargeDictionary = api.ChargeService
                                        .Capture("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", new Decimal(100.00));
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```ruby
@bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bancomer.create(:charges)

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
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).

##Devolver un cargo

> Definición

```shell
Comercio
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/refund

Cliente
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}/refund
```

```php
<?
Comercio
$charge = $bancomer->charges->get(transactionId);
$charge->refund(refundData);

Cliente
$customer = $bancomer->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
$charge->refund(refundData);
?>
```

```java
//Cliente
bancomerAPI.charges().refund(String customerId, RefundParams request);

//Comercio
bancomerAPI.charges().refund(RefundParams request);
```

```csharp
//Cliente
bancomerAPI.ChargeService.Refund(string customer_id, string transaction_id, string description);

//Comercio
bancomerAPI.ChargeService.Refund(string transaction_id, string description);
```

```ruby
#Cliente
@charges=@bancomer.create(:charges)
@charges.refund(transaction_id, request_hash, customer_id)

#Comercio
@charges=@bancomer.create(:charges)
@charges.refund(transaction_id, request_hash)
```

> Ejemplo de petición con cliente

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
BancomerAPI api = new BancomerAPI(
        "https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
RefundParams request = new RefundParams();
request.chargeId("tryqihxac3msedn4yxed");
request.description("Monto de cargo devuelto");
request.amount(new BigDecimal("100.00"));

Map chargeAsMap = api.charges().refund("ag4nktpdzebjiye1tlze", request);
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Dictionary<String, Object> chargeDictionary = api.ChargeService
            .Refund("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", "Monto de cargo devuelto", , new Decimal(100.00));
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
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
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}

Comercio
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges/{TRANSACTION_ID}
```

```php
<?
Comercio
$charge = $bancomer->charges->get(transactionId);

Cliente
$customer = $bancomer->customers->get(customerId);
$charge = $customer->charges->get(transactionId);
?>
```

```java
//Cliente
bancomerAPI.charges().get(String customerId, String transactionId);

//Comercio
bancomerAPI.charges().get(String transactionId);
```

```csharp
//Cliente
bancomerAPI.ChargeService.Get(string customer_id, string transaction_id);

//Comercio
bancomerAPI.ChargeService.Get(string transaction_id);
```

```ruby
#Cliente
@charges=@bancomer.create(:charges)
@charges.get(transaction_id, customerId)

#Comercio
@charges=@bancomer.create(:charges)
@charges.get(transaction_id)
```

> Ejemplo de petición con cliente

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
BancomerAPI api = new BancomerAPI(
        "https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Map chargeAsMap = api.charges().get("ag4nktpdzebjiye1tlze", "tr6cxbcefzatd10guvvw");
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Dictionary<String, Object> chargeDictionary = api.ChargeService.Get("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed");
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```ruby
@bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bancomer.create(:charges)

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
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).
