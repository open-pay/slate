# Guía Rápida


Esta es una guía rápida del flujo de operación y descripción de cada  punto con el fin de acompañar el desarrollo de los comercios.
Recomendamos ampliamente  leer las especificaciones de integración de  manera detallada antes de comenzar a desarrollar.


##Cargos con VPOS

Diagrama de Flujo de la Operación.

![Cargo VPOS](images/charge-vpos.png)

**Nota : Todas los comercios nacen por default con autenticación 3d Secure y VPOS**

1.- El tarjetahabiente entra a la página web del comercio,  selecciona sus productos una vez seleccionados y dentro del carrito de compras  da click en la opción pagar.

2.-  El comercio genera una petición con un, objeto JSON que contiene los campos enlistados en ["Cargos con VPOS"](#con-vpos). Dentro del objeto  se deberá incluir un campo con la url a donde se redirige el flujo al finalizar la transacción, ya sea autorizada o rechazada.

         **Ejemplo de la URL:**  	"redirect_url": "https://micomercio.com"

  **Nota:** los Datos que se incluyen en este objeto son de la compra. No son data sensible.


3.-  BBVA  devuelve una respuesta con un objeto JSON de nombre “transaction” que contiene la URL a la que se tiene que dirigir al tarjetahabiente para capturar los datos en la VPOS El campo **“id” (string)** es un Identificador único asignado por BBVA al momento de su creación.  El comercio tiene que asociar un número de orden de la venta con este ID.

4.- El comercio redirecciona al tarjetahabiente a la URL que despliega el VPOS, la cual viaja en el objeto Json de nombre “transaction”

**Ejemplo:** "url" :

"https://sand-api.ecommercebbva.com/v1/mptdggroasfcmqs8plpy/charges/trywj1kyx7vczirifkyw/card_capture"

5.- El tarjetahabiente, ingresa los datos sensibles en el VPOS, número de tarjeta, CVV, fecha de vencimiento, y envía la información directamente a BBVA  

5.5.- Se realiza la autenticación 3d Secure, por parte del banco emisor de la Tarjeta de Débito o Crédito

6.- BBVA procesa la transacción y redirecciona al tarjetahabiente a la URL que envió el comercio en el paso “2”         

7.- El comercio recibe la petición desde el navegador del cliente y utiliza el id de la transacción para consultar el resultado (Autorizada o Rechazada) mediante el servicio [Obtener un Cargo](#obtener-un-cargo) este campo ID  se asoció el identificador de orden de la venta  en el paso número 3.

 **Ejemplo de la URL:**  "redirect_url": "https://micomercio.com"

Incluyendo en la URL, el Id de la transacción ...

 Ej .- https://www.micomercio.com?**id=tr72356487234bd238d**


 8 .-  El comercio hace una petición al servicio [Obtener un Cargo](#obtener-un-cargo)  Se pide el estatus de la transacción al servidor de BBVA  y se responde un objeto  “Objeto transacción“.

Nota .-   El comercio genera su recibo de compra en base a la información obtenida del  objeto “Obtener un Cargo”
Se  deberá pedir el estatus de la transacción al servidor de BBVA  y este responde un objeto  “Objeto transacción “ . con la data que se deberá mostrar en el recibo de pago .




**IMPORTANTE**

Siempre se debe incluir la llave secreta y el MID así como la Versión

POST https://sand-api.ecommercebbva.com/v1/{MERCHANT_ID}/charges.

Para realizar peticiones a la API, es necesario enviar la llave de API (API Key) en todas tus llamadas a nuestros servidores. ​La llave la puedes obtener desde el [dashboard](https://sand-portal.ecommercebbva.com).

Llave de API:

**Privada.-** Para llamadas entre servidores y con acceso total a todas las operaciones de la API (nunca debe ser compartida).



##Cargos con tarjeta (SIN VPOS)

**¡ IMPORTANTE !**

Para utilizar el cargo sin Vpos se debe solicitar autorización con su ejecutivo de cuenta!!!


Diagrama de Flujo de la Operación.

![Cargo VPOS](images/charge-custom-form.png)


1.- El tarjetahabiente entra a la página web del comercio, selecciona sus productos una vez seleccionados y dentro del carrito de compras da click en la opción pagar.
Dentro del Checkout del comercio se capturan los data sensible tales como número de tarjeta, CVV, fecha de vencimiento, y se envía la información directamente a BBVA  

2.- El comercio crea un  un objeto Json que contienen los campos enlistados en cargos  “Con tarjeta” y se agrega el objeto "card" con la data sensible del tarjetahabiente.

 Dentro del objeto se deberá incluir  la url en donde se redirige el flujo al finalizar la transacción, ya sea autorizada o rechazada.

         **Ejemplo de la URL.-**  	"redirect_url": "https:/micomercio.com"

3.-  BBVA  devuelve una respuesta con un objeto JSON de nombre “transaction” que contiene la URL a la que se tiene que dirigir al tarjetahabiente para la autenticación 3D Secure.
Esta URL se encuentra  dentro de la respuesta en el objeto"payment_method":

**Ejemplo de la URL.-**  

https://sandbox-api.openpay.mx/v1/md8r38qyiyiprpmim9yy/charges/trrla2nopehlfx31fbrg/redirect/

 El campo **“id” (string)** es un Identificador único asignado por BBVA al momento de su creación.  El comercio tiene que asociar un número de orden de la venta con este ID .

3.5.- Se realiza la autenticación del tarjetahabiente  por medio de 3d Secure con banco emisor de la Tarjeta de Débito o Crédito

4.-  BBVA procesa la transacción y  redirecciona al tarjetahabiente a la URL que envió el comercio en el paso “2”         

5.- El comercio recibe la petición desde el navegador del cliente y utiliza el id de la transacción para consultar el resultado (Autorizada o Rechazada) mediante el servicio [“Obtener un Cargo”](#obtener-un-cargo) este campo ID  se asoció el identificador de orden de la venta  en el paso número 3.

 **Ejemplo de la URL.-**  "redirect_url": "https://micomercio.com"

 Incluyendo en la URL, el Id de la transacción ...

 Ej .- https://www.micomercio.com?**id=tr72356487234bd238d**

 6.- El comercio hace una petición con el servicio [“Obtener un Cargo”](#obtener-un-cargo) Se pide el estatus de la transacción al servidor de BBVA  y se responde un objeto  “Objeto transacción “ .

**Nota.-**   El comercio genera su recibo de compra en base a la información obtenida del  objeto “Obtener un Cargo”
Se  deberá pedir el estatus de la transacción al servidor de BBVA  y este responde un objeto  “Objeto transacción “ . con la data que se deberá mostrar en el recibo de pago .
