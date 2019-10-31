
#Errores

Openpay regresa objetos de JSON en las respuestas del servicio, incluso en caso de errores por lo que cuando exista un error.

##Objeto Error

> Ejemplo de objeto

```json
{
    "category" : "request",
    "description" : "The customer with id 'm4hqp35pswl02mmc567' does not exist",
    "http_code" : 404,
    "error_code" : 1005,
    "request_id" : "1981cdb8-19cb-4bad-8256-e95d58bc035c",
    "fraud_rules": [
        "Billing <> BIN Country for VISA/MC"
    ]
}
```

```shell

```

```php

```

```java
//Para el caso de java, toda operación regresara una instancia de la clase "OpenpayServiceException" la cual contendrá esta información del error.
```

```csharp
//Para el caso de C Sharp, toda operación regresará una instancia de la clase "OpenpayException" la cual contendrá esta información del error.
```

```javascript

```

```ruby
#Para el caso de Ruby, toda operación puede regresar cualquiera de las siguientes excepciones:

# => OpenpayException: Para errores genericos, como acceso a recursos invalidos, etc.
# => OpenpayConnectionException: Para errores relacionados con problemas en la conexión al servidor.
# => OpenpayTransactionException: Para errores relacionados durante la ejecución de las operaciones.
```

Propiedad | Descripción
--------- | -----
category    |***string*** <br/>**request:** Indica un error causado por datos enviados por el cliente. Por ejemplo, una petición inválida, un intento de una transacción sin fondos. <br/><br/>**internal:** Indica un error del lado de Openpay, y ocurrira muy raramente. <br/><br/>**gateway:** Indica un error durante la transacción de los fondos de una tarjeta a la cuenta de Openpay o de la cuenta hacia un banco o tarjeta.
error_code  |***numeric*** <br/>El código del error de Openpay indicando el problema que ocurrió.
description |***string*** <br/>Descripción del error.
http_code   |***string*** <br/>Código de error HTTP de la respuesta.
request_id  |***string*** <br/>Identificador de la petición.
fraud_rules  |***array*** <br/> Arreglo con la lista de coincidencia de reglas definidas para deteccion de fraudes.

##Códigos de error

###Generales
Código    | Error HTTP  |Causa
--------- | ----------- | --------
1000  |500 Internal Server Error  |Ocurrió un error interno en el servidor de Openpay
1001  |400 Bad Request   |El formato de la petición no es JSON, los campos no tienen el formato correcto, o la petición no tiene campos que son requeridos.
1002  |401 Unauthorized  |La llamada no esta autenticada o la autenticación es incorrecta.
1003  |422 Unprocessable Entity  |La operación no se pudo completar por que el valor de uno o más de los parametros no es correcto.
1004  |503 Service Unavailable |Un servicio necesario para el procesamiento de la transacción no se encuentra disponible.
1005  |404 Not Found | Uno de los recursos requeridos no existe.
1006  |409 Conflict  | Ya existe una transacción con el mismo ID de orden.
1007  |402 Payment Required | La transferencia de fondos entre una cuenta de banco o tarjeta y la cuenta de Openpay no fue aceptada.
1008  |423 Locked | Una de las cuentas requeridas en la petición se encuentra desactivada.
1009  |413 Request Entity too large  | El cuerpo de la petición es demasiado grande.
1010  |403 Forbidden  |Se esta utilizando la llave pública para hacer una llamada que requiere la llave privada, o bien, se esta usando la llave privada desde JavaScript.

###Almacenamiento

Código    | Error HTTP  |Causa
--------- | ----------- | --------
2002  |409 Conflict | La tarjeta con este número ya se encuentra registrada en el cliente.
2003  |409 Conflict | El cliente con este identificador externo (External ID) ya existe.
2004  |422 Unprocessable Entity | El dígito verificador del número de tarjeta es inválido de acuerdo al algoritmo Luhn.
2005  |400 Bad Request | La fecha de expiración de la tarjeta es anterior a la fecha actual.
2006  |400 Bad Request | El código de seguridad de la tarjeta (CVV2) no fue proporcionado.
2007  |412 Precondition Failed | El número de tarjeta es de prueba, solamente puede usarse en Sandbox.
2009  |412 Precondition Failed | El código de seguridad de la tarjeta (CVV2) no es valido.

###Tarjetas
Código    | Error HTTP  |Causa
--------- | ----------- | --------
3001  |402 Payment Required | La tarjeta fue declinada.
3002  |402 Payment Required | La tarjeta ha expirado.
3003  |402 Payment Required | La tarjeta no tiene fondos suficientes.
3004  |402 Payment Required | La tarjeta ha sido identificada como una tarjeta robada.
3005  |402 Payment Required | La tarjeta ha sido identificada como una tarjeta fraudulenta.
3006  |412 Precondition Failed | La operación no esta permitida para este cliente o esta transacción.
3008  |412 Precondition Failed | La tarjeta no es soportada en transacciones en linea.
3009  |402 Payment Required | La tarjeta fue reportada como perdida.
3010  |402 Payment Required | El banco ha restringido la tarjeta.
3011  |402 Payment Required | El banco ha solicitado que la tarjeta sea retenida. Contacte al banco.
3012  |412 Precondition Failed | Se requiere solicitar al banco autorización para realizar este pago.

###Cuentas
Código    | Error HTTP  |Causa
--------- | ----------- | --------
4001  |412 Preconditon Failed | La cuenta de Openpay no tiene fondos suficientes.
