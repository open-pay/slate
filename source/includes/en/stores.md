#Stores

The object represents a convenience store

##Store object

> Object example:

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
      "state": "BOGOTA",
      "city": "BOGOTA",
      "postal_code": "110111",
      "country_code": "CO"
    },
    "paynet_chain": {
      "name": "EXTRA",
      "logo": "http://www.openpay.mx/logotipos/extra.png",
      "thumb": "http://www.openpay.mx/thumb/extra.png",
      "max_amount": 99999.99
    }
  }
```

Property | Description
--------- | -----------
id_store|***string*** <br/>Unique identifier assigned at the time of its creation.
id|***string*** <br/>nique identifier by chain.
name|***datetime*** <br/>Store name.
last_update|***string*** <br/>Last date of update in format ISO 8601.
[geolocation](#objeto-geolocation)| ***oject*** <br/>Store geographical representation by coordinates, latitude and longitude.
[address](#objeto-dirección)|***object*** <br/>Store address.
[paynet_chain](#objeto-paynetchain)|***object*** <br/>Paynet chain to which it belongs.

##Get list of shops by location

> Definition

```shell
GET https://api.openpay.mx/stores?latitud={latitud}&longitud={longitud}&kilometers={radio}&amount={monto}
```

```php
<?
// =============================
// No implemented
// =============================
?>
```

```java
// =============================
// No implemented
// =============================
```

```csharp
// =============================
// No implemented
// =============================
```

```javascript
// =============================
// No implemented
// =============================
```

```ruby
# =============================
# No implemented
# =============================
```

> Request example

```shell
curl https://api.openpay.mx/stores?latitud=20.618975&longitud=-100.422290&kilometers=1.5&amount=4000 \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

> Response example

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
      "state": "BOGOTA",
      "city": "BOGOTA",
      "postal_code": "110111",
      "country_code": "CO"
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
      "state": "BOGOTA",
      "city": "BOGOTA",
      "postal_code": "110311",
      "country_code": "CO"
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

Gets the trade account details. Only it required to indicate the unique id of trade to be obtained.

###Resquest

Property  | Description
--------- | -----------
latitud | ***numeric*** (required) <br>Latitude of geographical location Store
longitud | ***numeric*** (required) <br>Longitud of geographical location Store
kilometers | ***numeric*** (required) <br>Radius distance in kilometers search
amount | ***numeric*** (required) <br>Purchase amount

###Response
If there are stores close range a settlement with stores found it is returned.

