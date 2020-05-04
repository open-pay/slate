#Clientes

Los clientes son recursos en Openpay que se manejan dentro de su cuenta de comercio y puede representar usuarios, clientes o socios segun el tipo de negocio.

A los clientes les puedes agregar tarjetas para despues realizar transacciones de Cargo

##Objeto Cliente

> Ejemplo de objeto

```json
{
    "id": "awfx3738muksxzgrynwb",
    "name": "Pedro Diego",
    "last_name": "Alatorre Martínez",
    "email": "pedro.alatorre@comercio.com",
    "phone_number": "5744484951",
    "status": "active",
    "balance": 0.00,
    "creation_date": "2018-10-31T11:39:21-06:00",
    "external_id": null,
    "address" : null,
    "customer_address": {
        "department": "Medellín",
        "city": "Antioquía",
        "additional": "Avenida 7f bis # 138-58 Apartamento 942"
    },
    "clabe": null
}
```

Propiedad | Descripción
--------- | -----
id            |***string*** <br/>Identificador único del cliente.
creation_date |***datetime*** <br/>Fecha y hora en que se creó el cliente  en formato ISO 8601
name          |***string*** <br/>Nombre del cliente.
last_name     |***string*** <br/>Apellidos del cliente.
email         |***string*** <br/>Cuenta de correo electrónico del cliente.
phone_number  |***numeric*** <br/>Número telefónico del Cliente.
status        |***string*** <br/>Estatus de la cuenta del cliente puede ser active o deleted. Si la cuenta se encuentra en estatus deleted no se permite realizar ninguna transacción.
balance       |***numeric*** <br/>Saldo en la cuenta con dos decimales.
creation_date |***datetime*** <br/>Fecha en que se creó el nuevo cliente.
external_id   |***string*** <br/>Identificador externo único para el cliente asignado por el comercio.
[customer_address](#objeto-direcci-n) |***object*** <br/>Dirección del Cliente. Usada comúnmente como dirección de envío.
clabe	      |***string***  <br/>No tiene uso por el momento.

##Crear un nuevo cliente

> Definición

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

> Ejemplo de petición

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   'external_id' : '',
   "name": "Pedro Diego",
   "last_name": "Alatorre Martínez",
   "email": "pedro.alatorre@comercio.com",
   "phone_number" : "5744484951",
   "customer_address": {
   	   "department":"Medellín",
	   "city":"Antioquía",
	   "additional":"Avenida 7f bis # 138-58 Apartamento 942"
   }
}'
```

```php
<?
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');

$customerData = array(
     'external_id' => '',
     'name' => 'Pedro Diego',
     'last_name' => 'Alatorre Martínez',
     'email' => 'pedro.alatorre@comercio.com',
     'phone_number' => '16362801',
     'customer_address' => array(
         'department' => 'Medellín',
         'city' => 'Antioquía',
         'additional' => 'Avenida 7f bis # 138-58 Apartamento 942'
      )
   );

$customer = $openpay->customers->add($customerData);
?>
```

```java



```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer request = new Customer();
request.ExternalId = "idExterno0101";
request.Name = "Pedro Diego";
request.LastName = "Alatorre Martínez";
request.Email = "pedro.alatorre@comercio.com";
request.PhoneNumber = "16362801";
request.RequiresAccount = false;
CustomerAddress customerAddress = new CustomerAddress();
customerAddress.Department = "Medellín";
customerAddress.City = "Bogota";
customerAddress.Additional = "Avenida 7f bis # 138-58 Apartamento 942";
request.CustomerAddress = customerAddress;

request = api.CustomerService.Create(request);
```

```javascript
var customerRequest = {
   'name': 'Pedro Diego',
   'last_email': 'Alatorre Martínez',
   'email': 'pedro.alatorre@comercio.com',
   'phone_number': '16362801',
   'requires_account': false,
   'address_customer': {
   	'department': 'Medellín',
	'city': 'Bogota',
	'additional': 'Avenida 7f bis # 138-58 Apartamento 942'
   }
   };

openpay.customers.create(customerRequest, function(error, customer) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@customers=@openpay.create(:customers)
address_customer={
      "department" => "Medellín",
      "city" => "Bogota",
      "additional" => "Avenida 7f bis # 138-58 Apartamento 942"
   }
request_hash={
     "external_id" => nil,
     "name" => "Pedro Diego",
     "last_name" => "Alatorre Martínez",
     "email" => "pedro.alatorre@comercio.com",
     "requires_account" => false,
     "phone_number" => "16362801",
     "address_customer" => address_customer
   }

response_hash=@customers.create(request_hash)
```

