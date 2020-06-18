---
layout: faq
title: Vtex
category: plugin
tags: plugin
lang: es
---

# Vtex


## CONFIGURACIÓN DE PLUGIN OPENPAY EN SITIO WEB CON VTEX

Para poder configurar el plugin de Openpay en Vtex se debe seguir el siguiente flujo:
<p>
	<img src="/images/plugins/vtex_openpay_52.png">
</p>

A continuación, el detalle de cada punto señalado en el diagrama:


### **1.- CREAR CUENTA EN OPENPAY**

<ol>
<li>Ir al sitio web de <a href="https://openpay.mx/docs/testing.html">Openpay</a> y crear cuenta.
<br>
<blockquote>
<strong>Nota:</strong><em> Para hacer pruebas, crear la cuenta en ambiente <a href="https://openpay.mx/docs/testing.html">Sandbox</a>. Para operación real, pide tu pase a Producción
</em>
</blockquote>
</li>
<li>Entrar al Dashboard con los datos de acceso creados
</li>
<br>
<li>En barra superior, ir al icono de engrane y hacer click en la opción <strong>Credenciales de API</strong>
<br>
<br>
<img src="/images/plugins/vtex_openpay_02.png" alt="Credenciales API">
</li>
<br>
<br>
<li>Obtener ID (identificador del comercio), Llave privada y Llave pública (esta información se usará más adelante).
<br>
<br>
<img src="/images/plugins/vtex_openpay_03.png" alt="Datos">
<br>
<blockquote>
<strong>Nota: </strong><em>Las Credenciales de API son diferentes en cada ambiente. Debe guardar estos datos por separado y no confundirlos para que los ambientes de Sandbox y Producción funcionen correctamente.
</em>
</blockquote>
</li>
</ol>


### **2.- CONFIGURAR DEVICE ID EN GTM (GOOGLE TAG MANAGER)**

Para que su tienda VTEX funcione correctamente con Openpay, se requieren datos adicionales que se obtienen a través de Google Tag Manager (recomendamos que se cree una cuenta exclusiva para la integración de VTEX con Openpay para evitar posibles conflictos con otros contenedores)

<ol>
<li>Descargue desde GitHub la última versión del Contenedor GTM VTEX (archivo JSON) y guárdelo en su ordenador (<a href="https://github.com/open-pay/openpay-vtex/blob/master/GTM-Openpay.json">descargue aquí</a>)
</li>
<br>
<li>Ir a la URL <a href="http://www.google.com/tagmanager/">http://www.google.com/tagmanager/</a> . Si no tiene una cuenta, hacer click en <strong>Crear cuenta</strong>, si ya tiene una cuenta, ir al paso 5
</li>
<br>
<li>Capture los datos solicitados y haga click en el botón <strong>Guardar</strong> al finalizar
<br>
	<ol type="a">
	<li><strong>Nombre de cuenta:</strong> por ejemplo "Openpay"
	</li>
	<li><strong>País:</strong> México
	</li>
	<li><strong>Configuración del contenedor: </strong>URL del sitio (es sólo informativo)
	</li>
	<li><strong>Plataforma objetivo:</strong> Sitio web
	</li>
	</ol>
