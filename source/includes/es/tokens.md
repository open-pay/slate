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
POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/tokens
```

```java
//Merchant
bbvaAPI.tokens().create(List<Parameter> request);
```

```csharp
//Merchant
bbvaAPI.TokenService.Create(List<IParameter> request);
```

```ruby
#Merchant
@tokens=@bbva.create(:tokens)
@tokens.create(request_hash)
```

```php
<?
//Merchant
$token = $bbva->tokens->create($tokenRequest);
?>
```

> Ejemplo de petición

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/tokens \
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
BbvaAPI api = new BbvaAPI("https://sand-api.ecommercebbva.com/", "sk_08453429e4c54220a3a82ab4d974c31a", "miklpzr4nsvsucghm2qp");

List<Parameter> request = new ArrayList<Parameter>(Arrays.asList(
        new SingleParameter("card_number", "4111111111111111"),
        new SingleParameter("cvv2", "295"),
        new SingleParameter("expiration_month", "12"),
        new SingleParameter("expiration_year", "20"),
        new SingleParameter("holder_name", "Juan Perez Lopez")));

Map tokenAsMap = this.api.tokens().create(request);
ParameterContainer token = new ParameterContainer("token", tokenAsMap);
```
```csharp
BbvaAPI bbvaAPI = new BbvaAPI("sk_08453429e4c54220a3a82ab4d974c31a", "miklpzr4nsvsucghm2qp");

List<IParameter> request = new List<IParameter>{
    new SingleParameter("holder_nane", "Juan Perez Ramirez"),
    new SingleParameter("card_number", "4111111111111111"),
    new SingleParameter("cvv2", "022"),
    new SingleParameter("expiration_month", "12"),
    new SingleParameter("expiration_year", "20"),
};

Dictionary<String, Object> tokenDictionary = bbvaAPI.TokenService.Create(request);
ParameterContainer token = new ParameterContainer("token", tokenDictionary);
```
```ruby
@bbva=BbvaApi.new('mywvupjjs9xdnryxtplq', 'sk_92b25d3baec149e6b428d81abfe37006')
@tokens=@bbva.create(:tokens)

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
$bbva = Bbva::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');
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

$token = bbva->tokens->create($request);
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

```shell
GET https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/tokens/{TOKEN_ID}
```

```java
bbvaAPI.tokens().get(String tokenId);
```

```php
<?
$token = $bbva->tokens->get(tokenId);
?>
```

```ruby
@tokens=@bbva.create(:tokens)
@tokens.get(token_id)
```

```csharp
bbvaAPI.TokenService.Get(String token_id);
```

> Ejemplo de petición

```shell
curl https://sand-api.ecommercebbva.com/v1/mzdtln0bmtms6o3kck8f/tokens/k1n0mscnjwhxqia8q7cm \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```java
BbvaAPI api = new BbvaAPI("https://sand-api.ecommercebbva.com", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Map tokenAsMap = api.tokens().get("tr6cxbcefzatd10guvvw");
ParameterContainer token = new ParameterContainer("token", tokenAsMap);
```

```php
<?
$bbva = Bbva::getInstance('moiep6umtcnanql3jrxp', 'sk_3433941e467c1055b178ce26348b0fac');

$token = $bbva->tokens->get('a9ualumwnrcxkl42l6mh');
?>
```

```ruby
@bbva=BbvaApi.new("mzdtln0bmtms6o3kck8f","sk_e568c42a6c384b7ab02cd47d2e407cab")
@tokens=@bbva.create(:tokens)

response_hash=@tokens.get("ag4nktpdzebjiye1tlze")
```

```csharp
BbvaAPI api = new BbvaAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Dictionary<String, Object> tokenDictionary = api.TokenService.Get("tr6cxbcefzatd10guvvw");
ParameterContainer token = new ParameterContainer("token", tokenDictionary);
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
