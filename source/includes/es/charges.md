#Cargos
Los cargos se pueden realizar a tarjetas de crédito o débito. A cada cargo se le asigna un identificador único en el sistema.

En cargos a tarjeta puedes hacerlo desplegando un formulario para que el usuario capture los datos de la tarjeta.

##Con VPOS

Este tipo de cargo no requiere una tarjeta guardada o que hayas generado un token.

> Definición

```shell
Comercio
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges
```

```php
<?
Comercio
$bancomer->charges->create(chargeRequest);
?>
```

```java
//Comercio
bancomerAPI.charges().create(List<Parameter> request);
```

```csharp
//Comercio
bancomerAPI.ChargeService.Create(List<IParameter> request);
```

```ruby
#Comercio
@charges=@bancomer.create(:charges)
@charges.create(request_hash)
```

> Ejemplo de petición con comercio

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "affiliation_bbva" : "781500",
   "amount" : 100,
   "description" : "Cargo inicial a mi cuenta",
   "currency" : "MXN",
   "order_id" : "oid-00051",
   "customer": {
        "name": "Juan",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.com.mx",
        "phone_number": "555-444-3322"
   },
   "redirect_url": "https://sand-portal.ecommercebbva.com"
}'
```

```csharp
BancomerAPI api = new BancomerAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");

ParameterContainer customer = new ParameterContainer("customer");
    customer.AddValue("name", "Juan");
    customer.AddValue("last_name", "Vazquez Juarez");
    customer.AddValue("email", "juan.vazquez@empresa.com.mx");
    customer.AddValue("phone_number", "554-170-3567");

ParameterContainer request = new ParameterContainer("charge");
    request.AddValue("affiliation_bbva", "781500");
    request.AddValue("amount", "100.00");
    request.AddValue("description", "Cargo inicial a mi merchant");
    request.AddValue("currency", "MXN");
    request.AddValue("order_id", "oid-00051");
    request.AddValue("redirect_url", "https://sand-portal.ecommercebbva.com");
    request.AddMultiValue(customer):

Dictionary<String, Object> chargeDictionary = bancomerAPI.ChargeService.Create(request.ParameterValues);
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```java
BancomerAPI api = new BancomerAPI(
        "https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");

ParameterContainer customer = new ParameterContainer("customer");
    customer.addValue("name", "Juan");
    customer.addValue("last_name", "Vazquez Juarez");
    customer.addValue("email", "juan.vazquez@empresa.com.mx");
    customer.addValue("phone_number", "554-170-3567");

ParameterContainer charge = new ParameterContainer("charge");
    charge.addValue("affiliation_bbva", "781500");
    charge.addValue("amount", "100.00");
    charge.addValue("description", "Cargo inicial a mi merchant");
    charge.addValue("currency", "MXN");
    charge.addValue("order_id", "oid-00051");
    charge.addValue("redirect_url", "https://sand-portal.ecommercebbva.com");
    charge.addMultiValue(customer);

Map chargeAsMap = api.charges().create(charge.getParameterValues());
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```php
<?
$bancomer = Bancomer::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$chargeRequest = array(
    'affiliation_bbva' => '781500',
    'amount' => 100,
    'description' => 'Cargo inicial a mi merchant',
    'currency' => 'MXN',
    'order_id' => 'oid-00051',
    'redirect_url' => 'https://sand-portal.ecommercebbva.com',
    'customer' => array(
        'name' => 'Juan',
        'last_name' => 'Vazquez Juarez',
        'email' => 'juan.vazquez@empresa.com.mx',
        'phone_number' => '554-170-3567')
);

$charge = $bancomer->charges->create($chargeRequest);
?>
```

```ruby
@bancomer=BancomerApi.new("mptdggroasfcmqs8plpy","sk_326c6d0443f6457aae29ffbd48f7d1be")
@charges=@bancomer.create(:charges)
customer_hash={
    "name" => "Juan",
    "last_name" => "Vazquez Juarez",
    "phone_number" => "4423456723",
    "email" => "juan.vazquez@empresa.com.mx"
}

