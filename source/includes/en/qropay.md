#Charges with Qropay
From the API you can generate QR codes, with this codes your clients will be able to make charges from some mobile application.

<aside class="notice">
By using this payment method you will receive an instant notification after the customer makes the payment.
</aside>

***Flow to make charges with Qropay***</br> 
<img src="https://www.openpay.mx/img/cargo_por_qropay.png">

***Steps***</br> 
1. When you make a purchase from your website, the different payment's methods are shown, including offering to pay through Qropay.<br/>
2. The customer selects Qropay as a payment method.<br/>
3. From your server a request is sent to the API to create a pending charge.<br/>
4. Our server will create the pending charge and will respond with the same data together with a URL of the QR code in PNG format. <br/>
5. An HTML document is offered that can be embedded in your website to monitor the status of the charge with this payment method. <br/>
6. The customer makes the payment from the mobile application for Qropay. <br/>
7. It is validated and receives the payment <br/>
8. Notification of receipt of payment to your server <br/>

<aside class="notice">
The QR code will be available as long as its expiration time is not exceeded.
</aside>

##Create pending charge

> Definition

```plaintext--endpoints
Merchant
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/charges

Customer
POST https://sandbox-api.openpay.mx/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/charges
```

> Request example with client

```shell
curl -u sk_e568c42a6c384b7ab02cd47d2e407cab \
-H "Content-type: application/json" \
-X POST -d '{
   "method" : "qropay",
   "amount" : 949.00,
   "description" : "Qropay charge"
}' https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/charges
```

```php
$bancomer = Bancomer::getInstance('mzdtln0bmtms6o3kck8f', 'sk_e568c42a6c384b7ab02cd47d2e407cab');
$chargeRequest = array(
    'method' => 'qropay',
    'amount' => 100,
    'description' => 'Qropay charge');

$charge = $bancomer->charges->create($chargeRequest);
?>
```

```java
BancomerAPI api = new BancomerAPI("https://sandbox-api.openpay.mx", "sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

List<Parameter> request = new ArrayList<Parameter>(Arrays.asList(
    new SingleParameter("method", "qropay"),
    new SingleParameter("amount", "949.00"),
    new SingleParameter("description", "Qropay charge")
));

Map chargeAsMap = api.charges().create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeAsMap);
```

```csharp
BancomerAPI api = new BancomerAPI("sk_b05586ec98454522ac7d4ccdcaec9128", "maonhzpqm8xp2ydssovf");

List<IParameter> request = List<IParameter> {
    new SingleParameter("method", "qropay"),
    new SingleParameter("amount", "949.00"),
    new SingleParameter("description", "Qropay charge")
};

Dictionary<String, Object> chargeDictionary = bancomerAPI.ChargeService.Create(request);
ParameterContainer charge = new ParameterContainer("charge", chargeDictionary);
```

```ruby
@bancomer=BancomerApi.new("moiep6umtcnanql3jrxp","sk_3433941e467c4875b178ce26348b0fac")
@charges=@bancomer.create(:charges)

request_hash={
    "method" => "qropay",
    "amount" => 100.00,
    "description" => "Qropay charge"
}

response_hash=@charges.create(request_hash.to_hash)
```
> Response example

```json
{
    "id": "trfu5m6xzn6hiyn9jkzm",
    "authorization": null,
    "operation_type": "in",
    "method": "qropay",
    "transaction_type": "charge",
    "status": "charge_pending",
    "conciliated": false,
    "creation_date": "2018-04-25T18:45:16-05:00",
    "operation_date": "2018-04-25T18:45:16-05:00",
    "description": "Qropay charge",
    "error_message": null,
    "order_id": null,
    "due_date": "2018-04-26T23:59:59-05:00",
    "payment_method": {
        "type": "qropay",
        "qr_code": "https://sandbox-api.openpay.mx/qropay/mc2mzbvwpmnps8q0on6q/trfu5m6xzn6hiyn9jkzm/qrcode"
    },
    "amount": 949,
    "currency": "MXN",
    "fee": {
        "amount": 11.49,
        "tax": 0,
        "currency": "MXN"
    }
}
```

In order to receive a payment from a mobile device with a QR code it is necessary to make a call to our API by indicating in the `method` field the type` qropay`.
<br/>
If the request is correct you will receive a response with the information of the pending charge generated. The response includes a URL of the PNG image of the QR code.


###Request

Property | Descripción
--------- | -----
method | ***string*** (required) <br/>Debe contener el valor qropay para indicar que el pago se hará con codigo QR.
amount | ***numeric*** (required) <br/>Amount to charge. Must be an amount greater than zero, with up to two decimal digits.
description | ***string*** (required, longitud = 250) <br/>A description associated to the charge.

###Response

Returns a [transaction object](#transaction-object) with the charge information or with an [error response](#error-object).

##Charge Status

> Example

```html
<!DOCTYPE html>
<html>
    <head>
    ...
        <script type="text/javascript" src="https://openpay.s3.amazonaws.com/openpay-qropay.v1.js"></script>
    ...
        <script type="text/javascript">
            //merchantId    = Your merchant id
            //transactionId = Value of the id field of the transaction object returned when the pending charge was created
            function showIframeQR(merchantId, transactionId) {
                QroPay.setSandboxMode(true);  // Ignore line if you want to launch the request to the productive environment
                QroPay.setupIframe("iframeQR", merchantId, transactionId);
            }
        </script>
    </head>
    <body>
    ...
        <div id="iframeQR" />
    ...
    </body>
</html>
```

The JavaScript library [qropay] (https://openpay.s3.amazonaws.com/openpay-qropay.v1.js) is offered to insert an HTML document with the status of the QR code charge via an `iframe` tag. To use it you simply have to import it to your website. Done the previous thing you will be able to insert in `body` a label `div` in which an `iframe` will be inserted that will show an HTML document with the status of the position.

***Example of iframe with cargo status:***</br> 
<img src="https://www.openpay.mx/img/qropay/charge_completed.gif">