---
layout: faq
title:  PrestaShop
category: plugin
tags: plugin
lang: es
---

#PrestaShop 1.6 & 1.7

**¿Qué es Prestashop?**

PrestaShop es un software gratuito de comercio electrónico que le permite a sus usuarios montar tiendas online de manera sencilla y eficaz, eliminando las barreras técnicas y financieras que generalmente se requieren para abrir negocios de este tipo.

Ponemos a su disposición el plugin necesario para integrar los servicios de Openpay en su tienda de PrestaShop.

<div class="boton-grp boton-plugin">
<div class="blu-boton"><a href="https://github.com/open-pay/openpay-prestashop" target="_blank">Ver en GitHub</a></div>
</div>

Versiones soportadas
----------
* PrestaShop v1.6.1 o superior. 
* PrestaShop v1.7.2 o superior.

Requerimientos
----------
Es necesario que el servidor donde se encuentre alojado su comercio de PrestaShop cumpla con las siguientes pautas:

* Versión instalada de **PHP 5.6** o superior.
* Versión instalada de **MySQL 5.0** o mayor.
* Extensión de **PHP CURL** habilitada.
* Contar con un **certificado SSL** para su comercio electrónico, en caso de querer integrar cobros mediante tarjeta de crédito/débito

Instalación
----------

Para instalar los módulos de pago para Openpay en su sitio de PrestaShop debe seguir los siguientes pasos:

<section class="prestashop-install">
  <ul class="nav nav-tabs" id="TabInstall" role="tablist">
    <li class="nav-item">
      <a class="nav-link active" id="prestashop16-tab" data-toggle="tab" href="#prestashop16" role="tab" aria-controls="prestashop16" aria-selected="true">PrestaShop 1.6</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" id="prestashop17-tab" data-toggle="tab" href="#prestashop17" role="tab" aria-controls="prestashop17" aria-selected="false">PrestaShop 1.7</a>
    </li>
  </ul>
  <div class="tab-content" id="prestashopInstall">
    <div class="tab-pane fade show active" id="prestashop16" role="tabpanel" aria-labelledby="prestashop16-tab">
      <div class="row align-items-center">
        <ol class="prestashop-install__list">
          <li class="prestashop-install__list">Descargar el archivo ZIP con los contenidos del plugin. Puede descargar el plugin a través de <a href="https://github.com/open-pay/openpay-prestashop/blob/master/PS_1.6/openpayprestashop.zip?raw=true">este enlace</a>.
          </li>
          <li class="prestashop-install__list">En el panel de administración de PrestaShop, dirigirse a la sección <strong>Módulos y Servicios</strong> a través del menú lateral.</li>
          <figure class="prestashop-install__image prestashop-install__image--small">
            <img src="/images/plugins/prestashop/prestashop1.6_install_02.png" alt="Instalación de plugin PrestaShop paso 2" title="Paso 2">
          </figure>
          <li class="prestashop-install__list">Dar clic en la opción <strong>Añadir un nuevo módulo</strong> en la parte superior derecha de la pantalla.</li>
          <figure class="prestashop-install__image prestashop-install__image--full">
            <img src="/images/plugins/prestashop/prestashop1.6_install_03.png" alt="Instalación de plugin PrestaShop paso 3" title="Paso 3">
          </figure>
          <li class="prestashop-install__list">En el formulario que aparece, <strong>Seleccionar el archivo ZIP</strong> descargado, y dar clic en el botón <strong>Subir este módulo</strong>.</li>
          <figure class="prestashop-install__image prestashop-install__image--medium">
            <img src="/images/plugins/prestashop/prestashop1.6_install_04.png" alt="Instalación de plugin PrestaShop paso 4" title="Paso 4">
          </figure>
          <li class="prestashop-install__list">En la nueva pantalla, se instalará el módulo recién descargado. Dar clic en <strong>Instalar</strong>.</li>
          <figure class="prestashop-install__image prestashop-install__image--medium">
            <img src="/images/plugins/prestashop/prestashop1.6_install_05.png" alt="Instalación de plugin PrestaShop paso 5" title="Paso 5">
          </figure>
          <li>Confirmar que el plugin haya sido instalado correctamente.</li>
          <figure class="prestashop-install__image prestashop-install__image--full">
            <img src="/images/plugins/prestashop/prestashop1.6_install_06.png" alt="Instalación de plugin PrestaShop paso 6" title="Paso 6">
          </figure>
        </ol>
      </div>
    </div>
    <div class="tab-pane fade" id="prestashop17" role="tabpanel" aria-labelledby="prestashop17-tab">
      <div class="row align-items-center">
        <ol class="prestashop-install__list">
          <li class="prestashop-install__list">Descargar el archivo ZIP que contiene todos los módulos. Puede descargar los plugins a través de <a href="https://github.com/open-pay/openpay-prestashop/blob/master/PS_1.7/openpayprestashop.zip?raw=true">este enlace</a>.
          </li>
          <li>Descomprimir el archivo descargado. Dentro encontrará los tres módulos de Openpay, pago con tarjetas, pago en tiendas y pagos con SPEI.
          </li>
          <figure class="prestashop-install__image prestashop-install__image--medium">
            <img src="/images/plugins/prestashop/prestashop_install_01.png" alt="Instalación de plugin PrestaShop paso 2" title="Paso 2">
          </figure>
          <li class="prestashop-install__list">En el panel de administración de PrestaShop, dirigirse a la sección <strong>Module Manager</strong> a través del menú lateral.</li>
          <figure class="prestashop-install__image prestashop-install__image--ssmall">
            <img src="/images/plugins/prestashop/prestashop_install_02.png" alt="Instalación de plugin PrestaShop paso 2" title="Paso 2">
          </figure>
          <li class="prestashop-install__list">Dar clic en la opción <strong>Subir un módulo</strong> en la parte superior derecha de la pantalla.</li>
          <figure class="prestashop-install__image prestashop-install__image--full">
            <img src="/images/plugins/prestashop/prestashop_install_03.png" alt="Instalación de plugin PrestaShop paso 3" title="Paso 3">
          </figure>
          <blockquote>
          <p>La siguiente secuencia debe realizarse por cada plugin que se desee instalar.</p>
          </blockquote>
          <li class="prestashop-install__list">En el formulario que aparece, seleccionar o arrastrar <strong>el archivo ZIP</strong> del plugin descargado.</li>
          <figure class="prestashop-install__image prestashop-install__image--small">
            <img src="/images/plugins/prestashop/prestashop_install_04.png" alt="Instalación de plugin PrestaShop paso 4" title="Paso 4">
          </figure>
          <li class="prestashop-install__list">Listo, el módulo Openpay se ha activado con éxito.</li>
          <figure class="prestashop-install__image prestashop-install__image--small">
            <img src="/images/plugins/prestashop/prestashop_install_05.png" alt="Instalación de plugin PrestaShop paso 5" title="Paso 5">
          </figure>
        </ol>
      </div>
    </div>
  </div>
</section>