</li>
<br>
<li>Aceptar Términos de uso para continuar
</li>
<br>
<li>Hacer login en <a href="http://www.google.com/tagmanager/">http://www.google.com/tagmanager/</a> para la tienda que vamos a configurar
</li>
<br>
<li>Se mostrará el dashboard principal. Ir al menú y hacer click en <strong>Administrador</strong>
</li>
<br>
<li>En las opciones de contenedor, del lado derecho de la pantalla aparecerá su identificador de GTM que tiene un formato como éste: <em>GTM-A1B2CDE</em>. Debe guardar el ID ya que se utilizará más adelante.
<br>
<br>
<img src="/images/plugins/vtex_openpay_43.png">
</li>
<br>
<li>Hacer click en <strong>Importar contenedor</strong>
<br>
<br>
<img src="/images/plugins/vtex_openpay_44.png">
</li>
<br>
<li>Haga click en <strong>Elija el archivo del contenedor</strong>, seleccione el archivo contenedor que descargó en el paso 1 y presione Abrir o Aceptar
</li>
<br>
<li>En la opción Elegir espacio de trabajo presione el botón <strong>Nuevo</strong>
</li>
<br>
<li>Elija un nombre para su Espacio de trabajo (Si no está seleccionada, elija la opción Combinar / Cambiar el nombre de etiquetas, activadores y variables en conflicto)
<br>
<br>
<img src="/images/plugins/vtex_openpay_45.png">
</li>
<br>
<li>Presione el botón <strong>Confirmar</strong>
</li>
<br>
<li>Aparecerá el contenedor en su Tag Manager del lado izquierdo. Haga click en <strong>Variables</strong>
<br>
<br>
<img src="/images/plugins/vtex_openpay_46.png">
</li>
<br>
<li>Ir a Variables definidas por el usuario y cambie los valores como se señala:
<br>
<br>
<img src="/images/plugins/vtex_openpay_47.png">
<br>
<br>
	Si es ambiente <strong>Sandbox</strong>
	<br>
	<ol>
	<li type="disc"><strong>openpay_merchant_id:</strong> ID de su comercio en Openpay
	</li>
	<li type="disc"><strong>openpay_public_key:</strong> Llave pública de su comercio en Openpay
	</li>
	<li type="disc"><strong>openpay_sandbox_mode:</strong> true
	</li>
	</ol>
<br>
	Si es ambiente <strong>Producción</strong>
	<br>
	<ol>
	<li type="disc"><strong>openpay_merchant_id:</strong> ID de su comercio en Openpay
	</li>
	<li type="disc"><strong>openpay_public_key:</strong> Llave pública de su comercio en Openpay
	</li>
	<li type="disc"><strong>op_sandbox_mode:</strong> false
	</li>
	</ol>
</li>
<br>
<li>Guarde los cambios y haga click en el botón superior derecho <strong>Enviar</strong>. Esto inicia el proceso de publicación de su contenedor con los cambios que realizó en las variables.
<br>
<br>
<img src="/images/plugins/vtex_openpay_48.png">
</li>
<br>
<li>En la pantalla “Configuración de envío” validar que se muestre seleccionada la opción “Publicar y crear versión” y que en la parte inferior se muestre “Entorno de publicación Live”. Hacer click en el botón <strong>Publicar</strong>.
<br>
<br>
<img src="/images/plugins/vtex_openpay_49.png">  
</li>
</ol>
<br>
Si se publicó correctamente, su GTM está listo para ser consumido por el sistema VTEX, al cual le agregaremos el ID que obtuvimos en el paso 7
<br>
<br>
<ol>
<li value="17">Ingresar a <a href="https://vtex.com/">Vtex</a> e ir a <strong>Panel de Administración > Configuración de la tienda > Checkout</strong> y dar click en el botón con icono de engrane
<br>
<br>
<img src="/images/plugins/vtex_openpay_50.png">
</li>
<br>
<li>Hacer click en la opción <strong>Checkout</strong>, introduzca su GTM ID y presione <strong>Guardar</strong>. Con esto VTEX insertará el código de GTM en su tienda en línea.
<br>
<br>
<img src="/images/plugins/vtex_openpay_51.png">
</li>
</ol>
<br>
<br>
<br>


### **3.- CONFIGURAR PAYMENT PROVIDER EN VTEX**

<ol>
<li>Ir al administrador de Payment Provider de <a href="https://vtex.com/">Vtex</a>
</li>
<br>
<li>Acceder a <strong>Transacciones > Pagos > Configuración > Afiliaciones</strong>
</li>
<br>
<li>Hacer click en la opción <strong>Openpay</strong>
</li>
<br>
<li>Capturar los campos solicitados.
<br>
<br>
	Para ambiente <strong>Sandbox</strong> capturar:
	<br>
	<ol>
	<li type="disc"><strong>Application Key:</strong> ID (identificador del comercio en Openpay)
	</li>
	<li type="disc"><strong>Application Token:</strong> Llave privada (obtenida de Openpay)
	</li>
	</ol>
	<br>
	Para ambiente <strong>Producción</strong> capturar:
	<ol>
	<li type="disc"><strong>Application Key:</strong> Prefijo (LIVE_) + ID (identificador del comercio en Openpay)
	<br>
	<br>
	<img src="/images/plugins/vtex_openpay_05.png" alt="Datos">
	</li>
	<br>
	<li type="disc"><strong>Application Token:</strong> Llave privada (obtenida de Openpay)
	<br>
	</li>
	</ol>
