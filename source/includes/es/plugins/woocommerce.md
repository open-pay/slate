---
layout: faq
title:  WooCommerce
category: plugin
tags: plugin
lang: es
---

#WooCommerce

**¿Qué es WooCommerce?**

WooCommerce es un plugin para sitios basados en WordPress que le permite a sus usuarios convertirlos en comercios electrónicos de manera fácil y rápida.

Los plugins de Openpay para WooCommerce le permite configurar y añadir nuestros métodos de pago soportados (tarjeta de crédito/débito, tiendas de conveniencia y SPEI) dentro del flujo compra de su tienda en línea.

<div class="boton-grp boton-plugin">
<!--div class="blu-boton"><a href="https://github.com/open-pay/openpay-woocommerce/blob/master/openpay-cards.zip?raw=true">Plugin Tarjetas</a></div-->
<!--div class="blu-boton"><a href="https://github.com/open-pay/openpay-woocommerce/blob/master/openpay-stores.zip?raw=true">Plugin Tiendas</a></div-->
</div>
<div class="boton-grp boton-plugin">
<div class="blu-boton"><a href="https://github.com/open-pay/openpay-wordpress" target="_blank">Ver en GitHub</a></div>
</div>

Requerimientos
----------

Es necesario que el servidor donde se encuentre alojada su tienda de WordPress cuente con las siguientes características:

* Versión instalada de **PHP 5.6** o mayor.
* Versión instalada de **MySQL 5.0** o mayor.
* Extensión de **Apache mod_rewrite** habilitada.
* Versión instalada de **WordPress 4.9** o mayor.
* Versión instalada del plugin **WooCommerce hasta 4.0.0**.
* Extensión de **PHP CURL** habilitada.
* Contar con un **certificado SSL** para su comercio electrónico.

Instalación
----------

<ol class="installation">
<li>En su panel de administración de WordPress, dirigirse a la sección <strong>Plugins -> Add New</strong>, ubicado en el menú lateral.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_install_01.png" alt="Instalación de plugin WooCommerce paso 2" title="Paso 2"></center>
<li>En el buscador, escribe la palabra clave <strong>Openpay</strong> para buscar las opciones de pago disponibles. </li>
<center style="padding-right:40px; margin:10px 0;"><img src="/img/plugins/woocommerce_install_02.png" alt="Instalación de plugin WooCommerce paso 3" title="Paso 3" style="width: 100%;"></center>
<li>En los resultados de la búsqueda, identifica el plugin del método de pago deseado y hacer clic en <strong>Install Now.</strong>. Al terminar la instalación, se debe <strong>activar el plugin</strong>.</li>
<div class="row installation__step3">
    <div class="col-xl-6 col-lg-6 col-md-6 col-sm-12 col-xs-12">
        <center style="margin:10px 0;"><img src="/img/plugins/woocommerce_install_03.png" alt="Instalación de plugin WooCommerce paso 4" title="Paso 4" class="installation__image"></center>
    </div>
    <div class="col-xl-6 col-lg-6 col-md-6 col-sm-12 col-xs-12">
        <center style="margin:10px 0;"><img src="/img/plugins/woocommerce_install_04.png" alt="Instalación de plugin WooCommerce paso 5" title="Paso 5" class="installation__image"></center>
    </div>
</div>

</ol>

Configuración
----------

<ol>
<li>En su panel de administración de WordPress, dirigirse a la sección <strong>WooCommerce -> Settings</strong>, ubicado en el menú lateral.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_01.png" alt="Configuración de plugin WooCommerce paso 1" title="Paso 1"></center>
<li>Modificar el valor <strong>Currency</strong> del formulario por la opción <strong>Mexican Peso ($)</strong>. Guardar los cambios mediante el botón <strong>Save changes</strong> ubicado al final del formulario.</li>
<center style="margin:10px 0;"><img src="/img/plugins/subscriptions_config_02.png" style="" alt="Configuración de plugin WooCommerce paso 2" title="Paso 2"></center>
<li>Para activar y desactivar las opciones de <strong>pagos</strong>, deberá seguir los siguientes pasos.</li>
<center style="padding-right:40px; margin:10px 0;"><img src="/img/plugins/woocommerce_config_03.png" alt="Configuración de plugin WooCommerce paso 3" title="Paso 3" style="width:100%;"></center>
<ol type="a">
    <li>Dirigirse a la pestaña <strong>Payments</strong> ubicada en la parte superior de las configuraciones de Woocommerce.</li>
    <li>Activar la opción de <strong>pago</strong> deseada.</li>
    <li>Dar clic en el bóton <strong>Manage</strong> para comenzar con la configuración.</li>
