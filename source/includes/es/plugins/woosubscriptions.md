---
layout: faq
title:  WooSubscriptions
category: plugin 
tags: plugin
lang: es
---

#WooSubscriptions

**¿Qué es WooCommerce Subscriptions?**

WooSubscriptions ofrece un conjunto de herramientas para su comercio en WordPress que le permitirán vender productos o servicios bajo la modalidad pagos recurrentes. Es decir, el cliente realiza la compra de un artículo una sola vez y WooSubscriptions se encarga de gestionar los cargos correspondientes de manera automática y periódica.

Nuestro plugin para WooSubscriptions le permite configurar su comercio para que pueda utilizar a Openpay como la plataforma de pagos para validar y procesar dichos cargos recurrentes.

<div class="boton-grp boton-plugin">
<div class="blu-boton"><a href="https://github.com/open-pay/openpay-woosubscriptions/archive/master.zip">Descargar Plugin</a></div>
<div class="blu-boton"><a href="https://github.com/open-pay/openpay-woosubscriptions">Ver en GitHub</a></div>
</div>

Versiones soportadas
----------

* **WordPress** 3.8 en adelante
* Plugin **WooCommerce** 2.0 en adelante
* Plugin **WooSubscriptions** 1.5 en adelante

Requerimientos
----------

Es necesario que el servidor donde se encuentre alojado su tienda de WordPress cuente con las siguientes características:

* Versión instalada de **PHP 5.2.4** o mayor.
* Versión instalada de **MySQL 5.0** o mayor.
* Extensión de **Apache mod_rewrite** habilitada.
* Versión instalada de **WordPress 3.8** o mayor.
* Versión instalada del plugin **WooCommerce 2.0** o mayor.
* Versión instalada del plugin **WooSubscriptions 1.5** o mayor.
* Extensión de **PHP CURL** habilitada.
* Contar con un **certificado SSL** para su comercio electrónico.

Instalación
----------

Para instalar el plugin de Suscripciones Openpay en su comercio de WordPress tiene que seguir los siguientes pasos:

<ol>
<li>Descargar el archivo ZIP con los contenidos del plugin. Puede descargar el plugin a través de <a href="https://github.com/open-pay/openpay-woosubscriptions/archive/master.zip">este enlace</a>.</li>
<li>En su panel de administración de WordPress, dirigirse a la sección <strong>Plugins -> Add New</strong>, ubicado en el menú lateral.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_install_01.png" alt="Instalación de plugin Suscripciones paso 2" title="Paso 2"></center>
<li>Dar clic en la opción <strong>Upload Plugin</strong>, ubicado en la parte superior de la pantalla.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_install_02.png" alt="Instalación de plugin Suscripciones paso 3" title="Paso 3"></center>
<li>Ubicar el archivo ZIP descargado en el paso 1 y proporcionarlo al formulario de instalación de plugins. Dar clic en el botón <strong>Install Now</strong></li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_install_03.png" alt="Instalación de plugin Suscripciones paso 4" title="Paso 4"></center>
<li>Confirmar que el plugin haya sido instalado correctamente.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_install_04.png" alt="Instalación de plugin Suscripciones paso 5" title="Paso 5"></center>
</ol>

Configuración
----------

<ol>
<li>En su panel de administración de WordPress, dirigirse a la sección <strong>WooCommerce -> Settings</strong>, ubicado en el menú lateral.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_01.png" alt="Configuración de plugin Suscripciones paso 1" title="Paso 1"></center>
<li>Modificar el valor <strong>Currency</strong> del formulario por la opción <strong>Mexican Peso ($)</strong>. Guardar los cambios mediante el botón <strong>Save changes</strong> ubicado al final del formulario.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_02.png" alt="Configuración de plugin Suscripciones paso 2" title="Paso 2"></center>
<li>Identificar las credenciales de API asignadas a su comercio dentro del panel de administración de Openpay.</li>
<center style="margin:10px 0;"><img src="/img/plugins/prestashop_config_01.png" alt="Configuración de plugin Suscripciones paso 3" title="Paso 3"></center>
<blockquote>
<p>Para ver las credenciales, dar clic en el engrane del menú superior derecho y luego seleccionar la opción <strong>Credenciales de API</strong></p>
</blockquote>
<li>En su panel de administración de WordPress, dirigirse a la sección <strong>Plugins -> Installed Plugins</strong>, ubicado en el menú lateral.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_03.png" alt="Configuración de plugin Suscripciones paso 4" title="Paso 4"></center>
<li>Ubicar el elemento <strong>Openpay WooSubscriptions</strong> dentro del listado de plugins instalados. Dar clic en el vínculo <strong>Activate</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_04.png" alt="Configuración de plugin Suscripciones paso 5" title="Paso 5"></center>
<li>Volver a consultar el listado de plugins instalados y dar clic en la opción <strong>Settings</strong> del plugin.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_05.png" alt="Configuración de plugin Suscripciones paso 6" title="Paso 6"></center>
<li>Dar clic en la opción <strong>Openpay</strong>, ubicado en la parte inferior derecha de la pantalla (en la pestaña <strong>Checkout</strong>).</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_06.png" alt="Configuración de plugin Suscripciones paso 7" title="Paso 7"></center>
<li>Completar el formulario de configuración contemplando los siguientes tópicos:</li>
<ul>
<li><strong>Enable/Disable</strong>: Habilita el uso de Openpay como plataforma de pagos.</li>
<li><strong>Title, Description</strong>: Campos de texto informativo que se le muestran al usuario durante su compra.</li>
<li><strong>Sandbox mode</strong>: Determina si el plugin va a funcionar en entorno de pruebas (Sandbox) o Producción.</li>
<li><strong>Production Merchant ID, Secret Key, Public Key</strong>: Credenciales de API para utilizar el plugin en entorno productivo.</li>
<li><strong>Sandbox Merchant ID, Secret Key, Public Key</strong>: Credenciales de API para utilizar el plugin en entorno de pruebas (Sandbox).</li>
<li><strong>Openpay Checkout Image</strong>: URL a una imagen decorativa referente al método de pago que se le presenta al usuario durante el proceso de compra.</li>
<blockquote>
<p>Para esta imagen se recomienda utilizar la siguiente URL: <strong>http://www.openpay.mx/img/logo.png</strong></p>
</blockquote>
</ul>
<li>Guardar los cambios en la configuración dando clic sobre el botón <strong>Save changes</strong> ubicado al final del formulario.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_07.png" alt="Configuración de plugin Suscripciones paso 9" title="Paso 9"></center>
<li>En la pantalla de ajustes del plugin, dar clic en la opción <strong>Checkout Options</strong>, ubicado en la parte inferior izquierda de la pantalla (en la pestaña <strong>Checkout</strong>).</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_08.png" alt="Configuración de plugin Suscripciones paso 10" title="Paso 10"></center>
<li>En la sección <strong>Payment Gateways</strong> (al final de la pantalla) marcar la opción <strong>Tarjeta de crédito o débito (Openpay)</strong> y guardar los cambios mediante el botón <strong>Save Changes</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_09.png" alt="Configuración de plugin Suscripciones paso 11" title="Paso 11"></center>
</ol>