request_hash={
    "affiliation_bbva" => "781500",
    "amount" => 100.00,
    "currency" => "MXN",
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
    "redirect_url" => "https://sand-portal.ecommercebbva.com",
    "customer" => customer_hash
}

response_hash=@charges.create(request_hash.to_hash)
```

> Ejemplo de respuesta

```json
{
    "id": "trz8v1n3g992xtylohts",
    "authorization": null,
    "operation_type": "in",
    "method": "card",
    "transaction_type": "charge",
    "status": "charge_pending",
    "conciliated": false,
    "creation_date": "2019-04-03T03:57:58-06:00",
    "operation_date": "2019-04-03T03:57:58-06:00",
    "description": "Pago",
    "error_message": null,
    "order_id": "oid-00051",
    "payment_method": {
        "type": "redirect",
        "url": "https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/trywj1kyx7vczirifkyw/card_capture"
    },
    "currency": "MXN",
    "amount": 100.00,
    "customer": {
        "name": "Juan",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.com.mx",
        "phone_number": "555-444-3322",
        "address": null,
        "creation_date": "2019-04-03T03:57:58-06:00",
        "external_id": null,
        "clabe": null
    }
}
```

###Petición

Propiedad | Descripción
--------- | -----
affiliation_bbva|***string*** (requerido) <br/>Debe contener el número de afiliación.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
currency | ***string*** (opcional) <br/>Tipo de moneda del cargo. Por el momento solo se soportan 2 tipos de monedas: Pesos Mexicanos(MXN) y Dólares Americanos(USD).
order_id | ***string*** (requerido, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.
[customer](#objeto-cliente)|***objeto*** (requerido) <br/>Información del cliente al que se le realiza el cargo. Se puede ocupar los mismos parámetros usados en la creación de un cliente pero no se creará una cuenta al cliente. <br/><br/> **Nota:** Este parámetro solo se puede utilizar creando el cargo a nivel comercio<br/><br/>Si desea crear un cliente y llevar un historial de sus cargos consulte como [Objeto Cliente](#objeto-cliente) y realice el cargo a nivel cliente.
[payment_plan](#objeto-paymentplan)|***objeto*** (opcional) <br/>Datos del plan de meses sin intereses que se desea utilizar en el cargo. Ver [Objeto PaymentPlan](#objeto-paymentplan).
redirect_url | ***string*** (requerido) <br/>Usado para cargos de tipo redirect. Indica la url a la que redireccionar despues de una transaccion exitosa en el fomulario de pago de BBVA.
use_3d_secure | ***string*** (opcional) <br/>Por defecto el valor es TRUE, si el comercio tiene habilitada la configuración para no utilizar 3d secure, entonces podrá enviar el parámetro en FALSE.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).

## Con tarjeta

> Definición

```shell
Comercio
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges
```

```php
<?
Comercio
$bancomer->charges->create(chargeRequest);
?>
```

```java
//Comercio
bancomerAPI.charges().create(List<Parameter> request);
```

```csharp
//Comercio
bancomerAPI.ChargeService.Create(List<IParameter> request);
```

```ruby
#Comercio
@charges=@bancomer.create(:charges)
@charges.create(request_hash)
```

> Ejemplo de petición con comercio

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "affiliation_bbva" : "781500",
   "amount" : 100,
   "description" : "Cargo inicial a mi cuenta",
   "currency" : "MXN",
   "order_id" : "oid-00051",
   "customer": {
        "name": "Juan",
        "last_name": "Vazquez Juarez",
        "email": "juan.vazquez@empresa.com.mx",
        "phone_number": "555-444-3322"
   },
   "card" : {
        "holder_name" : "Juan Vazquez",
        "card_number" : "4242424242424242",
        "expiration_month" : "12",
        "expiration_year" : "21",
        "cvv2" : "842"

   }
   "redirect_url": "https://sand-portal.ecommercebbva.com"
}'
```

