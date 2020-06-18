---
layout: faq
title:  Shopify
category: plugin
tags: plugin
lang: es
---

#Shopify

**¿Qué es Shopify?**

Shopify es una plataforma de e-commerce que le permite crear, configurar y poner en funcionamiento su propia tienda en línea de manera fácil y rápida.

Se ha desarrollado una aplicación para Shopify que le permitirá usar nuestros métodos de pago dentro de su comercio. De esta forma sus clientes, al finalizar su compra, podrán obtener una ficha de pago para el método de pago elegido; por otro lado, su tienda de Shopify será notificada automáticamente una vez que se haya realizado un pago.

<div class="boton-grp boton-plugin">
	<div class="blu-boton">
	<!-- https://apps.shopify.com/openpay-online-payments -->
		<a href="https://www.shopify.com/login?redirect=authorize_gateway%2F1041416" target="_blank">
			Ver Aplicación
		</a>
	</div>
</div>

Requerimientos
----------

* Contar con una tienda en Shopify (https://es.shopify.com/).

Instalación
----------

<ol>
<li>Iniciar sesión con su tienda de Shopify</li>
<li>En el menú lateral, dirigirse a "Apps". En la esquina superior derecha, clic en "Visitar App Store".</li>
<center style="margin:10px 0;"><img src="/img/plugins/shopify_install_01.png" alt="Instalación de app Shopify paso 2" title="Paso 2"><img src="/img/plugins/shopify_install_02.png" alt="Instalación de app Shopify paso 2" title="Paso 2" style="margin-left:20px;"></center>
<li>En el campo de búsqueda ingresar <strong>Openpay Online Payments</strong> y dar clic sobre el resultado que aparezca.</li>
<li>Dar clic en el botón <strong>"Get"</strong> ubicado a la derecha.</li>
<center style="margin:10px 0;"><img src="/img/plugins/shopify_install_03.png" alt="Instalación de app Shopify paso 4" title="Paso 4"></center>
<li>Finalmente, clic en el botón <strong>Install App</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/shopify_install_04.png" alt="Instalación de app Shopify paso 5" title="Paso 5"></center>
</ol>

Configuración
----------

<ol>
<li>En el panel de administración de su tienda Shopify, dirigirse a <strong>Settings -> Payments</strong>.</li>
<li>Buscar la sección <strong>Manual Payments</strong> y seleccionar la opción <strong>Create a new custom payment method</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/shopify_config_01.png" alt="Configuración de app Shopify paso 2" title="Paso 2"></center>
<li>Por cada método de pago que quiera habilitar tome en cuenta lo siguiente:</li>
<ul>
<li>El <strong>Nombre</strong> del método de pago se muestra dentro del flujo de compra de un Cliente, elija un nombre corto que identifique fácilmente el tipo de pago.</li>
<li>Los <strong>Detalles adicionales</strong> se muestran junto con el Nombre del método de pago, su intención es describir cómo funciona dicho método, de esta forma el Cliente pueda determinar si le conviene utilizarlo o no.</li>


</ul>
<li>Diríjase a la configuración de la aplicación Openpay, ubicada en <strong>Apps -> Installed</strong>. Complete el formulario considerando lo siguiente:</li>
<ul>
<li>Seleccione el <strong>Modo de Operación</strong> de la aplicación. Utilice <strong>Modo Sandbox</strong> sólo para realizar pruebas.</li>
<li>Ingrese sus credenciales <strong>Merchant ID y Secret Key</strong> de Openpay para cada ambiente. Puede obtener dichas credenciales en su <a href="https://dashboard.openpay.mx/" target="_blank">Dashboard</a>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/api_keys_config.png" alt="Api Keys" title="Openpay"></center>

</ul>
<li>Presione el botón <strong>Guardar</strong>, ubicado en la esquina superior derecha, para guardar los cambios realizados en su configuración.</li>
<center style="margin:10px 0;"><img src="/img/plugins/shopify_config_02.png" alt="Configuración de app Shopify paso 4" title="Paso 4"></center>
</ol>

#Shopify pagos con Tarjeta

Configuración
----------

<ol>
	<li>Da click en el siguiente botón para habilitar los pagos con tarjeta a través de Openpay.</li>
	<center style="margin-top:10px;margin-bottom:10px;">
		<div class="blu-boton">
			<a href="https://www.shopify.com/login?redirect=authorize_gateway%2F1041416" target="_blank">Habilitar Pagos con tarjeta.</a>
		</div>
	</center>
	<li>Presiona el botón <strong>Add payment gateway</strong>.</li>
	<center style="margin:10px 0;"><img src="/img/plugins/shopify_config_03.png" alt="Configuración de app Shopify tarjetas paso 2" title="Paso 2"></center>
	<li>Utilice sus credenciales <strong>Merchant ID y Secret Key</strong> de Openpay para cada ambiente. Puede obtener dichas credenciales en su <a href="https://dashboard.openpay.mx/" target="_blank">Dashboard</a>.</li>
	<center style="margin:10px 0;"><img src="/img/plugins/api_keys_config.png" alt="Api Keys" title="Openpay"></center>
	<li>Ingresa el <strong>Merchant ID</strong> y <strong>Private Key</strong>.</li>
	<li>Selecciona la casilla <strong>Use test mode</strong> para operar en el entorno Sandbox con las credenciales de pruebas.</li>
	<center style="margin:10px 0;"><img src="/img/plugins/shopify_config_cc.png" alt="Configuración de tarjetas de crédito" title="Paso 2"></center>
	<li>Por último presiona el botón <strong>Actvate</strong>.</li>
</ol>
