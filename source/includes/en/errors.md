#Errors

Bbva returns JSON objects in the service responses. 

##Error Object

> Object example 

```json
{
    "category" : "request",
    "description" : "The customer with id 'm4hqp35pswl02mmc567' does not exist",
    "http_code" : 404,
    "error_code" : 1005,
    "request_id" : "1981cdb8-19cb-4bad-8256-e95d58bc035c",
    "fraud_rules": [
        "Billing <> BIN Country for VISA/MC"
    ]
}
```

```java
//For Java every operation will return an instance of the "BbvaServiceException" class which will have the error information. ```

```csharp
//For C Sharp,  every operation will return an instance of the "BbvaException" class which will have the error information.
```

```ruby
#For Ruby, every operation can return any of the following exceptions:

# => BbvaException: For generic errors, like invalid resources, etc.
# => BbvaConnectionException: For errors related with server connection problems.
# => BbvaTransactionException: For errors during operations implementation.
```

Property | Description
--------- | -----
category    |***string*** <br/>**request:**  Indicates an error caused by data sent by the customer. For example, an invalid request, an attempt at a transaction without funds or a transfer to an account that does not exist. <br/><br/>**internal:** Indicates an error on Bbva side, and will occur very rarely. <br/><br/>**gateway:** Indicates an error during the transaction of funds from one card to the Bbva account or from the account to a bank or card.
error_code  |***numeric*** <br/>Bbva numeric error code indicating a problem happened.
description |***string*** <br/>Error description.
http_code   |***string*** <br/>HTTP error code  of the response.
request_id  |***string*** <br/> Request identifier.
fraud_rules |***array*** <br/> Array with antifraud rules broken according to fraud detection rules.

##Error codes

###General
Code    | HTTP Error |Cause
--------- | ----------- | --------
1000 | 500 Internal Server Error | An internal error occurred on the Bbva server 
1001 | 400 Bad Request | The format of the request is not JSON, the fields do not have the correct format, or the request does not have fields that are required.
1002 | 401 Unauthorized | The call is not authenticated or the authentication is incorrect.
1003 | 422 Unprocessable Entity | The operation could not be completed because the value of one or more of the parameters is incorrect.
1004 | 503 Service Unavailable | A necessary for processing the transaction service is unavailable.
1005 | 404 Not Found | One of the resources requested does not exist.
1006 | 409 Conflict | A transaction with the same order ID already exists.
1007 | 402 Payment Required | The transfer of funds from a bank account or card to the Bbva account was not accepted.
1008 | 423 Locked | One of the accounts required in the request is deactivated.
1009 | 413 Request Entity too large | The request body is too large.

###Storage

Code    | HTTP Error |Cause
--------- | ----------- | --------
2001 | 409 Conflict | The bank account with this CLABE is already registered on the customer.
2002 | 409 Conflict | The card with this number is already registered on the customer.
2003 | 409 Conflict | Customer with this external identifier (External ID) already exists.
2004 | 422 Unprocessable Entity | The check digit card number is invalid according to the Luhn algorithm.
2005 | 400 Bad Request | The expiration date of the card is prior to the current date.
2006 | 400 Bad Request | Security code card (CVV2) was not provided.
2007 | 412 Precondition Failed | The card number is a test number and can only be used in Sandbox.
2008 | 412 Precondition Failed | The consulted card is not valid for points.

###Cards
Code    | HTTP Error |Cause
--------- | ----------- | --------
3001 | 402 percent Required | The card was declined.
3002 | 402 Payment Required | The card has expired.
3003 | 402 Payment Required | The card has insufficient funds.
3004 | 402 Payment Required | The card has been identified as a stolen card.
3005 | 402 Payment Required | The card has been identified as a fraudulent card.
3006 | 412 Precondition Failed | The operation is not allowed for this customer or this transaction.
3008 | 412 Precondition Failed | The card is not supported in online transactions.
3009 | 402 Payment Required | The card was reported missing.
3010 | 402 Payment Required | The bank has restricted the card.
3011 | 402 Payment Required | The bank has requested that the card is retained. Contact the bank.
3012 | 412 Precondition Failed | A bank authorization is required to make this payment.

###Accounts
Code    | HTTP Error |Cause
--------- | ----------- | --------
4001  |412 Preconditon Failed | The Bbva account has not enough funds.