</li>
<br>
<li>Hacer click en el botón <strong>Salva</strong>
</li>
<br>
<li>Configurar en Vtex los métodos de pago a emplear en el e-commerce (<a href="#2metodos">ver detalle</a>)
</li>
<br>
<li>Configurar en Openpay los webhook (<a href="#3webhooks">ver detalle</a>)
</li>
</ol>



### **4.- VALIDACIÓN DE CONFIGURACIÓN CORRECTA**

<ol>
<li>Realizar procesos de compra con diferentes escenarios (puede ver mas detalle en la sección <a href="https://openpay.mx/docs/testing.html">Pruebas</a>)
</li>
<br>
<li>Verificar que el resultado para cada escenario es el esperado. En caso de no obtener el resultado esperado se deberá validar nuevamente la configuración y en caso de tener un resultado exitoso, se deberá solicitar a Openpay una cuenta de producción.
<br>
<blockquote>
<strong>Nota:</strong> <em> En el caso del método de Pago en Tiendas, se debe validar que en la pantalla “Confirmación de pago” se muestre correctamente el botón “Referencia” como se ve en la siguiente imagen
</em>
</blockquote>
<br>
<br>
<img src="/images/plugins/vtex_openpay_41.png" alt="Validación">

</li>
</ol>



## CONFIGURAR MÉTODOS DE PAGO EN VTEX
<p id="2metodos"></p>
En Openpay contamos con 3 formas de pago:
<br>
<ol>
<li type="disc"> <strong>TARJETAS</strong>
<br>
Aquí se consideran todos los pagos por Tarjeta de Crédito, Débito y Servicio, siempre y cuando estén operados por Visa, MasterCard, American Express, Carnet.
También se incluye los pagos con Puntos Bancomer, Santander y Scotiabank (POINTS).
</li>
<br>
<li type="disc"> <strong>TRANSFERENCIAS INTERBANCARIAS</strong>
<br>
Son las transferencias interbancarias, como pueden ser SPEI o simplemente dar los datos de la cuenta CLABE para mostrar datos de transferencia del comercio.
</li>
<br>
<li type="disc"> <strong>PAGO EN TIENDAS</strong>
<br>
Se muestra el número de referencia para realizar el pago en cualquiera de los establecimientos de la Red Paynet. Los establecimientos se pueden consultar en paynet.com.mx
</li>
</ol>
<br>

Para configurar cualquiera de los métodos de pago mencionados debemos de:

<ol>
<li>Ir al administrador de Payment Provider en <a href="https://vtex.com/">Vtex</a>
</li>
<br>
<li>Acceder al path <strong>Transacciones > Pagos > Configuración > Planes de pago</strong> y hacer click en el botón <strong>Agregar</strong>
	<br>
	<br>
	<img src="/images/plugins/vtex_openpay_07.png">
 </li>
<li>Se mostrará una pantalla con diversas opciones donde hay que buscar y seleccionar el método de pago a configurar.
<blockquote>
<strong>Nota:<em> Sólo para los métodos de pago <strong>Pago en tiendas</strong> y <strong>Transferencias interbancarias</strong> seguir las siguientes indicaciones:</em></strong>
</blockquote>
	<ol type="a">
	<li><strong>Pago en tiendas:</strong> Buscar en sección de Pago personalizado con la leyenda “Pago en tienda”
	<br>
	<br>
	<img src="/images/plugins/vtex_openpay_08.png">
	</li>
	<li><strong>Transferencias interbancarias:</strong> Buscar en sección de Otro con la leyenda “SPEI”
	<br>
	<br>
	<img src="/images/plugins/vtex_openpay_11.png">
	</li>
	</ol>
</li>
<li>En la pantalla de configuración del método de pago seleccionado, hacer click en la afiliación de Openpay y marcarlo como activo
	<br>
	<br>
	<img src="/images/plugins/vtex_openpay_09.png">
