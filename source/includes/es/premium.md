---
layout: guide
title: Cargo con token
category: card-charge
navigation_weight: 1
tags: card-charge
lang: es
---


[openpayjs]: /docs/openpayjs.html
[fraud-tool]: /docs/fraud-tool.html
[sandbox-register]: https://sandbox-dashboard.openpay.mx/merchant/register
[libraries]: /integracion.html
[html-code]: https://s3.amazonaws.com/openpay-code-examples/new_charge_with_card.html
[formulario-tarjeta]: http://public.openpay.mx/Formulario_Tarjeta.zip
[errors]: errors.html
[tests]:https://www.openpay.mx/docs/testing.html
[webhooks]:https://www.openpay.mx/docs/webhooks.html
[versions]: versions.html


# Premium


Esta es una guía rápida del flujo de operación y descripción de cada  punto con el fin de acompañar el desarrollo de los comercios.
Recomendamos ampliamente  leer las especificaciones de integración de  manera detallada antes de comenzar a desarrollar.


##Cargo con tarjeta tokenizada



A todos nos gusta recibir pagos, es por ello empezaremos con un guía para ver la forma de hacerlo.

Esta guía hace uso de la librería de [Openpay.js][openpayjs], para enviar la información de la tarjeta directamente a Openpay. Usando esta librería aparte de ser la forma más sencilla de guardar una tarjeta permite minimizar el alcance de una certificación PCI Compliance.

###Flujo para realizar cargos a tarjeta###

  <img src="https://public.openpay.mx/images/Cargo_con_tarjetas.png" alt="drawing" width="700"/>
  
  
Pasos:

1. [Implementación del sistema antifraude][fraud-tool] generando un "device_session_id"
2. Tokenización de la tarjeta de crédito o débito usando la librería [Openpay.js][openpayjs]
3. Toda la información de la compra se envía a tu servidor
4. Desde tu servidor se crea el cargo en Openpay
5. Openpay envía la instrucción de cargo al banco emisor y regresa la respuesta


Creación del formulario
--------------------------------
>  Código del formulario.

```html
<form action="#" method="POST" id="payment-form">
    <input type="hidden" name="token_id" id="token_id">
    <input type="hidden" name="use_card_points" id="use_card_points" value="false">
    <div class="pymnt-itm card active">
        <h2>Tarjeta de crédito o débito</h2>
        <div class="pymnt-cntnt">
            <div class="card-expl">
                <div class="credit"><h4>Tarjetas de crédito</h4></div>
                <div class="debit"><h4>Tarjetas de débito</h4></div>
            </div>
            <div class="sctn-row">
                <div class="sctn-col l">
                    <label>Nombre del titular</label><input type="text" placeholder="Como aparece en la tarjeta" autocomplete="off" data-openpay-card="holder_name">
                </div>
                <div class="sctn-col">
                    <label>Número de tarjeta</label><input type="text" autocomplete="off" data-openpay-card="card_number"></div>
                </div>
                <div class="sctn-row">
                    <div class="sctn-col l">
                        <label>Fecha de expiración</label>
                        <div class="sctn-col half l"><input type="text" placeholder="Mes" data-openpay-card="expiration_month"></div>
                        <div class="sctn-col half l"><input type="text" placeholder="Año" data-openpay-card="expiration_year"></div>
                    </div>
                    <div class="sctn-col cvv"><label>Código de seguridad</label>
                        <div class="sctn-col half l"><input type="text" placeholder="3 dígitos" autocomplete="off" data-openpay-card="cvv2"></div>
                    </div>
                </div>
                <div class="openpay"><div class="logo">Transacciones realizadas vía:</div>
                <div class="shield">Tus pagos se realizan de forma segura con encriptación de 256 bits</div>
            </div>
            <div class="sctn-row">
                    <a class="button rght" id="pay-button">Pagar</a>
            </div>
        </div>
    </div>
</form>
```

Para pedirle al usuario la información de la tarjeta y poder realizar los pasos 1 y 2 es necesario tener un formulario indicándole al cliente las tarjetas soportadas y que el pago será vía Openpay.

<img src="https://public.openpay.mx/images/ejemplo_cobro_tarjeta4.png" alt="drawing" width="700"/>

El HTML completo del formulario lo puedes descargar [aquí][formulario-tarjeta]


Es muy importante que los campos en donde se va a introducir la información de la tarjeta tenga el atributo <code>data_openpay_card</code> ​ya que esto permitirá a la librería de Openpay encontrar la información.

