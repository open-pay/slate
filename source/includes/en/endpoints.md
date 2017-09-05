# API Endpoints

> Available resourcers

<br/>
<br/>

> a) By Merchant

```
/v1/{MERCHANT_ID}/...

/fees
/fees/{FEE_ID}
/charges
/charges/{TRANSACTION_ID}
/payouts
/payouts/{TRANSACTION_ID}
/cards
/cards/{CARD_ID}
/customers
/customers/{CUSTOMER_ID}
/plans
/plans/{PLAN_ID}
​/tokens
/tokens/{TOKEN_ID}
```

> b) By Customer

```
/v1/{MERCHANT_ID}/customers/{CUSTOMER_ID}/...

/cards
/cards/{CARD_ID}
/bankaccounts
/bankaccounts/{BANKACCOUNT_ID}
/charges
/charges/{TRANSACTION_ID}
/payouts
/payouts/{TRANSACTION_ID}
/transfers
/transfers/{TRANSACTION_ID}
/subscriptions
/subscriptions/{SUBSCRIPTION_ID}
```

The Openpay REST API has a test environment (sandbox) and a production environment. For integrating your system with Openpay, use the credentials that were generated when you signed up. Once you are ready to move to production environment and your request is approved, new credentials will be generated for accessing the production environment.

The following URIs are the basis of the endpoints for the supported environments:

* **Test**, URI base: <br/> `https://sandbox-api.openpay.mx`<br/><br/>
* **Production**, URI base: <br/>`https://api.openpay.mx`<br/>

A complete endpoint consists of the base URI of the environment, the identifier of the Merchant and the resource.

For example, if we want to create a new customer, the endpoint would be::

<code>POST https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers</code>

In order to create a complete request is necessary to send the right HTTP headers and the information in JSON format.

<aside class="notice">
 All the examples of this documentation are based on the testing environment.
</aside>