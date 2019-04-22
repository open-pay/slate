# API Endpoints

> Available resourcers

<br/>
<br/>

```
/v1/{MERCHANT_ID}/charges
/v1/{MERCHANT_ID}/charges/{TRANSACTION_ID}
```

The Bancomer REST API has a test environment (sandbox) and a production environment. For integrating your system with Bancomer, use the credentials that were generated when you signed up. Once you are ready to move to production environment and your request is approved, new credentials will be generated for accessing the production environment.

The following URIs are the basis of the endpoints for the supported environments:

* **Test**, URI base: <br/> `https://sand-api.ecommercebbva.com`<br/><br/>
* **Production**, URI base: <br/>`https://api.ecommercebbva.com`<br/>

A complete endpoint consists of the base URI of the environment, the identifier of the Merchant and the resource.

For example, if we want to create a new charge, the endpoint would be::

<code>POST https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges</code>

In order to create a complete request is necessary to send the right HTTP headers and the information in JSON format.

<aside class="notice">
 All the examples of this documentation are based on the testing environment.
</aside>