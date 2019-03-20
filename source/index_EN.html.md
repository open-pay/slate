---
title: API Reference

language_tabs:
  - shell: cURL
  - php: PHP
  - java: JAVA
  - csharp: C#
  #- javascript : Node.js
  - ruby: Ruby

includes:
  - en/endpoints
  - en/authentication
  - en/errors
  - en/charges
  - en/qropay
  - en/tokens
  - en/common_objects

lang: EN
---

# Introduction

The API is designed on [REST](http://es.wikipedia.org/wiki/Representational_State_Transfer),  therefore you'll find that URLs are oriented to resources and that HTTP response codes are used to indicate errors in the API.

All the API responses are in [JSON](http://www.json.org/) format, including the errors.

<!---
In the case to use the existents API clients ([Java](https://github.com/open-pay/bancomer-java), [Php](https://github.com/open-pay/bancomer-php), [C#](https://github.com/open-pay/bancomer-dotnet), [Python](https://github.com/open-pay/bancomer-python), [Ruby](https://github.com/open-pay/bancomer-ruby), [NodeJS](https://github.com/open-pay/bancomer-node)), the responses are specifically of type defined in the clients and their respective languajes.
-->