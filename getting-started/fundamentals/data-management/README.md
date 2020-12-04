# Data management

## Overview

code.store platform allows you use two database types for your services:

* \*\*\*\*[**Postgres**](https://www.postgresql.org/)\*\*\*\*
* \*\*\*\*[**Redis**](https://redis.io/)\*\*\*\*

Based on standards for building a microservice architecture, we follow [database-per-service](https://microservices.io/patterns/data/database-per-service.html) design pattern and generate separate database for each service. 

{% hint style="info" %}
Connection details are provided in `env` variables.
{% endhint %}

{% hint style="info" %}
You can manage your data using visual data manager using [backoffice](https://app.code.store/) on the service page _\(will be available soon\)_
{% endhint %}

## Postgres

code.store platform by default creates a Postgres database for each your service. You can enable or disable database using `codestore.yaml` configuration file in the root service directory. 

You have no limits in your database and can store any data there, code.store platform takes care of the scaling of your relational database so your database can keep up with the increasing demands of your application or applications.

To disable or enable Postgres database for your service just set it in `skipDatabase` flag. 

* true - to disable Postgres database
* false _\(default value\)_ - to enable it

```text
serviceConfiguration:
  skipDatabase: true
```

You can find connection to your database in context variable which available inside each `handler` method. More information about `context` objects can be found in [GraphQL](../services/graphql.md#context) and [REST](../services/rest.md#context) sections.

{% hint style="info" %}
To apply changes just push your service code using `cs push` command
{% endhint %}

## Redis

To disable or enable Redis database for your service just set it in `enableRedis` flag. 

* true - to enable Redis database
* false _\(default value\)_ - to disable it

```text
serviceConfiguration:
  enableRedis: true
```

You have no limits in your Redis database and can store any data there, code.store platform takes care of the scaling of memory usage so your database can keep up with the increasing demands of your application or applications.

To get credentials for Redis database use next env variables:

> REDIS\_HOST
>
> REDIS\_PORT

More information about accessing environment variables can be found in [Environment variables](../services/environment-variables.md#redis-variables) section.





