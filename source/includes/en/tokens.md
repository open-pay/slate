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
          "line3":"Bogota",
          "state":"Bogota",
          "city":"Bogota",
          "postal_code":"110511",
          "country_code":"CO"
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

```
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/tokens
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/tokens \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "card_number":"4111111111111111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "cvv2":"110",
   "address":{
      "city":"QuerÃƒÂ©taro",
      "country_code":"CO",
      "postal_code":"110511",
      "line1":"Av 5 de Febrero",
      "line2":"Roble 207",
      "line3":"col carrillo",
      "state":"Bogota"
   }
}' 
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
         "state":"Bogota",
         "city":"QuerÃƒÂ©taro",
         "postal_code":"110511",
         "country_code":"CO"
      },
      "creation_date":null,
      "brand":"visa"
   }
}
```

To create a token using Openpay you need to send the object with the info that will be stored.  Once the token it's stored, you can't get the number and secutirty code because this information is encrypted.

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

```
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/tokens/{TOKEN_ID}
```

> Request example

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/tokens/k1n0mscnjwhxqia8q7cm \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
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
         "state":"Bogota",
         "city":"QuerÃƒÂ©taro",
         "postal_code":"110511",
         "country_code":"CO"
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

