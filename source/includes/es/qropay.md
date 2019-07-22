#Pagos con Qropay
Desde la API se pueden generar códigos QR, con los cuales tus clientes podrán realizar pagos desde una aplicación móvil.

<aside class="notice">
Mediante el uso de este método de pago podrás recibir una notificación instantes despues de que tu cliente realice el pago.
</aside>

***Flujo para realizar cargos con Qropay***</br> 
<img src="https://www.openpay.mx/img/cargo_por_qropay.png">

***Pasos***</br> 
1. Al realizar una compra desde tu sitio web se muestran los distintos medios de pago, entre ellos se ofrece pagar por medio de Qropay.<br/>
2. El cliente selecciona Qropay como medio de pago.<br/>
3. Desde tu servidor se lanza una petición al API para crear un cargo pendiente.<br/>
4. Nuestro servidor creará el cargo pendiente y responderá con los datos del mismo junto con una URL del código QR en formato PNG.<br/>
5. Se ofrece un documento HTML que puede ser incrustado en tu sitio web para monitorear el estatus del cargo con este medio de pago.<br/>
6. El cliente realiza el pago desde la aplicación móvil para Qropay.<br/>
7. Se valida y recibe el pago<br/>
8. Se notifica la recepción del pago a tu servidor<br/>

<aside class="notice">
El código QR estará disponible mientras no se exceda su tiempo de expiración.
</aside>

##Crear cargo pendiente

> Definición

```plaintext--endpoints
Comercio
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges

Cliente
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

> Ejemplo de petición con cliente

```shell
curl -u sk_e568c42a6c384b7ab02cd47d2e407cab \
-H "Content-type: application/json" \
-X POST -d '{
   "method" : "qropay",
   "amount" : 949.00,
   "description" : "Cargo qropay"
}' https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/charges
```

```php
$bbva = Bbva::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');
$chargeRequest = array(
    'method' => 'qropay',
    'amount' => 100,
    'description' => 'Cargo qropay');

$charge = $bbva->charges->create($chargeRequest);
?>
```

```java
BbvaAPI api = new BbvaAPI(
        "https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

List<Parameter> request = new ArrayList<Parameter>(Arrays.asList(
    new SingleParameter("method", "qropay"),
    new SingleParameter("amount", "949.00"),
    new SingleParameter("description", "Cargo qropay")
));

Map chargeAsMap = api.charges().create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```csharp
BbvaAPI api = new BbvaAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

List<IParameter> request = List<IParameter> {
    new SingleParameter("method", "qropay"),
    new SingleParameter("amount", "949.00"),
    new SingleParameter("description", "Cargo qropay")
};

Dictionary<String, Object> chargeDictionary = bbvaAPI.ChargeService.Create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```ruby
@bbva=BbvaApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bbva.create(:charges)

request_hash={
    "method" => "qropay",
    "amount" => 100.00,
    "description" => "Cargo qropay"
}

response_hash=@charges.create(request_hash.to_hash)
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
        "qr_code": "https://sand-api.ecommercebbva.com/qropay/mc2mzbvwpmnps8q0on6q/trfu5m6xzn6hiyn9jkzm/qrcode"
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

Para poder recibir un pago desde un dispositivo móvil con un código QR es necesario realizar una llamada a nuestra API indicando en el campo `method` el tipo `​qropay`.
<br/>
Si la petición es correcta recibirás una respuesta con la información del cargo pendiente generado. La respuesta incluye una URL de la imagen PNG del código QR.


###Petición

Propiedad | Descripción
--------- | -----
method | ***string*** (requerido) <br/>Debe contener el valor qropay para indicar que el pago se hará con codigo QR.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al cargo.

###Respuesta

Regresa un [objeto de transacción](#objeto-transacci-n) con la información del cargo o una [respuesta de error](#objeto-error).

##Estado del Pago

> Ejemplo

```html
<!DOCTYPE html>
<html>
    <head>
    ...
        <script type="text/javascript" src="https://openpay.s3.amazonaws.com/openpay-qropay.v1.js"></script>
    ...
        <script type="text/javascript">
            //merchantId    = Tu id de comerciante
            //transactionId = Valor del campo id del objeto transacción regresado al crearse el cargo pendiente
            function showIframeQR(merchantId, transactionId) {
                QroPay.setSandboxMode(true);  // Omitir línea si se desea lanzar la petición al ambiente productivo
                QroPay.setupIframe("iframeQR", merchantId, transactionId);
            }
        </script>
    </head>
    <body>
    ...
        <div id="iframeQR" />
    ...
    </body>
</html>
```

Se ofrece la librería JavaScript [qropay](https://openpay.s3.amazonaws.com/openpay-qropay.v1.js) para insertar un documento HTML con el estatus del cargo con código QR vía una etiqueta `iframe`. Para usarla simplemente deberás importarla a tu sitio web. Hecho lo anterior podrás insertar en el `body` una etiqueta `div` en la cual se insertará un `iframe que mostrará un documento HTML con el estatus del cargo.

***Ejemplo del iframe con el estatus del cargo:***</br> 
<img src="https://www.openpay.mx/img/qropay/charge_completed.gif">
