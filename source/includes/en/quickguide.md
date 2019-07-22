# Quick Guide


This is a quick guide to the flow of operation and description of each point in order to accompany the development of the stores. We highly recommend reading the integration specifications in detail before starting to develop.


##Charges with VPOS

Flow Chart of the Operation.

![Cargo VPOS](images/charge-vpos.png)

**Note : All merchants are created by default with 3d Secure authentication and VPOS**

1.- The cardholder enters the web page of the store, selects their products once selected and inside the shopping cart clicks on the option to pay.

2.- The merchant generates a request with a JSON object that contains the fields listed in ["Charges with VPOS"] (#with-vpos). Within the object, a field must be included with the URL to which the flow is redirected at the end of the transaction, whether authorized or rejected.

         **Example of URL:**  	"redirect_url": "https://micomercio.com"

  **Note:** The data that is included in this object is from the purchase. They are not sensitive data.


3.- BBVA returns a response with a JSON object named "transaction" that contains the URL to which the cardholder must be directed to capture the data in the VPOS The field **"id" (string)** is a unique assigned identifier by BBVA at the time of its creation. The merchant has to associate a sale order number with this ID.

4.- The merchant redirects the cardholder to the URL that displays the VPOS, which travels in the Json object named "transaction"

**Example:** "url" :

"https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/trywj1kyx7vczirifkyw/card_capture"

5.- The cardholder, enters the sensitive data in the VPOS, card number, CVV, expiration date, and sends the information directly to BBVA

5.5.- 3d Secure authentication is carried out by the issuing bank of the Debit or Credit Card

6.- BBVA processes the transaction and redirects the cardholder to the URL sent by the merchant in step "2"

7.- The merchant receives the request from the client's browser and uses the id of the transaction to query the result (Authorized or Rejected) through the [Get a Charge](#get-a-charge) service this ID field was associated with the identifier of Order of sale in step number 3.

 **Example of URL:**  "redirect_url": "https://micomercio.com"

 Including in the URL, the ID of the transaction ...

 Ej .- https://www.micomercio.com?**id=tr72356487234bd238d**


 8 .- The merchant makes a request to the [Get a Charge](#get-a-charge) service The status of the transaction is requested from the BBVA server and an object "Transaction object" is answered.

 **Note.-** The merchant generates your purchase receipt based on the information obtained from the object "Get a Charge"
 The status of the transaction must be requested from the BBVA server and the latter responds to an object "Transaction object". with the data that should be shown on the payment receipt.




**IMPORTANT**

Always include the secret key and the MID as well as the Version

POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges.

To make requests to the API, it is necessary to send the API key (API Key) in all your calls to our servers. You can get the key from the [dashboard](https://sand-portal.ecommercebbva.com).

API key:

**Private.-** For requests between servers and with full access to all API operations (it should never be shared).



##Charges with card (WITHOUT VPOS)

**¡ IMPORTANT !**

To use the charge without VPOS you must request authorization with your account executive !!!


Flow Chart of the Operation.

![Cargo VPOS](images/charge-custom-form.png)


1.- The cardholder enters the web page of the store, selects their products once selected and inside the shopping cart clicks on the option to pay. Within the Trade Checkout, sensitive data such as card number, CVV, expiration date are captured and the information is sent directly to BBVA  

2.- The trade creates a Json object containing the fields listed in "With card" charges and the "card" object is added with the cardholder's sensitive data.

 Within the object should include the url where the flow is redirected at the end of the transaction, whether authorized or rejected.

         **Example of URL.-**  	"redirect_url": "https:/micomercio.com"

3.- BBVA returns the response with a JSON object named "transaction" that contains the URL to which the cardholder must be directed for 3D Secure authentication.
This URL is located within the response in the "payment_method" object:

**Example of URL.-**  

https://sand-api.ecommercebbva.com/v1/md8r38qyiyiprpmim9yy/charges/trrla2nopehlfx31fbrg/redirect/

 The field **"id" (string)** is a unique identifier assigned by BBVA at the time of its creation. The merchant has to associate a sale order number with this ID.

3.5.- Authentication of the cardholder is carried out by means of 3d Secure with the issuing bank of the Debit or Credit Card

4.- BBVA processes the transaction and redirects the cardholder to the URL sent by the merchant in step "2"

5.- The merchant receives the request from the client's browser and uses the transaction id to query the result (Authorized or Rejected) through the  ["Get a Charge"](#get-a-charge) service this ID field was associated with the order identifier of the sale in step number 3.

 **Example of URL.-**  "redirect_url": "https://micomercio.com"

 Including in the URL, the ID of the transaction ...

 Ej .- https://www.micomercio.com?**id=tr72356487234bd238d**

 6.- The trade makes a request with the ["Get a Charge"](#get-a-charge) service The status of the transaction is requested from the BBVA server and an object "Transaction object" is answered.

**Note.-** The merchant generates your purchase receipt based on the information obtained from the object "Obtain a Position"
The status of the transaction must be requested from the BBVA server and the latter responds to an object "Transaction object". with the data that should be shown on the payment receipt.


##Troubleshooting

If you have any questions you can check the issues section of the library you are using:

* [Java](https://github.com/EcommerceBBVA/BBVA-JAVA)
* [Ruby](https://github.com/EcommerceBBVA/BBVA-RUBY)
* [.NET](https://github.com/EcommerceBBVA/BBVA-CSHARP)
* [PHP](https://github.com/EcommerceBBVA/BBVA-PHP)
