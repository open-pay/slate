#Pagos con Qropay
Desde la API de Openpay se pueden generar códigos QR, con los cuales tus clientes podrán realizar pagos desde una aplicación móvil.

<aside class="notice">
Mediante el uso de este método de pago podrás recibir una notificación instantes despues de que tu cliente realice el pago.
</aside>
##Crear cargo pendiente

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Cliente
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

> Ejemplo de petición con cliente

```shell
curl -u sk_e568c42a6c384b7ab02cd47d2e407cab \
-H "Content-type: application/json" \
-X POST -d '{
   "method" : "qropay",
   "amount" : 949.00,
   "description" : "Cargo qropay"
}' https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges
```

```php

```

```java
BancomerAPI api = new BancomerAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

List<Parameter> request = new ArrayList<Parameter>(Arrays.asList(
    new SingleParameter("method", "qropay"),
    new SingleParameter("amount", "949.00"),
    new SingleParameter("description", "Cargo qropay")
));

Map chargeAsMap = api.charges().create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

List<IParameter> request = List<IParameter> {
    new SingleParameter("method", "qropay"),
    new SingleParameter("amount", "949.00"),
    new SingleParameter("description", "Cargo qropay")
};

Dictionary<String, Object> chargeDictionary = bancomerAPI.ChargeService.Create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```ruby

```
> Ejemplo de respuesta

```json
{
    "id": "trfu5m6xzn6hiyn9jkzm",
    "authorization": null,
    "operation_type": "in",
    "method": "qropay",
    "transaction_type": "charge",
    "status": "charge_pending",
    "conciliated": false,
    "creation_date": "2018-04-25T18:45:16-05:00",
    "operation_date": "2018-04-25T18:45:16-05:00",
    "description": "Cargo qropay",
    "error_message": null,
    "order_id": null,
    "due_date": "2018-04-26T23:59:59-05:00",
    "payment_method": {
        "type": "qropay",
        "qr_code": "https://sandbox-api.openpay.mx/qropay/mc2mzbvwpmnps8q0on6q/trfu5m6xzn6hiyn9jkzm/qrcode"
    },
    "amount": 949,
    "currency": "MXN",
    "fee": {
        "amount": 11.49,
        "tax": 0,
        "currency": "MXN"
    }
}
```

Para poder recibir un pago desde un dispositivo móvil con un código QR es necesario realizar una llamada a nuestra API indicando en el campo method el tipo ​qropay.
<br/>
Si la petición es correcta recibirás una respuesta con la información del cargo pendiente generado. La respuesta incluye una URL de la imagen PNG del código QR.


###Petición

Propiedad | Descripción
--------- | -----
method | ***string*** (requerido) <br/>Debe contener el valor qropay para indicar que el pago se hará con codigo QR.
amount | ***numeric*** (requerido) <br/>Debe contener el valor qropay para indicar que el pago se hará con codigo QR.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.

###Respuesta
Regresa un objeto de transacción con la información del cargo o una respuesta de error.

##Estado del Pago

Openpay ofrece la librería JavaScript https://openpay.s3.amazonaws.com/openpay-qropay.v1.js para insertar un documento HTML con el estatus del cargo con código QR vía una etiqueta iframe. Para usarla simplemente deberás importarla a tu sitio web. Hecho lo anterior podrás insertar en el body una etiqueta div en la cual se insertará un iframe que mostrará un documento HTML con el estatus del cargo.