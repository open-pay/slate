#PSE
Los cargos a cuentas de banco se pueden realizar por medio de PSE.
Al crear un pago PSE se genera una url para continuar el flujo de pago.

Se requiere la información de un cliente, o puede usarse el id de un cliente existente.

##Con nuevo cliente, ó id de cliente existente

> Definición

```shell
Comercio
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/pse

Cliente
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/pse
```

```php
<?
Comercio
$openpay->pses->create($pseRequest);

Cliente
$customer = $openpay->customers->get($customerId);
$customer->pses->create($pseRequest);
?>
```

```java



```

```javascript



```

```csharp
//Cliente
openpayAPI.PseService.Create(string customer_id, PseRequest request);

//Comercio
openpayAPI.PseService.Create(PseRequest request);
```

```ruby



```

> Ejemplo de petición con comercio

```shell
curl https://sandbox-api.openpay.co/v1/mzdtln3bqtms6o3kck2f/charges \
   -u sk_e562c42a6q384b2ab02cd47d2n301uwk: \
   -H "Content-type: application/json" \
   -X POST -d '{
   "country" : "COL",
   "amount" : 716,
   "currency" : "COP",
   "description" : "Cargo inicial a mi cuenta",
   "order_id" : "oid-12524",
   "iva" : "190",
   "customer" : {
        "name" : "Cliente Colombia",
        "last_name" : "Vazquez Juarez",
        "email" : "juan.vazquez@empresa.co",
        "phone_number" : "4448936475",
        "requires_account" : false,
        "customer_address" : {
        	"department" : "Medellín",
        	"city" : "Antioquía",
        	"additional" : "Avenida 7m bis #174-25 Apartamento 637"
        }
   }
}'
```

```php
<?
$openpay = Openpay::getInstance('mzdtln3bqtms6o3kck2f', 'sk_e562c42a6q384b2ab02cd47d2n301uwk');
$customer = array(
    'name' => 'Pedro',
    'last_name' => 'Gutierrez',
    'email' => 'pedro.gutierrez@company.co',
    'phone_number' => '571983873875',
    'requires_account' => false,
    'customer_address' => array(
        'department' => 'Medellín',
        'city' => 'Antioquia',
        'additional' => 'Avenida 7r bis #144-28 Apartamento 423'
    )
);

$pseRequest = array(
    'country' => 'COL',
    'amount' => 10000,
    'currency' => 'COP',
    'description' => 'pago pse',
    'order_id' => 'oid-12524',
    'iva' => '190',
    'customer' => $customer
);

$pse = $openpay->pses->create($pseRequest);
?>
```

```java



```

```csharp
OpenpayAPI api = new OpenpayAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

Customer customer = new Customer();
customer.Name = "Juan";
customer.LastName = "Vazquez Perez";
customer.PhoneNumber = "571627926831";
customer.Email = "juan.vazquez@empresa.co";

Address address = new Address();
address.Department = "Medellín";
address.City = "Antioquia";
address.Additional = "Avenida 18e bis #17-28 Apartamento 451";

customer.Address = address;

PseRequest request = new PseRequest();
request.Customer = customer;
request.Country = "COL";
request.Description = "Pago PSE";
request.Amount = 10000;
request.Iva = "190";
request.Currency = "COP";
request.OrderId = "oid-00051";

Pse pse = openpayAPI.PseService.Create(request);
```

```javascript



```

```ruby



```

> Ejemplo de respuesta

```json
{
	"redirect_url":"https://sandbox-api.openpay.mx/v1/maonhzpqm8xp2ydssovf/customers/ah8tdi7gr9zll6ejijuu/checkouts/ckqtz7smmjffvc4jgfko/pse"
}
```

En la respuesta que contiene el campo <code>redirect_url</code>, se continúa el flujo para realizar el pago PSE.

<aside class="notice">
Puedes realizar el pago con la cuenta del comercio o la cuenta de un cliente. </br>
</aside>

***Sistema antifraude personalizado***</br>
Es posible enviar información adicional a la plataforma Openpay para incrementar su base de conocimientos, esto le permitirá aplicar reglas personalizadas de acuerdo al giro del comercio y de manera oportuna, con el propósito de detectar con la mayor efectividad posible los intentos de fraude.

<aside class="notice">
Para utilizar esta característica es necesario enviar como parte del contenido, la propiedad <code>metadata</code>, el cual contendrá un listado de campos personalizados de antrifraude, con la información propia del comercio que se desea tomar en cuenta al momento de validar y aplicar un pago. Póngase en contacto con el departamento de soporte de Openpay para habilitar esta funcion. </br>
</aside>


###Petición

Propiedad | Descripción
--------- | -----
country|***string*** (requerido) <br/>Debe contener el valor **COL** para indicar que el país es Colombia.
amount | ***numeric*** (requerido) <br/>Cantidad del cargo. Debe ser una cantidad con valor entero mayor a cero.
currency | ***string*** (requerido) <br/>Tipo de moneda del pago. Por el momento solo se soportan 1 tipo de moneda: Pesos Colombianos(COP).
iva | ***string*** (requerido) <br/>Debe contener el valor de IVA, es campo solo informativo, no tiene ningún efecto sobre el campo amount.
description | ***string*** (requerido, longitud = 250) <br/>Una descripción asociada al pago.
order_id | ***string*** (opcional, longitud = 100) <br/>Identificador único del pago. Debe ser único entre todos los pagos.
[customer](#crear-un-nuevo-cliente)|***objeto*** (requerido) <br/>Información del cliente al que se le realiza el pago. Se puede ocupar los mismos parámetros usados en la creación de un cliente pero no se creará una cuenta al cliente. <br/><br/> **Nota:** Este parámetro solo se puede utilizar creando el pago a nivel comercio<br/><br/>Si desea crear un cliente y llevar un historial de sus pagos consulte como [crear un cliente](#crear-un-nuevo-cliente) y realice el pago a nivel cliente.
metadata |  ***list(key, value)*** (opcional) <br/>Listado de campos personalizados de antifraude, estos campos deben de apegarse a las [reglas para creación de campos personalizados de antifraude](#reglas-para-creación-de-campos-personalizados-de-antifraude)


###Respuesta
Regresa una url con la información para continuar el pago PSE o una [respuesta de error](#objeto-error).
