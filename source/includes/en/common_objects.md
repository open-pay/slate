#Common Objects

Information for objects shared in request and response.

##Transaction Object

> Object example:

```json
{
    "id": "tryqbk08mmjihwejd3si",
    "authorization": "faa33f71-f122-4efc-9",
    "operation_type": "in",
    "method": "bank_account",
    "transaction_type": "charge",
    "status": "completed",
    "conciliated": true,
    "creation_date": "2018-10-19T11:14:33-05:00",
    "operation_date": "2018-10-19T11:14:45-05:00",
    "description": "1 Calzado M",
    "error_message": null,
    "order_id": "161951571501672795",
    "customer_id": "azxhcjwagajxtfciuytw",
    "due_date": "2019-10-18T11:34:33-05:00",
    "amount": 54627.00,
    "currency": "COP",
    "payment_method": {
        "type": "redirect",
        "url": "https://myecommerce.co/shopping-cart/"
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
amount| ***numeric*** <br/>Transaction full amount.
description|***string*** <br/>Transaction description.
error_message| ***string*** <br/>If the transaction is in *failed* status, this field will include the error message.
customer_id| ***string*** <br/>Unique identifier for the customer who this transaction belongs.  If the value is null the transaction belongs to Merchant account.
currency| ***string*** <br/>Currency used in the operation by default is COP (Colombia pesos).
bank_account| ***object*** <br/>Bank account data used for the transaction.  See the *BankAccount* object.
card| ***object*** <br/>Credit card data used in the transaction.  See the *Card* object.


## Address Object

> Object example:

```json
{
   "department":"Medellín",
   "city":"Antioquia",
   "additional":"Avenida 7g bis #229-32 Apartamento 511"
}
```

Property | Description
--------- | -----------
department | ***string*** (required) <br/>Departament.
city | ***string*** (required) <br/>City.
additional | ***string*** (required) <br/>Additional information to specify the address data.


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
