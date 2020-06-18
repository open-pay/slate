---
layout: guide
title:  Redireccionamiento
category: card-charge
navigation_weight: 2
tags: card-charge
lang: es
---


[openpayjs]: /docs/openpayjs.html
[fraud-tool]: /docs/fraud-tool.html
[sandbox-register]: https://sandbox-dashboard.openpay.mx/merchant/register
[libraries]: /integracion.html
[html-code]: https://s3.amazonaws.com/openpay-code-examples/new_charge_with_card.html
[formulario-tarjeta]: https://public.openpay.mx/FormularioTarjeta.zip
[errors]: errors.html
[transaction-object]: http://www.openpay.mx/docs/api/?java#objeto-transacci-n
[tests]:https://www.openpay.mx/docs/testing.html
[webhooks]:https://www.openpay.mx/docs/webhooks.html


#Redireccionamiento

Otra forma de hacer cargos con tarjeta sin la necesidad de implementar un formulario de pago en tu sitio, es mediante la utilización de un formulario que Openpay proporciona.

Resumen de pasos:

1. Crear un cargo que contenga el atributo <b>confirm</b> en <b>false</b> y una url a la cual direccionar una vez concluido el pago.
2. En base a la respuesta del cargo creado, redirigir al usuario a la url contenida en el objeto payment_method regresado.
3. Que el cliente llene la información solicitada y realize el pago en el formulario.
4. Si el pago fué exitoso dar clic en el botón continuar.
5. El pago está hecho.

Creación del cargo
--------------------------------

> Ejemplo de creación de un cargo utilizando el formulario de pago de Openpay.


```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "method" : "card",
   "amount" : 111,
   "description" : "Cargo desde terminal virtual de 111",
   "customer" : {
        "name" : "Mario",
        "last_name" : "Benedetti Farrugia",
        "phone_number" : "1111111111",
        "email" : "mario_benedetti@miempresa.mx"
   },
   "confirm" : "false",
   "send_email":"false",
   "redirect_url":"http://www.openpay.mx/index.html"
}'
```



```php
<?php
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');
$customer = array(
     'name' => 'Mario',
     'last_name' => 'Benedetti Farrugia',
     'phone_number' => '1111111111',
     'email' => 'mario_benedetti@miempresa.mx');

$chargeRequest = array(
    "method" : "card",
    'amount' => 111,
    'description' => 'Cargo desde terminal virtual de 111',
    'customer' => $customer,
    'send_email' => false,
    'confirm' => false,
    'redirect_url' => 'http://www.openpay.mx/index.html')
;

$charge = $openpay->charges->create($chargeRequest);
?>
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx",
  "sk_e568c42a6c384b7ab02cd47d2e407cab", "mzdtln0bmtms6o3kck8f");

Customer customer = new Customer();
customer.setName("Mario");
customer.setLastName("Benedetti Farrugia");
customer.setPhoneNumber("1111111111");
customer.setEmail("mario_benedetti@miempresa.mx");

BigDecimal amount = new BigDecimal("111");
String description = "Cargo desde terminal virtual de 111";
String redirectUrl = "http://www.openpay.mx/index.html";
boolean sendEmail = false;
boolean confirm = false;

CreateCardChargeParams chargeParams = new CreateCardChargeParams()
.amount(amount)
.description(description)
.customer(customer)
.sendEmail(sendEmail)
.confirm(confirm)
.redirectUrl(redirectUrl);

Charge charge = api.charges().create(chargeParams);

```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_e568c42a6c384b7ab02cd47d2e407cab", "mzdtln0bmtms6o3kck8f");
ChargeRequest request = new ChargeRequest();
Customer customer = new Customer();
customer.Name = "Mario";
customer.LastName = "Benedetti Farrugia";
customer.PhoneNumber = "1111111111";
customer.Email = "mario_benedetti@miempresa.mx";

