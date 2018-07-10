# API Endpoints

> Recurso disponibles

<br/>
<br/>

> a) Por Comercio

```
/v1/{MERCHANT_ID}/...
/charges
/charges/{TRANSACTION_ID}
​/tokens
/tokens/{TOKEN_ID}
```



La API REST tiene un ambiente de pruebas (sandbox) y un ambiente de producción. Usa las credenciales que se generaron al momento de tu registro para realizar la integración de tu sistema. Una vez que estes listo para pasar a producción y tu solicitud sea aprobada, se generarán nuevas credenciales para acceder al ambiente de producción.

La siguientes URIs forman la base de los endpoints para los ambientes soportados:

* **Pruebas**, URI base: <br/> `https://sandbox-api.openpay.mx`<br/><br/>
* **Producción**, URI base: <br/>`https://api.openpay.mx`<br/>

Un endpoint completo esta formado por la URI base del ambiente, el identificador del comercio y el recurso.

Por ejemplo, si queremos crear un nuevo cliente, el endpoint sería:

<code>POST https://sandbox-api.openpay.mx/v1/mzdtln0bmtms6o3kck8f/customers</code>

Para crear una petición completa es necesaria envíar las cabeceras HTTP correctas y la información en formato JSON.

<aside class="notice">
Todos los ejemplos de está documentación están apuntados al ambiente de pruebas.
</aside>