> Ejemplo de respuesta

```json
{
    "id": "awfx3738muksxzgrynwb",
    "name": "Pedro Diego",
    "last_name": "Alatorre Martínez",
    "email": "pedro.alatorre@comercio.com",
    "phone_number": "5744484951",
    "status": "active",
    "balance": 0.00,
    "creation_date": "2018-10-31T11:39:21-06:00",
    "external_id": null,
    "address": null,
    "customer_address": {
        "department": "Medellín",
        "city": "Antioquía",
        "additional": "Avenida 7f bis # 138-58 Apartamento 942"
    },
    "clabe": null
}
```

Crea un objeto cliente.

###Petición

Propiedad | Descripción
--------- | ------
external_id | ***string*** (opcional, longitud = 100)  <br/> Identificador externo único para el cliente asignado por el comercio.
name        | ***string*** (requerido, longitud = 100)<br/>Nombre(s) del cliente.
last_name   | ***string*** (opcional, longitud = 100)<br/>Apellidos del cliente.
email       | ***string*** (requerido, longitud = 100)<br/>Cuenta de correo electrónico del Cliente.
requires_account | ***boolean***  (opcional, default = true) <br/> Enviar con valor **false** si requiere que el cliente se cree sin cuenta para manejo del saldo. *Para usar módulo PSE este campo debe ir en false.*
phone_number| ***string*** (opcional, longitud = 100) <br/>Número telefónico del Cliente.
[customer_address](#objeto-direcci-n) | ***object*** (opcional) <br/>Dirección del Cliente. Usada comúnmente como dirección de envío.

###Respuesta

Un [objeto cliente](#objeto-cliente) en caso que se hayan enviado todos los datos correctamente, o una [respuesta de error](#objeto-error) si ocurrió algun problema en la creación.


##Actualizar un cliente

> Definición

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

> Ejemplo de petición

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/anbnldwgni1way3yp2dw \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X PUT -d '{
   "name": "customer name",
   "email": "customer_email@me.com",
    "customer_address": {
        "department": "Medellín",
        "city": "Antioquía",
        "additional": "Avenida 7f bis # 138-58 Apartamento 942"
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



```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Customer request = new Customer();
request.Name = "Julian Gerardo";
request.LastName = "López Martínez";
request.Email = "julian.martinez@gmail.com";
request.PhoneNumber = "16362801";
CustomerAddress customerAddress = new CustomerAddress();
customerAddress.Department = "Medellín";
customerAddress.City = "Antioquia";
customerAddress.Additional = "Avenida 11e bis #152-43 Apartamento 508";
request.CustomerAddress = customerAddress;

request = api.CustomerService.Update(request);
```

```javascript
var customerRequest = {
    'name': 'customer name',
    'email': 'customer_email@me.com',
    "customer_address": {
        "department": "Medellín",
        "city": "Antioquía",
        "additional": "Avenida 7f bis # 138-58 Apartamento 942"
    }

};

openpay.customers.update('anbnldwgni1way3yp2dw', customerRequest, function(error, customer) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@customers=@openpay.create(:customers)
address_customer={
      "department" => "Medellín",
      "city" => "Antioquía",
      "additional" => "Antioquía",
      "additional" => "Avenida 7f bis # 138-58 Apartamento 942"
   }
   
request_hash={
     "external_id" => nil,
     "name" => "customer name",
     "last_name" => nil,
     "email" => "customer_email@me.com",
     "requires_account" => true,
     "phone_number" => "44209087654",
     "address_customer" => address_customer
   }

response_hash=@customers.update(request_hash.to_hash)
```

> Ejemplo de respuesta

```json
{
    "id": "awfx3738muksxzgrynwb",
    "name": "Pedro Diego",
    "last_name": "Alatorre Martínez",
    "email": "pedro.alatorre@comercio.com",
    "phone_number": "5744484951",
    "status": "active",
    "balance": 0.00,
    "creation_date": "2018-10-31T11:39:21-06:00",
    "external_id": null,
    "address": null,
    "customer_address": {
        "department": "Medellín",
        "city": "Antioquía",
        "additional": "Avenida 7f bis # 138-58 Apartamento 942"
    },
    "clabe": null
}

```

Actualiza uno o más datos del cliente.

###Petición

Propiedad | Descripción
--------- | ------
name| ***string*** (requerido, longitud = 100)<br/>Nombre(s) del cliente.
last_name| ***string*** (opcional, longitud = 100) <br/>Apellidos del cliente.
email| ***string*** (requerido, longitud = 100)<br/>Cuenta de correo electrónico del Cliente.
phone_number| ***string*** (opcional, longitud = 100) <br/>Número telefónico del Cliente.
[customer_address](#objeto-direcci-n)| ***object*** <br/>Dirección del Cliente. Usada comúnmente como dirección de envío.

###Respuesta

Regresa un [objeto cliente](#objeto-cliente) con la información actualizada, o una [respuesta de error](#objeto-error) si ocurrió algun problema en la actualización.

##Obtener un cliente existente

> Definición

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

> Ejemplo de petición

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

> Ejemplo de respuesta

```json
{
    "id": "awfx3738muksxzgrynwb",
    "name": "Pedro Diego",
    "last_name": "Alatorre Martínez",
    "email": "pedro.alatorre@comercio.com",
    "phone_number": "5744484951",
    "status": "active",
    "balance": 0,
    "creation_date": "2018-10-31T11:39:21-06:00",
    "external_id": null,
    "address": null,
    "customer_address": {
        "department": "Medellín",
        "city": "Antioquía",
        "additional": "Avenida 7f bis # 138-58 Apartamento 942"
    },
    "clabe": null
}

```

Obtiene la información actual de un cliente existente. Solo es necesario especificar el identificador que fue regresado al momento de crear el cliente.

###Petición

Propiedad | Descripción
--------- | ------
id| _**string**_ (requerido, longitud = 45)<br/>Identificador único del cliente que se desea obtener.

###Respuesta

Si el identificador existe regresa un [objeto cliente](#objeto-cliente) con la información del cliente.

##Eliminar un cliente

> Definición

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

> Ejemplo de petición

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


Elimina un cliente permanentemente. Openpay mantiene los registros de las operaciones.
El cliente no se podrá borrar si su saldo es mayor a 0 (para cliente con manejo de saldo)

###Petición

Propiedad | Descripción
--------- | ------
id| _**string**_ (requerido, longitud = 45)<br/> Identificador único del cliente a borrar.

###Respuesta
Si el cliente se borra correctamente la respuesta es vacía, si no se puede borrar se regresa un [objeto error](#objeto-error) indicando el motivo.

##Listado de clientes

> Definición

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

> Ejemplo de petición

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

> Ejemplo de respuesta

```json
[{
    "id": "awfx3738muksxzgrynwb",
    "name": "Pedro Diego",
    "last_name": "Alatorre Martínez",
    "email": "pedro.alatorre@comercio.com",
    "phone_number": "5744484951",
    "status": "active",
    "balance": 0.00,
    "creation_date": "2018-10-31T11:39:21-06:00",
    "external_id": null,
    "address": null,
    "customer_address": {
        "department": "Medellín",
        "city": "Antioquía",
        "additional": "Avenida 7f bis # 138-58 Apartamento 942"
    },
    "clabe": null
}]
```
Regresa una lista de los cliente registrados, si desea delimitar el resultado se pueden utilizar los filtros.

###Petición
Puede realizar una búsqueda utilizando los siguiente parámetros como filtros.

Propiedad | Descripción
--------- | ------
external_id| _**string**_ <br/>Identificador único del cliente  asignado por el comercio que se desea obtener.
creation| ***date*** <br/>Igual a la fecha de creación del cliente. Formato yyyy-mm-dd
creation[gte]| ***date*** <br/>Mayor a la fecha de creación del cliente .Formato yyyy-mm-dd
creation[lte]| ***date*** <br/>Menor a la fecha de creación del cliente .Formato yyyy-mm-dd
offset| ***numeric*** <br/>Número de registros a omitir al inicio, por defecto 0.
limit| ***numeric*** <br/>Número de registros que se requieren, por defecto 10.

###Respuesta

Regresa un arreglo de [objetos cliente](#objeto-cliente).
