#Customers

Customers are Openpay resources that are handled within the Merchant account and can represent users, customers or partners according to the type of Merchant.

You can add cards  to the customers so you can make transactions like Charges.

##Customer object

> Object example

```json
{
   "id":"cz4nkhrlcu9k7qd4lwqx",
   "creation_date":"2018-11-08T12:04:46-06:00",
   "name":"Rodrigo",
   "last_name":"Velazco Perez",
   "email":"rodrigo.velazco@payments.com",
   "phone_number":"16362801",
   "external_id":"cliente1",
   "status":"active",
   "balance":103,
   "address":{
      "line1":"Av. 5 de febrero No. 1080 int Roble 207",
      "line2":"Carrillo puerto",
      "line3":"Esquina Ramón Pérez",
      "postal_code":"110831",
      "state":"Bogotá",
      "city":"Bogotá",
      "country_code":"CO"
   }
}
```

Property | Description
--------- | -----
id            |***string*** <br/>Customer unique identifier.
creation_date |***datetime*** <br/>Date and time when the customer was created in ISO 8601 format.
name          |***string*** <br/>Name of the customer.
last_name     |***string*** <br/>Last name of the customer.
email         |***string*** <br/>Email of the customer.
phone_number  |***numeric*** <br/>Telephone number of the customer.
status        |***string*** <br/>Account status of the customer can be active or deleted. If the account is on deleted status, no transaction is allowed.
balance       |***numeric*** <br/>Account balance with two decimal digits.
[address](#addres-object) |***object*** <br/>Address of the customer. It is usually used as shipping address.

##Create a new customer

> Definition

```shell
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers
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

> Request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers \
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
     'requires_account' => false,
     'phone_number' => '16362801',
     'address' => array(
         'line1' => 'Calle 10',
         'line2' => 'col. san pablo',
         'line3' => 'Esquina Ramón Pérez',
         'state' => 'Bogota',
         'city' => 'Bogota',
         'postal_code' => '110731',
         'country_code' => 'CO'
      )
   );

$customer = $openpay->customers->add($customerData);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer request = new Customer();
request.externalId("idExterno0101");
request.name("Julian Gerardo");
request.lastName("López Martínez");
request.email("julian.martinez@gmail.com");
request.phoneNumber("16362801");
request.requiresAccount(false);
Address address = new Address();
address.city("Bogota");
address.countryCode("CO");
address.state("Bogota");
address.postalCode("110731");
address.line1("Av. Pie de la cuesta #12");
address.line2("Desarrollo San Pablo");
address.line3("Esquina Ramón Pérez");
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
request.PhoneNumber = "16362801";
request.RequiresAccount = false;
Address address = new Address();
address.City = "Bogota";
address.CountryCode = "CO";
address.State = "Bogota";
address.PostalCode = "110731";
address.Line1 = "Av. Pie de la cuesta #12";
address.Line2 = "Desarrollo San Pablo";
address.Line3 = "Esquina Ramón Pérez";
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
      "line3" => "Esquina Ramón Pérez",
      "state" => "Bogota",
      "city" => "Bogota",
      "postal_code" => "111071",
      "country_code" => "CO"
   }
request_hash={
     "external_id" => nil,
     "name" => "customer name",
     "last_name" => nil,
     "email" => "customer_email@me.com",
     "requires_account" => false,
     "phone_number" => "16362801",
     "address" => address_hash
   }

response_hash=@customers.create(request_hash.to_hash)
```

> Response example

```json
{
   "id":"anbnldwgni1way3yp2dw",
   "name":"customer name",
   "last_name":null,
   "email":"customer_email@me.com",
   "phone_number":null,
   "address":null,
   "creation_date":"2018-05-20T16:47:47-05:00",
   "external_id":null,
   "store": {
       "reference": "OPENPAY02DQ35YOY7",
       "barcode_url": "https://sandbox-api.openpay.co/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   }
}
```

Create a customer object.

###Request

Property | Description
--------- | ------
external_id | ***string*** (optional, length = 100)  <br/> Unique external identifier of the customer assigned for the Merchant.
name        | ***string*** (required, length = 100)<br/>Name of the customer.
last_name   | ***string*** (optional, length = 100)<br/>Last name of the customer.
email       | ***string*** (required, length = 100)<br/>Email of the customer.
requires_account | ***boolean***  (optional, default = true) <br/>Send it with **false** value if you need to create the customer without an account to manage the balance.
phone_number| ***string*** (optional, length = 100) <br/>Telephone number of the customer.
[address](#address-object) | ***object*** (optional) <br/>Address of the customer. It is usually used as shipping address.

###Response

Returns a [customer object](#customer-object) when all the data were sent correctly, or returns an [error response](#error-object) if a problem happened.


##Update a customer

> Definition

```shell
PUT https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}
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

> Request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/anbnldwgni1way3yp2dw \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X PUT -d '{
   "name": "customer name",
   "email": "customer_email@me.com",
   "address":{
      "city":"Bogota",
      "state":"Bogota",
      "line1":"Calle 10",
      "postal_code":"111071",
      "line2":"col. san pablo",
      "line3":"Esquina Ramón Pérez",
      "country_code":"CO"
   },
   "phone_number":"16362801"
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer request = new Customer();
request.name("Julian Gerardo");
request.lastName("López Martínez");
request.email("julian.martinez@gmail.com");
request.phoneNumber("16362801");
Address address = new Address();
address.city("Bogota");
address.countryCode("10");
address.state("Bogota");
address.postalCode("111071");
address.line1("Av. Pie de la cuesta #12");
address.line2("Desarrollo San Pablo");
address.line3("Esquina Ramón Pérez");
request.address(address);

request = api.customers().update(request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer request = new Customer();
request.Name = "Julian Gerardo";
request.LastName = "López Martínez";
request.Email = "julian.martinez@gmail.com";
request.PhoneNumber = "16362801";
Address address = new Address();
address.City = "Bogota";
address.CountryCode = "CO";
address.State = "Bogota";
address.PostalCode = "111071";
address.Line1 = "Av. Pie de la cuesta #12";
address.Line2 = "Desarrollo San Pablo";
address.Line3 = "Esquina Ramón Pérez";
request.Address = address;

request = api.CustomerService.Update(request);
```

```javascript
var customerRequest = {
    'name': 'customer name',
    'email': 'customer_email@me.com',
    'address':{
      'city':'Bogota',
      'state':'Bogota',
      'line1':'Calle 10',
      'postal_code':'111071',
      'line2':'col. san pablo',
      'line3':'Esquina Ramón Pérez',
      'country_code':'CO'
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
      "line3" => "Esquina Ramón Pérez",
      "state" => "Bogota",
      "city" => "Bogota",
      "postal_code" => "111071",
      "country_code" => "CO"
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

> Response example

```json
{
   "id":"anbnldwgni1way3yp2dw",
   "name":"customer name",
   "last_name":null,
   "email":"customer_email@me.com",
   "phone_number":"16362801",
   "address":{
      "line1":"Calle 10",
      "line2":"col. san pablo",
      "line3":"Esquina Ramón Pérez",
      "state":"Bogota",
      "city":"Bogota",
      "postal_code":"111071",
      "country_code":"CO"
   },
   "store": {
      "reference": "OPENPAY02DQ35YOY7",
      "barcode_url": "https://sandbox-api.openpay.co/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
   "creation_date":"2018-05-20T16:47:47-05:00",
   "external_id":null
}
```

Updates one or more data of the customer.

###Request

Property | Description
--------- | ------
name        | ***string*** (required, length = 100)<br/>Name of the customer.
last_name   | ***string*** (optional, length = 100)<br/>Last name of the customer.
email       | ***string*** (required, length = 100)<br/>Email of the customer.
phone_number| ***string*** (optional, length = 100) <br/>Telephone number of the customer.
[address](#address-object) | ***object*** (optional) <br/>Address of the customer. It is usually used as shipping address.

###Response

Returns a [customer object](#customer-object) with the updated info, or returns an [error response](#error-object) if a problem happened while updating.


##Get an existing customer

> Definition

```shell
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}
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

> Request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/anbnldwgni1way3yp2dw \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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

> Response example

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
      "line3":"Esquina Ramón Pérez",
      "state":"Bogota",
      "city":"Bogota",
      "postal_code":"111071",
      "country_code":"CO"
   },
   "store": {
       "reference": "OPENPAY02DQ35YOY7",
       "barcode_url": "https://sandbox-api.openpay.co/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
   "creation_date":"2018-05-20T16:47:47-05:00",
   "external_id":null
}
```

Gets the current information of an existing customer. You only need to specify the id returned when creating the customer.

###Request

Property | Description
--------- | ------
id| _**string**_ (required, legth = 45)<br/>Unique identifier of the customer.

###Response

If the identifier exists, it returns a [customer object](#customer-object) with the customer information.

##Delete a customer

> Definition

```shell
DELETE https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}
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

> Request example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/anbnldwgni1way3yp2dw \
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
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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


Deletes a customer permanently. All the related subscriptions will be canceled. Openpay keeps the operations records.

###Request

Property | Description
--------- | ------
id| _**string**_ (required, length = 45)<br/> Unique identifier of the customer you want to delete.

###Response
If the customer is deleted correctly, it returns an empty response, if the customer can not be deleted it returns a [error object](#error-object) explaining the reason.

##List of customers

> Definition

```shell
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers
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

> Request example

```shell
curl -g "https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers?creation[gte]=2013-11-01&limit=2" \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json"
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$findDataRequest = array(
    'creation[gte]' => '2018-01-01',
    'creation[lte]' => '2018-12-31',
    'offset' => 0,
    'limit' => 5);

$customerList = $openpay->customers->getList($findDataRequest);
?>
```

```java
final Calendar dateGte = Calendar.getInstance();
final Calendar dateLte = Calendar.getInstance();
dateGte.set(2018, 5, 1, 0, 0, 0);
dateLte.set(2018, 5, 15, 0, 0, 0);

OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
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
request.CreationGte = new Datetime(2018, 5, 1);
request.CreationLte = new DateTime(2018, 5, 15);
request.Offset = 0;
request.Limit = 100;

List<Customer> customers = api.CustomerService.List(request);
```

```javascript
var searchParams = {
  'creation[gte]' : '2018-11-01',
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

> Response example

```json
[{
   "id":"cpjdhf754ythr65yu9k7q",
   "creation_date":"2018-11-08T12:04:46-06:00",
   "name":"Rodrigo",
   "last_name":"Velazco Perez",
   "email":"rodrigo.velazco@payments.com",
   "phone_number":"16362801",
   "status":"active",
   "balance":142.5,
   "store": {
       "reference": "OPENPAY02DQ35YOY7",
       "barcode_url": "https://sandbox-api.openpay.co/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
}, {
   "id":"cz4nkhrlcu9k7qd4lwqx",
   "creation_date":"2018-11-07T14:54:46-06:00",
   "name":"Eriberto",
   "last_name":"Rodriguez Lopez",
   "email":"eriberto.rodriguez@payments.com",
   "phone_number":"16362801",
   "status":"active",
   "balance":103,
   "store": {
       "reference": "∑",
       "barcode_url": "https://sandbox-api.openpay.co/barcode/∑?width=1&height=45&text=false"
  }
}]
```
Returns a list of registered customers, if you want to delimit the result you may use filters.

###Request
You can search using the following parameters as filters.

Property | Description
--------- | ------
external_id| _**string**_ <br/>Unique customer id generated by the merchant and associated to the customer by the external_id field of the create customer request
creation| ***date*** <br/>Same as the customer creation date. Format yyyy-mm-dd
creation[gte]| ***date*** <br/>After the customer creation date .Format yyyy-mm-dd
creation[lte]| ***date*** <br/>Before the customer creation date.Format yyyy-mm-dd
offset| ***numeric*** <br/>Number of records to skip at the beginning, default 0.
limit| ***numeric*** <br/>Number of required records, default 10.

###Response

Returns an array of [customer object](#customer-object).
