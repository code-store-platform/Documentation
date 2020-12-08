# Communication

## Overview

When you include services to you project there might be a cases, when services should communicate with each other. code.store platform allows inter-HTTP communication

{% hint style="info" %}
We are working hard on the platform functionality and soon we will provide an opportunity to organize inter-service communication through message-brokers.
{% endhint %}

## Routing concept

Services, which project includes and deployed in one [environment](../environments.md#project-environments) can communicate with each other. 

To call GraphQL or REST API of another service on the same [environment](../environments.md#project-environments) - make an HTTP request, where URL should build by next pattern: `http://{SERVICE_NAME}-service` Each service has an internal URL which available only per environment. 

Let's imagine that we have service "example", which deployed to the development environment. This service can be accessed by another service on the development [environment](../environments.md#project-environments) by next URL:

```text
http://example-service
```

## HTTP request example

 To provide an HTTP call to service install any HTTP client, for example [axios](https://www.npmjs.com/package/axios) using npm:

```text
npm i axios
```

Import [axios](https://www.npmjs.com/package/axios) dependency in your code:

```text
import axios from 'axios';
```

And execute request yo your service. In example below you can find simple HTTP request to `[GET] /rest/hello` route of `example` service:

```text
const result = await axios.get('http://service-example/rest/hello');
```

The result of HTTP request execution will be available in the result object. 



