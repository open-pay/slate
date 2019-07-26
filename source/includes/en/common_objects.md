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
id | _**string**_ <br/> Unique identifier assigned by Openpay at the moment of creation.
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
