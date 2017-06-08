#Tiendas

El objeto representa una tienda de conveniencia

##Objeto Tienda

> Ejemplo de Objeto:

```json
{
    "id_store": 4913,
    "id": 115,
    "name": "0503 SAN PABLO -QRO",
    "last_update": "2016-02-04T00:52:16-06:00",
    "status": "active",
    "geolocation": {
      "lng": -100.421865,
      "lat": 20.618171,
      "place_id": "ChIJwSN2wpNa04URsDryLW517lg"
    },
    "address": {
      "line1": "AV. 5 DE FEBRERO KM 7.5 NO 1341",
      "line2": "SAN PABLO",
      "line3": null,
      "state": "QUERETARO",
      "city": "QUERETARO",
      "postal_code": "76030",
      "country_code": "MX"
    },
    "paynet_chain": {
      "name": "EXTRA",
      "logo": "http://www.openpay.mx/logotipos/extra.png",
      "thumb": "http://www.openpay.mx/thumb/extra.png",
      "max_amount": 99999.99
    }
  }
```

Propiedad | Descripción
--------- | -----------
id_store|***string*** <br/>Identificador único asignado al momento de su creación.
id|***string*** <br/>Identificador único por cadena.
name|***datetime*** <br/>Nombre de la tienda.
last_update|***string*** <br/>Fecha de la ultima actualizacion de la tienda en formato ISO 8601.
[geolocation](#objeto-geolocation)| ***objeto*** <br/Representacion geografica de la tienda por medio de coordenadas, Latitud y Longitud.
[address](#objeto-dirección)|***objeto*** <br/>Direccion de la tienda.
[paynet_chain](#objeto-paynetchain)|***objeto*** <br/>Cadena paynet a la que pertence.

##Obtener lista de tiendas por ubicación

> Definición

```shell
GET https://api.openpay.mx/stores?latitud={latitud}&longitud={longitud}&kilometers={radio}&amount={monto}
```

```php
<?
// =============================
// Funcionalidad no implementada
// =============================
?>
```

```java
// =============================
// Funcionalidad no implementada
// =============================
```

```csharp
// =============================
// Funcionalidad no implementada
// =============================
```

```javascript
// =============================
// Funcionalidad no implementada
// =============================
```

```ruby
# =============================
# Funcionalidad no implementada
# =============================
```

> Ejemplo de petición

```shell
curl https://api.openpay.mx/stores?latitud=20.618975&longitud=-100.422290&kilometers=1.5&amount=4000 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

> Ejemplo de respuesta

```json
[
  {
    "id_store": 4913,
    "id": 115,
    "name": "0503 SAN PABLO -QRO",
    "last_update": "2016-02-04T00:52:16-06:00",
    "status": "active",
    "geolocation": {
      "lng": -100.421865,
      "lat": 20.618171,
      "place_id": "ChIJwSN2wpNa04URsDryLW517lg"
    },
    "address": {
      "line1": "AV. 5 DE FEBRERO KM 7.5 NO 1341",
      "line2": "SAN PABLO",
      "line3": null,
      "state": "QUERETARO",
      "city": "QUERETARO",
      "postal_code": "76030",
      "country_code": "MX"
    },
    "paynet_chain": {
      "name": "EXTRA",
      "logo": "http://www.openpay.mx/logotipos/extra.png",
      "thumb": "http://www.openpay.mx/thumb/extra.png",
      "max_amount": 99999.99
    }
  },
  {
    "id_store": 4726,
    "id": 68,
    "name": "ASTURIANO TECNOLOGICO",
    "last_update": "2016-02-04T00:52:16-06:00",
    "status": "active",
    "geolocation": {
      "lng": -100.410136,
      "lat": 20.61632,
      "place_id": "EktQcm9sIFRlY25vbMOzZ2ljbyBOdGUgOTk5LCBTYW4gUGFibG8sIFNhbnRpYWdvIGRlIFF1ZXLDqXRhcm8sIFFyby4sIE3DqXhpY28"
    },
    "address": {
      "line1": "PROLONGACION TECNOLOGICO NORTE #999",
      "line2": "SAN PABLO",
      "line3": null,
      "state": "QUERETARO",
      "city": "QUERETARO",
      "postal_code": "76159",
      "country_code": "MX"
    },
    "paynet_chain": {
      "name": "EL ASTURIANO",
      "logo": "http://www.openpay.mx/logotipos/asturiano.png",
      "thumb": "http://www.openpay.mx/thumb/asturiano.png",
      "max_amount": 99999.99
    }
  }
]
```

Obtiene los detalles la cuenta del comercio. Solo se requiere indicar el id unico del comercio que se quiere obtener.

###Petición

Propiedad     | Descripción
--------- | -----------
latitud | ***numeric*** (requerido) <br>Latitud de la ubicacion geografica de la tienda 
longitud | ***numeric*** (requerido) <br>Longitud de la ubicacion geografica de la tienda 
kilometers | ***numeric*** (requerido) <br>Distancia del radio de la busqueda en kilometros
amount | ***numeric*** (requerido) <br>Monto de la compra

###Respuesta
Si se encuentran tiendas cerca del rango se devolverá un arreglo con las tiendas encontradas.

