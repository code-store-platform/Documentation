# REST

## Overview

At the moment, code.store's platform supports a simple file-system-based routing of REST API endpoints. 

REST endpoints are based on [Express](https://expressjs.com/) framework, so you can use all Express features to build your application.  Using REST-based on [Express](https://expressjs.com/) you are able to create endpoints of different methods \(such as GET, POST, PUT, DELETE, PATH…\), define your route paths, handlers, work with route parameters, define your middlewares… 

code.store platform simplifies the process of creating endpoints and their handlers using flexible configuration and provides an ability to generate a couple of entities.

## Endpoints

code.store platform exposes the **`http://{your service url}/rest/{endpoint}`** route, where **`{endpoint}`** is getting routed to the file **`./src/rest/{http method}.{endpoint}.ts`**. 

![Endpoint handler](../../../.gitbook/assets/untitled-2020-09-22-1039-3-.png)

In order to create an endpoint, you need to create a new file in the `src/rest` folder \(by default, no such directory exists\) the name of which will contain the request method \(GET, POST, PUT, DELETE ...\) at the beginning of the name and the name of the route. For example:

* request GET **`http://localhost:3000/rest/helloWorld`** will be routed to **`src/rest/get.helloWorld.ts`**
* request POST **`http://localhost:3000/rest/user/create`** will get routed to **`src/rest/post.user.create.ts`**

{% hint style="info" %}
Commands: **cs :generate:rest -m get -n helloWorld**  and  **cs :generate:rest -m get -n helloWorld** will avoid the manual step of endpoint creation and generate files from the previous example with predefined handlers. We strongly recommend using this way of endpoint creation. More information about endpoints generation can be found in [**Generation - REST**](../generation/rest.md) section. 
{% endhint %}

### Handlers

Each newly created endpoint file must export a function that contains the business logic. Exported function takes two arguments: **event** and **context,** which contains a connection to the database and mapped request object. Each handler may release any business logic you need. You can import any library, connect to the database, execute queries...  Here an example of "hello world" handler:

```typescript
import { Handler } from 'codestore-utils';

const handler: Handler = async (event, context) => {
  // your code goes here
  return 'Hello, world!';
}

export default handler;
```

{% hint style="info" %}
By running **`cs generate:rest -m get -n helloWorld`** we will generate the following file at **`src/rest/get.helloWorld.ts`**:
{% endhint %}

### Context

Handler function takes two arguments: **event** and **context**. 

**event** - is an object, which provides mapped request objects. Query `params`, request `body`, request `headers` can be accessed here. Below you can find an interface of event object:

```typescript
interface HandlerEvent {
  params: {
    query: {
      [key: string]: string;
    };
  };
  body: {
    [key: string]: string;
  };
  headers: {
    [key: string]: string;
  };
  req: Request;
  res: Response;
  next: NextFunction;
}
```

In cases, when `params`, `body` and `headers` are not enough to implement you can access `req` and `res` object. REST endpoints are based on [Express](https://expressjs.com/) framework and allow you to use all features of this framework. **event** object exposes [request](http://expressjs.com/en/api.html#req) and [response](http://expressjs.com/en/api.html#res) objects, which are Express objects and can be used in the handler as you wish.

{% hint style="info" %}
If you use response middlewares execute **next\(\)** function from **event** object at the end of the handler execution context.
{% endhint %}

The next POST request **`curl -X POST 'http://localhost:3000/rest/helloWorld?hello=world' --data '{ "test": "object" }' -H "Content-Type: application/json"`** will result in the following _event_ object:

```javascript
{
  "params": {
    "query": {
      "hello": "world"
    }
  },
  "body": {
    "test": "object"
  },
  "headers": {
    "host": "localhost:3000",
    "user-agent": "curl/7.64.1",
    "accept": "*/*",
    "content-type": "application/json",
    "content-length": "20"
  }
}
```

`context` - is an object, which provides [TypeORM](https://typeorm.io) connection object. In case if database is available for your service - you can access it and establish a connection with database. 

```typescript
db: {
    connection: Connection;
};
```

The _context_ argument contains the database connection property which you can use with your TypeORM entities:

```typescript
context.db.connection.getRepository(...);
```

As you can see, the concept is very simple but is very powerful at the same time, as it allows you to create custom REST endpoints, which could be used for integration with OAuth provides, Stripe or other payment systems which require callbacks!

### Response

There is no need to use an Express response object to generate a server response, just return `string` in case if string response is required or return an object, which will be sent as `JSON` response, following the next interface:

```text
interface HandlerResponse {
  status?: number;
  data: any;
}
```

` status` - will set a status code of HTTP response

`data` - is a custom JSON object

```text
import { Handler } from 'codestore-utils';

const handler: Handler = async (event, context) => {

  return { status: 201, data: { hello: 'world' };
}

export default handler;
```

The result of handler execution will be a JSON object `{ hello: 'world' }` with `201` status code.

{% hint style="info" %}
As alternative Express **`event.res`**object can be used to set a custom response.
{% endhint %}

## Middlewares

code.store platform allows create middleware functions, which are similar to [Express middlewares.](http://expressjs.com/en/guide/using-middleware.html#using-middleware) To create middleware function for any route you should follow the next steps:

* create a file with a handler function in `src/rest-middlewares` 
* apply middleware function in a configuration file `codestore.yaml`
* specify your business logic inside handler file

### Create a handler file

Create folder rest-middlewares inside src directory if it not exists. To create this folder just execute in root service directory following CLI command:

```text
mkdir src/rest-middlewares
```

Then, create a new file, which will contain code with your middleware function.  For example, let's define a `permissions` middleware function, which will be in `src/rest-middlewares/permissions.middleware.ts` file with the following content:

```text
export default ({req, res, next}, context)=>{
  next();
}
```

This is a default [Express](https://expressjs.com/) middleware, which different method signature. 

The first argument - is an object, which includes `req`, `res` objects and `next` function. 

`req` - is an [Express request](http://expressjs.com/en/api.html#req) object which represents the HTTP request and has properties for the request query string, parameters, body, HTTP headers, and so on

`res` - is an Express response object which represents the HTTP response that an Express app sends when it gets an HTTP request.

`next` - is a function which invokes to pass control to the next [middleware](http://expressjs.com/en/guide/using-middleware.html#using-middleware) function. 

The second argument `context`- is an object, which provides [TypeORM](https://typeorm.io) connection object. In case if a database is available for your service - you can access it and establish a connection it. 

```text
db: {
    connection: Connection;
};
```

{% hint style="info" %}
Also, using `cs generate:middleware` command you can generate files with middleware functions. To learn more visit [Generation section](../generation/middlewares.md).
{% endhint %}

### Apply middleware function in a configuration file

To apply middleware function just modify rest object in `codestore.yaml` and define which middleware function should be applied on which route. 

Below you can find an example of `permissions` middleware function which located in `src/rest-middlewares/permissions.middleware.ts` file which applied to `[GET] /hello` route in `src/rest/get.hello.ts` file:

```text
rest:
  routes:
    - path: /hello
      handler: /rest/get.hello
      method: GET
      requestMiddlewares:
        - /rest-middlewares/permissions.middleware

```

Middleware function can be applied **before** or **after** [handler](rest.md#handlers) execution. code.store platform allowed `request` and `response` middleware functions. 

To execute middleware function before [`handler`](rest.md#handlers) execution, just define your middleware function in `requestMiddlewares` object of `codestore.yaml` and use responseMiddleware to execute middleware function after [`handler`](rest.md#handlers) execution.

{% hint style="success" %}
In example above `permissions` middleware function specified for `/hello` route in the `requestMiddleware` scope and will be execute before route `handler` function. 
{% endhint %}





















