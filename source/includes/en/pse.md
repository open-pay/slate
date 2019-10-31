#PSE
Charges to bank accounts can be made through PSE.
When creating a PSE payment, a url is generated to continue the payment flow.

Customer information is required, or the id of an existing customer can be used.

##With new customer, or existing customer id

> Definition

```shell
Merchant
POST https://sandbox-api.openpay.co/v1/{MERCHANT_ID}/pse

Customer
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
//Customer
openpayAPI.PseService.Create(string customer_id, PseRequest request);

//Merchant
openpayAPI.PseService.Create(PseRequest request);
```

```ruby



```

> Merchant request example

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

> Response example

```json
{
	"redirect_url":"https://sandbox-api.openpay.mx/v1/maonhzpqm8xp2ydssovf/customers/ah8tdi7gr9zll6ejijuu/checkouts/ckqtz7smmjffvc4jgfko/pse"
}
```

In the response that contains <code>redirect_url</code> field, the flow is continued to make the PSE payment.

<aside class="notice">
You can make the payment with the merchant account or the customer account.
</aside>

***Customized antifraud system***</br>
You can send extra data to Openpay in order to increase number of variables and get better results in antifraud detection for your payments.

<aside class="notice">
If you want to use this feature you need to send <code>metadata</code> property with all fields you think can help to decide when a payment is a fraud trying. Call support line to enable this feature</br>
</aside>

###Request

Property | Description
--------- | -----
country|***string*** (required) <br/> It must contain the value **COL** to indicate that the country is Colombia.
amount | ***string*** (required) <br/> Payment amount. It must be an amount with an integer value greater than zero.
currency | ***string*** (required) <br/>currency for payment. At the moment only 1 type of currency is supported: Colombian Peso (COP).
iva | ***string*** (required) <br/>It must contain the VAT value, it is informational only, it has no effect on the amount field.
description | ***string*** (required, length = 250) <br/>A description associated to the payment.
order_id | ***string*** (optional, length = 100) <br/>Unique identifier of payment. Must be unique among all payments.
[customer](#create-a-new-customer)| ***object*** (required) <br/>Customer information who is payer. You can use the same parameters used in the creation of a customer but an account for the customer will not be created. <br/><br/> **Note:** This parameter can be used only by creating the payment at the merchant level<br/><br/> To create a customer and keep a record of their payments history refer to [create a customer] (#create-a-new-customer) and do the payment at the customer level.
metadata |  ***list(key, value)*** (optional) <br/>Field list to send antifraud system, It must be according to [Rules to send custom antifraud fields] (#custom-to-send-antifraud-fields).


###Response
Return a url with the information to continue the PSE payment or an [error response](#error-object).
