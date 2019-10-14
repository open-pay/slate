#Plans

Plans are an Openpay resource that allows create templates for subscriptions.  Using plans you can define the amount and frequency of recurrent charges.


##Plan Object

> Object example

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

Property | Description
--------- | ------
id | ***string*** <br/> Unique plan identifier.
creation_date | ***datetime*** <br/> Date and time in which the plan was created in ISO 8601 format.
name  | ***string*** <br/> Plan name.
amount | ***numeric*** <br/> Amount that will be applied once the subscription is charged.  It has to be more than zero.
currency | ***string*** <br/> Currency used in the operation, by default is COP (Colombian pesos).
repeat_every | ***numeric*** <br/>  Time units in which the subscription will be charged.  For example, repeat_unit=month and repeat_every=2 indicates that it will be charged every 2 months.
repeat_unit | ***string*** <br/> Describes the charge unit frequency.  It can be weekly(week), monthly(month) or yearly (year).
retry_times | ***numeric*** <br/> Number of attempts to try to charge the subscription.  When the attempts have been exhausted, the status field is determined by the field *status_after_retry*.
status | ***string*** <br/> Plan status can be *active* or *deleted*.  If the plan is in *deleted* state it doesn't allow to register new subscriptions under this plan but existing subscriptions will be charged.
status_after_retry | ***string*** <br/> This field indicates the status in which the subscription will be set once all the charge attempts have been exhausted.  It can be *unpaid* or *cancelled*.
trial_days | ***numeric*** <br/> Number of trial days this subscription will have by default.

##Create a new Plan
 
> Definition

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
#Customere
@plans=@openpay.create(:plans)
@plans.create(request_hash)
```

> Request example

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
  'amount': 150
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

> Response example

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

Creates a new plan for allowing customers to subscribe.

###Request


Property | Description
--------- | ------
name | ***string*** (required, length = 255) <br/>Plan's name.
amount | ***numeric*** (required) <br/> Amount that will be charged at subscription.  It needs to be more than zero.
repeat_every | ***numeric*** (required) <br/>Time units in which the subscription will be charged.  For example, repeat_unit=month and repeat_every=2 indicates that it will be charged every 2 months.
repeat_unit | ***numeric*** (required) <br/>Describes the charge unit frequency.  It can be weekly(week), monthly(month) or yearly (year).
retry_times | ***numeric*** (optional) <br/> Number of attempts to try to charge the subscription.  When the attempts have been exhausted, the status field is determined by the field *status_after_retry*.
status_after_retry | ***string*** (required, values = "UNPAID/CANCELLED") <br/>This field indicates the status in which the subscription will be set once all the charge attempts have been exhausted.  It can be *unpaid* or *cancelled*.
trial_days | ***numeric*** (required) <br/> Number of trial days this subscription will have by default.
 

###Response
Returns the created [plan object](#plan-object) or an error in case an issue occurred.


##Update existing plans.

> Definition

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
#Customer
@plans=@openpay.create(:plans)
@plans.update(request_hash, plan_id)
```

> Request example

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

> Response example

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
 
Updates the plan information.  It requires a plan id and only certain fields can be updated.

###Request
Property | Description
--------- | ------
name | ***string*** (optional, length = 80) <br/>Plan's name.
trial_days | ***numeric*** (optional) <br/> Number of trial days this subscription will have by default.


###Response
Returns a [plan object](#plan-object) with the updated information or an [error response](#error-object) if a problem occurred with the update.

##Get a plan

> Definition

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
#Customer
@plans=@openpay.create(:plans)
@plans.get(plan_id)
```

> Request example

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

> Response example

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

It gets the plan details.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Plan identifier.

###Response
Returns a [plan object](#plan-object)

##Delete a plan

> Definition

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
#Customer
@plans=@openpay.create(:plans)
@plans.delete(plan_id)
```

> Request example

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

When a plan is deleted it won't allow to create more subscriptions associated with it, however the subscriptions already associated will continue to be charged.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Identifier of the plan that will be deleted.

###Response
If the plan is deleted correctly the response will be empty, if it cannot be deleted an [error object](#error-object) will be returned indicating the reason.


##Plan list
> Definition

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
#Customer
@plans=@openpay.create(:plans)
@plans.all
```

> Request example

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

> Response example

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
Returns the details of all active plans.

###Request
You can search using the following parameters:

Property  | Description
--------- | ------
creation| ***date*** <br/> Same as creation date.  Format yyyy-mm-dd.
creation[gte]| ***date*** <br/>After creation date. Format: yyyy-mm-dd.
creation[lte]| ***date*** <br/>Before the creation date. Format: yyyy-mm-dd.
offset| ***numeric*** <br/>Number of records to skip from the beggining, by default is 0.
limit| ***numeric*** <br/>Number of records to return, by default is 10.

###Response
A list of [plan objects](#plan-object) registered according to the given parameters, sort by creation date in descending order.

