#Objetos Comunes

Información de objetos compartidos en peticiones y respuestas.

##Objeto Transacción

> Ejemplo de Objeto:

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

Propiedad | Descripción
--------- | -----------
id | _**string**_ <br/> Identificador único asignado por Openpay al momento de su creación.
authorization | ***string*** <br/>Número de autorización generado por el procesador.
transaction_type| ***string*** <br/>Tipo de transacción que fue creada: fee, charge, payout, transfer.
operation_type| ***string*** <br/>Tipo de afectación en la cuenta: in, out.
method| ***string*** <br/>Tipo de método usado en la transacción: card, bank o customer.
creation_date| ***datetime***  <br/>Fecha de creación de la transacción en formato ISO 8601.
order_id| ***string*** <br/>Referencia única o número de orden/transacción.
status| ***string*** <br/>Estatus actual de la transacción. Posibles valores: completed, in_progress, failed.
amount| ***numeric*** <br/>Cantidad de la transacción a dos decimales.
description|***string*** <br/>Descripción de la transacción.
error_message| ***string*** <br/>Si la transacción está en status: failed, en este campo se mostrará la razón del fallo.
customer_id| ***string*** <br/>Identificar único del cliente al cual pertence la transacción. Si es valor es nulo, la transacción pertenece a la cuenta del comercio.
currency| ***string*** <br/>Moneda usada en la operación, por default es COP.
bank_account| ***objeto*** <br/>Datos de la cuenta bancaria usada en la transacción. Ver objeto BankAccoount
card| ***objeto*** <br/>Datos de la tarjeta usada en la transacción. Ver objeto Card

##Objeto Dirección

> Ejemplo de Objeto:

```json
{
   "department":"Medellín",
   "city":"Antioquia",
   "additional":"Avenida 7g bis #229-32 Apartamento 511"
}
```

Propiedad | Descripción
--------- | -----------
department | ***string*** (requerido) <br/>Departamento.
city | ***string*** (requerid) <br/>Ciudad.
additional | ***string*** (requerido) <br/>Información adicional para especificar la dirección.


##Objeto Transaction Status

Value | Description
--------- | -----------
IN_PROGRESS | Transacción en proceso
COMPLETED | Transacción ejecutadá correctamente
REFUNDED | Transacción reembolsada
CHARGEBACK_PENDING | Transacción con contracargo pendiente
CHARGEBACK_ACCEPTED | Transacción con contracargo aceptado
CHARGEBACK_ADJUSTMENT | Transacción con ajuste de contracargo
CHARGE_PENDING | Transacción de cargo que no ha sido pagada
CANCELLED | Transacción de cargo que no fue pagada y se ha cancelado
FAILED | Transacción que se intentó pagar pero ocurrió algún error