```csharp
BancomerAPI api = new BancomerAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");

ParameterContainer customer = new ParameterContainer("customer");
    customer.AddValue("name", "Juan");
    customer.AddValue("last_name", "Vazquez Juarez");
    customer.AddValue("email", "juan.vazquez@empresa.com.mx");
    customer.AddValue("phone_number", "554-170-3567");

ParameterContainer card = new ParameterContainer("card");
    customer.AddValue("holder_name", "Juan Vazquez Juarez");
    customer.AddValue("card_number", "4242424242424242");
    customer.AddValue("expiration_month", "12");
    customer.AddValue("expiration_year", "21");
    customer.AddValue("cvv2", "842");

ParameterContainer request = new ParameterContainer("charge");
    request.AddValue("affiliation_bbva", "781500");
    request.AddValue("amount", "100.00");
    request.AddValue("description", "Cargo inicial a mi merchant");
    request.AddValue("currency", "MXN");
    request.AddValue("order_id", "oid-00051");
    request.AddValue("redirect_url", "https://sand-portal.ecommercebbva.com");
    request.AddMultiValue(customer);
    request.AddMultiValue(card):

Dictionary<String, Object> chargeDictionary = bancomerAPI.ChargeService.Create(request.ParameterValues);
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```java
BancomerAPI api = new BancomerAPI(
        "https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");

ParameterContainer customer = new ParameterContainer("customer");
    customer.addValue("name", "Juan");
    customer.addValue("last_name", "Vazquez Juarez");
    customer.addValue("email", "juan.vazquez@empresa.com.mx");
    customer.addValue("phone_number", "554-170-3567");

ParameterContainer card = new ParameterContainer("card");
    card.addValue("card_number", "4242424242424242");
    card.addValue("holder_name", "Juan Vazquez");
    card.addValue("expiration_year", "21");
    card.addValue("expiration_month", "12");
    card.addValue("cvv2", "842");

ParameterContainer charge = new ParameterContainer("charge");
    charge.addValue("affiliation_bbva", "781500");
    charge.addValue("amount", "100.00");
    charge.addValue("description", "Cargo inicial a mi merchant");
    charge.addValue("currency", "MXN");
    charge.addValue("order_id", "oid-00051");
    charge.addValue("redirect_url", "https://sand-portal.ecommercebbva.com");
    charge.addMultiValue(customer);
    charge.addMultiValue(card);

Map chargeAsMap = api.charges().create(charge.getParameterValues());
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```php
<?
$bancomer = Bancomer::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$chargeRequest = array(
    'affiliation_bbva' => '781500',
    'amount' => 100,
    'description' => 'Cargo inicial a mi merchant',
    'currency' => 'MXN',
    'order_id' => 'oid-00051',
    'redirect_url' => 'https://sand-portal.ecommercebbva.com',
    'card' => array(
            'holder_name' => 'Juan Vazquez',
            'card_number' => '4242424242424242',
            'expiration_month' => '12',
            'expiration_year' => '21'
            'cvv2' => '842'),
    'customer' => array(
        'name' => 'Juan',
        'last_name' => 'Vazquez Juarez',
        'email' => 'juan.vazquez@empresa.com.mx',
        'phone_number' => '554-170-3567')
);

$charge = $bancomer->charges->create($chargeRequest);
?>
```

```ruby
@bancomer=BancomerApi.new("mptdggroasfcmqs8plpy","sk_326c6d0443f6457aae29ffbd48f7d1be")
@charges=@bancomer.create(:charges)
customer_hash={
    "name" => "Juan",
    "last_name" => "Vazquez Juarez",
    "phone_number" => "4423456723",
    "email" => "juan.vazquez@empresa.com.mx"
}

card_hash={
    "holder_name" => "Juan Vazquez",
    "card_number" => "4242424242424242",
    "expiration_month" => "12",
    "expiration_year" => "21",
    "cvv2" => "842"
}

request_hash={
    "affiliation_bbva" => "781500",
    "amount" => 100.00,
    "currency" => "MXN",
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
    "redirect_url" => "https://sand-portal.ecommercebbva.com",
    "customer" => customer_hash,
    "card" => card_hash
}

response_hash=@charges.create(request_hash.to_hash)
```

