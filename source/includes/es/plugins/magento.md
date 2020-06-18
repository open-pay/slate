---
layout: faq
title:  Magento
category: plugin
tags: plugin
lang: es
---

#Magento

**¿Qué es Magento?**

Magento es una plataforma que permite la gestión de contenidos web para un comercio electrónico, ofreciendo una solución flexible y escalable sobre la cual se puede basar cualquier proyecto de tienda en línea.

El plugin de Openpay para Magento le permite configurar y añadir nuestros métodos de pago soportados (tarjeta de crédito/débito, tiendas de conveniencia y SPEI) dentro del flujo compra de su comercio electrónico.

<section class="magento">
    <div class="alert alert-warning magento__warning" role="alert">
        <p>Por motivos de seguridad, a partir del <strong>30 de junio del 2020</strong> Openpay dejará de soportar las actualizaciones de Magento 1. Invitamos a los usuarios a migrar sus plataforma a la brevedad antes de ser vulnerables a violaciones de seguridad que nos impidan ofrecerles el servicio.</p>
    </div>
</section>

Versiones soportadas
----------

* **Magento Community Edition** 1.9.2.4 en adelante

Plugins One-Page Checkout Soportados
----------

<ul>
<li><a href="https://www.magentocommerce.com/magento-connect/one-page-checkout.html" target="_blank">IWD One Page Checkout</a></li>
<li><a href="http://www.onestepcheckout.com/" target="_blank">OneStepCheckout</a></li>
<li><a href="https://store.onlinebizsoft.com/one-step-checkout.html" target="_blank">One Step Checkout OnlinebizSoft</a></li>
</ul>

Requerimientos
----------

Es necesario que el servidor donde se encuentre alojado su comercio electrónico basado en Magento cuente con las siguientes características:

* Versión instalada de **PHP 5.4** o mayor.
* Versión instalada de **MySQL 5.0** o mayor.
* Contar con un **certificado SSL** para su comercio electrónico.

Instalación
----------

<ol>
<li>Descargar el archivo ZIP con los contenidos del plugin. Puede descargar el plugin a través de <a href="https://github.com/open-pay/openpay-magento/blob/master/Openpay_Charges-2.0.0.tgz?raw=true">este enlace</a>.</li>
<li>En su panel de administración de Magento, dirigirse a la sección <strong>System -> Magento Connect -> Magento Connect Manager</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/magento_install_01.png" alt="Instalación de plugin Magento paso 2" title="Paso 2"></center>
<li>Cargar el archivo descargado en el Paso 1 dentro del formulario de la sección <strong>Manage Existing Extensions</strong>, dar clic en <strong>Upload</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/magento_install_02.png" alt="Instalación de plugin Magento paso 3" title="Paso 3"></center>
<li>Confirmar la instalación del plugin.</li>
<center style="margin:10px 0;"><img src="/img/plugins/magento_install_03.png" alt="Instalación de plugin Magento paso 4" title="Paso 4"></center>
</ol>

Configuración
----------

