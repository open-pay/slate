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
customer_id| ***string*** <br/>Identificardor único del cliente al cual pertence la transacción. Si el valor es nulo, la transacción pertenece a la cuenta del comercio.
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

##Objeto Store

> Ejemplo de Objeto:

```json
{
   "reference":"OPENPAY02DQ35YOY7",
   "barcode_url":"https://sandbox-api.openpay.mx/barcode/OPENPAY02DQ35YOY7?width=1&height=45&text=false",
   "paybin_reference":"0101990000001065",
   "barcode_paybin_url":"https://sandbox-api.openpay.mx/barcode/0101990000001065?width=1&height=45&text=false"
}
```

Propiedad           | Descripción
---------           | -----------
reference           | ***string*** <br/>Es la referencia con la que se puede ir a la tienda y realizar depósitos a la cuenta de Openpay.
barcode_url         | ***string*** <br/>Es la url con la cual se puede obtener el codigo de barras de la referencia.
paybin_reference   | ***string*** <br/>Es la referencia con la que se puede ir a cualquier tienda que acepte Paybin.
barcode_paybin_url | ***string*** <br/>Es la url con la cual se puede obtener el codigo de barras de la referencia Paybin.


##Objeto PaymentPlan

> Ejemplo de Objeto:

```json
{
   "payments":"6"
}
```

Propiedad | Descripción
--------- | -----------
payments | ***numeric*** <br/> Es el número de pagos en los cuales se pretende realizar un cargo a meses sin intereses (3, 6, 9, 12, 18).


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

##Objeto Geolocation

> Ejemplo de Objeto:

```json
{
  "lng": -100.421865,
  "lat": 20.618171,
  "place_id": "ChIJwSN2wpNa04URsDryLW517lg"
}
```

Propiedad | Descripción
--------- | -----------
lng | ***numeric*** <br/> Longitud, coordenada geográfica.
lat | ***numeric*** <br/> Latitud, coordenada geográfica.
place_id | ***string*** <br/>Identificacdor único en google maps

##Objeto PaynetChain

> Ejemplo de Objeto:

```json
{
      "name": "EXTRA",
      "logo": "http://www.openpay.mx/logotipos/extra.png",
      "thumb": "http://www.openpay.mx/thumb/extra.png",
      "max_amount": 99999.99
    }
```

Propiedad | Descripción
--------- | -----------
name | ***string*** <br/> Nombre de la cadena.
logo | ***string*** <br/> Url de la imagen del logotipo de la cadena.
thumb | ***string*** <br/> Url de la imagen miniatura del logotipo de la cadena.
max_amount | ***numeric*** <br/>Monto máximo de pago que aceptan las tiendas de la cadena

##Objeto Transaction Status

Value | Description
--------- | -----------
IN_PROGRESS | Transacción en proceso
COMPLETED | Transacción ejecutada correctamente
REFUNDED | Transacción reembolsada
CHARGEBACK_PENDING | Transacción con contracargo pendiente
CHARGEBACK_ACCEPTED | Transacción con contracargo aceptado
CHARGEBACK_ADJUSTMENT | Transacción con ajuste de contracargo
CHARGE_PENDING | Transacción de cargo que no ha sido pagada 
CANCELLED | Transacción de cargo que no fue pagada y se ha cancelado
FAILED | Transacción que se intentó pagar pero ocurrió algún error

