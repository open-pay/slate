---
layout: guide
title: 3D Secure
category: card-charge
navigation_weight: 5
tags: card-charge
lang: es
---

[obtener-cargo-con-id]: https://www.openpay.mx/docs/api/#con-id-de-tarjeta-o-token
[cargo-con-3d-secure]: https://www.openpay.mx/docs/api/#con-id-de-tarjeta-o-token
[pagos-con-tarjeta]: https://www.openpay.mx/docs/api/#con-id-de-tarjeta-o-token
[error-codes]: https://www.openpay.mx/docs/errors.html
[create-token]: https://www.openpay.mx/docs/api/#tokens
[objeto-customer]: https://www.openpay.mx/docs/api/#clientes
[payment-plan]: https://www.openpay.mx/docs/api/#planes
[tests]:https://www.openpay.mx/docs/testing.html
[webhooks]:https://www.openpay.mx/docs/webhooks.html

#3D Secure

3D secure nos permite realizar cargos más seguros, ya que tu cliente deberá autenticar su identidad directamente en el sistema del banco al cual pertenece su tarjeta.

A continuación, se muestra el flujo de cómo se realizar un cargo usando 3d Secure:

<img width="760px" src="http://img.openpay.mx/3d-secure-es.png"/>

Los pasos para integrar el flujo:

1. Crear transacción 3D Secure. - Se debe crear en Openpay una transacción indicando que sea desea utilizar 3D Secure. Ver: [Cargo 3D Secure con token][cargo-con-3d-secure].
2. Envió de URL de autenticación. - La respuesta del paso 1 será la URL a la que el cliente deberá ser re-dirigido para realizar el proceso de 3D Secure.
3. Re direccionamiento a URL de autenticación. - Una vez que el comercio tenga la URL de autenticación, deberá redirigir al cliente a la misma.
4. Autenticación 3D Secure. – El cliente realiza el proceso de autenticación con el banco emisor de la tarjeta.
5. Respuesta de autenticación. – El banco emisor envía a Openpay el resultado de la autenticación del cliente.
6. Re direccionamiento a URL de respuesta. - Openpay utiliza la URL definida por el comercio en el paso 1 para redirigir al cliente, a esta URL se envía el ID de la transacción como parámetro.
7. Generación de página de respuesta. – El navegador del cliente le solicita al comercio la página de respuesta (aceptado o rechazado).
8. Confirmación de Transacción. – El comercio mediante el ID obtiene estado de la transacción y genera la página de respuesta al cliente (Aceptado o Rechazado). Ver: [Obtener un cargo con ID][obtener-cargo-con-id]

Crear transacción 3D Secure con Token
------------------------------

> Ejemplo de petición:

```json 
{
  "method": "card",
  "amount": 6000.00,
  "description": " Cargo 3D Secure ",
  "order_id": "000000004",
  "source_id": "token1",
  "redirect_url":"http://www.openpay.mx/index.html",
  "use_3d_secure": "true"
}
```

Para utilizar este servicio se debe tener un Token, el cual puede ser obtenido de las siguientes maneras:

1. Token de cargo previo. – Si previamente se realizó un intento de cobro a la tarjeta siguiendo la guía de [Pagos con tarjeta][pagos-con-tarjeta] y el resultado fue un [código de error 3005 (Rechazo por riesgo)][error-codes], se puede usar el mismo token creado para 3D Secure.
2. Creación de nuevo Token. – Si no se cuenta con un token previo, se debe utilizar el [servicio de creación de token][create-token] para crea uno.

Una vez que tengas un token este deberá ser usado la propiedad source_id.

Propiedad                   |Tipo                              |Descripción
----------------------------|----------------------------------|-----------------
method                      |String (Requerido)                |Debe contener el valor card para indica que el cargo se hará de una tarjeta.
source_id                   |String (Requerido, longitud = 45) |ID de la tarjeta guardada o el id del token creado de donde se retirarán los fondos.
amount                      |Numeric (Requerido)               |Cantidad del cargo. Debe ser una cantidad mayor a cero, con hasta dos dígitos decimales.
currency                    |String (Opcional)                 |Tipo de moneda del cargo. Por el momento solo se soportan 2 tipos de monedas: Pesos Mexicanos(MXN) y Dólares Americanos(USD).
description                 |String (Requerido, longitud = 250)|Una descripción asociada al cargo.
order_id                    |String (Opcional, longitud = 100) |Identificador único del cargo. Debe ser único entre todas las transacciones.
[customer][objeto-customer] |Objeto (Opcional)                 |Información del cliente al que se le realiza el cargo. Ver objeto [Customer][objeto-customer].
[payment_plan][payment-plan]|Objeto (Opcional)                 |Datos del plan de meses sin intereses que se desea utilizar en el cargo. Ver Objeto [PaymentPlan][payment-plan].
metadata                    |List(key, value) (opcional)       |Listado de campos personalizados de antifraude, estos campos deben de apegarse a las reglas para creación de campos personalizados de antifraude.
use_3d_secure               |Boolean (requerido)               |Se debe especificar este parámetro en true manejar 3D Secure.
redirect_url                |String (opcional)                 |Indica la URL a la que se debe redireccionar después del resultado de autenticación 3D Secure.



Envío de URL de autenticación
------------------------------

> Ejemplo de petición:

```json 
{
  "id": "treqwygvw0hrjuvwbsf5",
  "authorization": "treqwygvw0hrjuvwbsf5",
  "operation_type": "in",
  "method": "card",
  "transaction_type": "charge",
  "card": {
  "type": "credit",
  "brand": "mastercard",
  "address": null,
  "card_number": "549138XXXXXX5100",
  "holder_name": "Heber Lazcano",
  "expiration_year": "20",
  "expiration_month": "12",
  "allows_charges": true,
  "allows_payouts": false,
  "bank_name": "Banamex",
  "bank_code": "002"
},
  "status": "charge_pending",
  "conciliated": true,
  "creation_date": "2017-03-17T20:52:47-06:00",
  "operation_date": "2017-03-17T20:52:51-06:00",
  "description": "Cargo 3D Secure",
  "error_message": null,
  "order_id": "000000004",
  "amount": 6,
  "payment_method": {
  "type": "redirect",
  "url": "https://api.openpay.mx/v1/mbgaszoxwqews3geshez/charges/treqwygvw0hrjuvwbsf5/redirect/"
},
"currency": "MXN" }
```

La respuesta a la petición de creación de cargo será un JSON con la información de la transacción a pagar por el usuario. Se debe poner especial atención en los siguientes parámetros:

<strong>Id</strong>. – ID único de la transacción creada, debe ser almacenado ya que será por medio de este ID que se envíe la respuesta una vez que el usuario realice la autenticación 3D Secure.

<strong>payment_method.url</strong>. – URL a donde se debe redirigir al usuario para iniciar el proceso.


Re direccionamiento a URL de respuesta
------------------------------

Una vez completa la autenticación del usuario en el sistema 3D Secure y recibida la respuesta en Openpay, se re-direccionará al usuario a la URL definida en el paso 1 (redirect_url) usando el ID de la transacción que se envió en el paso 2.

Ejemplo:

http://www.openpay.mx/index.html?id=treqwygvw0hrjuvwbsf5

 **Notas:**

 * Puedes simular diferentes resultados usando las tarjetas de [Pruebas][tests]
 * Implementa las [Notificaciones][webhooks] para conocer el estado de los pagos en tiempo real
