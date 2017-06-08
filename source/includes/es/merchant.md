
#Comercio

El objeto comercio permite consultar la información de tu cuenta a través de la API.

##Objeto Comercio

> Ejemplo de Objeto:

```json
{ 
   "id": "m9lrykwsmljagrfb38rs", 
   "creationDate": "2013-11-13T16:58:40-06:00", 
   "name": "Promociones en linea", 
   "email": "contacto@enlinea.com.mx", 
   "phone": "(321) 222-2222", 
   "status": "active", 
   "balance": 1000, 
   "clabe": "646180109400000542" 
} 
```

Propiedad | Descripción
--------- | -----------
id|***string*** <br/>Identificador único asignado al momento de su creación.
creation_date|***datetime*** <br/>Fecha de creación de la transacción en formato ISO 8601.
name|***string*** <br/>Nombre del comercio con el que se registró el comercio.
email|***string*** <br/>Cuenta de correo electrónico registrada para el comercio.
phone|***string*** <br/>Número teléfonico registrado del comercio.
status| ***string*** <br/>Estatus de la cuenta del Comercio puede ser active o deleted. Si la cuenta se encuentra en estatus deleted no se permite realizar ninguna transacción.
balance| ***numeric*** <br/>Saldo en la cuenta con dos decimales.
clabe | ***numeric***   <br/>Cuenta CLABE asociada con la que puede recibir fondos realizando una transferencia desde cualquier banco en México vía SPEI.

##Obtener un comercio

> Definición

```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}
```

```php
<?
// =============================
// Funcionalidad no implementada
// =============================
?>
```

```java
openpayAPI.merchant().get();
```

```csharp
// =============================
// Funcionalidad no implementada
// =============================
```

```javascript
openpay.merchant.get(callback);
```

```ruby
# =============================
# Funcionalidad no implementada
# =============================
```

> Ejemplo de petición

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Merchant merchant = api.merchant().get();
```

```javascript
openpay.merchant.get(function(error, merchant){
  // ...
});
```

> Ejemplo de respuesta

```json
{
   "name":"Demo Openpay",
   "email":"demo@openpay.mx",
   "phone":"(442) 258-1039",
   "status":"active",
   "balance":218.73,
   "clabe":"646180109400135624",
   "id":"mzdtln0bmtms6o3kck8f",
   "creation_date":"2014-01-23T10:45:53-06:00"
}
```

Obtiene los detalles la cuenta del comercio. Solo se requiere indicar el id unico del comercio que se quiere obtener.

###Petición

Propiedad     | Descripción
--------- | -----------
id | ***string*** (requerido, longitud = 45) <br>identificador único del comercio.

###Respuesta
Si el identificador es correcto regresa un objeto comercio.