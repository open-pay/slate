# Authentication

> Authentication example

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:

The -u parameter is responsible for the HTTP basic authentication (adding two points after the private key prevents the use of password)
```

```php
<? 
//Sandbox is used by default 
$bancomer = Bancomer::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c4875b178ce26348b0fac'); 
?>
```

```java
//Sandbox
final BancomerAPI api = new BancomerAPI("https://sand-api.ecommercebbva.com", "moiep6umtcnanql3jrxp", "sk_3433941e467c4875b178ce26348b0fac");

//Production
final BancomerAPI api = new BancomerAPI("https://api.ecommercebbva.com", "moiep6umtcnanql3jrxp", "sk_3433941e467c4875b178ce26348b0fac");
```

```csharp
//Sandbox
BancomerAPI bancomerAPI = new Bancomer("sk_3433941e467c4875b178ce26348b0fac", "moiep6umtcnanql3jrxp");
bancomerAPI.Production = false; // Default value = false

//Produtcion
BancomerAPI bancomerAPI = new Bancomer("sk_3433941e467c4875b178ce26348b0fac", "moiep6umtcnanql3jrxp");
bancomerAPI.Production = true;
```

```ruby
#Sandbox
bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")

#Production
bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac", true)


#Define the timeout for the requests
#This cllient uses a default 90 secs timeout. In order to configure the timeout used to create request to the bancomer services, you need to clearly define the kind of environment, followed by the new timeout value for the request:

#Syntax:
#   bancomer_prod=BancomerApi.new(merchant_id,private_key,isProduction,timeout)
#Example:
#   bancomer_prod=BancomerApi.new(merchant_id,private_key,false,30)
```

> Production 

```shell
You only need to use the URI base https://api.ecommercebbva.com
```

```php
<? 
Bancomer::setProductionMode(true); 
?>
```

```java
//You only need to use the URI base https://api.ecommercebbva.com
```

```csharp
bancomerAPI.Production = true;
```

```ruby
#You only need to pass a "true" value as the third argument when creating the BancomerApi object. 
```

To make requests to the Bancomer API, is necessary to send the API Key on all your calls to our servers. You can get the key from the [dashboard](https://sand-portal.ecommercebbva.com/login).

There are 2 types of API keys:

* **Private.-** 
For calls between servers and full access to all API operations (should never be shared).

<aside class="warning">
Keep this key safe and never share it to anyone.
</aside>

* **Public.-**
should only be used in JavaScript calls. This key is only allowed to create cards or create tokens.

<aside class="notice">
To make calls with your public key use the [Bancomer.js] library(#)
</aside>

For API authentication you must use the [basic access authentication]http://es.wikipedia.org/wiki/Autenticación_de_acceso_básica), where the API key is the username. The password is not required and it should be left blank for purposes of simplicity

<aside class="notice">
For security reasons, all requests must be through **HTTPS**.
</aside>
