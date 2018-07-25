#Tokens

El objetivo de generar tokens es que se capture la información de la tarjeta desde el navegador o dispositivo del usuario final para que dicha información no viaje a través de tu servidor y así puede evitar o reducir certificaciones PCI.

Para usar esta funcionalidad de la API, te recomendamos usar nuestra librería en JavaScript para cuando tu aplicación este en Web.

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
            "line3":"Queretaro",
            "state":"Queretaro",
            "city":"Queretaro",
            "postal_code":"76900",
            "country_code":"MX"
         },
         "creation_date":"2014-01-30T13:53:11-06:00",
         "brand":"visa"
      }
   }
```

Propiedad | Descripción
--------- | ------
id | ***string*** <br/>Identificador del token. Esté es el que deberás usar para posteriormente hacer un cargo.
card | ***object*** <br/>Datos de la tarjeta asociada al token. Ver [objeto tarjeta](#objeto-tarjeta)


##Crear un nuevo token

> Definición

```shell
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/tokens
```

```java
//Customer
bancomerAPI.tokens().create(String customerId, List<Parameter> request);

//Merchant
bancomerAPI.tokens().create(List<Parameter> request);
```

```csharp
//Customer
bancomerAPI.TokenService.Create(string customer_id, List<IParameter> request);

//Merchant
bancomerAPI.TokenService.Create(List<IParameter> request);
```

```ruby
#Customer
@tokens=@openpay.create(:tokens)
@tokens.create(request_hash, customer_id)

#Merchant
@tokens=@openpay.create(:tokens)
@tokens.create(request_hash)
```

```php
<?
//Customer
$customer = bancomer->customers->get(customerId);
$token = $customer->tokens->create($tokenRequest);

//Merchant
$token = $bancomer->tokens->create($tokenRequest);
?>
```

> Ejemplo de petición

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/tokens \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "card_number":"4111111111111111",
   "holder_name":"Juan Perez Ramirez",
   "expiration_year":"20",
   "expiration_month":"12",
   "cvv2":"110",
   "address":{
      "city":"Querétaro",
      "country_code":"MX",
      "postal_code":"76900",
      "line1":"Av 5 de Febrero",
      "line2":"Roble 207",
      "line3":"col carrillo",
      "state":"Queretaro"
   }
}'
```

```java
BancomerAPI api = new BancomerAPI("https://sandbox-api.openpay.mx/", "sk_08453429e4c54220a3a82ab4d974c31a", "miklpzr4nsvsucghm2qp");

List<Parameter> request = new ArrayList<Parameter>(Arrays.asList(
        new SingleParameter("card_number", "4111111111111111"),
        new SingleParameter("cvv2", "295"),
        new SingleParameter("expiration_month", "12"),
        new SingleParameter("expiration_year", "20"),
        new SingleParameter("holder_name", "Juan Perez Lopez")));

Token tokenCreated = this.api.tokens().create(request);

```
```csharp
BancomerAPI bancomerAPI = new BancomerAPI("sk_08453429e4c54220a3a82ab4d974c31a", "miklpzr4nsvsucghm2qp");

List<IParameter> request = new List<IParameter>{
    new SingleParameter("holder_nane", "Juan Perez Ramirez"),
    new SingleParameter("card_number", "4111111111111111"),
    new SingleParameter("cvv2", "022"),
    new SingleParameter("expiration_month", "12"),
    new SingleParameter("expiration_year", "20"),
};

Token tokenCreated = bancomerAPI.TokenService.Create(request);
```
```ruby
@bancomer=BancomerApi.new('mywvupjjs9xdnryxtplq', 'sk_92b25d3baec149e6b428d81abfe37006')
@tokens=@bancomer.create(:tokens)

token_hash={
    card_number '4111111111111111'
    holder_name 'Vicente Olmos'
    expiration_month '09'
    expiration_year '20'
    cvv2 '111'
    address { {
        postal_code: '76190',
        state: 'QRO',
        line1: 'LINE1',
        line2: 'LINE2',
        line3: 'LINE3',
        country_code: 'MX',
        city: 'Queretaro',
    } }
}

token=@tokens.create(token_hash)
```

```php
<?
$bancomer = Bancomer::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');
$address = array(
    'postal_code' => '76190',
    'state' => 'QRO',
    'line1' => 'LINE1',
    'line2' => 'LINE2'
    'line3' => 'LINE3',
    'country_code' => 'MX',
    'city' => 'Queretaro');

$request = array(
   	 'card_number' => 'Juan',
   	 'holder_name' => 'Vazquez Juarez',
   	 'expiration_month' => '12',
   	 'expiration_year' => '22',
   	 'cvv2' => '111',
   	 'address' => $address);

$token = bancomer->tokens->create($request);
?>
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
         "state":"Queretaro",
         "city":"Querétaro",
         "postal_code":"76900",
         "country_code":"MX"
      },
      "creation_date":null,
      "brand":"visa"
   }
}
```

Para la creación de un token es necesario enviar el objeto con la información a registrar. Una vez guardado el token no se puede obtener el número y código de seguridad ya que esta información es encriptada.

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
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/tokens/{TOKEN_ID}
```

> Ejemplo de petición

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/tokens/k1n0mscnjwhxqia8q7cm \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```java
//Token
bancomerAPI.tokens().get(String tokenId);
```

```php
<?
$token = $bancomer->tokens->get(tokenId);
?>
```

```ruby
#Token
@tokens=@bancomer.create(:tokens)
@tokens.get(token_id)
```

```csharp
bancomerAPI.TokenService.Get(String token_id);
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
         "state":"Queretaro",
         "city":"Querétaro",
         "postal_code":"76900",
         "country_code":"MX"
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
