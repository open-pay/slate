---
layout: faq
title:  Magento 2
category: plugin
tags: plugin
lang: es
---

#Magento 2

**¿Qué es Magento?**

Magento es una plataforma que permite la gestión de contenidos web para un comercio electrónico, ofreciendo una solución flexible y escalable sobre la cual se puede basar cualquier proyecto de tienda en línea.

El plugin de Openpay para Magento le permite configurar y añadir nuestros métodos de pago soportados (tarjeta de crédito/débito, tiendas de conveniencia y SPEI) dentro del flujo compra de su comercio electrónico.


Versiones soportadas
----------
* **Magento Community Edition** 2.1.1 en adelante


Requerimientos
----------
Es necesario que el servidor donde se encuentre alojado su comercio electrónico basado en Magento 2 cuente con las siguientes características:

* Versión instalada de **PHP 5.4** o mayor.
* Versión instalada de **MySQL 5.0** o mayor.
* Contar con un **certificado SSL** para su comercio electrónico.


Instalación
----------
Para la instalación de extensiones (plugins) en Magento 2 es necesario aplicar una serie de comandos en la terminal del servidor donde este alojada nuestra plataforma.

Para implementar las 3 diferentes formas de pago en tu tienda, será necesario instalar y habilitar cada uno de ellos por separado.

1) Ingresar desde la terminal de nuestro servidor a la carpeta raíz de Magento 2
2) Ingresar los siguientes comandos, los cuales descargarán las extensiones al proyecto y adicional a ello descargarán la librería de Openpay  de PHP:
<ol type="a">
  <li>
    <p><strong>Módulo de pagos con tarjeta de crédito</strong></p>
    <div markdown="0" class="php-code" style="display:none;">
{% highlight Bash %}
 composer require openpay/magento2-cards:3.0.*{% endhighlight %}
    </div>
  </li>
  <li>
    <p><strong>Módulo para pagos en efectivo</strong></p>
     <div markdown="0" class="php-code" style="display:none;">
{% highlight Bash %}
 # Para versiones de Magento < 2.3.0
 composer require openpay/magento2-stores:~3.0.0
 # Para versiones de Magento >= 2.3.0
 composer require openpay/magento2-stores:~3.3.0
{% endhighlight %}
    </div>
  </li>
  <li>
    <p><strong>Módulo para pagos vía SPEI</strong></p>
     <div markdown="0" class="php-code" style="display:none;">
{% highlight Bash %}
# Para versiones de Magento < 2.3.0
composer require openpay/magento2-banks:~3.0.0
# Para versiones de Magento >= 2.3.0
composer require openpay/magento2-banks:~3.3.0
 {% endhighlight %}
    </div>
  </li>
</ol>

3) Después se procede a habilitar los módulos, actualizar y limpiar cache de la plataforma:

```
php bin/magento module:enable Openpay_Cards --clear-static-content
php bin/magento module:enable Openpay_Stores --clear-static-content
php bin/magento module:enable Openpay_Banks --clear-static-content
php bin/magento setup:upgrade
php bin/magento cache:clean
```


