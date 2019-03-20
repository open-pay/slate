#Tokens

The objective is to created tokens from the user browser or device to capture the card information so this doesn't go through your server and you can avoid or reduce the PCI certification process.

To use this API functionality we recommend using our JavaScript library for your Web application and our Android and iOS SDK for mobile apps.

**Features**

* Tokens are created at Merchant level.
* Tokens are not link to any customer.
* After a token has been created it can only be use once to make a charge.

##Token Object

> Object example 

```json
{
    "id":"tokfa4swch8gr4icy2ma",
    "card":{
       "card_number":"1111",
       "holder_name":"Juan Perez Ramirez",
       "expiration_year":"20",
       "expiration_month":"04",
       "address":{
          "line1":"Av 5 de febrero",
          "line2":"Roble 207",
          "line3":"Queretaro",
          "state":"Queretaro",
          "city":"Queretaro",
          "postal_code":"76900",
          "country_code":"MX"
       },
       "creation_date":"2014-01-30T13:53:11-06:00",
       "brand":"visa",
       "points_card":false
    }
}
```

Property | Description
--------- | ------
id | ***string*** <br/>Token identifier.  This is the ID that you should use to perform operations.
card | ***object*** <br/>Card associated with the token.  See [card object](#card-object).


##Create a new token

> Definition

```shell
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/tokens
```

```java
//Merchant
bancomerAPI.tokens().create(List<Parameter> request);
```

```csharp
//Merchant
bancomerAPI.TokenService.Create(List<IParameter> request);
```

```ruby
#Merchant
@tokens=@bancomer.create(:tokens)
@tokens.create(request_hash)
```

```php
<?
//Merchant
$token = $bancomer->tokens->create($tokenRequest);
?>
```

> Request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/tokens \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "card_number":"4111111111111111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "cvv2":"110",
   "address":{
      "city":"Querétaro",
      "country_code":"MX",
      "postal_code":"76900",
      "line1":"Av 5 de Febrero",
      "line2":"Roble 207",
      "line3":"col carrillo",
      "state":"Queretaro"
   }
}'
```

```java
BancomerAPI api = new BancomerAPI("https://sand-api.ecommercebbva.com/", "sk_08453429e4c54220a3a82ab4d974c31a", "miklpzr4nsvsucghm2qp");

List<Parameter> request = new ArrayList<Parameter>(Arrays.asList(
        new SingleParameter("card_number", "4111111111111111"),
        new SingleParameter("cvv2", "295"),
        new SingleParameter("expiration_month", "12"),
        new SingleParameter("expiration_year", "20"),
        new SingleParameter("holder_name", "Juan Perez Lopez")));

Map tokenAsMap = this.api.tokens().create(request);
ParameterContainer token = new ParameterContainer("token", tokenAsMap);
```
```csharp
BancomerAPI bancomerAPI = new BancomerAPI("sk_08453429e4c54220a3a82ab4d974c31a", "miklpzr4nsvsucghm2qp");

List<IParameter> request = new List<IParameter>{
    new SingleParameter("holder_nane", "Juan Perez Ramirez"),
    new SingleParameter("card_number", "4111111111111111"),
    new SingleParameter("cvv2", "022"),
    new SingleParameter("expiration_month", "12"),
    new SingleParameter("expiration_year", "20"),
};

Dictionary<String, Object> tokenDictionary = bancomerAPI.TokenService.Create(request);
ParameterContainer token = new ParameterContainer("token", tokenDictionary);
```
```ruby
@bancomer=BancomerApi.new('mywvupjjs9xdnryxtplq', 'sk_92b25d3baec149e6b428d81abfe37006')
@tokens=@bancomer.create(:tokens)

token_hash={
    card_number '4111111111111111'
    holder_name 'Vicente Olmos'
    expiration_month '09'
    expiration_year '20'
    cvv2 '111'
    address { {
        postal_code: '76190',
        state: 'QRO',
        line1: 'LINE1',
        line2: 'LINE2',
        line3: 'LINE3',
        country_code: 'MX',
        city: 'Queretaro',
    } }
}

