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
   "affiliation_bbva" : "107098",
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
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

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
        "https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

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
$bancomer = Bancomer::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

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
@bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
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
        "url": "https://sand-api.ecommercebbva.com/v1/mppfjk5cznzjqvrxp64k/charges/trz8v1n3g992xtylohts/card_capture"
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

<aside class="notice">
Puedes realizar el cargo a la cuenta del comercio. </br>
</aside>

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
redirect_url | ***string*** (requerido) <br/>Usado para cargos de tipo redirect. Indica la url a la que redireccionar despues de una transaccion exitosa en el fomulario de pago de bancomer.
use_3d_secure | ***string*** (opcional) <br/>Por defecto el valor es TRUE, si el comercio tiene habilitada la configuración para no utilizar 3d secure, entonces podrá enviar el parámetro en FALSE.

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