</li>
<br>
<li>En la barra superior capturar la leyenda que corresponda al método de pago que se está configurando.
<blockquote>
<strong>Nota:</strong><em> Sólo para los métodos de pago <strong>Pago en tiendas</strong> y <strong>Transferencias interbancarias</strong> seguir las siguientes indicaciones:</em>
</blockquote>
	<ol type="a">
	<li><strong>Pago en tiendas:</strong> Pago en Tienda
	</li>
	<li><strong>Transferencias Interbancarias:</strong> SPEI
	</li>
	</ol>
<br>
<br>
<blockquote>
<strong>Nota:</strong> <em>Debido a configuraciones del conector, <strong>la leyenda a colocar en cada método de pago deberá de ser tal cual se indica en este paso</strong></em>
</blockquote>
</li>
</ol>


## CONFIGURACIÓN DE WEBHOOKS
<p id="3webhooks"></p>
En las configuraciones, es necesario la creación de un Webhoook, para notificar cuando se ha realizado un cargo a una tarjeta o cuando un depósito se ha realizado con éxito. La creación de un Webhook dentro de Openpay se realiza como se indica a continuación:

<ol>
<li>Ir al Dashboard de Openpay (<a href="sandbox-dashboard.openpay.mx/login">Sandbox</a> / <a href="https://dashboard.openpay.mx/login">Produccion</a>)
</li>
<br>
<li>En la barra superior hacer click en el icono de engrane y seleccionar “Configuraciones”
</li>
<br>
<li>Hacer click en el botón <strong>Agregar</strong> para abrir el formulario que deberá ser llenado de la siguiente manera:
	<ol>
	<li type="disc"> <strong>URL:</strong> Capturar la como se muestra la siguiente cadena conformada por URL (<em>https://vtex.openpay.mx/callbackvtex/</em>) y el ID del comercio
	<br>
	<p style="color:#FF0000">https://vtex.openpay.mx/callbackvtex/<strong>[ID]</strong></p>
	<blockquote>
	<strong style="color:#FF0000">[ID]:</strong> ID del comercio obtenido en Openpay en la ruta <strong>Inicio > Configuraciones (icono engrane) > Credenciales API</strong>
	</blockquote>
	</li>
	<li type="disc"><p> <strong>Eventos asociados:</strong> Se sugiere dejar el valor por default <strong>(Todos los eventos)</strong> pero en caso de no querer recibir todas las notificaciones, hacer click en <strong>Personalizar eventos</strong> y seleccionar solo los deseados (es obligatorio seleccionar al menos Cargos > Completados)</p>
	<blockquote>
	<p><strong>3D Secure</strong>: Para los comercios que cuenten con 3D Secure activo, seleccionar Cargos > Completados, Fallidos y Cancelados.</p>
	</blockquote>
	</li>
	<li type="disc"> <strong>Usar autenticación de acceso básica:</strong> Seleccionar este campo, capturar los datos solicitados y hacer click en el botón <strong>Guardar</strong>
	</li>
	 <center style="margin:10px 0;"><img src="/images/plugins/vtex_create_webhook.png"></center>
	</ol>
	<br>
<strong>¿Cómo obtener usuario y contraseña para dar de alta una webhook?</strong>
<blockquote>
	<ol type="a">
	<li>Ir a <a href="https://vtex.com/">Vtex</a> e ingresar con usuario Owner
	</li>
	<li>Ir al path Gestión de la cuenta > Cuentas > Openpay
	<br>
	<br>
	<center><img src="/images/plugins/vtex_openpay_23.png" style="width: 100%;"></center>
	<br>
	</li>
	<li>Una  vez  que  el  Owner  genere  una  Cuenta  y  Administre  el  Permiso,  se  mostrará por <strong>una  sola  ocasión</strong>  una  clave que deberá <strong>guardar</strong>
	</li>
	<li>En el formulario de Openpay (<a href="sandbox-dashboard.openpay.mx/login">Sandbox</a> / <a href="https://dashboard.openpay.mx/login">Produccion</a>)para dar de alta un webhook, capturar en el campo usuario el Access key y en el campo contraseña la cadena larga obtenidos en el paso anterior
	</li>
	</ol>
</blockquote>
</li>
</ol>


Una vez creado el webhook se debe <strong>informar al administrador de Openpay</strong> para actualizar el estado de de la URL a “Verificado”


<img src="/images/plugins/vtex_openpay_26.png">

 <br>
 <br>
 <br>
