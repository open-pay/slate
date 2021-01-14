---
title: API Reference

language_tabs:
  - shell: cURL
  - php: PHP
  - java: JAVA
  - csharp: C#
# - javascript : Node.js
  - ruby: Ruby

includes:
  - es/quickguide
  - es/endpoints
  - es/authentication
  - es/errors
  - es/charges
  #- es/qropay
  #- es/tokens
  - es/common_objects
  #- es/plugins

lang: ES
---

# Introducción

La API está diseñada sobre [REST](http://es.wikipedia.org/wiki/Representational_State_Transfer), por lo tanto encontrarás que las URL están orientadas a recursos y se usa códigos de respuesta HTTP para indicar los errores en la API.

Todas las respuestas de la API están en formato [JSON](http://www.json.org/), incluyendo errores.

En el caso de usar los clientes existentes del API de BBVA ([Java](https://github.com/EcommerceBBVA/BBVA-JAVA.git), [PHP](https://github.com/EcommerceBBVA/BBVA-PHP.git), [C#](https://github.com/EcommerceBBVA/BBVA-CSHARP.git), [Ruby](https://github.com/EcommerceBBVA/BBVA-RUBY.git)), las respuestas son específicamente del tipo definido en dichos clientes en sus respectivos lenguajes.
