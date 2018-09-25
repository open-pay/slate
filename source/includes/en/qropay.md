#Charges with Qropay
From Openpay API you can generate QR codes, con los cuales tus clientes podrán realizar pagos desde una aplicación móvil.

<aside class="notice">
Mediante el uso de este método de pago podrás recibir una notificación instantes despues de que tu cliente realice el pago.
</aside>
##Pago Pendiente

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

```

```csharp

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

Si la petición es correcta recibirás una respuesta con la información del cargo pendiente generado. La respuesta incluye una URL de la imagen PNG del código QR.

##Payment Status

Openpay ofrece la librería JavaScript https://openpay.s3.amazonaws.com/openpay-qropay.v1.js para insertar un documento HTML con el estatus del cargo con código QR vía una etiqueta iframe. Para usarla simplemente deberás importarla a tu sitio web. Hecho lo anterior podrás insertar en el body una etiqueta div en la cual se insertará un iframe que mostrará un documento HTML con el estatus del cargo.