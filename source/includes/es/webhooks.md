#Webhooks
Estos permiten notificar al cliente cuando un evento ha sucedido en la plataforma, para que el comercio pueda tomar las acciones correspondientes.

<aside class="notice">
Para que la Openpay invoque un webhook, es importante que se encuentre verificado.
</aside>


##Objeto Webhook

> Ejemplo de objeto

```json
  {
    "id" : "wxvanstudf4ssme8khmc",
    "url" : "http://requestb.in/11vxrsf1",
    "user" : "juanito",
    "password" : "passjuanito",
    "event_types" : [
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "chargeback.accepted"
    ],
    "status":"verified"
}
```

Propiedad | Descripción
--------- | -----
id            |***string*** <br/>Identificador único del webhook.
url           |***string*** <br/>URL del webhook
user          |***string*** <br/>Nombre de usuario para autenticación básica del webhook.
password      |***string*** <br/>Contraseña para autenticación básica del webhook.
event_types   |***array[string]*** <br/>Listado de eventos a los que respondera el webhook.
status        |***string*** <br/>Estado del webhook, indica si esta verificado (verified) o no esta verificado (unverified).

<aside class="success">
Los tipos de eventos soportados son:
</aside>

Evento                     | Categoría      | Descripción
-------------------------- | -------------- |------------
charge.refunded            | Cargos         | Informa cuando es reembolsado un cargo.
charge.failed              | Cargos         | Informa cuando un cargo fallo y no se aplico.
charge.cancelled           | Cargos         | Informa cuando un cargo es cancelado.
charge.created             | Cargos         | Informa cuando un cargo es programado.
charge.succeeded           | Cargos         | Informa cuando un cargo es aplicado.
charge.rescored.to.decline | Cargos         | Informa cuando a un cargo le es recalculado su score y es declinado.
subscription.charge.failed | Suscripción    | Informa cuando el cargo de una suscripción fallo.
payout.created             | Pagos          | Informa cuando un pago fue programado para el siguiente día.
payout.succeeded           | Pagos          | Informa cuando un pago programado se ha aplicado.
payout.failed              | Pagos          | Informa cuando un pago fallo.
transfer.succeeded         | Transferencias | Informa cuando se realiza una transferencia entre dos cuentas Openpay.
fee.succeeded              | Comisiones     | Informa cuando se cobra un Fee a un Customer.
fee.refund.succeeded       | Comisiones     | Informa cuando se reembolsa un Fee a un Customer.
spei.received              | SPEI           | Informa cuando se recibe un pago por SPEI para agregar fondos a la cuenta.
chargeback.created         | Contracargos   | Informa cuando se recibió un chargeback de una transacción y se esta iniciando la investigación.
chargeback.rejected        | Contracargos   | Informa cuando un contracargo fue rechazado.
chargeback.accepted        | Contracargos   | Informa cuando un contracargo fue aceptado.
order.created              | Orden          | Informa cuando una orden es creada y programada.
order.activated            | Orden          | Informa cuando una orden es activada.
order.payment.received     | Orden          | Informa cuando el pago de una orden es recibido.
order.completed            | Orden          | Informa cuando una orden es completada.
order.expired              | Orden          | Informa cuando una orden ha expirado.
order.cancelled            | Orden          | Informa cuando una orden es cancelada.
order.payment.cancelled    | Orden          | Informa cuando el pago de una orden es cancelado.


##Crear un Webhook

> Definición

```shell
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/webhooks
```

```php
<?
$webhook = $openpay->webhooks->create(webhook);
?>
```

```java
openpayAPI.webhooks().create(Webhook request);
```

```csharp
openpayAPI.WebhooksService.Create(Webhook request);
```

```javascript
openpay.webhooks.create(webhook, callback);
```

```ruby
@webhooks=@openpay.create(:webhooks)
@webhooks.create(request_hash)
```

