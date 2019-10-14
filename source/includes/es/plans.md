#Planes

Los planes son recursos en Openpay que permiten crear plantillas para las suscripciones. Con ellos podrás definir la cantidad y frecuencia con la que se realizarán los cargos recurrentes.

##Objeto Plan

> Ejemplo de objeto

```json
{
    "name": "Curso de ingles",
    "status": "active",
    "amount": 150,
    "currency": "COP",
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
amount | ***numeric*** <br/> Monto que se aplicara cada vez que se cobre la suscripción. Debe ser una cantidad mayor a cero.
currency | ***string*** <br/> Moneda usada en la operación, por default es COP
repeat_every | ***numeric*** <br/> Número de unidades tiempo entre los que se cobrara la suscripción. Por ejemplo, repeat_unit=month y repeat_every=2 indica que se cobrara cada 2 meses.
repeat_unit | ***string*** <br/> Especifica la frecuencia de cobro. Puede ser semanal(week), mensual(month) o anual(year).
retry_times | ***numeric*** <br/>  Numero de reintentos de cobro de la suscripción. Cuando se agotan los intentos se pone en el estatus determinado por el campo status_after_retry.
status | ***string*** <br/> Estatus del Plan puede ser active o deleted. Si el plan se encuentra en estado deleted no se permite registrar nuevas suscripciones, pero las que ya están registradas, se siguen cobrando.
status_after_retry | ***string*** <br/> Este campo especifica el status en el que se pondrá la suscripción una vez que se agotaron los intentos. Puede ser: unpaid o cancelled
trial_days | ***numeric*** <br/> Numero de días de prueba por defecto que tendrá la suscripción.

##Crear un nuevo plan

> Definición

```shell
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/plans
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
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/plans \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
  "amount": 150,
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
    'amount' => 150,
    'status_after_retry' => 'cancelled',
    'retry_times' => 2,
    'name' => 'Plan Curso Verano',
    'repeat_unit' => 'month',
    'trial_days' => '30',
    'repeat_every' => '1',
    'currency' => 'COP');

$plan = $openpay->plans->add($planDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Plan request = new Plan();
request.name("Curso de ingles");
request.amount(new BigDecimal("150"));
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
request.Amount = new Decimal(150);
request.RepeatEvery = 1;
request.RepeatUnit = "week";
request.RetryTimes = 2;
request.StatusAfterRetry = "unpaid";
request.TrialDays = 30;

request = api.PlanService.Create(request);
```

```javascript
var planRequest = {
  'amount': 150,
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
     "amount" => 150,
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
   "amount":150,
   "currency":"COP",
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
amount | ***numeric*** (requerido) <br/>Monto que se aplicara cada vez que se cobre la suscripción. Debe ser una cantidad mayor a cero.
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
PUT https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/plans/{PLAN_ID}
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
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/plans/p8e6x3hafqqsbmnoevrt \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
   "amount":150,
   "currency":"COP",
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
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/plans/{PLAN_ID}
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
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/plans/p8e6x3hafqqsbmnoevrt \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$plan = $openpay->plans->get('pduar9iitv4enjftuwyl');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
   "amount":150,
   "currency":"COP",
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
DELETE https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/plans/{PLAN_ID}
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
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/plans/p8e6x3hafqqsbmnoevrt \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/plans
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
curl -g "https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/plans?limit=10" \
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

$planList = $openpay->plans->getList($findDataRequest);
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

List<Plan> plans = api.plans().list(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2019, 5, 1);
request.CreationLte = new DateTime(2019, 5, 15);
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
        "currency": "COP",
        "id": "patpflacwilazguj6bem",
        "creation_date": "2019-05-13T09:43:52-06:00",
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
        "currency": "COP",
        "id": "pjl7wfryrrd1tznr0fnl",
        "creation_date": "2019-05-13T11:36:40-06:00",
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
