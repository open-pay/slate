#Plugins
Documentación para instalar y configurar nuestros plugins de pago en las diferentes plataformas de e-commerce. 

Los plugins BBVA le permiten configurar y añadir el método de pago con tarjetas de crédito/débito, dentro del flujo de compra de su tienda en linea. 

##WooCommerce
WooCommerce es un plugin para sitios basados en WordPress que le permite a sus usuarios convertirlos en comercios electrónicos de manera fácil y rápida.

###Requerimientos
Es necesario que el servidor donde se encuentre alojada su tienda de WordPress cuente con las siguientes características:

* Versión instalada de **PHP 5.6** o mayor.
* Versión instalada de **MySQL 5.0** o mayor.
* Extensión de Apache **mod_rewrite** habilitada.
* Versión instalada de **WordPress 4.9** o mayor.
* Versión instalada del plugin **WooCommerce hasta 4.5.2**.
* Extensión de **PHP CURL** habilitada.
* Contar con un **certificado SSL** para su comercio electrónico.

###Instalación
1.- Descargar el archivo ZIP que contiene el plugin de pago con tarjetas de crédito/débito. Puede descargar el plugin a través de este [enlace](https://github.com/open-pay/openpay-woocommerce/blob/master/openpay-cards.zip?raw=true).

2.- En su panel de administración de WordPress, dirigirse a la sección **Plugins -> Añadir nuevo**, ubicado en el menú lateral.

3.- En la parte superior de la página se encuentra la opción **Subir Plugin**. Al hacer clic se muestra una pantalla para seleccionar nuestro archivo ZIP descargado en el paso 1, seleccionamos y completamos la instalación del plugin.

4.- Una vez instalado correctamente hacer clic en **Activar plugin**.

![Instalación Plugin BBVA](images/plugins/bbva_woocmx_install.gif)

###Configuración 
1.- En su panel de administración de WordPress, dirigirse a la sección **WooCommerce -> Ajustes**, ubicado en el menú lateral.

2.- Modificar el valor **Currency** del formulario por la opción **Mexican Peso ($)**. Guardar los cambios mediante el botón **Guardar los Cambios** ubicado al final del formulario.

3.- Para activar y desactivar la opción de pago, deberá seguir los siguientes pasos.

* Dirigirse a la pestaña **Pagos** ubicada en la parte superior de las configuraciones de Woocommerce.
* Activar la opción de pago **Openpay Cards**.
* Dar clic en el bóton **Gestionar** para comenzar con la configuración.

4.- Identificar las credenciales de API asignadas a su comercio dentro del panel de administración de BBVA.

![Configuración Plugin BBVA](images/plugins/bbva_woocmx_settings.gif)

5.- Completar la configuración del apartado de BBVA, contemplando los siguientes tópicos:

* **Habilitar módulo:** Habilita el uso de BBVA como plataforma de pagos.
* **Modo de pruebas:** Determina si el plugin va a funcionar en entorno de pruebas (Sandbox) o Producción.
* **Credenciales de BBVA (Merchant ID, Secret Key, Public Key):** Credenciales de API para utilizar el plugin (ya sea en modo Sandbox o Producción). Copiar y pegar cada dato (obtenido en el Paso anterior) como corresponda.
* **País:** Seleccionar el país donde se encuentra (México).
* **Número de afiliación:** Ingresa el número de afiliación BBVA
* **Pago con puntos:** Recibe pagos con Puntos BBVA.
* **Guardar tarjetas:** Habilita el guardado de tarjetas de crédito.
* **Meses sin intereses:** Puede hablitar o deshabilitar pagos con tarjeta con meses sin intereses seleccionando 3,6,9,12 y/o 18 meses sin intereses.
* **Monto mínimo MSI:** Define el monto mínimo de pago para meses sin intereses.

<aside class="notice">
Nota: Para que se muestre el campo <b>Número de afiliación</b> deberá guardar su configuración para que el plugin clasifique su comercio de manera automática. 
</aside>

6.- Guardar los cambios en la configuración dando clic sobre el botón **Guardar los Cambios** ubicado al final del formulario.

##Magento 2
Magento es una plataforma que permite la gestión de contenidos web para un comercio electrónico, ofreciendo una solución flexible y escalable sobre la cual se puede basar cualquier proyecto de tienda en línea.

###Versiones soportadas
* Magento Community Edition 2.1.1 en adelante

###Requerimientos
Es necesario que el servidor donde se encuentre alojado su comercio electrónico basado en Magento 2 cuente con las siguientes características:
* Versión instalada de **PHP 5.4** o mayor.
* Versión instalada de **MySQL 5.0** o mayor.
* Contar con un **certificado SSL** para su comercio electrónico.

###Instalación
Para la instalación de extensiones (plugins) en Magento 2 es necesario aplicar una serie de comandos en la terminal del servidor donde este alojada nuestra plataforma.

1.- Ingresar desde la terminal de nuestro servidor a la carpeta raíz de Magento 2

2.- Ingresar los siguientes comandos, los cuales descargarán las extensiones al proyecto y adicional a ello descargarán la librería de Openpay de PHP:

<aside>
composer require openpay/magento2-cards:3.1.*
</aside>

3.- Después se procede a habilitar los módulos, actualizar y limpiar cache de la plataforma:

<aside>
php bin/magento module:enable Openpay_Cards --clear-static-content<br/>
php bin/magento setup:upgrade<br/>
php bin/magento cache:clean<br/>
</aside>

###Configuración del plugin
1.- Identificar las credenciales de API asignadas a su comercio dentro del panel de administración de BBVA.

2.- En su panel de administración de Magento 2, dirigirse a la sección **Stores -> Configuration**.

3.- Una vez dentro de la pantalla de Configuración, ubicar en el menú lateral izquierdo **Sales -> Payment Methods**.

4.- Completar el formulario de configuración contemplando los siguientes puntos:

* **Habilitado.-** Para habilitar el módulo de pago.
* **Sandbox.-** Determina si el plugin va a funcionar en entorno de pruebas (Sandbox) o Producción.
* **Título.-** Nombre del método de pago que se mostrará en la tienda.
* **Credenciales de BBVA (Merchant ID, Llave Secreta, Llave Pública).-** Credenciales de API para utilizar el plugin (ya sea en modo Sandbox o Producción). Copiar y pegar cada dato (obtenido en el Paso 1) como corresponda.
* **País.-** Seleccionar el país donde se encuentra (México).
* **Número de afiliación:** Ingresa el número de afiliación BBVA
* **Pago con puntos.-** Recibe pagos con puntos con BBVA.
* **Guardar tarjetas.-** Permite a los usuarios registrados guardar sus tarjetas crédito/débito para agilizar sus futuras compras.
* **Tipos de tarjetas.-** Deberán de estar seleccionados los 2 tipos de tarjetas para aceptar todo tipo de tarjetas permitidas por BBVA.
* **Meses sin intereses.-** Puede hablitar o deshabilitar pagos con tarjeta con meses sin intereses seleccionando 3,6,9,12 y/o 18 meses sin intereses.
* **Configuración de países permitidos.-** Puede dejarse con la configuración por default que tiene o bien puede definirse únicamente a México.
* **Orden.-** Orden en que se mostrará este método de pago.

<aside class="notice">
Nota: Para que se muestre el campo <b>Número de afiliación</b> deberá guardar su configuración para que el plugin clasifique su comercio de manera automática. 
</aside>

5.- Finalizada la configuración dar clic en el botón **Save Config** que se encuentra en la esquina superior derecha de la pantalla.

6.- Una vez que se hayan guardado los cambios, Magento te solicitará que limpies la cache del sistema, y una vez hecho esto, tu tienda dispondrá de las formas de pago que ofrece BBVA.

##PrestaShop 1.7
PrestaShop es un software gratuito de comercio electrónico que le permite a sus usuarios montar tiendas online de manera sencilla y eficaz, eliminando las barreras técnicas y financieras que generalmente se requieren para abrir negocios de este tipo.

###Requerimientos
Es necesario que el servidor donde se encuentre alojado su comercio de PrestaShop cumpla con las siguientes pautas:
* PrestaShop v1.7.2 o superior.
* Versión instalada de **PHP 5.6** o superior.
* Versión instalada de **MySQL 5.0** o mayor.
* Extensión de **PHP CURL** habilitada.
* Contar con un **certificado SSL** para su comercio electrónico, en caso de querer integrar cobros mediante tarjeta de crédito/débito

###Instalación
Para instalar los módulos de pago para BBVA en su sitio de PrestaShop debe seguir los siguientes pasos:

1.- Descargar el archivo ZIP que contiene el método de pago con tarjetas de crédito/débito. Puede descargar el plugin a través de este [enlace](https://github.com/open-pay/openpay-prestashop/blob/master/PS_1.7/openpaycards.zip?raw=true).

2.- En el panel de administración de PrestaShop, dirigirse a la sección **Module Manager** a través del menú lateral.

3.- Dar clic en la opción **Subir un módulo** en la parte superior derecha de la pantalla.

4.- En el formulario que aparece, seleccionar o arrastrar **el archivo ZIP** del plugin descargado.

5.- Listo, el módulo BBVA se ha activado con éxito. 

![Instalación Plugin BBVA](images/plugins/bbva_ps17_install.gif)

###Configuración
1.- Identificar las credenciales de API asignadas a su comercio dentro del panel de administración de BBVA.

2.- En el panel de administración de PrestaShop, dirigirse a la sección **Module Manager** a través del menú lateral.

3.- A través del buscador situado en la parte superior, buscar los módulos de Openpay. Dar clic en Configurar al módulo del método de pago que desee seleccionar.

![Configuración Plugin BBVA](images/plugins/bbva_ps17_settings.gif)

4.- Completar el formulario de configuración contemplando los siguientes puntos:

* **Modo Sandbox.-** Seleccione el modo de operación del plugin: Sandbox (para realizar pruebas) o Producción.
* **Autenticación con BBVA.-** Ingresar las credenciales de API obtenidas en el primer paso.
* **País.-** Seleccionar el país donde se encuentra (México).
* **Número de afiliación:** Ingresa el número de afiliación BBVA
* **Pago con puntos.-** Recibe pagos con puntos con BBVA. 
* **Guardar tarjetas.-** Permite a los usuarios registrados guardar sus tarjetas crédito/débito para agilizar sus futuras compras.
* **Meses sin intereses.-** Configura que opciones de meses sin intereses serán mostradas para pago con tarjetas de crédito.

<aside class="notice">
Nota: Para que se muestre el campo <b>Número de afiliación</b> deberá guardar su configuración para que el plugin clasifique su comercio de manera automática. 
</aside>

5.- Presionar el botón **Guardar configuración**, una vez que haya completado el formulario.

##OpenCart
OpenCart es una solución gratuita basada en Web diseñada para poner en marcha un comercio electrónico con el mínimo de configuraciones y ajustes requeridos.

###Versiones soportadas
* **OpenCart 2.0.1.1** en adelante

###Requerimientos
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

###Instalación
Para instalar los plugins de BBVA en su comercio de OpenCart tiene que seguir los siguientes pasos:
1.- Descargar el archivo ZIP que contiene el plugin para pagos con tarjetas de crédito/débito. Puede descargar el plugin a través de este [enlace](https://github.com/open-pay/openpay-opencart/blob/master/OpenpayCards.ocmod.zip?raw=true).

2.- En su panel de administración de OpenCart, dirigirse a la sección **Extensions -> Installer**. Dar clic en la opción **Upload** y seleccionar el archivo ZIP del plugin del método de pago que desee instalar.

3.- Ir a la sección **Extensions -> Payments**, ubicar en el listado el plugin recién subido y dar clic en la opción **Install**.

4.- Confirmar que el plugin se haya instalado exitosamente.

![Instalación Plugin BBVA](images/plugins/bbva_cart_install.gif)

###Configuración
1.- Identificar las credenciales de API asignadas a su comercio dentro del panel de administración de BBVA.

2.- En su panel de administración de OpenCart, dirigirse a la sección **Extensions -> Payments**. Ubicar el plugin instalado recientemente y dar clic en la opción **Edit**.

![Configuración Plugin BBVA](images/plugins/bbva_cart_settings.gif)

3.- Completar el formulario de configuración contemplando los siguientes puntos:

* **Test mode:** Define si el plugin estará trabajando en entorno de pruebas o producción.
* **País:** Seleccionar el país donde se encuentra (México).
* **Número de afiliación:** Ingresa el número de afiliación BBVA
* **Test Merchant ID, Secret Key, Publishable Key:** Credenciales de API (ver paso 1) de la cuenta de BBVA del comercio, en entorno de pruebas.
* **Live Merchant ID, Secret Key, Publishable Key:** Credenciales de API (ver paso 1) de la cuenta de BBVA del comercio, en entorno de producción.
* **Status:** Determina si el método de pago estará disponible dentro del flujo de compra de tus cliente.
* **Título:** Nombre del método de pago a mostrar a los usuarios al momento de realizar una compra.
* **Total:** Monto mínimo de la compra para que el método de pago pueda ser utilizado.
* **Ordenamiento:** Orden en que se mostrará este método de pago.
* **Pago con puntos.-** Recibe pagos con puntos con BBVA.
* **Guardar tarjetas.-** Permite a los usuarios registrados guardar sus tarjetas crédito/débito para agilizar sus futuras compras.
* **Meses sin intereses.-** Puede hablitar o deshabilitar pagos con tarjeta con meses sin intereses seleccionando 3,6,9,12 y/o 18 meses sin intereses.

<aside class="notice">
Nota: Para que se muestre el campo <b>Número de afiliación</b> deberá guardar su configuración para que el plugin clasifique su comercio de manera automática. 
</aside>

4.- Guardar los cambios usando el botón ubicado en la esquina superior derecha de la pantalla.

5.- Confirmar que la configuración del plugin haya sido guardada exitosamente.



