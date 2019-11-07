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
  - en/endpoints
  - en/authentication
  - en/errors
  - en/charges
  - en/pse
  - en/customers
  - en/transfers
  - en/cards
  - en/plans
  - en/subscriptions
  - en/webhooks
  - en/tokens
  - en/stores
  - en/common_objects

toc_footers:
 - #
 - #

lang: EN
---

# Introduction

The Openpay API is designed on [REST](http://es.wikipedia.org/wiki/Representational_State_Transfer),  therefore you'll find that URLs are oriented to resources and that HTTP response codes are used to indicate errors in the API.

All the API responses are in [JSON](http://www.json.org/) format, including the errors.

In the case to use the existents Openpay API clients ([Java](https://github.com/open-pay/openpay-java), [Php](https://github.com/open-pay/openpay-php), [C#](https://github.com/open-pay/openpay-dotnet)), the responses are specifically of type defined in the clients and their respective languajes.
