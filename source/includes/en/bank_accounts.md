#Bank Accounts

You can store multiple bank accounts by Merchant or customer for withdraw funds later.

##Bank account object

> Object example 

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


Property | Description
--------- | ------
id | ***string*** <br/>ID of the bank account.
holder_name | ***string*** <br/>Holder's full name.
alias | ***string*** <br/>Name by which the bank account is identified.
clabe | ***string*** <br/>CLABE number assigned to the account.
bank_name | ***string*** <br/>Abbreviated name of the bank where the account resides, based on the following catalog of [Bank codes](http://es.wikipedia.org/wiki/CLABE#C.C3.B3digo_de_Banco).
bank_code | ***string*** <br/> Bank code where the account resides, based on the following catalog [Bank Codes](http://es.wikipedia.org/wiki/CLABE#C.C3.B3digo_de_Banco).
creation_date | ***datetime*** <br/>Date and time when the bank account was created in ISO 8601 format.


##Create a bank account
 
> Definition

```shell
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/bankaccounts
```

```php
<?
$customer = $bbva->customers->get(customerId);
$bankaccount = $customer->bankaccounts->add(bankDataRequest);
?>
```

```java
//Customer
BbvaAPI.bankAccounts().create(String customerId, BankAccount request);
```

```csharp
//Customer
BbvaAPI.BankAccountService.Create(string customer_id, BankAccount request);
```

```javascript
bbvaAPI.customers.bankaccounts.create(customerId, bankaccountRequest, callback);
```

```ruby
#Customer
@bank_accounts=@bbva.create(:bankaccounts)
@bank_accounts.create(request_hash, customer_id)
```

> Request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/bankaccounts \
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
$bbva = Bbva::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$bankDataRequest = array(
    'clabe' => '072910007380090615',
    'alias' => 'Cuenta principal',
    'holder_name' => 'Teofilo Velazco');

$customer = $bbva->customers->get('a9ualumwnrcxkl42l6mh');
$bankaccount = $customer->bankaccounts->add($bankDataRequest);
?>
```

```java
BbvaAPI api = new BbvaAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
BankAccount request = new BankAccount();
request.holderName("Juan Hernández Sánchez");
request.alias("Cuenta principal");
request.clabe("032XXXXXXXXXX59719");

request = api.bankAccounts().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
BbvaAPI api = new BbvaAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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

bbva.customers.bankaccounts.create('a9pvykxz4g5rg0fplze0', bankaccountRequest, function(error, bankaccount) {
  // ...
});
```

```ruby
@bbva=Bbva.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@bank_accounts=@bbva.create(:bankaccounts)
request_hash={
     "holder_name" => "Juan Hernández Sánchez",
     "alias" => "Cuenta principal",
     "clabe" => "032XXXXXXXXXX59719"
   }

response_hash=@bank_accounts.create(request_hash.to_hash, "asynwirguzkgq2bizogo")
```

> Response example

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

Creates and assigns a bank account to a specific customer.

###Request


Property | Description
--------- | ------
holder_name | ***string*** (required, length  = 80) <br/>Holder's full name.
alias | ***string*** (optional, length = 45)<br/>Name by which the bank account is identified.
clabe | ***string*** (required, length  = 45) <br/>CLABE number assigned to the account.

###Response
Returns a [bank account object](#bank-account-object) or an error when a there is a problem.

##Get a bank account

> Definition

```shell
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/bankaccounts/{BANK_ACCOUNT_ID}
```

```php
<?
$customer = $bbva->customers->get(customerId);
$bankaccount = $customer->bankaccounts->get(bankAccountId);
?>
```

```java
//Customer
bbvaAPI.bankAccounts().get(String customerId, String bankAccountId);
```

```csharp
//Customer
bbvaAPI.BankAccountService.Get(string customer_id, string bank_account_id);
```

```javascript
bbvaAPI.customers.bankaccounts.get(customerId, bankaccountId, callback);
```

```ruby
#Customer 
@bank_accounts=@bbva.create(:bankaccounts)
@bank_accounts.get(customer_id, bankaccount_id)
```

> Request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/bankaccounts/buyj4apkwilpp2jfxr9r \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
``` 

```php
<?
$bbva = Bbva::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $bbva->customers->get('a9ualumwnrcxkl42l6mh');
$bankaccount = $customer->bankaccounts->get('b4vcouaavwuvkpufh0so');
?>
```

```java
BbvaAPI api = new BbvaAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
BankAccount bankAccount = api.bankAccounts().get("a9pvykxz4g5rg0fplze0", "buyj4apkwilpp2jfxr9r");
```

```csharp
BbvaAPI api = new BbvaAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
BankAccount bankAccount = api.BankAccountService.Get("a9pvykxz4g5rg0fplze0", "buyj4apkwilpp2jfxr9r");
```

```javascript
bbvaAPI.customers.bankaccounts.get('a9pvykxz4g5rg0fplze0', 'buyj4apkwilpp2jfxr9r', function(error, bankaccount){
  // ...
});
```

```ruby
@bbva=BbvaApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@bank_accounts=@bbva.create(:bankaccounts)

response_hash=@bank_accounts.get("asynwirguzkgq2bizogo", "buyj4apkwilpp2jfxr9r")
```

> Response example

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

It obtains the details of the bank account assigned to a customer.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Unique identifier of the bank account.

###Response
Returns a [bank account object](#bank-account-object)

##Delete a bank account

> Definition

```shell
DELETE https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/bankaccounts/{BANK_ACCOUNT_ID}
```

```php
<?
$customer = $bbva->customers->get(customerId);
$bankaccount = $customer->bankaccounts->get(bankAccountId);
$bankaccount->delete();
?>
```

```java
//Customer
bbvaAPI.bankAccounts().delete(String customerId, String bankAccountId);
```

```csharp
//Customer
bbvaAPI.BankAccountService.Delete(string customer_id, string bank_account_id);
```

```javascript
bbva.customers.bankaccounts.delete(customerId,bankaccountId, callback);
```

```ruby
#Customer
@bank_accounts=@bbva.create(:bankaccounts)
@bank_accounts.delete(customer_id, bankaccount_id)
```

> Request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/bankaccounts/buyj4apkwilpp2jfxr9r \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -X DELETE
```

```php
<?
$bbva = Bbva::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $bbva->customers->get('a9ualumwnrcxkl42l6mh');
$bankaccount = $customer->bankaccounts->get('b4vcouaavwuvkpufh0so');
$bankaccount->delete();
?>
```

```java
BbvaAPI api = new BbvaAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.bankAccounts().delete("a9pvykxz4g5rg0fplze0", "buyj4apkwilpp2jfxr9r");
```

```csharp
BbvaAPI api = new BbvaAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.BankAccountService.Delete("a9pvykxz4g5rg0fplze0", "buyj4apkwilpp2jfxr9r");
```

```javascript
bbva.customers.bankaccounts.delete('a9pvykxz4g5rg0fplze0','buyj4apkwilpp2jfxr9r', function(error){
  // ...
});
```

```ruby
@bbva=BbvaApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@bank_accounts=@bbva.create(:bankaccounts)

response_hash=@bank_accounts.delete("asynwirguzkgq2bizogo", "buyj4apkwilpp2jfxr9r")
```

Deletes the bank account associated with the customer. The transactions that are associated with this account are unchanged and will continue for you to consult them.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length  = 45) <br/> Unique identifier of the bank account.

###Response
If the bank account is removed correctly the answer is empty, if it can not be deleted a [error object](#error-object) indicating the reason is returned.

##List of bank accounts
> Definition

```shell
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/bankaccounts
```

```php
<?
$customer = $bbva->customers->get(customerId);
$bankaccountList = $customer->bankaccounts->getList(findDataRequest);
?>
```

```java
//Customer
bbvaAPI.bankAccounts().list(String customerId, SearchParams request);
```

```csharp
//Customer
bbvaAPI.BankAccountService.List(string customer_id, SearchParams request = null);
```

```javascript
bbva.customers.bankaccounts.list(customerId, callback);
bbva.customers.bankaccounts.list(customerId, searchParams, callback);
```

```ruby
#Customer
@bank_accounts=@bbva.create(:bankaccounts)
@bank_accounts.all(customer_id)
```

> Request example

```shell
curl -g "https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/bankaccounts?limit=2" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: 
```

```php
<?
$bbva = Bbva::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$findDataRequest = array(
    'creation[gte]' => '2013-01-01',
    'creation[lte]' => '2013-12-31',
    'offset' => 0,
    'limit' => 5);

$customer = $bbva->customers->get('a9ualumwnrcxkl42l6mh');
$bankaccountList = $customer->bankaccounts->getList($findDataRequest);
?>
```

```java
final Calendar dateGte = Calendar.getInstance();
final Calendar dateLte = Calendar.getInstance();
dateGte.set(2014, 5, 1, 0, 0, 0);
dateLte.set(2014, 5, 15, 0, 0, 0);
        
BbvaAPI api = new BbvaAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.creationGte(dateGte.getTime());
request.creationLte(dateLte.getTime());
request.offset(0);
request.limit(100);
        
List<BankAccount> bankAccounts = api.bankAccounts().list("a9pvykxz4g5rg0fplze0", request);
```

```csharp
BbvaAPI api = new BbvaAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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

bbva.customers.bankaccounts.list('ag4nktpdzebjiye1tlze', searchParams, function(error, list){
  // ...
});
```

```ruby
@bbva=BbvaApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@bank_accounts=@bbva.create(:bankaccounts)

response_hash=@bank_accounts.all("asynwirguzkgq2bizogo")
```

> Response Example

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
   "bank_name":"BBVA",
   "alias":null,
   "holder_name":"Juan Hernández Sánchez",
   "creation_date":"2013-11-14T18:07:45-06:00"
}]
```
Returns the details of all the bank accounts of the customer specified on the request.


###Request
You can search using the following parameters as filters.

Property | Description
--------- | ------
creation| ***date*** <br/>Same as creation date. Format yyyy-mm-dd
creation[gte]| ***date*** <br/>After the creation date. Format yyyy-mm-dd
creation[lte]| ***date*** <br/>Before the creation date. Format yyyy-mm-dd
offset| ***numeric*** <br/>Number of records to skip at the beginning, default 0.
limit| ***numeric*** <br/>Number of required records, default 10.

###Response
List of [bank account objects](#bank-account-object) registered according to the given parameters, sorted by creation date in descending order. 

