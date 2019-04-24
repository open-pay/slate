#Common Objects

Information for objects shared in request and response.

##Transaction Object

> Object example:

```json
{
   "id":"trehwr2zarltvae56vxl",
   "authorization":null,
   "transaction_type":"payout",
   "operation_type":"out",
   "currency":"MXN",
   "method":"bank",
   "creation_date":"2013-11-14T18:29:35-06:00",
   "order_id":"000001",
   "status":"in_progress",
   "amount":500,
   "description":"Winning payments",
   "error_message":null,
   "customer_id":"afk4csrazjp1udezj1po",
   "bank_account":{
      "rfc":ONE316015PM1,
      "mobile":null,
      "alias":null,
      "bank_name":"BANCOMER",
      "creation_date":"2013-11-14T18:29:34-06:00",
      "clabe":"012XXXXXXXXXX24616",
      "holder_name":"Juan Tapia Trejo",
      "bank_code":"012"
   }
}
```

Property | Description
--------- | -----------
id | _**string**_ <br/> Unique identifier assigned by Bancomer at the moment of creation.
authorization | ***string*** <br/>Authorization number created by the processor entity.
transaction_type| ***string*** <br/>Transaction type: fee, charge, payout, transfer.
operation_type| ***string*** <br/>Operation type in the account: in, out.
method| ***string*** <br/>Transaction method type: card, bank o customer.
creation_date| ***datetime***  <br/>Transaction creation date in ISO 8601 format.
order_id| ***string*** <br/>Unique transaction and reference number.
status| ***string*** <br/>Current transaction status.  Possible values: completed, in_progress, failed.
amount| ***numeric*** <br/>Transaction full amount, including two decimal places.
description|***string*** <br/>Transaction description.
error_message| ***string*** <br/>If the transaction is in *failed* status, this field will include the error message.
customer_id| ***string*** <br/>Unique identifier for the customer who this transaction belongs.  If the value is null the transaction belongs to Merchant account.
currency| ***string*** <br/>Currency used in the operation by default is MXN (Mexican pesos).
bank_account| ***object*** <br/>Bank account data used for the transaction.  See the *BankAccount* object.
card| ***object*** <br/>Credit card data used in the transaction.  See the *Card* object.
card_points| ***object*** <br/>Contains information about the reward points used for payment, if they were used. See the [CardPoints object](#cardpoints-object) 

## Address Object

> Object example:

```json
{
   "line1":"Av 5 de Febrero",
   "line2":"Roble 207",
   "line3":"col carrillo",
   "state":"Queretaro",
   "city":"QuerÃ©taro",
   "postal_code":"76900",
   "country_code":"MX" 
}
```

Property | Description
--------- | -----------
line1 | ***string*** (required) <br/>The first line is the card owner address. It's commonly used to indicate street address and number.
line2 | ***string*** <br/>Second addres line, commonly use to indicate interior number, suite number  or county.
line3 | ***string*** <br/>Third address line, commonly use to to indicate the neighborhood.
postal_code | ***string*** (required) <br/>Zip code
state | ***string*** (required) <br/>State
city | ***string*** (required) <br/>City
country_code | ***string*** (required) <br/>Country code, in the two character format: ISO_3166-1.

##PaymentPlan Object

> Object example:

```json
{
   "payments":"6"
}
```

Property | Description
--------- | -----------
payments | ***numeric*** <br/> Plan data months without interest is desired as use in the charge (3, 6, 9, 12, 18).

##Cardpoints Object

> Object example:

```json
{
    "used": 134,
    "remaining": 300,
    "caption": "TRANSACCION APROBADA. ME OBLIGO EN LOS TERMINOS Y CONDICIONES DEL PROGRAMA RECOMPENSAS SANTANDER. PARA CUALQUIER DUDA O ACLARACION LLAME AL 01800 RECOMPE (73-266-73).",
    "amount": 10
}
```

Property | Description
--------- | -----------
used | ***numeric*** <br/> Amount of points used in the payment.
remaining | ***numeric*** <br/> Amount of points remaining in the card after the payment.
amount | ***numeric*** <br/>Transaction amount paid using points.
caption | ***string*** (opcional) <br/> A message to be shown to the customer in their ticket or receipt.

##Object PaynetChain

> Object example:

```json
{
      "name": "EXTRA",
      "logo": "http://www.bancomer.mx/logotipos/extra.png",
      "thumb": "http://www.bancomer.mx/thumb/extra.png",
      "max_amount": 99999.99
}
```

Property | Description
--------- | -----------
name | ***string*** <br/> Chain name.
logo | ***string*** <br/> URL logo image chain.
thumb | ***string*** <br/> URL thumbnail image chain.
max_amount | ***numeric*** <br/>Maximum payment amount that accept chain stores

##Object Transaction Status

Value | Description
--------- | -----------
IN_PROGRESS| Transaction is in progress
COMPLETED| Transaction was succesfully completed
REFUNDED| Transaction that has been refunded
CHARGEBACK_PENDING| Transaction that has a pending chargeback
CHARGEBACK_ACCEPTED| Transaction that has an accepted chargeback
CHARGEBACK_ADJUSTMENT| Transaction that has an ajust for chargeback
CHARGE_PENDING| Transaction that is waiting to be paid 
CANCELLED| Transaction that was not paid and has been cancelled
FAILED| Transaction that was paid but ocurred an error

##Customer object

> Ejemplo de Objeto:

```json
{
   "id":"cz4nkhrlcu9k7qd4lwqx",
   "creation_date":"2013-11-08T12:04:46-06:00",
   "name":"Rodrigo",
   "last_name":"Velazco Perez",
   "email":"rodrigo.velazco@payments.com", 
   "phone_number":"4425667045",
   "external_id":"cliente1",
   "status":"active",
   "balance":103,
   "address":{
      "line1":"Av. 5 de febrero No. 1080 int Roble 207",
      "line2":"Carrillo puerto",
      "line3":"Zona industrial carrillo puerto",
      "postal_code":"06500",
      "state":"Querétaro",
      "city":"Querétaro",
      "country_code":"MX"
   },
   "store": {
       "reference": "OPENPAY02DQ35YOY7",
       "barcode_url": "https://sandbox-api.openpay.mx/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false"
   },
   "clabe": "646180109400423323"
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
clabe         |***numeric*** <br/>CLABE account used to receive funds by transfer from any bank in Mexico.
[address](#addres-object) |***object*** <br/>Address of the customer. It is usually used as shipping address.
[store](#store-object) |_*object**_ <br/>Contains reference string to go to Store and make deposits, the url to generate barcode is contained too.

##Card Object

> Object example 

```json
{
   "type":"debit",
   "brand":"mastercard",
   "address":{
      "line1":"Av 5 de Febrero",
      "line2":"Roble 207",
      "line3":"col carrillo",
      "state":"Queretaro",
      "city":"Querétaro",
      "postal_code":"76900",
      "country_code":"MX"
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
   "customer_id":"a2b79p8xmzeyvmolqfja",
   "points_card":true
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
[address](#address-object) |***object*** <br/>Billing address of cardholder.
allows_charges |***boolean*** <br/>It allows to know if you can make charges to the card.
allows_payouts |***boolean*** <br/>It allows to know if you can send payments to the card. 
brand |***string*** <br/>Card brand: visa, mastercard, carnet or american express.
type |***string*** <br/>Card Type: debit, credit, cash, etc.
bank_name |***string*** <br/>Name of the issuing bank.
bank_code |***string*** <br/>Code of the issuing bank.
customer_id |***string*** <br/>Customer identifier to which the card belongs. If the card is at Merchant level this value is null.
points_card |***boolean*** <br/>Indicates whether the card allows the use of reward points.
