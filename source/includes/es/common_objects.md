#Objetos Comunes

Información de objetos compartidos en peticiones y respuestas.

##Objeto Transacción

> Ejemplo de Objeto:

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
   "description":"Pago de ganancias",
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
currency| ***string*** <br/>Moneda usada en la operación, por default es MXN.
bank_account| ***objeto*** <br/>Datos de la cuenta bancaria usada en la transacción. Ver objeto BankAccoount
card| ***objeto*** <br/>Datos de la tarjeta usada en la transacción. Ver objeto Card
card_points| ***objeto*** <br/>Datos de los puntos de la tarjeta usados para el pago, si fueron utilizados. Ver [objeto CardPoints](#objeto-cardpoints)

##Objeto Dirección

> Ejemplo de Objeto:

```json
{
   "line1":"Av 5 de Febrero",
   "line2":"Roble 207",
   "line3":"col carrillo",
   "state":"Queretaro",
   "city":"Querétaro",
   "postal_code":"76900",
   "country_code":"MX"
}
```

Propiedad | Descripción
--------- | -----------
line1 | ***string*** (requerido) <br/>Primera línea de dirección del tarjeta habiente. Usada comúnmente para indicar la calle y número exterior e interior.
line2 | ***string*** <br/>Segunda línea de la dirección del tarjeta habiente. Usada comúnmente para indicar condominio, suite o delegación.
line3 | ***string*** <br/>Tercer línea de la dirección del tarjeta habiente. Usada comúnmente para indicar la colonia.
postal_code | ***string*** (requerido) <br/>Código postal del tarjeta habiente
state | ***string*** (requerido) <br/>Estado del tarjeta habiente
city | ***string*** (requerido) <br/>Ciudad del tarjeta habiente
country_code | ***string*** (requerido) <br/>Código del país del tarjeta habiente a dos caracteres en formato ISO_3166-1


##Objeto PaymentPlan

> Ejemplo de Objeto:

```json
{
   "payments":"6",
   "payments_type": "WITH_INTEREST",
   "deferred_months": "3"
}
```

Propiedad | Descripción
--------- | -----------
payments | ***numeric*** <br/> Es el número de pagos en los cuales se pretende realizar un cargo a meses con/sin intereses (3, 6, 9, 12, 18).
payments_type | ***string*** <br/> Indica el tipo de pagos:  <br/>***WITHOUT_INTEREST*** (meses ***sin*** intereses)  <br/>***WITH_INTEREST*** (meses ***con*** intereses)  
deferred_months | ***numeric*** <br/> Indica la cantidad de meses que será diferido el pago inicial (1,2,3,6).
##Objeto CardPoints

> Ejemplo de Objeto:

```json
{
    "used": 134,
    "remaining": 300,
    "caption": "TRANSACCION APROBADA. ME OBLIGO EN LOS TERMINOS Y CONDICIONES DEL PROGRAMA RECOMPENSAS SANTANDER. PARA CUALQUIER DUDA O ACLARACION LLAME AL 01800 RECOMPE (73-266-73).",
    "amount": 10
}
```

Propiedad | Descripción
--------- | -----------
used | ***numeric*** <br/> Cantidad de puntos usados para realizar este pago.
remaining | ***numeric*** <br/> Cantidad de puntos restantes en la tarjeta después de realizar el pago.
amount | ***numeric*** <br/>Monto de la transacción que fue pagado mediante puntos.
caption | ***string*** (opcional) <br/> Mensaje a mostrar al cliente en su recibo o ticket de compra.


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