> Ejemplo de respuesta

```json
{
    "id": "trocmtrnivm5scpfguvl",
    "authorization": "trocmtrnivm5scpfguvl",
    "operation_type": "in",
    "method": "card",
    "transaction_type": "charge",
    "card": {
        "type": "credit",
        "brand": "visa",
        "address": null,
        "card_number": "424242XXXXXX4242",
        "holder_name": "Juan Vazquez",
        "expiration_year": "21",
        "expiration_month": "12",
        "allows_charges": true,
        "allows_payouts": false,
        "bank_name": "BANCOMER",
        "points_type": "bancomer",
        "bank_code": "012",
        "points_card": true
    },
    "status": "charge_pending",
    "conciliated": true,
    "creation_date": "2019-04-24T10:43:06-05:00",
    "operation_date": "2019-04-24T10:43:06-05:00",
    "description": "Pago",
    "error_message": null,
    "order_id": "1556120584928",
    "amount": 105.32,
    "customer": {
        "name": "Juan",
        "last_name": "Perez",
        "email": "juanperez@example.com",
        "phone_number": "554-170-3567",
        "address": {
            "line1": "Calle Morelos #12 - 11",
            "line2": "Colonia Centro",
            "line3": "Cuauhtémoc",
            "state": "Queretaro",
            "city": "Queretaro",
            "postal_code": "12345",
            "country_code": "MX"
        },
        "creation_date": "2019-04-24T10:43:06-05:00",
        "external_id": null,
        "clabe": null
    },
    "payment_method": {
        "type": "redirect",
        "url": "https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/trocmtrnivm5scpfguvl/redirect/"
    },
    "currency": "MXN"
}
```

###Petición

Propiedad | Descripción
--------- | -----
affiliation_bbva|***string*** (requerido) <br/>Debe contener el número de afiliación.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.
currency | ***string*** (opcional) <br/>Tipo de moneda del cargo. Por el momento solo se soportan 2 tipos de monedas: Pesos Mexicanos(MXN) y Dólares Americanos(USD).
order_id | ***string*** (requerido, longitud = 100) <br/>Identificador único del cargo. Debe ser único entre todas las transacciones.
[customer](#objeto-cliente)|***objeto*** (requerido) <br/>Información del cliente al que se le realiza el cargo. Se puede ocupar los mismos parámetros usados en la creación de un cliente pero no se creará una cuenta al cliente. <br/><br/> **Nota:** Este parámetro solo se puede utilizar creando el cargo a nivel comercio<br/><br/>Si desea crear un cliente y llevar un historial de sus cargos consulte como [Objeto Cliente](#objeto-cliente) y realice el cargo a nivel cliente.
[card](#objeto-tarjeta)|***objeto*** (requerido) <br/> Información de la tarjeta de donde se retirarán los fondos.
redirect_url | ***string*** (requerido) <br/>Usado para cargos de tipo redirect. Indica la url a la que redireccionar despues de una transaccion exitosa en el fomulario de pago de BBVA.
use_3d_secure | ***string*** (opcional) <br/>Por defecto el valor es TRUE, si el comercio tiene habilitada la configuración para no utilizar 3d secure, entonces podrá enviar el parámetro en FALSE.

###Respuesta
Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).

##Confirmar un cargo

> Definición

```shell
Comercio
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}/capture
```

```php
<?
Comercio
$charge = $bancomer->charges->get(transactionId);
$charge->capture(captureData);
?>
```

```java
//Comercio
bancomerAPI.charges().confirmCapture(ConfirmCaptureParams request);
```

```csharp
//Comercio
bancomerAPI.ChargeService.Capture(string transaction_id, Decimal? amount);
```

```ruby
#Comercio
@charges=@bancomer.create(:charges)
@charges.capture(transaction_id)
```

> Ejemplo de petición con comercio

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/tryqihxac3msedn4yxed/capture \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be: \
   -H "Content-type: application/json" \
   -X POST -d '{
    "amount" : 100.00
} '
```

```php
<?
$bancomer = Bancomer::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$captureData = array('amount' => 100.00);