Observa que para los datos de la tarjeta no se está ocupando el atributo <code>name</code> esto para que al momento de enviar el formulario a tu servidor los datos de la tarjeta no viajen en la petición ya que sólo los vamos a ocupar para crear el token.

En el formulario de ejemplo anterior no se incluyen los campos "amount" y "description" pero deberan incluirse al hacer el submit al servidor.


Sistema antifraude (Paso 1)
--------------------------------

> Con el siguiente código se cargan las librerías necesarios para la generación del id de dispositivo:

```html
<head>
  <script type="text/javascript"
        src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
  <script type="text/javascript"
        src="https://js.openpay.mx/openpay.v1.min.js"></script>
<script type='text/javascript'
  src="https://js.openpay.mx/openpay-data.v1.min.js"></script>
</head>
```

Con el siguiente código se inicializa el valor para el device_session_id:

```html 

<script type="text/javascript">
 $(document).ready(function() {
  OpenPay.setId('mzdtln0bmtms6o3kck8f');
  OpenPay.setApiKey('pk_f0660ad5a39f4912872e24a7a660370c');
  var deviceSessionId = OpenPay.deviceData.setup("payment-form", "deviceIdHiddenFieldName");
  });
</script>
```

El parámetro <code>payment-form</code>, recibe el id del formulario que contiene la información del cargo que se enviara a tu servidor. Indica a la librería que en ese formulario es donde se va a agregar un campo oculto con el valor del <code>device_session_id</code>.

El parámetro <code>deviceIdHiddenFieldName</code>, recibe el nombre del campo oculto donde se asignara el <code>device_session_id</code>. Este dato es importante si piensas recuperar el valor del hidden y enviar mediante un submit.

Tokenización y envío de datos (Paso 2 y 3)
--------------------------------

Una vez que tenemos nuestro formulario creado, vamos a programar que en el botón de enviar se cree un token utilizando la librería [Openpay.js][openpayjs].

> Primero agregamos al <code>head</code> el archivo de [Openpay.js][openpayjs] y de JQuery:

```html
<head>
  <script type="text/javascript"
        src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
  <script type="text/javascript"
        src="https://js.openpay.mx/openpay.v1.min.js"></script>
</head>
```


>​Luego asignamos a la librería de Openpay nuestro <code>merchant-id</code> y nuestra llave pública (<code>public-key</code>):

```html
<script type="text/javascript">
     $(document).ready(function() {
            OpenPay.setId('mzdtln0bmtms6o3kck8f');
            OpenPay.setApiKey('pk_f0660ad5a39f4912872e24a7a660370c');
            OpenPay.setSandboxMode(true);
    });
</script>
```

> Y por último atrapamos el evento de clic del botón "Pagar" para que en lugar de que haga el submit del formulario realice la función "tokenize" de la tarjeta:

```javascript
$('#pay-button').on('click', function(event) {
       event.preventDefault();
       $("#pay-button").prop( "disabled", true);
       OpenPay.token.extractFormAndCreate('payment-form', success_callbak, error_callbak);                
});
```

Como puedes ver estamos pasando como parámetro el nombre del formulario creado, esto para que la librería obtengan los datos de la tarjeta y haga la petición a Openpay.

Si todo sale bien se llamará el método ***success_callback*** en el cual asignaremos el valor id del token creado al campo <code>token_id</code> y enviaremos los datos al servidor:


```javascript
var success_callbak = function(response) {
              var token_id = response.data.id;
              $('#token_id').val(token_id);
              $('#payment-form').submit();
};
```

Si existe un problema en la llamada mostramos el error en un alert:


```javascript
var error_callbak = function(response) {
     var desc = response.data.description != undefined ?
        response.data.description : response.message;
     alert("ERROR [" + response.status + "] " + desc);
     $("#pay-button").prop("disabled", false);
};
```

<a name="puntos"><a/>
> Para mayor referencia del uso de la librería consulta la página de [Openpay.js][openpayjs]


Crear cargo (Paso 4 y 5)
--------------------------------

Ahora sólo resta hacer el cargo desde tu servidor, para esto crearemos una instancia de Openpay con el <code>merchant-id</code> y el <code>private-key</code> y luego con los valores del formulario haremos el cargo:

<div class="curl-code" style="display:none;">
```Bash
curl -u sk_e568c42a6c384b7ab02cd47d2e407cab \
-H "Content-type: application/json" \
-X POST -d '{
   "method":"card",
   "amount": {amount},
   "source_id": "{token_id}",
   "description": "{description}",
    "device_session_id":
"{device_session_id}" }' https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges
```
</div>

