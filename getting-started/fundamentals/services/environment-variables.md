# Environment Variables

## Overview

By default, each service has different variables, which depends on environment. For example, database environments, which available on development environment may differ from staging environment, and so on... For more information about environments, see the [**Environments**](../environments.md) section. Depends on service language, environment variables can be accessed in different ways. 

To access environment variables using **TypeScript** or **JavaScript** language use:

```text
process.env
```

{% hint style="info" %}
code.store platform guarantees a high level of security, but we do not recommend displaying secret variables in the stdout or other sources.
{% endhint %}

Below, you can find information about available environment variables which code.store platform set by default.

## Service Environment Variables

`PROJECT_ID` internal ID of the project on the code.store platform

`ENVIRONMENT_ID` name of the [environment](../environments.md), where service deployed

`SERVICE_ID` internal ID of the service on the code.store platform

## Database Environment Variables

### Postgres Variables

`DATABASE_HOST` connection host

`DATABASE_PORT` connection port

`DATABASE_NAME` name of the database

`DATABASE_USERNAME` name of the user which can access to services database

### Redis Variables

`REDIS_HOST` Redis connection host

`REDIS_PORT` Redis connection port  

## Language based environment variables

### TypeScript & JavaScript

`NODE_VERSION` node version, which deployed service used