Configuración del plugin
----------
<section class="mgsettings">
  <ol class="mgsettings__list">
    <li class="mgsettings__item">
      <p>Identificar las credenciales de API asignadas a su comercio dentro del panel de administración de Openpay.</p>
      <figure class="mgsettings__image mgsettings__image--small">
        <img src="/images/plugins/woocommerce/wc_settings_04.png" alt="Configuración de plugin Magento2 paso 1" title="Paso 1">
      </figure>
      <blockquote>
        <p>Para ver las credenciales, dar clic en el engrane del menú superior derecho y luego seleccionar la opción <strong>Credenciales de API</strong></p>
      </blockquote>
    </li>
    <li class="mgsettings__item">
      <p>En su panel de administración de Magento 2, dirigirse a la sección <strong>Stores -> Configuration</strong>.</p>
      <figure class="mgsettings__image mgsettings__image--medium">
        <img src="/images/plugins/magento2/magento2_settings_02.png" alt="Configuración de plugin Magento 2 paso 2" title="Paso 2">
      </figure>
    </li>
    <li class="mgsettings__item">
      <p>Una vez dentro de la pantalla de Configuración, ubicar en el menú lateral izquierdo <strong>Sales -> Payment Methods.</strong></p>
      <figure class="mgsettings__image mgsettings__image--medium">
        <img src="/images/plugins/magento2/magento2_settings_03.png" alt="Configuración de plugin Magento 2 paso 3" title="Paso 3">
      </figure>
    </li>
    <li class="mgsettings__item"> 
      <p>Configurar el apartado de Openpay.</p>
      <h3 class="mgsettings__subtitle">Configuración general</h3>
      <div class="mgsettings__content">
        <ul>
            <li><strong>Habilitado.-</strong> Para habilitar el módulo de pago.</li>
            <li><strong>Sandbox.-</strong> Determina si el plugin va a funcionar en entorno de pruebas (Sandbox).</li>
            <li><strong>Título.-</strong> Nombre del método de pago que se mostrará en la tienda.</li>
            <li><strong>Credenciales de Openpay (Merchant ID, Llave Secreta, Llave Pública).- </strong> Credenciales de API para utilizar el plugin (ya sea en modo Sandbox o Producción). Copiar y pegar cada dato (obtenido en el Paso 1) como corresponda.</li>
            <li><strong>País.- </strong> Seleccionar el país donde se encuentra (México, Colombia).</li>
        </ul>
        <figure class="mgsettings__image mgsettings__image--medium">
            <img src="/images/plugins/magento2/magento2_settings_04_general.png" alt="Configuración de plugin Magento 2 paso 4 General" title="Paso 4 General">
        </figure>
      </div>
      <h3 class="mgsettings__subtitle">Configuración pago con tarjeta</h3>
      <div class="mgsettings__content">
        <ul>
            <li><strong>¿Cómo procesar el cargo?</strong> Define el tipo de cargo que se realizará:
              <ol>
              <li>Directo: Se realizará una evaluación del cargo y se rechazará si el sistema antifraude detectó alguna anomalía.</li>
                <li>3D Secure: Se realizará un redireccionamiento al banco para que el cliente sea autenticado en su banco.</li>
                <li>Autenticación selectiva: Se realizará una evaluación del cargo y si el sistema antifraude detecta alguna anomalía, se ejecutará un cargo 3D secure.</li>
              </ol>
            </li>
            <li><strong>Configuración del cargo.-</strong> Indica si el cargo se hace o no inmediatamente.</li>
            <li><strong>Pago con puntos.- </strong>Recibe pagos con puntos con BBVA, Santander y citibanamex.</li>
            <li><strong>Guardar tarjetas.-</strong> Permite a los usuarios registrados guardar sus tarjetas crédito/débito para agilizar sus futuras compras. </li>
            <li><strong>Tipos de tarjetas.-</strong>Deberán de estar seleccionados los 3 tipos de tarjetas para aceptar todo tipo de tarjetas permitidas por Openpay.</li>
            <li><strong>Meses sin intereses.- </strong> Puede hablitar o deshabilitar pagos con tarjeta con meses sin intereses seleccionando 3,6,9,12 y/o 18 meses sin intereses.</li>
            <li><strong>Configuración de países permitidos.-</strong> Puede dejarse con la configuración por default que tiene o bien puede definirse únicamente a México.</li>
            <li><strong>Orden.-</strong> Orden en que se mostrará este método de pago.</li>
        </ul>
        <figure class="mgsettings__image mgsettings__image--medium">
          <img src="/images/plugins/magento2/magento2_settings_04_cards.png" alt="Configuración de plugin Magento 2 paso 4 Cards" title="Paso 4 Cards">
        </figure>
      </div>
      <h3 class="mgsettings__subtitle">Configuración pagos en tiendas</h3>
      <div class="mgsettings__content">
        <ul>
          <li><strong>Fecha límite para pago.-</strong> Definir el número de horas que tendrá el cliente una vez emitido el recibo de pago. </li>
          <li><strong>Configuración de países permitidos.-</strong> Puede dejarse con la configuración por default que tiene o bien puede definirse únicamente a México.</li>
          <li><strong>Mostrar Mapa.- </strong> Al generarse el recibo de pago, se desplegará un mapa que muestra las tiendas de conveniencia más cercanas. </li>
          <li><strong>Orden.-</strong> Orden en que se mostrará este método de pago.</li>
        </ul>
        <div class="row align-items-center">
           <div class="col-xl-6 col-lg-6 col-md-6 col-sm-12 col-xs-12">
            <figure class="mgsettings__image mgsettings__image--medium">
                <img src="/images/plugins/magento2/magento2_settings_04_stores.png" alt="Configuración de plugin Magento 2 paso 4 Stores" title="Paso 4 Stores">
            </figure>
          </div>
          <div class="col-xl-6 col-lg-6 col-md-6 col-sm-12 col-xs-12">
            <figure class="mgsettings__image mgsettings__image--medium">
                <img src="/images/plugins/magento2/magento2_settings_04_stores_checkout.png" alt="Configuración de plugin Magento 2 paso 4 Stores" title="Paso 4 Stores">
            </figure>
          </div>
        </div>
      </div>
      <h3 class="mgsettings__subtitle">Configuración pago vía SPEI</h3>
      <div class="mgsettings__content">
        <ul>
          <li><strong>Fecha límite para pago.-</strong> Definir el número de horas que tendrá el cliente una vez emitido el recibo de pago.</li>
          <li><strong>Configuración de países permitidos.-</strong> Puede dejarse con la configuración por default que tiene o bien puede definirse únicamente a México.</li>
          <li><strong>Orden.-</strong> Orden en que se mostrará este método de pago.</li>
        </ul>
        <div class="row align-items-center">
          <div class="col-xl-6 col-lg-6 col-md-6 col-sm-12 col-xs-12">
            <figure class="mgsettings__image mgsettings__image--medium">
              <img src="/images/plugins/magento2/magento2_settings_04_spei.png" alt="Configuración de plugin Magento 2 paso 4 SPEI" title="Paso 4 SPEI">
          </figure>
          </div>
          <div class="col-xl-6 col-lg-6 col-md-6 col-sm-12 col-xs-12">
            <figure class="mgsettings__image mgsettings__image--medium">
              <img src="/images/plugins/magento2/magento2_settings_04_spei_checkout.png" alt="Configuración de plugin Magento 2 paso 4 SPEI" title="Paso 4 SPEI">
          </figure>
          </div>
        </div>
      </div>
      <blockquote>
        <p>Finalizada la configuración dar clic en el botón <strong>Save Config</strong> que se encuentra en la esquina superior derecha de la pantalla.</p>
      </blockquote>
    </li>
    <li class="mgsettings__item">
    Una vez que se hayan guardado los cambios, Magento te solicitará que limpies la cache del sistema, y una vez hecho esto, tu tienda dispondrá de las formas de pago que ofrece Openpay.
      <figure class="mgsettings__image mgsettings__image--full">
        <img src="/images/plugins/magento2/magento2_config_07.png" alt="Configuración de plugin Magento 2 paso 7" title="Paso 7">
      </figure>
      <figure class="mgsettings__image mgsettings__image--full">
        <img src="/images/plugins/magento2/magento2_config_08.png" alt="Configuración de plugin Magento 2 paso 8" title="Paso 8">
      </figure>
    </li>
  </ol>
</section>

Notificaciones de pago en tienda y SPEI
----------
> **Importante:** Dependiendo del tipo de notificación que se configure se deben utilizar la siguientes URL:

{% highlight html %}
Store payments -> https://[eCommerce domain]/stores/payments/confirm
​SPEI (wire transfer) -> https://[eCommerce domain]/banks/payments/confirm
{% endhighlight %}

> **Importante:** Es necesario verificar que el Webhook haya sido creado de forma correcta en Openpay.

<ol class="mgnotifications__list">
<li class="mgnotifications__item">En su panel de configuración de Openpay ir a <b>Ajustes (ícono de engrane) -> Configuraciones</b>.</li>
<center style="margin:10px 0;"><img src="/images/plugins/woocommerce_webhook_02.png" alt="Configuración de notificaciones Magento paso 1" title="Paso 1"></center>
<li class="mgnotifications__item">Ubicar el apartado de <b>Webhooks</b>. Si el webhook fue configurado correctamente habrá un registro en estado <b>Verificado</b>.</li>
<figure class="mgnotifications__image mgnotifications__image--medium">
  <img src="/images/plugins/webhook_verificado.png" alt="Configuración de notificaciones Magento paso 2" title="Paso 2">
</figure>
</ol>
