#Cards
Within the Openpay platform you can add cards to the customer's account, delete them, recover some in specific and list them.

You can store multiple debit and / or credit cards at Merchant or customer level for making charges later without the need to enter the information again.

##Card Object

> Object example

```json
{
   "type":"debit",
   "brand":"mastercard",
   "address":null,
   "id":"kgipbqixvjg3gbzowl7l",
   "card_number":"1111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "allows_charges":true,
   "allows_payouts":false,
   "creation_date":"2018-12-12T17:50:00-06:00",
   "bank_name":"BANCO DE COLOMBIA",
   "bank_code":"000",
   "customer_id":"a2b79p8xmzeyvmolqfja"
}
```

Property | Description
--------- | ------
id            |***string*** <br/>Unique identifier of the card.
creation_date |***datetime*** <br/>Date and time when the card was created in ISO 8601 format.
holder_name |***string***  <br/>Name of the cardholder.
card_number |***numeric***  <br/>Card Number, it can be 16 or 19 digits.
cvv2 |***numeric***  <br/>Security code as it appears on the back of the card. Usually 3 digits..
expiration_month |***numeric***  <br/>Expiration month as it appears on the card.
expiration_year |***numeric***  <br/>Expiration year as it appears on the card.
[address](#address-object) |***object*** <br/>It is not used at this time.
allows_charges |***boolean*** <br/>It allows to know if you can make charges to the card.
allows_payouts |***boolean*** <br/>It allows to know if you can send payments to the card.
brand |***string*** <br/>Card brand: visa, mastercard, carnet or american express.
type |***string*** <br/>Card Type: debit, credit, cash, etc.
bank_name |***string*** <br/>Name of the issuing bank.
bank_code |***string*** <br/>Code of the issuing bank.
customer_id |***string*** <br/>Customer identifier to which the card belongs. If the card is at Merchant level this value is null.

##Create a card

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/cards

Customer
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->add(cardDataRequest);

//Merchant
$card = $openpay->cards->add(cardDataRequest);
?>
```

```java
//Customer
openpayAPI.cards().create(String customerId, Card request);

//Merchant
openpayAPI.cards().create(Card request);
```

```csharp
//Customer
openpayAPI.CardService.Create(string customer_id, Card card);

//Merchant
openpayAPI.CardService.Create(Card card);
```

```javascript
// Merchant
openpay.cards.create(cardRequest, callback);

// Customer
openpay.customers.cards.create(customerId, cardRequest, callback);
```

```ruby
#Customer
@cards=@openpay.create(:cards)
@cards.create(request_hash, customer_id)

#Merchant
@cards=@openpay.create(:cards)
@cards.create(request_hash)
```

> Customer Request example

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
    'device_session_id' => 'kR1MiQhz2otdIuUlQkbEyitIqVMiI16f'
);

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

request_hash={
     "holder_name" => "Juan Perez Ramirez",
     "card_number" => "411111XXXXXX1111",
     "cvv2" => "110",
     "expiration_month" => "12",
     "expiration_year" => "20",
     "device_session_id" => "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f"
   }

response_hash=@cards.create(request_hash.to_hash, "asynwirguzkgq2bizogo")
```

> Response example

```json
{
     "id": "kulqltitbq0wnk3l2q3c",
     "type": "debit",
     "brand": "visa",
     "address": null,
     "card_number":"411111XXXXXX1111",
     "holder_name":"Juan Perez Ramirez",
     "expiration_year":"20",
     "expiration_month":"12",
     "allows_charges":true,
     "allows_payouts":true,
     "creation_date":"2018-05-21T17:31:01-05:00",
     "bank_name":"BBVA",
     "bank_code":"000"
}
```

When a card is created the customer must be specified, if the customer is not specified the card will be registered for the Merchant account. Once the card is saved, it can not obtain the number and security code.

<aside class = "notice">
**Note:** When stored in Openpay, all cards  are validated by making an authorization for $ 10.00 which is returned at the time.
</aside>

When saving a card, an ID will be created which can be used to make card charges, payouts to a card or just for getting the not sensitive card information.

You can use the antifraud system implementation. The <code>device_session_id</code> property must be generated using JavaScript API, see [Fraud detection using device data](https://github.com/open-pay/openpay-js#fraud-detection-using-device-data).

###Request

Property | Description
--------- | ------
holder_name |***string*** (required, length  = 80) <br/>Name of the cardholder.
card_number |***numeric*** (required) <br/>Card Number, it can be 16 or 19 digits.
cvv2 |***numeric*** (required) <br/>Security code as it appears on the back of the card. Usually 3 digits.
expiration_month |***numeric*** (required) <br/>Expiration month as it appears on the card.
expiration_year |***numeric*** (required) <br/>Expiration year as it appears on the card.
device_session_id | ***string*** (optional, length = 255) <br/>Device identifier generated by antifraud tool.


###Response
Returns a [card object](#card-object) when it is created correctly or returns an [error response](#error-object) if a problem happened during the creation.


##Create a card with token

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/cards

Customer
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->add(cardDataRequest);

//Merchant
$card = $openpay->cards->add(cardDataRequest);
?>
```

```java
//Customer
openpayAPI.cards().create(String customerId, Card card);

//Merchant
openpayAPI.cards().create(Card card);
```

```csharp
//Customer
openpayAPI.CardService.Create(string customer_id, Card request);

//Merchant
openpayAPI.CardService.Create(Card request);
```

```javascript
// Merchant
openpay.cards.create(cardRequest, callback);

// Customer
openpay.customers.cards.create(customerId, cardRequest, callback);
```

```ruby
#Customer
@cards=@openpay.create(:cards)
@cards.create(request_hash, customer_id)

#Merchant
@cards=@openpay.create(:cards)
@cards.create(request_hash)
```

> Request example

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


> Response example

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
    "bank_code": "000",
   "customer_id":"a2b79p8xmzeyvmolqfja"
}
```

Creates a card from a token obtained from the browser or from the customer’s device. This way prevents the sensitive card information passes through your servers.

###Request
Property | Description
--------- | ------
token_id| ***string*** (required, length = 45) <br/> Token identifier generated in the the browser or in the customer’s device.
device_session_id| ***string*** (required, length = 255) <br/> Identifier of the device generated by the antifraud tool.

###Response
Returns a [card object](#card-object)

##Get a card

> Definition

```shell
Merchant
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/cards/{CARD_ID}

Customer
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}
```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->get(cardId);

//Merchant
$card = $openpay->cards->get(cardId);
?>
```

```java
//Customer
openpayAPI.cards().get(String customerId, String cardId);

//Merchant
openpayAPI.cards().get(String cardId);
```

```csharp
//Customer
openpayAPI.CardService.Get(string customer_id, string card_id);

//Merchant
openpayAPI.CardService.Get(string card_id);
```

```javascript
// Merchant
openpay.cards.get(cardId, callback);

// Customer
openpay.customers.cards.get(customerId, cardId, callback);
```

```ruby
#Customer
@cards=@openpay.create(:cards)
@cards.get(card_id, customer_id)

#Merchant
@cards=@openpay.create(:cards)
@cards.get(card_id)
```

> Request example

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

> Response example

```json
{
     "id": "kulqltitbq0wnk3l2q3c",
     "type": "debit",
     "brand": "visa",
     "address": null,
     "card_number":"411111XXXXXX1111",
     "holder_name":"Juan Perez Ramirez",
     "expiration_year":"20",
     "expiration_month":"12",
     "allows_charges":true,
     "allows_payouts":true,
     "creation_date":"2018-05-21T17:31:01-05:00",
     "bank_name":"BBVA",
     "bank_code":"000"
}
```

It obtains the details of the card by using its id.

<aside class="notice">
**Note:** It will never return sensitive data as the code and card number, only the first 6 and last 4 digits will be displayed.
</aside>

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Card unique identifier.

###Response
Returns a [card object](#card-object)

##Delete a card

> Definition

```shell
Merchant
DELETE https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/cards/{CARD_ID}

Customer
DELETE https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}
```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$card = $customer->cards->get(cardId);
$card->delete();

//Merchant
$card = $openpay->cards->get(cardId);
$card->delete();
?>
```

```java
//Customer
openpayAPI.cards().delete(String customerId, String cardId);

//Merchant
openpayAPI.cards().delete(String cardId);
```

```csharp
//Customer
openpayAPI.CardService.Delete(string customer_id, string card_id);

//Merchant
openpayAPI.CardService.Delete(string card_id);
```

```javascript
// Merchant
openpay.cards.delete(cardId, callback);

// Customer
openpay.customers.cards.delete(customerId, cardId, callback);
```

```ruby
#Customer
@cards=@openpay.create(:cards)
@cards.delete(card_id, customer_id)

#Merchant
@cards=@openpay.create(:cards)
@cards.delete(card_id)
```

> Request example

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

To remove it is only necessary to provide the card identifier.

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Card unique identifier.

###Response
If the card is removed correctly the answer is empty, if it can not be deleted a [error object] (#error-object) indicating the reason is returned.


##List of cards
> Definition

```shell
Merchant
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers

Customer
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards
```

```php
<?
//Customer
$customer = $openpay->customers->get(customerId);
$cardList = $customer->cards->getList(findDataRequest);

//Merchant
$cardList = $openpay->cards->getList(findDataRequest);
?>
```

```java
//Customer
openpayAPI.cards().list(String customerId, SearchParams request);

//Merchant
openpayAPI.cards().list(SearchParams request);
```

```csharp
//Customer
openpayAPI.CardService.List(string customer_id, SearchParams request = null);

//Merchant
openpayAPI.CardService.List(SearchParams request = null);
```

```javascript
// Merchant
openpay.cards.list(callback);
openpay.cards.list(searchParams, callback);

// Customer
openpay.cards.list(customerId, callback);
openpay.cards.list(customerId, searchParams, callback);
```

```ruby
#Customer
@cards=@openpay.create(:cards)
@cards.all(customer_id)

#Merchant
@cards=@openpay.create(:cards)
@cards.all
```

> Request example

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

> Response example

```json
[
	{
	"id": "kulqltitbq0wnk3l2q3c",
	"type": "debit",
	"brand": "visa",
	"address": null,
	"card_number":"411111XXXXXX1111",
	"holder_name":"Juan Perez Ramirez",
	"expiration_year":"20",
	"expiration_month":"12",
	"allows_charges":true,
	"allows_payouts":true,
	"creation_date":"2018-05-21T17:31:01-05:00",
	"bank_name":"BBVA",
	"bank_code":"000"
	},
	{
	"id":"kgjy0jiami01kkpdoywr",
	"type":"debit",
	"brand":"mastercard",
	"address": null,
	"card_number":"1111",
	"holder_name":"Pedro Paramo",
	"expiration_year":"15",
	"expiration_month":"12",
	"allows_charges":true,
	"allows_payouts":true,
	"creation_date":"2013-11-19T13:26:12-06:00",
	"bank_name":"BBVA BANCOMER",
	"bank_code":"012"
	}
]
```

Returns a list of registered Merchant or customer cards, if you want to narrow the result you can use filters.

### Request
You can search using the following parameters as filters.

Property | Description
--------- | ------
creation| ***date*** <br/>Same as creation date. Format yyyy-mm-dd
creation[gte]| ***date*** <br/>After the creation date. Format yyyy-mm-dd
creation[lte]| ***date*** <br/>Before the creation date. Format yyyy-mm-dd
offset| ***numeric*** <br/>Number of records to skip at the beginning, default 0.
limit| ***numeric*** <br/>Number of required records, default 10.

###Response
List of [card objects] (#card-object) registered according to the parameters provided, sorted by creation date in descending order.

## Updating a card

> Definition

```plaintext
Merchant
PUT https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/cards/{CARD_ID}

Customer
PUT https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/cards/{CARD_ID}
```

> Request example

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

> Response example

```json
{
}
```

Updates the card data from the browser or from the customer's device.  It also allows to send a cvv2 code that will be used in the next transaction done with this card.
This prevents sensitive information from passing through your servers.

###Request
Property  | Description
--------- | ------
holder_name |***string*** (optional) <br/>Name of the cardholder.
cvv2 |***string***  (optional)<br/>Security code as it appears on the back of the card. Usually 3 digits.
expiration_month |***numeric*** (optional) <br/>Expiration month as it appears on the card.
expiration_year |***numeric*** (optional) <br/>Expiration year as it appears on the card.
merchant_id | **string** (conditional) <br/> Merchant ID to use to validate this card. Required when using a merchant group.

###Response
Returns an empty JSON object. Please consider that this response may be extended in the future.
