
# Autenticación

> Ejemplo de autenticación

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:

El parámetro -u se ocupa para realizar la autenticación HTTP Basic 
(al agregar dos puntos después de la llave privada se previene el uso de contraseña)
```

```php
<?
//Por default se usa el ambiente de sandbox
$bancomer = Bancomer::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c4875b178ce26348b0fac');
?>
```

```java
//Sandbox
final BancomerAPI api = new BancomerAPI(
        "https://sandbox-api.openpay.mx", "moiep6umtcnanql3jrxp", "sk_3433941e467c4875b178ce26348b0fac");

//Produccion
final BancomerAPI api = new BancomerAPI(
        "https://api.openpay.mx", "moiep6umtcnanql3jrxp", "sk_3433941e467c4875b178ce26348b0fac");
```

```csharp
//Sandbox
BancomerAPI bancomerAPI = new BancomerAPI("sk_3433941e467c4875b178ce26348b0fac", "moiep6umtcnanql3jrxp");
bancomerAPI.Production = false; // Default value = false

//Produccion
BancomerAPI bancomerAPI = new BancomerAPI("sk_3433941e467c4875b178ce26348b0fac", "moiep6umtcnanql3jrxp");
bancomerAPI.Production = true;
```

```ruby
#Sandbox
bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")

#Produccion
bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac", true)


#Definir timeout para los request's
#Este cliente maneja un timeout por defecto de 90 seg., para configurar el timeout usado para crear los request a los 
# servicios, es necesario definir explícitamente el tipo de ambiente, seguido del nuevo valor del timeout para el request:

#Sintaxis:
#   bancomer_prod=BancomerApi.new(merchant_id,private_key,isProduction,timeout)
#Example:
#   bancomer_prod=BancomerApi.new(merchant_id,private_key,false,30)
```

> Producción

```shell
Solo es necesario usar la URI base https://api.openpay.mx
```

```php
<?
Bancomer::setProductionMode(true);
?>
```

```java
//Solo es necesario usar la URI base https://api.openpay.mx
```

```csharp
bancomerAPI.Production = true;
```

```ruby
#Solo es necesario pasar como tercer argumento un "true" cuando se crea el objeto BancomerApi
```

Para realizar peticiones a la API, es necesario enviar la llave de API (API Key) en todas tus llamadas a nuestros  servidores. ​La llave la puedes obtener desde el [dashboard](https://sandbox-bancomer.bancomer.mx/login).

Existen 2 tipos de llaves de API:

* **Privada.-**
Para llamadas entre servidores y con acceso total a todas las operaciones de la API (nunca debe ser  compartida).

<aside class="warning">
Manten esta llave segura y nunca la compartas con nadie.
</aside>

* **Pública.-**
Sólo se debe utilizar en llamadas desde JavaScript. Esta llave sólo tiene permitido realizar crear tokens

<aside class="notice">
Para hacer llamadas con tu llave pública utiliza la librería [Bancomer.js](#)
</aside>

Para la autenticación al API debes usar [autenticación de acceso básica](http://es.wikipedia.org/wiki/Autenticación_de_acceso_básica), donde la llave de API es el nombre de usuario. La contraseña no es requerida y debe dejarse en blanco por fines de simplicidad.

<aside class="notice">
Por razones de seguridad todas las peticiones deben ser vía **HTTPS**.
</aside>
