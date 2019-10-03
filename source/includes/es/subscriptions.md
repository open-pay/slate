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
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions
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
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/subscriptions \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "card":{
      "card_number":"4111111111111111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "cvv2":"110",
      "device_session_id":"kR1MiQhz2otdIuUlQkbEyitIqVMiI16f"
   },
   "plan_id":"pbi4kb8hpb64x0uud2eb"
}'
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$subscriptionDataRequest = array(
    'trial_end_date' => '2014-01-01',
    'plan_id' => 'pbi4kb8hpb64x0uud2eb',
    'card' => array(
         'card_number' => '4111111111111111',
         'holder_name' => 'Juan Perez Ramirez',
         'expiration_year' => '20',
         'expiration_month' => '12',
         'cvv2' => '110',
         'device_session_id' => 'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f'));

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$subscription = $customer->subscriptions->add($subscriptionDataRequest);
?>
```

```java
final Calendar trialEndDate = Calendar.getInstance();
trialEndDate.set(2014, 5, 1, 0, 0, 0);

OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Subscription request = new Subscription();
request.planId("pbi4kb8hpb64x0uud2eb");
request.trialEndDate(trialEndDate.getTime());
Card card = new Card();
card.cardNumber("4111111111111111");
card.holderName("Juan Perez Ramirez");
card.cvv2("110");
card.expirationMonth(12);
card.expirationYear(20);
card.deviceSessionId("kR1MiQhz2otdIuUlQkbEyitIqVMiI16f");
request.card(card);

request = api.subscriptions().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Subscription request = new Subscription();
request.PlanId = "idPlan-01001";
request.TrialEndDate = new Datetime(2014, 5, 1);
Card card = new Card();
card.HolderName = "Juan Perez Ramirez";
card.CardNumber = "4111111111111111";
card.Cvv2 = "110";
card.ExpirationMonth = "12";
card.ExpirationYear = "20";
card.DeviceSessionId = "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f";
request.Card = card;

request = api.SubscriptionService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var subscriptionRequest = {
   'card':{
      'card_number':'4111111111111111',
      'holder_name':'Juan Perez Ramirez',
      'expiration_year':'20',
      'expiration_month':'12',
      'cvv2':'110',
      'device_session_id':'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f'
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
card_hash={
     "holder_name" => "Juan Perez Ramirez",
     "card_number" => "4111111111111111",
     "cvv2" => "110",
     "expiration_month" => "12",
     "expiration_year" => "20",
     "device_session_id" => "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f"
   }
request_hash={
     "plan_id" => "pbi4kb8hpb64x0uud2eb",
     "trial_end_date" => "2014-06-20",
     "card" => card_hash
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
      "bank_name":"BANCO DE BOGOTÁ",
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

Crea una suscripción para un cliente existente. Se puede ocupar una tarjeta previamente creada o se pueden enviar los datos de la tarjeta en donde se realizarán los cargos, estos últimos pueden incluir la propiedad <code>device_session_id</code> para usar la herramienta antifraudes, véase [Fraud detection using device data](https://github.com/open-pay/openpay-js#fraud-detection-using-device-data).

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
PUT https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions/{subscriptionId}
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
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/subscriptions/s0gmyor4yqtyv1miqwr0 \
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

OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
      "bank_name":"BANCO DE BOGOTÁ",
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

##Obtener una suscripción

> Definición

```shell
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions/{SUBSCRIPTION_ID}
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
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/subscriptions/s0gmyor4yqtyv1miqwr0 \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
DELETE https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions/{SUBSCRIPTION_ID}
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
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/subscriptions/s0gmyor4yqtyv1miqwr0 \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/subscriptions
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
curl -g "https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/subscriptions?limit=10" \
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

OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
