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
alias | ***string*** <br/>Nombre por el cual se identifica a la cuenta bancaria.
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