> Ejemplo de petición 

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/webhooks \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
    "url" : "http://requestb.in/11vxrsf1",
    "user" : "juanito",
    "password" : "passjuanito",
    "event_types" : [
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "chargeback.accepted"
    ]
}' 
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$webhook = array(
    'url' => 'http://requestb.in/11vxrsf1',
    'user' => 'juanito',
    'password' => 'passjuanito',
    'event_types' => array(
      'charge.refunded',
      'charge.failed',
      'charge.cancelled',
      'charge.created',
      'chargeback.accepted'
    )
    );

$webhook = $openpay->webhooks->create($webhook);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Webhook request = new Webhook();
request.url("http://requestb.in/11vxrsf1");
request.user("juanito");
request.password("passjuanito");
request.addEventType("charge.refunded");
request.addEventType("charge.failed");

Webhook webhook = api.webhooks().create(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Webhook request = new Webhook();
request.Url = "http://requestb.in/11vxrsf1";
request.User = "juanito";
request.Password = "passjuanito";
request.AddEventType("charge.refunded");
request.AddEventType("charge.failed");

Webhook webhook = api.WebhookService.Create(request);
```

```javascript
var webhook_params = {                                            
    'url' : 'http://requestb.in/11vxrsf1',
    'user' : 'juanito',
    'password' : 'passjuanito',
    'event_types' : [
      'charge.refunded',
      'charge.failed',
      'charge.cancelled',
      'charge.created',
      'chargeback.accepted'
    ]
};

openpay.webhooks.create(webhook_params, function(error, webhook){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@webhooks=@openpay.create(:webhooks)
request_hash={
    "url" => "http://requestb.in/11vxrsf1",
    "user" => "juanito",
    "password" => "passjuanito",
    "event_types" => [
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "chargeback.accepted"
    ]
   }

response_hash=@webhooks.create(request_hash.to_hash)
```

> Ejemplo de respuesta

```json
{
  "id" : "wkn0t30zfxpmhr5usgfa",
  "url" : "http://requestb.in/qt3bq0qt",
  "user" : "juanito",
  "event_types" : [
    "charge.succeeded",
    "charge.created",
    "charge.cancelled",
    "charge.failed"
  ],
  "status" : "verified"
}
```

Al crear un nuevo webhook se hará una petición a la url indicada para verificar el webhook.

Al momento de guardar el webhook se generará un id que podrá ser usado para eliminar o simplemente obtener la información no sensible del webhook.


###Petición

Propiedad | Descripción
--------- | -----
url           |***string*** <br/>URL del webhook
user          |***string*** <br/>Nombre de usuario para autenticación básica del webhook.
password      |***string*** <br/>Contraseña para autenticación básica del webhook.
event_types   |***array[string]*** <br/>Listado de eventos a los que respondera el webhook.

###Respuesta
Regresa un [objeto webhook](#objeto-webhook) cuando se creó correctamente o una respuesta de error si ocurrió algún problema en la creación.



##Obtener un Webhook

> Definición

```shell
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/webhooks/{WEBHOOK_ID}
```

```php
<?
$webhook = $openpay->webhooks->get(webhookId);
?>
```

```java
openpayAPI.webhooks().get(String webhookId);
```

```csharp
openpayAPI.WebhooksService.Get(string webhookId);
```

```javascript
openpay.webhooks.get(webhookId, callback);
```

```ruby
@webhooks=@openpay.create(:webhooks)
@webhooks.get(webhookId)
```

> Ejemplo de petición

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/webhooks/wxvanstudf4ssme8khmc \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" 
``` 

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$webhook = $openpay->webhooks->get('wxvanstudf4ssme8khmc');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Webhook webhook = api.webhooks().get("wxvanstudf4ssme8khmc");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Webhook webhook = api.WebhooksService.Get("wxvanstudf4ssme8khmc");
```

```javascript
openpay.webhooks.get('wxvanstudf4ssme8khmc', function(error, webhook){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@webhooks=@openpay.create(:webhooks)

response_hash=@webhooks.get("wxvanstudf4ssme8khmc")
```

> Ejemplo de respuesta

```json
  {
    "id" : "wxvanstudf4ssme8khmc",
    "url" : "http://requestb.in/11vxrsf1",
    "user" : "juanito",
    "event_types" : [
      "verification",
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "charge.succeeded",
      "subscription.charge.failed",
      "payout.created",
      "payout.succeeded",
      "payout.failed",
      "transfer.succeeded",
      "fee.succeeded",
      "spei.received",
      "chargeback.created",
      "chargeback.rejected",
      "chargeback.accepted"
    ],
    "status" : "verified"
  }
```

Obtiene los detalles de un webhook solicitándolo con su id. 

<aside class="notice">
**Nota:** Nunca se regresarán datos sensibles como son el password para accesar al webhook.
</aside>


###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador único del webhook

###Respuesta
Regresa un [objeto webhook](#objeto-webhook)


##Eliminar un Webhook

> Definición

```shell
DELETE https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/webhooks/{WEBHOOK_ID}
```

```php
<?
$webhook = $openpay->webhooks->get(webhookId);
$webhook->delete();
?>
```

```java
openpayAPI.webhooks().delete(String webhookId);
```

```csharp
openpayAPI.WebhooksService.Delete(string webhook_id);
```

```javascript
openpay.webhooks.delete(webhookId, callback);
```

```ruby
@webhooks=@openpay.create(:webhooks)
@webhooks.delete(webhook_id)
```

> Ejemplo de petición con cliente

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/webhooks/wxvanstudf4ssme8khmc \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -X DELETE
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$webhook = $openpay->webhooks->get('wxvanstudf4ssme8khmc');
$webhook->delete();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.webhooks().delete("wxvanstudf4ssme8khmc");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.WebhooksService.Delete("wxvanstudf4ssme8khmc");
```

```javascript
openpay.webhooks.delete('wxvanstudf4ssme8khmc', function(error) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@webhooks=@openpay.create(:webhooks)

response_hash=@webhooks.delete("wxvanstudf4ssme8khmc")
```

Elimina un webhook del comercio.

Para eliminarlo sólo es necesario proporcionar el identificador del webhook.


###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador único del webhook

###Respuesta
Si el webhook se borra correctamente la respuesta es vacía, si no se puede borrar se regresa un [objeto error](#objeto-error) indicando el motivo. 



##Listado de Webhook

> Definición

```shell
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/webhooks
```

```php
<?
$webhookList = $openpay->webhooks->getList();
?>
```

```java
openpayAPI.webhooks().list();
```

```csharp
openpayAPI.WebhooksService.List();
```

```javascript
openpay.webhooks.list(callback);
```

```ruby
@webhooks=@openpay.create(:webhooks)
@webhooks.all
```

> Ejemplo de petición

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/webhooks \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" 
``` 

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$webhookList = $openpay->webhooks->getList();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
List<Webhook> webhooks = api.webhooks().list();
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
List<Webhook> webhooks = api.WebhooksService.List();
```

```javascript
openpay.webhooks.list(function(error, list){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@webhooks=@openpay.create(:webhooks)

response_hash=@webhooks.all
```

> Ejemplo de respuesta

```json
[
  {
    "id" : "wDashboard185",
    "event_types" : [
      "verification",
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "charge.succeeded",
      "subscription.charge.failed",
      "payout.created",
      "payout.succeeded",
      "payout.failed",
      "transfer.succeeded",
      "fee.succeeded",
      "spei.received",
      "chargeback.created",
      "chargeback.rejected",
      "chargeback.accepted"
    ],
    "url" : "http://requestb.in/11vxrsf1",
    "status" : "verified"
  },
  {
    "id" : "wDashboard186",
    "event_types" : [
      "verification",
      "charge.refunded",
      "charge.failed",
      "charge.cancelled",
      "charge.created",
      "charge.succeeded",
      "subscription.charge.failed"
    ],
    "url" : "http://requestb.in/1fhpiog1",
    "status" : "verified"
  }
]
```

Regresa una lista de webhooks registrados por comercio.

<aside class="notice">
**Nota:** Nunca se regresarán datos sensibles como son el password para accesar al webhook.
</aside>


###Petición

###Respuesta
Listado de objetos [objeto webhook](#objeto-webhook) registrados de acuerdo a los parámetros proporcionados.