$customer = $bancomer->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->get('tryqihxac3msedn4yxed');
$charge->capture($captureData);
?>
```

```java
BancomerAPI api = new BancomerAPI(
        "https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
ConfirmCaptureParams request = new ConfirmCaptureParams();
request.chargeId("tryqihxac3msedn4yxed");
request.amount(new BigDecimal("100.00"));

Map chargeAsMap = api.charges().confirmCapture("ag4nktpdzebjiye1tlze", request);
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
Dictionary<String, Object> chargeDictionary = api.ChargeService
                                        .Capture("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", new Decimal(100.00));
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```ruby
@bancomer=BancomerApi.new("mptdggroasfcmqs8plpy","sk_326c6d0443f6457aae29ffbd48f7d1be")
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
Confirmar un cargo creado con la propiedad de <code>capture = "false"</code>,  este método es la segunda parte de la [creación de un cargo con tarjeta](#con-id-de-tarjeta-o-token) y puede confirmar el monto capturado en la primera llamada o un monto menor.


**Nota:** Solo se pueden confirmar cargos a tarjeta. Para cancelar el cargo creado se debe hacer una llamada al método [Devolver un cargo](#devolver-un-cargo)


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
```

```php
<?
Comercio
$charge = $bancomer->charges->get(transactionId);
$charge->refund(refundData);
?>
```

```java
//Comercio
bancomerAPI.charges().refund(RefundParams request);
```

```csharp
//Comercio
bancomerAPI.ChargeService.Refund(string transaction_id, string description);
```

```ruby
#Comercio
@charges=@bancomer.create(:charges)
@charges.refund(transaction_id, request_hash)
```

> Ejemplo de petición con comercio

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/tr6cxbcefzatd10guvvw/refund \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "description" : "devolución",
   "amount" : 100.00
} '
```

```php
<?
$bancomer = Bancomer::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$refundData = array(
    'description' => 'devolución',
    'amount' => 100);

$charge = $bancomer->charges->get('ag4nktpdzebjiye1tlze');
$charge->refund(refundData);
?>
```

```java
BancomerAPI api = new BancomerAPI(
        "https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
RefundParams request = new RefundParams();
request.chargeId("tryqihxac3msedn4yxed");
request.description("Monto de cargo devuelto");
request.amount(new BigDecimal("100.00"));

Map chargeAsMap = api.charges().refund("ag4nktpdzebjiye1tlze", request);
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
Dictionary<String, Object> chargeDictionary = api.ChargeService
            .Refund("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed", "Monto de cargo devuelto", , new Decimal(100.00));
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```ruby
@bancomer=BancomerApi.new("mptdggroasfcmqs8plpy","sk_326c6d0443f6457aae29ffbd48f7d1be")
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
```

```php
<?
Comercio
$charge = $bancomer->charges->get(transactionId);
?>
```

```java
//Comercio
bancomerAPI.charges().get(String transactionId);
```

```csharp
//Comercio
bancomerAPI.ChargeService.Get(string transaction_id);
```

```ruby
#Comercio
@charges=@bancomer.create(:charges)
@charges.get(transaction_id)
```

> Ejemplo de petición con comercio

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/customers/tr6cxbcefzatd10guvvw \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be:
```

```php
<?
$bancomer = Bancomer::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');

$customer = $bancomer->customers->get('ag4nktpdzebjiye1tlze');
$charge = $customer->charges->get('tr6cxbcefzatd10guvvw');
?>
```

```java
BancomerAPI api = new BancomerAPI(
        "https://sand-api.ecommercebbva.com", "sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
Map chargeAsMap = api.charges().get("ag4nktpdzebjiye1tlze", "tr6cxbcefzatd10guvvw");
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
Dictionary<String, Object> chargeDictionary = api.ChargeService.Get("ag4nktpdzebjiye1tlze", "tryqihxac3msedn4yxed");
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```ruby
@bancomer=BancomerApi.new("mptdggroasfcmqs8plpy","sk_326c6d0443f6457aae29ffbd48f7d1be")
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
