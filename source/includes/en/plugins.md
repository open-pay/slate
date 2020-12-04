#Plugins
Documentation to install and configure our payment plugins on the different e-commerce platforms. 

Our plugins lets you add and configure BBVA's supported payment methods (credit/debit cards), to be available within the shopping flow of your online store.

##WooCommerce
WooCommerce is a plugin that enables users to convert their WordPress sites into a fully functional online store, in a quick and easy fashion.

###Requirements
It is required for the server that hosts your WordPress store to fulfill the following:

* **PHP 5.6** or greater.
* **MySQL 5.0** or greater.
* **Apache mod_rewrite** extension enabled.
* **WordPress 4.9** or greater.
* **WooCommerce 4.5.2** plugin.
* **PHP CURL** extension enabled.
* Have a **SSL certificate** for your eCommerce, in case you wish to accept credit card payments.

###Installation
1.- Download the ZIP file with the plugin contents. You can use [this link](https://github.com/open-pay/openpay-woocommerce/blob/master/openpay-cards.zip?raw=true) to download it.

2.- On your WordPress admin panel, go to **Plugins -> Add New**, placed on the lateral menu.

3.- Click the **Upload Plugin** option, placed on the upper side of the screen. Pick the ZIP downloaded on step 1 on the plugin installation form. Click the **Install Now** button.

4.- When installation is complete, the plugin must be activated

![BBVA Plugin Installation](images/plugins/bbva_woocmx_install.gif)

###Setup 
1.- On your WordPress admin panel, go to **WooCommerce -> Settings**, placed on the lateral menu.

2.- Modify the value **Currency** for the appropiate one according your business. Save your changes by clicking the button **Save changes** by the end of the form.

3.- To activate and deactivate the payment options, you must follow these steps.

* Go to the **Payments** tab located at the top of the Woocommerce settings.
* Activate the desired payment option.
* Click on the **Manage** button to start the configuration.

4.- On your BBVA admin panel, identify the API credentials assigned to your merchant account.

![BBVA Plugin Configuration](images/plugins/bbva_woocmx_settings.gif)

5.- Fill in the configuration form keeping in mind the following guidelines:

* **Enable module**: Enables or disables BBVA as the payment platform for your eCommerce.
* **Test mode (Sandbox)**: Determines whether the plugin is working on a testing environment (Sandbox) or productive environment.
* **BBVA credentials (Merchant ID, Secret Key, Public Key)**: API credentials to use (whether you are on Sandbox or Productive environments). Copy and paste each value (check step 3) accordingly.
* **Country:** Select country (Mexico, Colombia).
* **Affiliation number:** Enter the BBVA affiliation number.
* **Payment with points:** To receive payments with BBVA Points.
* **Save cards:** Enable saving credit cards..
* **Months without interest:** You can enable or disable card payments to months without interest by selecting 3,6,9,12 and / or 18.
* **Minimum amount MSI:** Defines the minimum payment amount for months without interest.

<aside class="notice">
Important: To show the <strong>Affiliation number</strong> field, you must save your configuration so that the plugin will classify your e-commerce automatically. 
</aside>

6.- Save your changes by clicking the **Save changes** button placed by the end of the settings form.

##Magento 2
Magento is a web platform that allows content management for online stores, offering a flexible and scalable solution on which any eCommerce can be built.

###Supported versions
* **Magento Community Edition** 2.1.1 or greater

###Requirements
It is required for the server that hosts your Magento 2 store to fulfill the following:

* **PHP v5.4** or greater.
* **MySQL v5.0** or greater.
* Have a **certificado SSL** for your eCommerce, in case you wish to accept credit card payments.

###Installation
For the installation of extensions in Magento 2 is necessary to execute some commands in the server terminal where our platform is hosted. To implement the three payment methods in your store, it is necessary to install and enable each one separately.

1.- Start the terminal application and navigate to your Magento 2 root folder.

2.- Execute the commands to install each of the modules:

<aside>
composer require openpay/magento2-cards:3.1.*
</aside>

3.- Enable the modules, update and clear cache of the platform to complete the installation process.

<aside>
php bin/magento module:enable Openpay_Cards --clear-static-content<br/>
php bin/magento setup:upgrade<br/>
php bin/magento cache:clean<br/>
</aside>

###Setup
1.- On your BBVA admin panel, identify the API credentials assigned to your merchant account.

2.- On your Magento 2 admin panel, go to **Stores -> Configuration**.

3.- Click on the **Sales -> Payment** Methods link, on the lateral menu.

4.- Fill in the configuration form keeping in mind the following guidelines:

* **Habilitado (Enabled).-** Enables or disables BBVA as the payment platform for your eCommerce.
* **Sandbox.-** Determines whether the plugin is working on a testing environment (Sandbox) or productive environment.
* **Título (Title).-** Name of the payment method displayed in the store.
* **BBVA credentials (Merchant ID, Secret Key, Public Key).-** API credentials to use (whether you are on Sandbox or Productive environments). Copy and paste each value (check step 1) accordingly.
* **País (Country).-** Select country (Mexico, Colombia).
* **Affiliation number.-** Enter the BBVA affiliation number.
* **Pago con puntos (Payment with points).-** Receive point payments with BBVA, Santander and citibanamex.
* **Guardar tarjetas (Save cards).-** Enable saving credit cards.
* **Tipos de tarjetas (Credit card types).-** The 2 types of cards must be selected to accept all types of cards allowed by BBVA.
* **Meses sin intereses (Months without interest).-** You can enable or disable card payments to months without interest by selecting 3,6,9,12 or 18.
* **Configuración de países permitidos (Payment from applicable countries, payment from specific countries).-** you can leave the default configuration or define only Mexico.
* **Orden (Sort order).-** Order in which the payment method is shown.

<aside class="notice">
Important: To show the <strong>Affiliation number</strong> field, you must save your configuration so that the plugin will classify your e-commerce automatically. 
</aside>

5.- Save your changes by clicking **Save Config**, on the upper right corner of the screen.

6.- Clear the cache via **Admin Panel** to complete the installation process.

##PrestaShop 1.7
PrestaShop is a free eCommerce software that allows users to setup online stores on a quick and easy fashion, cutting off the technical and financial complications that are usually involved in this kind of business.

###Requirements
It is required for the server that hosts your PrestaShop store to fulfill the following:

* **PrestaShop v1.7.2** or greater.
* **PHP 5.6** or greater.
* **MySQL 5.0** or greater.
* **PHP CURL** extension enabled.
* Have a **SSL certificate** for your eCommerce, in case you wish to accept credit card payments.

###Installation
In order to install the BBVA module on your PrestaShop store you need to follow these steps:

1.- Download the ZIP file containing all the modules. You can use [this link](https://github.com/open-pay/openpay-prestashop/blob/master/PS_1.7/openpaycards.zip?raw=true) to download it.

2.- On your PrestaShop admin panel, go to **Module Manager** using the lateral menu.

3.- Click **Add new module** on the upper right corner of the screen.

4.- Drag and drop the ZIP of the downloaded module.

5.- And you're done, the BBVA module has been activated successfully.

![BBVA Plugin Installation](images/plugins/bbva_ps17_install.gif)

###Setup
1.- On your BBVA admin panel, identify the API credentials assigned to your merchant account.

2.- On your PrestaShop admin panel, go to **Module Manager** using the lateral menu.

3.- On the search field placed on the top, type in **openpay**. Click **Configure** on the search result.

![BBVA Plugin Configuration](images/plugins/bbva_ps17_settings.gif)

4.- Fill in the configuration form keeping in mind the following guidelines:

* **Sandbox.-** Select the operation mode of the module: Sandbox (for testing purposes) or Production.
* **BBVA authentication.-** Write in the API credentials obtained on Step 1.
* **País (Country).-** Select country (Mexico, Colombia).
* **Affiliation number.-** Enter the BBVA affiliation number.
* **Payment with points.-** Receive point payments with BBVA.
* **Save cards.-** Enable saving credit cards.
* **Months without interest.-** Set up options for months without interest will be shown for payment with credit cards.

<aside class="notice">
Important: To show the <strong>Affiliation number</strong> field, you must save your configuration so that the plugin will classify your e-commerce automatically. 
</aside>

5.- Click **Save configuration**, once the form is completed.

##OpenCart
OpenCart is a free web platform that enables users to quickly start an eCommerce with the minimum amount of settings and configurations required.

###Supported versions
* **OpenCart 2.0.1.1** or greater

###Requirements
It is required for the server that hosts your OpenCart store to fulfill the following:

* Apache web server
* **PHP 5.2** or greater.
* **MySQL 5.0** or greater.
* Have a **SSL certificate** for your eCommerce domain.

It is also necessary that the installed PHP version comply with these settings:

* **Register Globals** disabled.
* **Magic Quotes GPC** disabled.
* File uploads enabled.
* **Session Auto Start** disabled.
* **GD (with PNG image processing)** extension enabled.
* **cURL** extension enabled.
* **ZIP** extension enabled.

###Installation
In order to install the BBVA plugins on your OpenCart store you need to follow these steps:

1.- Download the ZIP file that contains all the plugins. You can use [this link](https://github.com/open-pay/openpay-opencart/blob/master/OpenpayCards.ocmod.zip?raw=true) to download it.

2.- On your OpenCart admin panel, go to **Extensions -> Installer.** Click the **Upload** button, browse and select the ZIP file of the payment method's plugin you want to install.

3.- Go to **Extensions -> Payments**, find in the list the uploaded plugin and click the Install option.

4.- Look for the success message.

![BBVA Plugin Installation](images/plugins/bbva_cart_install.gif)

###Setup
1.- On your BBVA admin panel, identify the API credentials assigned to your merchant account.

2.- On your OpenCart admin panel, go to **Extensions -> Payments**. Find the recently installed plugin and click the **Edit** button.

![BBVA Plugin Configuration](images/plugins/bbva_cart_settings.gif)

3.- Fill in the configuration form keeping in mind the following guidelines:

* **Test mode:** Defines whether the plugin is working on a testing or a productive environment.
* **País (Country):** Select country (Mexico, Colombia).
* **Affiliation number:** Enter the BBVA affiliation number.
* **Test Merchant ID, Secret Key, Publishable Key:** BBVA's merchant account API credentials (check out step 1), on testing environment.
* **Live Merchant ID, Secret Key, Publishable Key:** BBVA's merchant account API credentials (check out step 1), on productive environment.
* **Status:** Defines whether the payment method will be available to your customers or not.
* **Title:** Payment method caption to be shown to your customer on your eCommerce's shopping flow.
* **Total:** Minimum purchase amount to make available the payment method.
* **Sort order:** Order in which the payment method is shown.
* **Payment with points.-** Receive point payments with BBVA, Santander and citibanamex.
* **Save cards.-** Enable saving credit cards.
* **Months without interest.-** You can enable or disable card payments to months without interest by selecting 3,6,9,12 or 18.

<aside class="notice">
Important: To show the <strong>Affiliation number</strong> field, you must save your configuration so that the plugin will classify your e-commerce automatically. 
</aside>

4.- Save your changes by clicking the button on the upper right corner of the screen.

5.- Look for the success message.



