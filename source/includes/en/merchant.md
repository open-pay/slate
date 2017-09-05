#Merchant
The *merchant* object allows you to query info related to your account using the API,

##Merchant Object

> Object example:

```json
{ 
   "id": "m9lrykwsmljagrfb38rs", 
   "creationDate": "2013-11-13T16:58:40-06:00", 
   "name": "Promociones en linea", 
   "email": "contacto@enlinea.com.mx", 
   "phone": "(321) 222-2222", 
   "status": "active", 
   "balance": 1000, 
   "clabe": "646180109400000542" 
} 
```

Property | Description
--------- | -----------
id|***string*** <br/>Unique identifier assigned on creation.
creation_date|***datetime*** <br/>Transaction creation date in ISO 8601 format.
name|***string*** <br/>Registered merchant name.
email|***string*** <br/>Email account registered for the merchant.
phone|***string*** <br/>Phone number registered for the merchant.
status| ***string*** <br/>Merchant account status, it can be *active* or *deleted*.  If the account is in *deletate* status no transactions are allowed.
balance| ***numeric*** <br/>Balance in the account with two decimal placess.
clabe | ***numeric***   <br/>Linked CLABE account where funds can be received from any bank in Mexico using SPEI.



##Request a Merchant Object

> Definition



```shell
GET https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}
```


```php
<?
// =============================
// Not yet implemented.
// =============================
?>
```


```java
openpayAPI.merchant().get();

```


```csharp
// =============================
// Not yet implemented.
// =============================
```


```javascript
openpay.merchant.get(callback);
```

Ruby


```ruby
# =============================
# Not yet implemented.
# =============================
```



> Request example:

```shell
curl https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f \
   -u sk_e568c42a6c384b7ab02cd47d2e407cab:
```

```java
OpenpayAPI api = new OpenpayAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");
Merchant merchant = api.merchant().get();
```

```javascript
openpay.merchant.get(function(error, merchant){
  // ...
});
```

> Response example:

```json
{
   "name":"Demo Openpay",
   "email":"demo@openpay.mx",
   "phone":"(442) 258-1039",
   "status":"active",
   "balance":218.73,
   "clabe":"646180109400135624",
   "id":"mzdtln0bmtms6o3kck8f",
   "creation_date":"2014-01-23T10:45:53-06:00"
}
```

Returns the merchant account details.  Only the unique merchant identifier is required.

###Request

Property | Description
--------- | -----------
id | ***string*** (required, longitude = 45) <br>unique merchant identifier.

###Response
If the identifier is correct it will return a merchant object.

