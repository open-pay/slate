# Authentication

> Authentication example

```shell
curl https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges \
   -u sk_326c6d0443f6457aae29ffbd48f7d1be:

The -u parameter is responsible for the HTTP basic authentication (adding two points after the private key prevents the use of password)
```

```php
<?
//Sandbox is used by default
$bancomer = Bancomer::getInstance('mptdggroasfcmqs8plpy', 'sk_326c6d0443f6457aae29ffbd48f7d1be');
?>
```

```java
//Sandbox
final BancomerAPI api = new BancomerAPI("https://sand-api.ecommercebbva.com", "mptdggroasfcmqs8plpy", "sk_326c6d0443f6457aae29ffbd48f7d1be");

//Production
final BancomerAPI api = new BancomerAPI("https://api.ecommercebbva.com", "mptdggroasfcmqs8plpy", "sk_326c6d0443f6457aae29ffbd48f7d1be");
```

```csharp
//Sandbox
BancomerAPI bancomerAPI = new Bancomer("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
bancomerAPI.Production = false; // Default value = false

//Produtcion
BancomerAPI bancomerAPI = new Bancomer("sk_326c6d0443f6457aae29ffbd48f7d1be", "mptdggroasfcmqs8plpy");
bancomerAPI.Production = true;
```

```ruby
#Sandbox
bancomer=BancomerApi.new("mptdggroasfcmqs8plpy","sk_326c6d0443f6457aae29ffbd48f7d1be")

#Production
bancomer=BancomerApi.new("mptdggroasfcmqs8plpy","sk_326c6d0443f6457aae29ffbd48f7d1be", true)


#Define the timeout for the requests
#This cllient uses a default 90 secs timeout. In order to configure the timeout used to create request to the BBVA services, you need to clearly define the kind of environment, followed by the new timeout value for the request:

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

To make requests to the BBVA API, is necessary to send the API Key on all your calls to our servers. You can get the key from the [dashboard](https://sand-portal.ecommercebbva.com/login).

API key:

* **Private.-**
For calls between servers and full access to all API operations (should never be shared).

<aside class="warning">
Keep this key safe and never share it to anyone.
</aside>

For API authentication you must use the [basic access authentication](https://en.wikipedia.org/wiki/Basic_access_authentication), where the API key is the username. The password is not required and it should be left blank for purposes of simplicity

<aside class="notice">
For security reasons, all requests must be through **HTTPS**.
</aside>
