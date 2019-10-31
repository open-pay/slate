---
title: API Reference

language_tabs:
  - shell: cURL
  - php: PHP
  - java: JAVA
  - csharp: C#
  - javascript : 
  - ruby: 
  
includes:
  - es/endpoints
  - es/authentication
  - es/errors
  - es/charges
  - es/pse
  - es/customers
  - es/transfers
  - es/cards
  - es/plans
  - es/subscriptions
  - es/fees
  - es/webhooks
  - es/tokens
  - es/stores
  - es/common_objects

toc_footers:
 - #
 - #
 
---

# Introducción

La API de Openpay está diseña sobre [REST](http://es.wikipedia.org/wiki/Representational_State_Transfer), por lo tanto encontrarás que las URL están orientadas a recursos y se usa códigos de respuesta HTTP para indicar los errores en la API.

Todas las respuestas de la API están en formato [JSON](http://www.json.org/), incluyendo errores.

En el caso de usar los clientes existentes del API de Openpay ([Java](https://github.com/open-pay/openpay-java), [Php](https://github.com/open-pay/openpay-php), [C#](https://github.com/open-pay/openpay-dotnet)), las respuestas son específicamente del tipo definido en dichos clientes en sus respectivos lenguajes.