<ol>
<li>Identificar las credenciales de API asignadas a su comercio dentro del panel de administración de Openpay.</li>
<center style="margin:10px 0;"><img src="/img/plugins/prestashop_config_01.png" alt="Configuración de plugin Magento paso 1" title="Paso 1"></center>
<blockquote>
<p>Para ver las credenciales, dar clic en el engrane del menú superior derecho y luego seleccionar la opción <strong>Credenciales de API</strong></p>
</blockquote>
<li>En su panel de administración de Magento, dirigirse a la sección <strong>System -> Configuration</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/magento_config_01.png" alt="Configuración de plugin Magento paso 2" title="Paso 2"></center>
<li>Expandir el apartado <strong>States Options</strong> y seleccionar todos los países a los cuales desea vender. Guardar los cambios mediante el botón <strong>Save Config</strong>, ubicado en la esquina superior derecha de la pantalla.</li>
<center style="margin:10px 0;"><img src="/img/plugins/magento_config_05.png" alt="Configuración de plugin Magento paso 3" title="Paso 3"></center>
<li>Dar clic en el enlace <strong>Sales -> Payment Methods</strong>, ubicado en el menú lateral.</li>
<center style="margin:10px 0;"><img src="/img/plugins/magento_config_02.png" alt="Configuración de plugin Magento paso 4" title="Paso 4"></center>
<li>Completar el apartado <strong>Openpay - Configuración General</strong> contemplando los siguientes tópicos:</li>
<ul>
<li><strong>Modo pruebas (Sandbox)</strong>: Determina si el plugin va a funcionar en entorno de pruebas (seleccionando <strong>Enable</strong>) o Producción (seleccionando <strong>Disable</strong>).</li>
<li><strong>Llave pública, ID de comercio, Llave privada</strong>: Credenciales de API para utilizar el plugin (ya sea en modo Sandbox o Producción). Copiar y pegar cada dato (obtenido en el Paso 1) como corresponda.</li>
</ul>
<center style="margin:10px 0;"><img src="/img/plugins/magento_config_03.png" alt="Configuración de plugin Magento paso 5" title="Paso 5"></center>
<li>Completar el apartado <strong>Openpay - Tarjetas de crédito y débito</strong> utilizando como referencia la siguiente imagen:</li>
<center style="margin:10px 0;"><img src="/img/plugins/magento_config_04.png" alt="Configuración de plugin Magento paso 6" title="Paso 6"></center>
<blockquote>
<p>El campo <strong>Enabled</strong> determina si aceptará el comercio como método de pago tarjetas de crédito y débito.</p>
</blockquote>
<li>Completar el apartado <strong>Openpay - Tiendas de Conveniencia</strong> utilizando como referencia la siguiente imagen:</li>
<center style="margin:10px 0;"><img src="/img/plugins/magento_config_06.png" alt="Configuración de plugin Magento paso 7" title="Paso 7"></center>
<blockquote>
<p>El campo <strong>Enabled</strong> determina si aceptará el comercio como método de pago en tiendas de conveniencia.</p>
</blockquote>
<li>Completar el apartado <strong>Openpay - Transferencias Interbancarias (SPEI)</strong> utilizando como referencia la siguiente imagen:</li>
<center style="margin:10px 0;"><img src="/img/plugins/magento_config_07.png" alt="Configuración de plugin Magento paso 8" title="Paso 8"></center>
<blockquote>
<p>El campo <strong>Enabled</strong> determina si aceptará el comercio como método de pago por transferencia interbancaria.</p>
</blockquote>
<li>Guardar los cambios mediante el botón <strong>Save Config</strong>, ubicado en la esquina superior derecha de la pantalla.</li>
</ol>

Notificaciones de pago en tienda y SPEI
----------
> **Importante:** Dependiendo del tipo de notificación que se configure se deben utilizar la siguientes URLs:

{% highlight html %}
Store payments -> https://[eCommerce domain]/stores/payments/confirm
​SPEI (wire transfer) -> https://[eCommerce domain]/banks/payments/confirm
{% endhighlight %}

> **Importante:** Es necesario verificar que el Webhook haya sido creado de forma correcta en Openpay.

<ol>
<li>En su panel de configuración de Openpay ir a <strong>Ajustes (ícono de engrane) -> Configuraciones</strong>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/woocommerce_webhook_02.png" alt="Configuración de notificaciones Magento paso 1" title="Paso 1"></center>
<li>Ubicar el apartado de <strong>Webhooks</strong>. Si el webhook fue configurado correctamente habrá un registro en estado <b>Verificado</b>.</li>
<center style="margin:10px 0;"><img src="/img/plugins/webhook_verificado.png" alt="Configuración de notificaciones Magento paso 2" title="Paso 2"></center>
</ol>
