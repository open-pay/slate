# Authentication

> Authentication example

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln0bmtms6o3kck8f/charges \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:

The -u parameter is responsible for the HTTP basic authentication (adding two points after the private key prevents the use of password)
```

```php
<?
//Sandbox is used by default
$openpay = Openpay::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c4875b178ce26348b0fac');
?>
```

```java
//Sandbox
final OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.co", "moiep6umtcnanql3jrxp", "sk_3433941e467c4875b178ce26348b0fac");

//Production
final OpenpayAPI api = new OpenpayAPI("https://api.openpay.co", "moiep6umtcnanql3jrxp", "sk_3433941e467c4875b178ce26348b0fac");
```

```javascript
var Openpay = require('openpay');
var openpay = new Openpay('moiep6umtcnanql3jrxp','sk_3433941e467c4875b178ce26348b0fac');
```

```csharp
//Sandbox
OpenpayAPI openpayAPI = new OpenpayAPI("sk_3433941e467c4875b178ce26348b0fac", "moiep6umtcnanql3jrxp");
openpayAPI.Production = false; // Default value = false

//Produtcion
OpenpayAPI openpayAPI = new OpenpayAPI("sk_3433941e467c4875b178ce26348b0fac", "moiep6umtcnanql3jrxp");
openpayAPI.Production = true;
```

```ruby
#Sandbox
openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")

#Production
openpay=OpenpayApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac", true)


#Define the timeout for the requests
#This cllient uses a default 90 secs timeout. In order to configure the timeout used to create request to the openpay services, you need to clearly define the kind of environment, followed by the new timeout value for the request:

#Syntax:
#   openpay_prod=OpenpayApi.new(merchant_id,private_key,isProduction,timeout)
#Example:
#   openpay_prod=OpenpayApi.new(merchant_id,private_key,false,30)
```

> Production

```shell
You only need to use the URI base https://api.openpay.co
```

```php
<?
Openpay::setProductionMode(true);
?>
```

```java
//You only need to use the URI base https://api.openpay.co
```

```csharp
openpayAPI.Production = true;
```

```javascript
openpay.setProductionReady(true);
```

```ruby
#You only need to pass a "true" value as the third argument when creating the OpenpayApi object.
```

To make requests to the Openpay API, is necessary to send the API Key on all your calls to our servers. You can get the key from the [dashboard](https://sandbox-dashboard.openpay.co).

There are 2 types of API keys:

* **Private.-**
For calls between servers and full access to all API operations (should never be shared).

<aside class="warning">
Keep this key safe and never share it to anyone.
</aside>

* **Public.-**
should only be used in JavaScript calls. This key is only allowed to create cards or create tokens.

<aside class="notice">
To make calls with your public key use the <a href="https://github.com/open-pay/openpay-js">Openpay.js</a> library(#)
</aside>

For API authentication you must use the [basic access authentication]http://es.wikipedia.org/wiki/Autenticación_de_acceso_básica), where the API key is the username. The password is not required and it should be left blank for purposes of simplicity

<aside class="notice">
For security reasons, all requests must be through **HTTPS**.
</aside>
