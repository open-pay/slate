---
title: API Reference

language_tabs:
  - shell: cURL
  - php: PHP
  - java: JAVA
  - csharp: C#

includes:
  - en/endpoints
  - en/authentication
  - en/errors
  - en/charges
  - en/payments
  - en/customers
  - en/transfers
  - en/cards
  - en/bank_accounts
  - en/plans
  - en/subscriptions
  - en/fees
  - en/webhooks
  - en/tokens
  - en/merchant
  - en/stores
  - en/common_objects
  - en/electronic_invoice

toc_footers:
 - <a href='#'>Sign Up for a Developer Key</a>
 - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

lang: EN
---

# Introduction

The Openpay API is designed on [REST](http://es.wikipedia.org/wiki/Representational_State_Transfer),  therefore you'll find that URLs are oriented to resources and that HTTP response codes are used to indicate errors in the API.

All the API responses are in [JSON](http://www.json.org/) format, including the errors.

In the case to use the existents Openpay API clients ([Java](https://github.com/open-pay/openpay-java), [Php](https://github.com/open-pay/openpay-php), [C#](https://github.com/open-pay/openpay-dotnet), [Python](https://github.com/open-pay/openpay-python), [Ruby](https://github.com/open-pay/openpay-ruby), [NodeJS](https://github.com/open-pay/openpay-node)), the responses are specifically of type defined in the clients and their respective languajes.