<div class="php-code" style="display:none;">
```php
<?php
$openpay = Openpay::getInstance('mzdtln0bmtms6o3kck8f',
  'sk_e568c42a6c384b7ab02cd47d2e407cab');

$customer = array(
     'name' => $_POST["name"],
     'last_name' => $_POST["last_name"],
     'phone_number' => $_POST["phone_number"],
     'email' => $_POST["email"],);

$chargeData = array(
    'method' => 'card',
    'source_id' => $_POST["token_id"],
    'amount' => $_POST["amount"], // formato númerico con hasta dos dígitos decimales. 
    'description' => $_POST["description"],
    'use_card_points' => $_POST["use_card_points"], // Opcional, si estamos usando puntos
    'device_session_id' => $_POST["deviceIdHiddenFieldName"],
    'customer' => $customer
    );

$charge = $openpay->charges->create($chargeData);
?>
```
</div>

<div class="java-code" style="display:none;">
```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx",
  "sk_e568c42a6c384b7ab02cd47d2e407cab", "mzdtln0bmtms6o3kck8f");

Customer customer = new Customer();
customer.setName(name);
customer.setLastName(lastName);
customer.setPhoneNumber(phoneNumber);
customer.setEmail(email);

CreateCardChargeParams charge = new CreateCardChargeParams()
                .cardId(token_id)
                .amount(amount)
                .description(description)
                .deviceSessionId(deviceSessionId)
                .customer(customer);



// Opcional, si estamos usando puntos
charge.useCardPoints(useCardPoints);

Charge charge = this.api.charges().create(charge);
```
</div>

<div class="dotnet-code" style="display:none;">
```csharp
OpenpayAPI api = new OpenpayAPI("sk_e568c42a6c384b7ab02cd47d2e407cab", "mzdtln0bmtms6o3kck8f");

Customer customer = new Customer();
customer.Name = name;
customer.LastName = lastName;
customer.PhoneNumber = phoneNumber;
customer.Email = email;

ChargeRequest request = new ChargeRequest();
request.Method = "card";
request.SourceId = tokenId;
request.Amount = new Decimal(amount);
request.Description = description;
request.DeviceSessionId = deviceSessionId;
request.Customer = customer;

// Opcional, si estamos usando puntos
request.UseCardPoints = useCardPoints;

Charge charge = api.ChargeService.Create(request);
```
</div>

<div class="nodejs-code" style="display:none;">
```javascript
var chargeRequest = {
   'source_id' : token_id,
   'method' : 'card',
   'amount' : amount,
   'description' : description,
   'device_session_id' : device_session_id,
   'customer' : {
        'name' : name,
        'last_name' : last_name,
        'phone_number' : phone_number,
        'email' : email
   }
}

// Opcional, si estamos usando puntos
chargeRequest.use_card_points = use_card_points;

openpay.customers.charges.create(chargeRequest, function(error, charge) {
  // ...
});
```
</div>

<div class="ruby-code" style="display:none;">
```ruby
@openpay=OpenpayApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@charges=@openpay.create(:charges)

customer_hash={
    "name" => name,
    "last_name" => last_name,
    "phone_number" => phone_number,
    "email" => email
}

request_hash={
    "method" => "card",
    "source_id" => token_id,
    "amount" => amount,
    "description" => description,
    "use_card_points" => use_card_points,   # Opcional, si estamos usando puntos
    "device_session_id" => device_session_id,
    "customer" => customer_hash
  }

response_hash=@charges.create(request_hash.to_hash)
```
</div>

**¡¡Listo!!** Ya tenemos un cargo creado con tarjeta.

Si existiera un error recibiriamos una excepción la cual debemos capturar y manejar, para mas información consulta la [seccion de errores][errors]


> **Notas:**
> * Los campos amount, description, etc.. que no están en el formulario de ejemplo, son datos propios de tu aplicación que deben haberse obtenido antes del formulario de pago.
> * En el campo amount, puede ser utilizado un String con formato punto decimal.
> * Si deseas ver como realizar el procedimiento en otro lenguaje consulta nuestra sección de [integración][libraries].
> * El código HTML completo se encuentra [aquí][formulario-tarjeta]. ***(La página no funciona completamente, deberás descargarla y realizar la implementación del POST en tu servidor)***.
> * Asegúrate que tu integración cumple con los requisitos de compatibilidad de versiones [más detalles][versions]
> * Puedes simular diferentes resultados usando las tarjetas de [Pruebas][tests]
> * Implementa las [Notificaciones][webhooks] para conocer el estado de los pagos en tiempo real



