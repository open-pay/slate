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