request.Method = "card";
request.Amount = new Decimal(111.00);
request.Description = "Cargo desde terminal virtual de 111";
request.OrderId = "oid-00051";
request.Confirm = false;
request.SendEmail = false;
request.RedirectUrl = "http://www.openpay.mx/index.html";
request.Customer = customer;

Charge charge = api.ChargeService.Create(request);
```


```javascript
var chargeRequest = {
   'method' : 'card',
   'amount' : 111,
   'description' : 'Cargo desde terminal virtual de 111',
   'customer' : {
        'name' : 'Mario',
        'last_name' : 'Benedetti Farrugia',
        'phone_number' : '1111111111',
        'email' : 'mario_benedetti@miempresa.mx'
   },
  'send_email' : false,
  'confirm' : false,
  'redirect_url' : 'http://www.openpay.mx/index.html')
}

openpay.charges.create(chargeRequest, function(error, charge) {
  // ...
});
```

```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@charges=@openpay.create(:charges)
customer_hash={
    "name" => "Mario",
    "last_name" => "Benedetti Farrugia",
    "phone_number" => "1111111111",
    "email" => "mario_benedetti@miempresa.mx"
}

request_hash={
    "method" => "card",
    "amount" => 100.00,
    "description" => "Cargo inicial a mi merchant",
    "order_id" => "oid-00051",
    "customer" => customer_hash,
    "send_email" => false,
    "confirm" => false,
    "redirect_url" => "http://www.openpay.mx/index.html"
}

response_hash=@charges.create(request_hash.to_hash)
```

Redirigir al formulario de Openpay
----------------------------------

Si la llamada es correcta entonces se regresará una respuesta con un [objeto transacción.][transaction-object] en estado pendiente representado en el lenguaje utilizado.

**Respuesta:**

```json
{
  "id": "trq7yrthx5vc4gtjdkwg",
  "authorization": null,
  "method": "card",
  "operation_type": "in",
  "transaction_type": "charge",
  "status": "charge_pending",
  "conciliated": false,
  "creation_date": "2016-09-09T18:52:02-05:00",
  "operation_date": "2016-09-09T18:52:02-05:00",
  "description": "Cargo desde terminal virtual de 111",
  "error_message": null,
  "amount": 111,
  "currency": "MXN",
  "payment_method": {
    "type": "redirect",
    ***"url": "https://sandbox-api.openpay.mx/v1/mexzhpxok3houd5lbvz1/charges/trq7yrthx5vc4gtjdkwg/card_capture"***
  },
  "customer": {
    "name": "Mario",
    "last_name": "Benedetti Farrugia",
    "email": "mario_benedetti@miempresa.mx",
    "phone_number": "1111111111",
    "creation_date": "2016-09-09T18:52:02-05:00",
    "clabe": null,
    "external_id": null
  }
}
```

Redirigir al usuario a la url contenida en el atributo url que se encuentra dentro del objeto payment_method.


<img src="https://public.openpay.mx/images/ejemplo_formulario_op.png" alt="drawing" width="700"/>

Llenar datos de pago
----------------------------------

Que el usuario llene los datos solicitados y de clic en ***Realizar Pago***


<img src="https://public.openpay.mx/images/ejemplo_formulario_op_fullData.png" alt="drawing" width="700"/>

Dar clic en Continuar
----------------------------------

Si el pago fué exitoso que el usuario de clic en ***Continuar***


<img src="https://public.openpay.mx/images/ejemplo_formulario_op_success.png" alt="drawing" width="700"/>

Esto redirecciona a la url que se proporcionó al crear el cargo (en el caso del ejemplo la página de Openpay) dando por terminado el flujo del pago.


<img src="https://public.openpay.mx/images/ejemplo_formulario_op_redirect.png" alt="drawing" width="700"/>

 **Notas:**

 * Puedes simular diferentes resultados usando las tarjetas de [Pruebas][tests]
 * Implementa las [Notificaciones][webhooks] para conocer el estado de los pagos en tiempo real
