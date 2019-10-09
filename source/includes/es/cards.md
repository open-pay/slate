#Tarjetas
Dentro de la plataforma Openpay podrás agregar tarjetas a la cuenta del cliente, eliminarlas, recuperar alguna en específico y listarlas​.

Se pueden almacenar múltiples tarjetas de débito y/o crédito a nivel cliente o a nivel comercio para realizar cargos posteriormente sin la necesidad de introducir nuevamente la información.

##Objeto Tarjeta

> Ejemplo de objeto

```json
{
   "type":"debit",
   "brand":"mastercard",
   "address":{
      "line1":"Av 5 de Febrero",
      "line2":"Roble 207",
      "line3":"col carrillo",
      "state":"Bogota",
      "city":"Bogotá",
      "postal_code":"110511",
      "country_code":"CO"
   },
   "id":"kgipbqixvjg3gbzowl7l",
   "card_number":"1111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "allows_charges":true,
   "allows_payouts":false,
   "creation_date":"2013-12-12T17:50:00-06:00",
   "bank_name":"DESCONOCIDO",
   "bank_code":"000",
   "customer_id":"a2b79p8xmzeyvmolqfja"
}
```

Propiedad | Descripción
--------- | ------
id            |***string*** <br/>Identificador único de la tarjeta.
creation_date |***datetime*** <br/>Fecha y hora en que se creó la tarjeta en formato ISO 8601
holder_name |***string***  <br/>Nombre del tarjeta habiente.
card_number |***numeric***  <br/>Número de tarjeta, puede ser de 16 o 19 dígitos.
cvv2 |***numeric***  <br/>Código de seguridad como aparece en la parte de atrás de la tarjeta. Generalmente 3 dígitos.
expiration_month |***numeric***  <br/>Mes de expiración tal como aparece en la tarjeta.
expiration_year |***numeric***  <br/>Año de expiración tal como aparece en la tarjeta.
[address](#objeto-direcci-n) |***object*** <br/>Dirección de facturación del tarjeta habiente.
allows_charges |***boolean*** <br/>Permite conocer si se pueden realizar cargos a la tarjeta.
allows_payouts |***boolean*** <br/>Permite conocer si se pueden realizar envíos de pagos a la tarjeta.
brand |***string*** <br/>Marca de la tarjeta: visa, mastercard, carnet o american express.
type |***string*** <br/>Tipo de la tarjeta: debit, credit, cash, etc.
bank_name |***string*** <br/>Nombre del banco emisor.
bank_code |***string*** <br/>Código del banco emisor.
customer_id |***string*** <br/>Identificador del cliente al que pertenece la tarjeta. Si la tarjeta es a nivel comercio este valor será null.

##Crear una tarjeta

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/cards

Cliente
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Cliente
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->add(cardDataRequest);

//Comercio
$card = $openpay->cards->add(cardDataRequest);
?>
```

```java
//Cliente
openpayAPI.cards().create(String customerId, Card request);

//Comercio
openpayAPI.cards().create(Card request);
```

```csharp
//Cliente
openpayAPI.CardService.Create(string customer_id, Card card);

//Comercio
openpayAPI.CardService.Create(Card card);
```

```javascript
// Comercio
openpay.cards.create(cardRequest, callback);

// Cliente
openpay.customers.cards.create(customerId, cardRequest, callback);
```

```ruby
#Cliente
@cards=@openpay.create(:cards)
@cards.create(request_hash, customer_id)

#Comercio
@cards=@openpay.create(:cards)
@cards.create(request_hash)
```

> Ejemplo de petición con cliente

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
  "holder_name":"DinnersClub",
  "card_number":"36728481533333",
  "cvv2":"651",
  "expiration_month":"07",
  "expiration_year":"21",
  "device_session_id" : "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f"
}'
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$cardDataRequest = array(
    'holder_name' => 'Teofilo Velazco',
    'card_number' => '4916394462033681',
    'cvv2' => '123',
    'expiration_month' => '12',
    'expiration_year' => '15',
    'device_session_id' => 'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f',
    'address' => array(
            'line1' => 'Privada Rio No. 12',
            'line2' => 'Co. El Tintero',
            'line3' => '',
            'postal_code' => '76920',
            'state' => 'Bogotá',
            'city' => 'Bogotá',
            'country_code' => 'CO'));

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$card = $customer->cards->add($cardDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card request = new Card();
request.holderName("Juan Perez Ramirez");
request.cardNumber("4111111111111111");
request.cvv2("110");
request.expirationMonth(12);
request.expirationYear(20);
request.deviceSessionId("kR1MiQhz2otdIuUlQkbEyitIqVMiI16f");
Address address = new Address();
address.city("Bogota");
address.countryCode("10");
address.state("Bogota");
address.postalCode("79125");
address.line1("Av. Pie de la cuesta #12");
address.line2("Desarrollo San Pablo");
address.line3("Qro. Qro.");
request.address(address);

request = api.cards().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card request = new Card();
request.HolderName = "Juan Perez Ramirez";
request.CardNumber = "4111111111111111";
request.Cvv2 = "110";
request.ExpirationMonth = "12";
request.ExpirationYear = "20";
request.DeviceSessionId = "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f";
Address address = new Address();
address.City = "Bogota";
address.CountryCode = "CO";
address.State = "Bogota";
address.PostalCode = "79125";
address.Line1 = "Av. Pie de la cuesta #12";
address.Line2 = "Desarrollo San Pablo";
address.Line3 = "Qro. Qro.";
request.Address = address;

request = api.CardService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var cardRequest = {
   'card_number':'4111111111111111',
   'holder_name':'Juan Perez Ramirez',
   'expiration_year':'20',
   'expiration_month':'12',
   'cvv2':'110',
   'device_session_id':'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f'
};

openpay.customers.cards.create('a9pvykxz4g5rg0fplze0', cardRequest, function(error, card)  {
    // ...    
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)
address_hash={
      "line1" => "Calle 10",
      "line2" => "col. san pablo",
      "line3" => "entre la calle 1 y la 2",
      "state" => "Bogota",
      "city" => "Bogota",
      "postal_code" => "76000",
      "country_code" => "CO"
   }
request_hash={
     "holder_name" => "Juan Perez Ramirez",
     "card_number" => "411111XXXXXX1111",
     "cvv2" => "110",
     "expiration_month" => "12",
     "expiration_year" => "20",
     "device_session_id" => "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f",
     "address" => address_hash
   }

response_hash=@cards.create(request_hash.to_hash, "asynwirguzkgq2bizogo")
```

> Ejemplo de respuesta

```json
{
    "id": "kulqltitbq0wnk3l2q3c",
    "type": "credit",
    "brand": "diners",
    "address": null,
    "card_number": "367284XXXX3333",
    "holder_name": "DinnersClub",
    "expiration_year": "21",
    "expiration_month": "07",
    "allows_charges": true,
    "allows_payouts": false,
    "creation_date": "2019-08-12T13:12:22-05:00",
    "bank_name": "BANCO DE BOGOTÁ",
    "bank_code": "000"
}
```

Cuando se crea una tarjeta debe especificarse cliente, si no se especifica el cliente la tarjeta quedará registrada para la cuenta del comercio. Una vez guardada la tarjeta no se puede obtener el número y código de seguridad.

<aside class="notice">
**Nota:** Todas las tarjetas al momento de guardarse en Openpay son validadas haciendo un autorización por $10.00 los cuales son devueltos en el momento.
</aside>

Al momento de guardar la tarjeta se generará un id que podrá ser usado para hacer cargos a la tarjeta, envíos a una tarjeta o simplemente obtener la información no sensible de la tarjeta.

Cuando se crea una tarjeta puede usarse o no la implementación del sistema antifraude. La propiedad <code>device_session_id</code> deberá ser generada desde el API JavaScript, véase [Fraud detection using device data](https://github.com/open-pay/openpay-js#fraud-detection-using-device-data).

###Petición

Propiedad | Descripción
--------- | ------
holder_name |***string*** (requerido, longitud = 80) <br/>Nombre del tarjeta habiente.
card_number |***numeric*** (requerido) <br/>Numero de tarjeta puede ser de 16 o 19 dígitos.
cvv2 |***numeric*** (requerido) <br/>Código de seguridad como aparece en la parte de atrás de la tarjeta. Generalmente 3 dígitos.
expiration_month |***numeric*** (requerido) <br/>Mes de expiración tal como aparece en la tarjeta.
expiration_year |***numeric*** (requerido) <br/>Año de expiración tal como aparece en la tarjeta.
device_session_id | ***string*** (opcional, longitud = 255) <br/>Identificador del dispositivo generado con la herramienta antifraudes.
[address](#objeto-direcci-n) |***object*** <br/>Dirección de facturación del tarjeta habiente.

###Respuesta
Regresa un [objeto tarjeta](#objeto-tarjeta) cuando se creó correctamente o una [respuesta de error](#objeto-error) si ocurrió algún problema en la creación.


##Crear una tarjeta con token

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/cards

Cliente
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Cliente
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->add(cardDataRequest);

//Comercio
$card = $openpay->cards->add(cardDataRequest);
?>
```

```java
//Cliente
openpayAPI.cards().create(String customerId, Card card);

//Comercio
openpayAPI.cards().create(Card card);
```

```csharp
//Cliente
openpayAPI.CardService.Create(string customer_id, Card request);

//Comercio
openpayAPI.CardService.Create(Card request);
```

```javascript
// Comercio
openpay.cards.create(cardRequest, callback);

// Cliente
openpay.customers.cards.create(customerId, cardRequest, callback);
```

```ruby
#Cliente
@cards=@openpay.create(:cards)
@cards.create(request_hash, customer_id)

#Comercio
@cards=@openpay.create(:cards)
@cards.create(request_hash)
```

> Ejemplo de petición con cliente

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
      "token_id":"tokgslwpdcrkhlgxqi9a",
      "device_session_id":"8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o"
   }'
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$cardDataRequest = array(
    'token_id' => 'tokgslwpdcrkhlgxqi9a',
    'device_session_id' => '8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o'
    );

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$card = $customer->cards->add($cardDataRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card request = new Card();
request.tokenId("tokgslwpdcrkhlgxqi9a");
request.deviceSessionId("8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o");

request = api.cards().create("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card request = new Card();
request.TokenId = "tokgslwpdcrkhlgxqi9a";
request.DeviceSessionId = "8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o";

request = api.CardService.Create("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var cardRequest = {
  'token_id' : 'tokgslwpdcrkhlgxqi9a',
  'device_session_id' : '8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o'
}

openpay.customers.cards.create('a9pvykxz4g5rg0fplze0', cardRequest, function(error, card)  {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)
request_hash={
     "token_id" => "tokgslwpdcrkhlgxqi9a",
     "device_session_id" => "8VIoXj0hN5dswYHQ9X1mVCiB72M7FY9o"
   }

response_hash=@cards.create(request_hash.to_hash, "asynwirguzkgq2bizogo")
```


> Ejemplo de respuesta

```json
{
    "id": "kh6u8t1agrjhh4sz3vlt",
    "type": "debit",
    "brand": "visa",
    "address": null,
    "card_number": "457562XXXXXX0326",
    "holder_name": "Jorge Lopez",
    "expiration_year": "19",
    "expiration_month": "12",
    "allows_charges": true,
    "allows_payouts": false,
    "creation_date": "2019-08-12T13:14:34-05:00",
    "bank_name": "BBVA COLOMBIA",
    "bank_code": "000"
}
```

Crea una tarjeta a partir de un token obtenido desde el navegador o dispositivo del cliente. Esta forma evita que la información sensible de la tarjeta pase por tus servidores.

###Petición
Propiedad | Descripción
--------- | ------
token_id| ***string*** (requerido, longitud = 45) <br/> Identificador del token generado en el navegador o dispositivo del cliente.
device_session_id| ***string*** (requerido, longitud = 255) <br> Identificador del dispositivo generado con la herramienta antifraudes

###Respuesta
Regresa un [objeto tarjeta](#objeto-tarjeta)

##Obtener una tarjeta

> Definición

```shell
Comercio
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/cards/{CARD_ID}

Cliente
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}
```

```php
<?
//Cliente
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->get(cardId);

//Comercio
$card = $openpay->cards->get(cardId);
?>
```

```java
//Cliente
openpayAPI.cards().get(String customerId, String cardId);

//Comercio
openpayAPI.cards().get(String cardId);
```

```csharp
//Cliente
openpayAPI.CardService.Get(string customer_id, string card_id);

//Comercio
openpayAPI.CardService.Get(string card_id);
```

```javascript
// Comercio
openpay.cards.get(cardId, callback);

// Cliente
openpay.customers.cards.get(customerId, cardId, callback);
```

```ruby
#Cliente
@cards=@openpay.create(:cards)
@cards.get(card_id, customer_id)

#Comercio
@cards=@openpay.create(:cards)
@cards.get(card_id)
```

> Ejemplo de petición con cliente

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards/ktrpvymgatocelsciak7 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json"
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$card = $customer->cards->get('k9pn8qtsvr7k7gxoq1r5');
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card card = api.cards().get("a9pvykxz4g5rg0fplze0", "ktrpvymgatocelsciak7");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Card card = api.CardService.Get("a9pvykxz4g5rg0fplze0", "ktrpvymgatocelsciak7");
```

```javascript
openpay.customers.cards.get('a9pvykxz4g5rg0fplze0', 'ktrpvymgatocelsciak7', function(error, card){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)

response_hash=@cards.get("ktrpvymgatocelsciak7", "asynwirguzkgq2bizogo")
```

> Ejemplo de respuesta

```json
{
    "id": "kh6u8t1agrjhh4sz3vlt",
    "type": "debit",
    "brand": "visa",
    "address": null,
    "card_number": "457562XXXXXX0326",
    "holder_name": "Jorge Lopez",
    "expiration_year": "19",
    "expiration_month": "12",
    "allows_charges": true,
    "allows_payouts": false,
    "creation_date": "2019-08-12T13:14:34-05:00",
    "bank_name": "BBVA COLOMBIA",
    "bank_code": "000"
}
```

Obtiene los detalles de una tarjeta solicitándola con su id.

<aside class="notice">
**Nota:** Nunca se regresarán datos sensibles como son el código de seguridad y del número de tarjeta sólo se mostraran los primeros 6 y los últimos 4 dígitos.
</aside>

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador único de la tarjeta

###Respuesta
Regresa un [objeto tarjeta](#objeto-tarjeta)

##Eliminar una tarjeta

> Definición

```shell
Comercio
DELETE https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/cards/{CARD_ID}

Cliente
DELETE https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}
```

```php
<?
//Cliente
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->get(cardId);
$card->delete();

//Comercio
$card = $openpay->cards->get(cardId);
$card->delete();
?>
```

```java
//Cliente
openpayAPI.cards().delete(String customerId, String cardId);

//Comercio
openpayAPI.cards().delete(String cardId);
```

```csharp
//Cliente
openpayAPI.CardService.Delete(string customer_id, string card_id);

//Comercio
openpayAPI.CardService.Delete(string card_id);
```

```javascript
// Comercio
openpay.cards.delete(cardId, callback);

// Cliente
openpay.customers.cards.delete(customerId, cardId, callback);
```

```ruby
#Cliente
@cards=@openpay.create(:cards)
@cards.delete(card_id, customer_id)

#Comercio
@cards=@openpay.create(:cards)
@cards.delete(card_id)
```

> Ejemplo de petición con cliente

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards/ktrpvymgatocelsciak7 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -X DELETE
```

```php
<?
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$customer = $openpay->customers->get('a9ualumwnrcxkl42l6mh');
$card = $customer->cards->get('k9pn8qtsvr7k7gxoq1r5');
$card->delete();
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.cards().delete("a9pvykxz4g5rg0fplze0", "ktrpvymgatocelsciak7");
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
api.CardService.Delete("a9pvykxz4g5rg0fplze0", "ktrpvymgatocelsciak7");
```

```javascript
openpay.customers.cards.delete('a9pvykxz4g5rg0fplze0', 'ktrpvymgatocelsciak7', function(error) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)

response_hash=@cards.delete("ktrpvymgatocelsciak7", "asynwirguzkgq2bizogo")
```

Elimina una tarjeta del cliente o comercio. Una vez eliminada no se permitirá hacer movimientos, sin embargo, se mantendrán todos los registros de operaciones que haya realizado y se podrán consultar en el dashboard.

Para eliminarla sólo es necesario proporcionar el identificador de la tarjeta.

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador único de la tarjeta

###Respuesta
Si la tarjeta se borra correctamente la respuesta es vacía, si no se puede borrar se regresa un [objeto error](#objeto-error) indicando el motivo.


##Listado de tarjetas
> Definición

```shell
Comercio
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers

Cliente
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Clientes
$customer = $openpay->customers->get(customerId);
$cardList = $customer->cards->getList(findDataRequest);

//Comercio
$cardList = $openpay->cards->getList(findDataRequest);
?>
```

```java
//Cliente
openpayAPI.cards().list(String customerId, SearchParams request);

//Comercio
openpayAPI.cards().list(SearchParams request);
```

```csharp
//Cliente
openpayAPI.CardService.List(string customer_id, SearchParams request = null);

//Comercio
openpayAPI.CardService.List(SearchParams request = null);
```

```javascript
// Comercio
openpay.cards.list(callback);
openpay.cards.list(searchParams, callback);

// Cliente
openpay.cards.list(customerId, callback);
openpay.cards.list(customerId, searchParams, callback);
```

```ruby
#Cliente
@cards=@openpay.create(:cards)
@cards.all(customer_id)

#Comercio
@cards=@openpay.create(:cards)
@cards.all
```

> Ejemplo de petición con cliente

```shell
curl -g "https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards?limit=2" \
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
$cardList = $customer->cards->getList($findDataRequest);
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
List<Card> cards = api.cards().list("a9pvykxz4g5rg0fplze0", request);
```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
SearchParams request = new SearchParams();
request.CreationGte = new Datetime(2014, 5, 1);
request.CreationLte = new DateTime(2014, 5, 15);
request.Offset = 0;
request.Limit = 100;

List<Card> cards = api.CardService.List("a9pvykxz4g5rg0fplze0", request);
```

```javascript
var searchParams = {
  'limit' : 2
};

openpay.customers.cards.list('ag4nktpdzebjiye1tlze', searchParams, function(error, list){
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@cards=@openpay.create(:cards)

response_hash=@cards.all("asynwirguzkgq2bizogo")
```

> Ejemplo de respuesta

```json
[
   {
      "id":"kxq1rpdymlcpxekvjsxm",
      "card_number":"1118",
      "holder_name":"Pedro Paramo",
      "expiration_year":"15",
      "expiration_month":"12",
      "allows_charges":true,
      "allows_payouts":true,
      "creation_date":"2013-11-20T09:22:25-06:00",
      "bank_name":"BBVA BANCOMER",
      "bank_code":"012",
      "type":"debit",
      "brand":"mastercard"
   },
   {
      "id":"kgjy0jiami01kkpdoywr",
      "card_number":"1111",
      "holder_name":"Pedro Paramo",
      "expiration_year":"15",
      "expiration_month":"12",
      "allows_charges":true,
      "allows_payouts":true,
      "creation_date":"2013-11-19T13:26:12-06:00",
      "bank_name":"BBVA BANCOMER",
      "bank_code":"012",
      "type":"debit",
      "brand":"mastercard"
   }
]
```

Regresa una lista de las tarjetas registrados por comercio o cliente, si desea delimitar el resultado se pueden utilizar los filtros.

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
Listado de [objetos tarjeta](#objeto-tarjeta) registrados de acuerdo a los parámetros proporcionados, ordenadas por fecha de creación en orden descendente.

## Actualizar tarjeta

> Definición

```plaintext
Comercio
PUT https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/cards/{CARD_ID}

Cliente
PUT https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}
```

> Ejemplo de petición con cliente

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/customers/ag4nktpdzebjiye1tlze/cards/kysc8pycq8hnlzivk1x4 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X PUT -d '{
      "cvv2":"000"
   }'
```

```javascript
```

> Ejemplo de respuesta

```json
{
}
```

Actualiza los datos de una tarjeta desde el navegador o dispositivo del cliente. También permite enviar un cvv2 que se usará en el próximo cargo que se realice a esta tarjeta.
De esta forma evita que la información sensible de la tarjeta pase por tus servidores.

###Petición
Propiedad | Descripción
--------- | ------
holder_name |***string*** (opcional) <br/>Nombre del tarjeta habiente.
cvv2      | ***string*** (opcional) <br/> Código de seguridad como aparece en la parte de atrás de la tarjeta. Generalmente 3 dígitos.
expiration_month |***numeric*** (opcional) <br/>Mes de expiración tal como aparece en la tarjeta.
expiration_year |***numeric*** (opcional) <br/>Año de expiración tal como aparece en la tarjeta.
merchant_id | ***string*** (condicional) <br/> ID del comercio. Usado solamente cuando se usa un grupo de comercio.


###Respuesta
Actualmente regresa un JSON sin datos. Considerar que se podría extender la respuesta en el futuro.
