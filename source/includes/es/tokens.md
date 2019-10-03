#Tokens

El objetivo de generar tokens es que se capture la información de la tarjeta desde el navegador o dispositivo del usuario final para que dicha información no viaje a través de tu servidor y así puede evitar o reducir certificaciones PCI.

Para usar esta funcionalidad de la API, te recomendamos usar nuestra librería en JavaScript para cuando tu aplicación este en Web y nuestros SDK's de Android o iOS para cuando este en móvil.

**Características**

* Se crean a nivel comercio
* No se ligan a ningún cliente
* Después de crearse solo se puede usar una sola vez, para hacer un cargo con token

##Objeto Token

> Ejemplo de objeto 

```json
{
      "id":"tokfa4swch8gr4icy2ma",
      "card":{
         "card_number":"1111",
         "holder_name":"Juan Perez Ramirez",
         "expiration_year":"20",
         "expiration_month":"04",
         "address":{
            "line1":"Av 5 de febrero",
            "line2":"Roble 207",
            "line3":"Bogota",
            "state":"Bogota",
            "city":"Bogota",
            "postal_code":"110511",
            "country_code":"CO"
         },
         "creation_date":"2014-01-30T13:53:11-06:00",
         "brand":"visa",
         "points_card":false
      }
   }
```

Propiedad | Descripción
--------- | ------
id | ***string*** <br/>Identificador del token. Esté es el que deberás usar para posteriormente hacer un cargo.
card | ***object*** <br/>Datos de la tarjeta asociada al token. Ver [objeto tarjeta](#objeto-tarjeta)


##Crear un nuevo token

> Definición

```
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/tokens
```

> Ejemplo de petición 

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/tokens \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "card_number":"4111111111111111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "cvv2":"110",
   "address":{
      "city":"Bogotá",
      "country_code":"CO",
      "postal_code":"110511",
      "line1":"Av 5 de Febrero",
      "line2":"Roble 207",
      "line3":"col carrillo",
      "state":"Bogota"
   }
}' 
```

> Ejemplo de respuesta

```json
{
   "id":"k1n0mscnjwhxqia8q7cm",
   "card":{
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "address":{
         "line1":"Av 5 de Febrero",
         "line2":"Roble 207",
         "line3":"col carrillo",
         "state":"Bogota",
         "city":"Bogotá",
         "postal_code":"110511",
         "country_code":"CO"
      },
      "creation_date":null,
      "brand":"visa"
   }
}
```

Para la creación de un token en Openpay es necesario enviar el objeto con la información a registrar. Una vez guardado el token no se puede obtener el número y código de seguridad ya que esta información es encriptada.

###Petición

Propiedad | Descripción
--------- | ------
holder_name |***string*** (requerido) <br/>Nombre del tarjeta habiente.
card_number |***numeric*** (requerido) <br/>Numero de tarjeta puede ser de 16 o 19 dígitos.
cvv2 |***numeric*** (requerido) <br/>Código de seguridad como aparece en la parte de atrás de la tarjeta. Generalmente 3 dígitos.
expiration_month |***numeric*** (requerido) <br/>Mes de expiración tal como aparece en la tarjeta.
expiration_year |***numeric*** (requerido) <br/>Año de expiración tal como aparece en la tarjeta.
address |***object*** (opcional)<br/>Dirección de facturación del tarjeta habiente.

###Repuesta
Regresa el [objeto token](#objeto-token) creado o una [respuesta de error](#objeto-error) si ocurrió algún problema en la creación.


##Obtener un token

> Definición

```
GET https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/tokens/{TOKEN_ID}
```

> Ejemplo de petición 

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/tokens/k1n0mscnjwhxqia8q7cm \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
``` 

> Ejemplo de respuesta

```json
{
   "id":"k1n0mscnjwhxqia8q7cm",
   "card":{
      "card_number":"411111XXXXXX1111",
      "holder_name":"Juan Perez Ramirez",
      "expiration_year":"20",
      "expiration_month":"12",
      "address":{
         "line1":"Av 5 de Febrero",
         "line2":"Roble 207",
         "line3":"col carrillo",
         "state":"Bogota",
         "city":"Bogotá",
         "postal_code":"110511",
         "country_code":"CO"
      },
      "creation_date":null,
      "brand":"visa"
   }
}
```

Obtiene los detalles de un token. Es necesario tener el id. 

<aside class="notice">
**Nota:** Nunca se regresarán datos sensibles como son el código de seguridad y del número de tarjeta.
</aside>

###Petición
Propiedad | Descripción
--------- | ------
id| ***string*** (requerido, longitud = 45) <br/> Identificador de token.

###Respuesta
Regresa un [objeto token](#objeto-token)

