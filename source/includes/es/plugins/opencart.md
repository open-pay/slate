---
layout: faq
title:  OpenCart
category: plugin 
tags: plugin
lang: es
---

#OpenCart

**¿Qué es OpenCart?**

OpenCart es una solución gratuita basada en Web diseñada para poner en marcha un comercio electrónico con el mínimo de configuraciones y ajustes requeridos.

Ponemos a su disposición nuestro plugin para OpenCart, el cual le permitirá configurar y añadir los métodos de pago soportados en Openpay (tarjeta de crédito/débito, tiendas de conveniencia y SPEI) dentro del flujo compra de su tienda basada en esta plataforma.

<div class="boton-grp boton-plugin">
<div class="blu-boton"><a href="https://github.com/open-pay/openpay-opencart/archive/master.zip">Descargar Plugin</a></div>
<div class="blu-boton"><a href="https://github.com/open-pay/openpay-opencart">Ver en GitHub</a></div>
</div>

Los plugins de Openpay descargados vienen organizados de la siguiente manera:

|Plugin    |Descripción
|----------|-----------
|**OpenpayBanks.ocmod.zip**  |Contiene el plugin para generar referencias de cobro que podrán ser pagadas por transferencia bancaria (SPEI)
|**OpenpayCards.ocmod.zip**   |Contiene el plugin para aceptar pagos con tarjeta de crédito o débito
|**OpenpayStores.ocmod.zip** |Contiene el plugin para generar referencias de cobro que podrán ser pagadas en tiendas de conveniencia

> **Nota:** Solo debe instalar los plugins para los métodos de pago que desee habilitar en su comercio.

Versiones soportadas
----------

* **OpenCart** 2.0.1.1 en adelante

Requerimientos
----------

Es necesario que el servidor donde se encuentre alojado su comercio de OpenCart cuente con las siguientes configuraciones:

* Servidor web Apache
* Versión instalada de **PHP 5.2** o mayor.
* Versión instalada de **MySQL 5.0** o mayor.
* Contar con un **certificado SSL** para su comercio electrónico.

Adicionalmente para la versión de PHP es necesario que cuente con ciertas características:

* Configuración **Register Globals** deshabilitada.
* Configuración **Magic Quotes GPC** deshabilitada.
* Configuración para subida de archivos habilitada.
* Configuración **Session Auto Start** deshabilitada.
* Extensión **GD (con procesamiento de imágenes PNG)** habilitada.
* Extensión **cURL** habilitada.
* Extensión **ZIP** habilitada.

Instalación
----------

Para instalar los plugins de Openpay en su comercio de OpenCart tiene que seguir los siguientes pasos:

> **Nota:** La siguiente secuencia debe realizarse por cada plugin que se desee instalar.

<ol>
<li>Descargar el archivo ZIP que contiene todos los plugins. Puede descargar los plugins a través de <a href="https://github.com/open-pay/openpay-opencart/archive/master.zip">este enlace</a>.</li>
<li>Descomprimir el archivo descargado. Dentro de la carpeta obtenida, descomprimir el archivo <strong>openpay_opencart_plugin_1.0.zip</strong>. Consultar la carpeta final resultante.</li>
<center style="margin:10px 0;"><img src="/img/plugins/opencart_install_05.png" alt="Instalación de plugin OpenCart paso 2" title="Paso 2"></center>
<li>En su panel de administración de OpenCart, dirigirse a la sección <strong>Extensions -> Extension Installer</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/opencart_install_01.png" alt="Instalación de plugin OpenCart paso 3" title="Paso 3"></center>
<li>Clic en el botón <strong>Upload</strong> y seleccionar el archivo ZIP del plugin del método de pago que desee instalar. El plugin comenzará a subirse al portal automáticamente.</li>
<center style="margin:10px 0;"><img src="/img/plugins/opencart_install_02.png" alt="Instalación de plugin OpenCart paso 4" title="Paso 4"></center>
<blockquote>
<p>Si al instalar el plugin aparece el error <strong>FTP needs to be enabled in the settings</strong>, es necesario aplicar un fix que puede ser descargado a través de <a href="http://www.opencart.com/index.php?route=extension/extension/info&extension_id=18892">este enlace</a>. Seguir las instrucciones proporcionadas en ese mismo sitio para aplicar exitosamente el ajuste.</p>
</blockquote>
<li>Ir a la sección <strong>Extensions -> Payments</strong>, ubicar en el listado el plugin recién subido y dar clic en la opción <strong>Install</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/opencart_install_03.png" alt="Instalación de plugin OpenCart paso 5" title="Paso 5"></center>
<li>Confirmar que el plugin se haya instalado exitosamente.</li>
<center style="margin:10px 0;"><img src="/img/plugins/opencart_install_04.png" alt="Instalación de plugin OpenCart paso 6" title="Paso 6"></center>
</ol>