token=@tokens.create(token_hash)
```

```php
<?
$bancomer = Bancomer::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');
$address = array(
    'postal_code' => '76190',
    'state' => 'QRO',
    'line1' => 'LINE1',
    'line2' => 'LINE2'
    'line3' => 'LINE3',
    'country_code' => 'MX',
    'city' => 'Queretaro');

$request = array(
   	 'card_number' => 'Juan',
   	 'holder_name' => 'Vazquez Juarez',
   	 'expiration_month' => '12',
   	 'expiration_year' => '22',
   	 'cvv2' => '111',
   	 'address' => $address);

$token = bancomer->tokens->create($request);
?>
```

> Response example

```json
{
   "id":"k1n0mscnjwhxqia8q7cm",
   "card":{
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "address":{
         "line1":"Av 5 de Febrero",
         "line2":"Roble 207",
         "line3":"col carrillo",
         "state":"Queretaro",
         "city":"QuerÃƒÂ©taro",
         "postal_code":"76900",
         "country_code":"MX"
      },
      "creation_date":null,
      "brand":"visa"
   }
}
```

To create a token using the API you need to send the object with the info that will be stored.  Once the token it's stored, you can't get the number and secutirty code because this information is encrypted.

###Request

Property | Description
--------- | ------
holder_name |***string*** (required) <br/>Account holder name.
card_number |***numeric*** (required) <br/>Card number between 16 to 19 digits.
cvv2 |***numeric*** (required) <br/>Security code like it appears in the back of the card.  Generally 3 digits.
expiration_month |***numeric*** (required) <br/>Expiration month, like it appears in the card.
expiration_year |***numeric*** (required) <br/>Expiration year, like it appears in the card.
address |***object*** (optional)<br/>Invoice address of the card owner.

###Response
Returs the created [token object](#token-object) or an [error response](#error-object) if an error ocurred during the creation.

##Get a Token

> Definition

```shell
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/tokens/{TOKEN_ID}
```

```java
bancomerAPI.tokens().get(String tokenId);
```

```php
<?
$token = $bancomer->tokens->get(tokenId);
?>
```

```ruby
@tokens=@bancomer.create(:tokens)
@tokens.get(token_id)
```

```csharp
bancomerAPI.TokenService.Get(String token_id);
```

> Request example

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/tokens/k1n0mscnjwhxqia8q7cm \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```java
BancomerAPI api = new BancomerAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Map tokenAsMap = api.tokens().get("tr6cxbcefzatd10guvvw");
ParameterContainer token = new ParameterContainer("token", tokenAsMap);
```

```php
<?
$bancomer = Bancomer::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$token = $bancomer->tokens->get('a9ualumwnrcxkl42l6mh');
?>
```

```ruby
@bancomer=BancomerApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@tokens=@bancomer.create(:tokens)

response_hash=@tokens.get("ag4nktpdzebjiye1tlze")
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Dictionary<String, Object> tokenDictionary = api.TokenService.Get("tr6cxbcefzatd10guvvw");
ParameterContainer token = new ParameterContainer("token", tokenDictionary);
```

> Response example

```json
{
   "id":"k1n0mscnjwhxqia8q7cm",
   "card":{
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "address":{
         "line1":"Av 5 de Febrero",
         "line2":"Roble 207",
         "line3":"col carrillo",
         "state":"Queretaro",
         "city":"QuerÃƒÂ©taro",
         "postal_code":"76900",
         "country_code":"MX"
      },
      "creation_date":null,
      "brand":"visa"
   }
}
```

Gets the token details.  The ID is required.

<aside class="notice">
**Note:** Sensible data like credit card number and security card will never be included in the response.
</aside>

###Request
Property | Description
--------- | ------
id| ***string*** (required, length = 45) <br/> Token ID

###Response
Returns a [token object](#token-object)