Configuración de módulos
----------
<section class="prestashop-settings">
  <ol class="prestashop-settings__list">
    <li class="prestashop-settings__item">Identificar las credenciales de API asignadas a su comercio dentro del panel de administración de Openpay.</li>
    <figure class="prestashop-settings__image prestashop-settings__image--small">
      <img src="/images/plugins/woocommerce/wc_settings_04.png" alt="Configuración de plugin PrestaShop paso 1" title="Paso 1">
    </figure>
    <blockquote>
    <p>Para ver las credenciales, dar clic en el engrane del menú superior derecho y luego seleccionar la opción <strong>Credenciales de API</strong></p>
    </blockquote>
    <li class="prestashop-settings__item"> Configurar el módulo dependiendo la versión instalada de PrestaShop. 
      <ul class="nav nav-tabs" id="TapSettings" role="tablist">
        <li class="nav-item">
          <a class="nav-link active" id="prestashop16_settings-tab" data-toggle="tab" href="#prestashop16_settings" role="tab" aria-controls="prestashop16_settings" aria-selected="true">PrestaShop 1.6</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" id="prestashop17_settings-tab" data-toggle="tab" href="#prestashop17_settings" role="tab" aria-controls="prestashop17_settings" aria-selected="false">PrestaShop 1.7</a>
        </li>
      </ul>
      <div class="tab-content" id="prestashopSettings">
        <div class="tab-pane fade show active" id="prestashop16_settings" role="tabpanel" aria-labelledby="prestashop16_settings-tab">
          <div class="row align-items-center">
            <ol class="prestashop-settings__list" type="a">
                <li class="prestashop-settings__item">En el panel de administración de PrestaShop, dirigirse a la sección <strong>Módulos y Servicios</strong> a través del menú lateral.</li>
                <figure class="prestashop-settings__image prestashop-settings__image--small">
                  <img src="/images/plugins/prestashop/prestashop1.6_install_02.png" alt="Configuración de plugin PrestaShop paso 2" title="Paso 2">
                </figure>
                <li class="prestashop-settings__item">A través del buscador de la izquierda, buscar el módulo de <strong>Openpay</strong>. Al resultado desplegado, dar click en <strong>Configurar</strong>.</li>
                <figure class="prestashop-settings__image prestashop-settings__image--full">
                  <img src="/images/plugins/prestashop/prestashop1.6_settings_02.png" alt="Configuración de plugin PrestaShop paso 3" title="Paso 3">
                </figure>
                <li class="prestashop-settings__item">
                  Complete el formulario de configuración ubicado en la parte inferior de la pantalla tomando en cuenta los siguientes puntos:
                  <ul>
                    <li>Seleccione el modo de operación del plugin: Sandbox (para realizar pruebas) o Producción.</li>
                    <li>Ingresar las credenciales de API obtenidas en el primer paso.</li>
                    <li>Configura que opciones de meses sin intereses serán mostradas para pago con tarjetas de crédito.</li>
                    <li>Define el monto mínimo de pago para meses sin intereses.</li>
                    <li>Ingresar la URL del sitio, este campo es muy importante debido a que será este parámetro el que se tome para la creación del Webhook (notificación de pagos), si el dominio o subdominio del sitio cambia será necesario actualizarlo.</li>
                    <li>Defina la cantidad de horas de validez para realizar un pago de Tiendas de Conveniencia y SPEI, en caso de aceptar dichos métodos de pago.</li>
                  </ul>
                  <figure class="prestashop-settings__image prestashop-settings__image--full">
                  <img src="/images/plugins/prestashop/prestashop1.6_settings_03.png" alt="Configuración de plugin PrestaShop paso 4" title="Paso 4">
                </figure>
                </li>
                <li class="prestashop-settings__item">Presionar el botón <strong>Guardar configuración</strong>, una vez que haya completado el formulario.</li>
            </ol>
          </div>
        </div>
        <div class="tab-pane fade" id="prestashop17_settings" role="tabpanel" aria-labelledby="prestashop17_settings-tab">
          <div class="row align-items-center">
            <ol class="prestashop-settings__list" type="a">
              <li class="prestashop-settings__item">En el panel de administración de PrestaShop, dirigirse a la sección <strong>Module Manager</strong> a través del menú lateral.</li>
              <figure class="prestashop-settings__image prestashop-settings__image--ssmall">
                <img src="/images/plugins/prestashop/prestashop_install_02.png" alt="Configuración de plugin PrestaShop paso 2" title="Paso 2">
              </figure>
              <li class="prestashop-settings__item">A través del buscador situado en la parte superior, buscar los módulos de <strong>Openpay</strong>. Dar clic en <strong>Configurar</strong> al módulo del método de pago que desee seleccionar.</li>
              <figure class="prestashop-settings__image prestashop-settings__image--full">
                <img src="/images/plugins/prestashop/prestashop_settings_03.png" alt="Configuración de plugin PrestaShop paso 3" title="Paso 3">
              </figure>
              <li class="prestashop-settings__item">
                Completar la configuración del apartado de Openpay:
              <h3 class="prestashop-settings__subtitle">Configuración pago con tarjeta</h3>
              <div class="prestashop-settings__content">
                <ul>
                  <li><strong>Modo Sandbox.- </strong>Seleccione el modo de operación del plugin: Sandbox (para realizar pruebas) o Producción.</li>
                  <li><strong>Autenticación con Openpay.- </strong>Ingresar las credenciales de API obtenidas en el primer paso.</li>
                  <li><strong>¿Cómo procesar el cargo? </strong>Define el tipo de cargo que se realizará: Directo, 3Dsecure o Autenticación Selectiva. </li>
                  <li><strong>Configuración del cargo.- </strong>Indica si el cargo se hace o no inmediatamente.</li>
                  <li><strong>Pago con puntos.- </strong>Recibe pagos con puntos con BBVA, Santander y citibanamex.</li>
                  <li><strong>Guardar tarjetas.- </strong>Permite a los usuarios registrados guardar sus tarjetas crédito/débito para agilizar sus futuras compras.</li>
                  <li><strong>Meses sin intereses.- </strong>Configura que opciones de meses sin intereses serán mostradas para pago con tarjetas de crédito.</li>
                </ul>
              </div>
              <figure class="prestashop-settings__image prestashop-settings__image--full">
                <img src="/images/plugins/prestashop/prestashop_settings_cards.png" alt="Configuración de plugin PrestaShop paso 4 Cards" title="Paso 4 Cards">
              </figure>
              <h3 class="prestashop-settings__subtitle">Configuración pagos en tiendas</h3>
              <div class="prestashop-settings__content">
                <ul>
                  <li>Seleccione el modo de operación del plugin: Sandbox (para realizar pruebas) o Producción.</li>
                  <li>Ingresar las credenciales de API obtenidas en el primer paso.</li>
                  <li>Ingresar la URL del sitio, este campo es muy importante debido a que será este parámetro el que se tome para la creación del Webhook (notificación de pagos), si el dominio o subdominio del sitio cambia será necesario actualizarlo.</li>
                  <li>Definir el número de horas que tendrá el cliente una vez emitido el recibo de pago.</li>
                  <li>Habilitar la opción, para mostrar el mapa de las tiendas más cercanas. </li>
                </ul>
              </div>
              <figure class="prestashop-settings__image prestashop-settings__image--full">
                  <img src="/images/plugins/prestashop/prestashop_settings_store.png" alt="Configuración de plugin PrestaShop paso 4 Store" title="Paso 4 Store">
                </figure>
                <h3 class="prestashop-settings__subtitle">Configuración pagos vía SPEI</h3>
                <div class="prestashop-settings__content">
                  <ul>
                    <li>Seleccione el modo de operación del plugin: Sandbox (para realizar pruebas) o Producción.</li>
                    <li>Ingresar las credenciales de API obtenidas en el primer paso.</li>
                    <li>Ingresar la URL del sitio, este campo es muy importante debido a que será este parámetro el que se tome para la creación del Webhook (notificación de pagos), si el dominio o subdominio del sitio cambia será necesario actualizarlo.</li>
                    <li>Definir el número de horas que tendrá el cliente una vez emitido el recibo de pago.</li>
                  </ul>
                </div>
                <figure class="prestashop-settings__image prestashop-settings__image--full">
                  <img src="/images/plugins/prestashop/prestashop_settings_spei.png" alt="Configuración de plugin PrestaShop paso 4 SPEI" title="Paso 4 SPEI">
                </figure>
              </li>
              <li class="prestashop-settings__item">Presionar el botón <strong>Guardar configuración</strong>, una vez que haya completado el formulario.</li>
            </ol>
          </div>
        </div>
      </div>
    </li>
  </ol>
</section>