Configuración
----------

> **Nota:** La siguiente secuencia debe realizarse por cada plugin que se desee instalar.

<ol>
<li>Identificar las credenciales de API asignadas a su comercio dentro del panel de administración de Openpay.</li>
<center style="margin:10px 0;"><img src="/img/plugins/prestashop_config_01.png" alt="Configuración de plugin OpenCart paso 1" title="Paso 1"></center>
<blockquote>
<p>Para ver las credenciales, dar clic en el engrane del menú superior derecho y luego seleccionar la opción <strong>Credenciales de API</strong>.</p>
</blockquote>
<li>En su panel de administración de OpenCart, dirigirse a la sección <strong>Extensions -> Payments</strong>. Ubicar el plugin instalado recientemente y dar clic en la opción <strong>Edit</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/opencart_config_01.png" alt="Configuración de plugin OpenCart paso 2" title="Paso 2"></center>
<li>Completar el formulario de configuración contemplando los siguientes puntos:</li>
<ul>
<li><strong>Test mode:</strong> Define si el plugin estará trabajando en entorno de pruebas o producción.</li>
<blockquote>
<p>Las credenciales de API que utilizará el plugin (ya sea de pruebas o producción) se tomarán con base a lo seleccionado en este campo.</p>
</blockquote>
<li><strong>Test Merchant ID, Secret Key, Publishable Key:</strong> Credenciales de API (ver paso 1) de la cuenta de Openpay del comercio, en entorno de pruebas.</li>
<li><strong>Live Merchant ID, Secret Key, Publishable Key:</strong> Credenciales de API (ver paso 1) de la cuenta de Openpay del comercio, en entorno de producción.</li>
<li><strong>Title:</strong> Nombre del método de pago a mostrar a los usuarios al momento de realizar una compra.</li>
<li><strong>Status:</strong> Determina si el método de pago estará disponible dentro del flujo de compra de tus cliente.</li>
<li><strong>Total:</strong> Monto mínimo de la compra para que el método de pago pueda ser utilizado.</li>
<li><strong>Deadline to pay (hours):</strong> Cantidad de horas que tiene el cliente para realizar el pago, una vez generado el pedido.</li>
<li><strong>Status - Authorized:</strong> Seleccionar <strong>Complete</strong>.</li>
<li><strong>Status - Captured:</strong> Seleccionar <strong>Pending</strong>.</li>
</ul>
<li>Guardar los cambios usando el botón ubicado en la esquina superior derecha de la pantalla.</li>
<center style="margin:10px 0;"><img src="/img/plugins/opencart_config_02.png" alt="Configuración de plugin OpenCart paso 4" title="Paso 4"></center>
<li>Confirmar que la configuración del plugin haya sido guardada exitosamente.</li>
<center style="margin:10px 0;"><img src="/img/plugins/opencart_config_03.png" alt="Configuración de plugin OpenCart paso 5" title="Paso 5"></center>
</ol>