</ol>
<li>Identificar las credenciales de API asignadas a su comercio dentro del panel de administración de Openpay.</li>
<center style="margin:10px 0;"><img src="/img/plugins/prestashop_config_01.png" alt="Configuración de plugin WooCommerce paso 4" title="Paso 4"></center>
<blockquote>
<p>Para ver las credenciales, dar clic en el engrane del menú superior derecho y luego seleccionar la opción <strong>Credenciales de API</strong></p>
</blockquote>
<li>Completar la configuración del apartado de Openpay, contemplando los siguientes tópicos:</li>
<ul>
<li><strong>Habilitar módulo</strong>: Habilita el uso de Openpay como plataforma de pagos.</li>
<li><strong>Modo de pruebas</strong>: Determina si el plugin va a funcionar en entorno de pruebas (Sandbox) o Producción.</li>
<li><strong>Credenciales de Openpay (Merchant ID, Secret Key, Public Key)</strong>: Credenciales de API para utilizar el plugin (ya sea en modo Sandbox o Producción). Copiar y pegar cada dato (obtenido en el Paso anterior) como corresponda.</li>
</ul>
<div class="row justify-content-center">
  <div class="col-xl-8 col-lg-8 col-md-8 col-sm-12 col-xs-12">
      <center style="margin:10px 0;"><img src="/img/plugins/woocommerce_config_05.png" alt="Configuración de plugin WooCommerce paso 4" title="Paso 5" style="width:100%;"></center>
  </div>
</div>
<ul class="nav nav-tabs" id="myTab" role="tablist">
  <li class="nav-item">
    <a class="nav-link active" id="card-tab" data-toggle="tab" href="#card" role="tab" aria-controls="card" aria-selected="true">Cards</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" id="store_spei-tab" data-toggle="tab" href="#store_spei" role="tab" aria-controls="store_spei" aria-selected="false">Tiendas / SPEI</a>
  </li>
</ul>
<div class="tab-content" id="paymentMethods">
  <div class="tab-pane fade show active" id="card" role="tabpanel" aria-labelledby="card-tab">
  <div class="row align-items-center">
     <div class="col-xl-7 col-lg-7 col-md-12 col-sm-12 col-xs-12">
      <ul>
        <li><strong>¿Cómo procesar el cargo?</strong>: Define el tipo de cargo que se realizará:</li>
        <ul>
            <li><strong>Directo</strong>: Se realizará una evaluación del cargo y se rechazará si el sistema antifraude detectó alguna anomalía.</li>
            <li><strong>3D Secure</strong>: Se realizará un redireccionamiento al banco para que el cliente sea autenticado en su banco.</li>
            <li><strong>Autenticación selectiva</strong>: Se realizará una evaluación del cargo y si el sistema antifraude detecta alguna anomalía, se ejecutará un cargo 3D secure.</li>
        </ul>
        <li><strong>Configuración del cargo</strong>: Indica si el cargo se hace o no inmediatamente.</li>
        <li><strong>Pago con puntos</strong>: Recibe pagos con Puntos BBVA. </li>
        <li><strong>Guardar tarjetas</strong>: Habilita el guardado de tarjetas de crédito. </li>
        <li><strong>Meses sin intereses</strong>: Puede hablitar o deshabilitar pagos con tarjeta con meses sin intereses seleccionando 3,6,9,12 y/o 18 meses sin intereses.</li>
        <li><strong>Monto mínimo MSI</strong>: Define el monto mínimo de pago para meses sin intereses. </li>
      </ul>
     </div>
      <div class="col-xl-5 col-lg-5 col-md-12 col-sm-12 col-xs-12">
         <center style="margin:10px 0;"><img src="/img/plugins/woocommerce_config_05_1.png" alt="Configuración de plugin WooCommerce paso 5" title="Paso 5" style="width: 100%;"></center>
      </div>
    </div>
  </div>
  <div class="tab-pane fade" id="store_spei" role="tabpanel" aria-labelledby="store_spei-tab">
    <div class="row align-items-center">
      <div class="col-xl-7 col-lg-7 col-md-12 col-sm-12 col-xs-12">
        <ul>
          <li><strong>Fecha límite de pago</strong>: Defina la cantidad de horas de validez para realizar un pago de Tiendas de Conveniencia y SPEI.</li>
          <li><strong>Mostrar mapa</strong>: Muestra las tiendas más cercanas al momento de generar el recibo de pago.</li>
        </ul>
      </div>
      <div class="col-xl-5 col-lg-5 col-md-12 col-sm-12 col-xs-12">
        <center style="margin:10px 0;"><img src="/img/plugins/woocommerce_config_05_2.png" alt="Configuración de plugin WooCommerce paso 5" title="Paso 5" style="width: 100%;"></center>
      </div>
    </div>
  </div>
</div>
<li>Guardar los cambios en la configuración dando clic sobre el botón <strong>Save changes</strong> ubicado al final del formulario.</li>
<center style="margin:10px 0;"><img src="/img/plugins/woocommerce_config_06.png" alt="Configuración de plugin WooCommerce paso 6" title="Paso 6" ></center>
</ol>
