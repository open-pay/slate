
# Autenticación

> Ejemplo de autenticación

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be:

El parámetro -u se ocupa para realizar la autenticación HTTP Basic 
(al agregar dos puntos después de la llave privada se previene el uso de contraseña)
```

```php
<?
//Por default se usa el ambiente de sandbox
$bbva = Bbva::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');
?>
```

```java
//Sandbox
final BbvaAPI api = new BbvaAPI(
        "https://sand-api.ecommercebbva.com", "mptdggroasfcmqs8plpy", "sk_326c6d0443f6457aae29ffbd48f7d1be");

//Produccion
final BbvaAPI api = new BbvaAPI(
        "https://api.ecommercebbva.com", "mptdggroasfcmqs8plpy", "sk_326c6d0443f6457aae29ffbd48f7d1be");
```

```csharp
//Sandbox
BbvaAPI bbvaAPI = new BbvaAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
bbvaAPI.Production = false; // Default value = false

//Produccion
BbvaAPI bbvaAPI = new BbvaAPI("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
bbvaAPI.Production = true;
```

```ruby
#Sandbox
bbva=BbvaApi.new("mptdggroasfcmqs8plpy","sk_326c6d0443f6457aae29ffbd48f7d1be")

#Produccion
bbva=BbvaApi.new("mptdggroasfcmqs8plpy","sk_326c6d0443f6457aae29ffbd48f7d1be", true)


#Definir timeout para los request's
#Este cliente maneja un timeout por defecto de 90 seg., para configurar el timeout usado para crear los request a los 
# servicios, es necesario definir explícitamente el tipo de ambiente, seguido del nuevo valor del timeout para el request:

#Sintaxis:
#   bbva_prod=BbvaApi.new(merchant_id,private_key,isProduction,timeout)
#Example:
#   bbva_prod=BbvaApi.new(merchant_id,private_key,false,30)
```

> Producción

```shell
Solo es necesario usar la URI base https://api.ecommercebbva.com
```

```php
<?
Bbva::setProductionMode(true);
?>
```

```java
//Solo es necesario usar la URI base https://api.ecommercebbva.com
```

```csharp
bbvaAPI.Production = true;
```

```ruby
#Solo es necesario pasar como tercer argumento un "true" cuando se crea el objeto BbvaApi
```

Para realizar peticiones a la API, es necesario enviar la llave de API (API Key) en todas tus llamadas a nuestros  servidores. ​La llave la puedes obtener desde el [dashboard](https://sand-portal.ecommercebbva.com/login).

Llave de API:

* **Privada.-**
Para llamadas entre servidores y con acceso total a todas las operaciones de la API (nunca debe ser  compartida).

<aside class="warning">
Manten esta llave segura y nunca la compartas con nadie.
</aside>

Para la autenticación al API debes usar [autenticación de acceso básica](http://es.wikipedia.org/wiki/Autenticación_de_acceso_básica), donde el nombre de usuario es la llave de API. La contraseña no es requerida y debe dejarse en blanco por fines de simplicidad.

<aside class="notice">
Por razones de seguridad todas las peticiones deben ser vía **HTTPS**.
</aside>
