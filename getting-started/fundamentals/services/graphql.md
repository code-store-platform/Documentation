# GraphQL

## Overview

code.store platform supports GraphQL and allows you to set up your GraphQL API in the quickest way. To make a developer's life easier code.store platform:

* by default runs GraphQL [Apollo Server](https://www.apollographql.com/docs/apollo-server/)
* provides an opportunity to generate database entities based on `graphql.schema`
* generate resolvers for your queries and mutations
* secure your GraphQL API from massive complex requests and DDoS attacks, and allows you to configure GraphQL query costs

Basic information about GraphQL can be found in [Recipes - GraphQL](../../recipes/graphql-schemas.md) section.

## Endpoint

By default, code.store platform runs [Apollo Server](https://www.apollographql.com/docs/apollo-server/) and GraphQL playground available via `/graphql` endpoint.

Local development: 

```graphql
http://localhost:3000/graphql
```

Remote address:

```graphql
  https://api.code.store/{service_url_hash}/graphql
```

### Schema

When you create a new service, we code.store platform generating it with default `schema.graphql` file, which contains services GraphQL schema. You can find it in `src` directory of the generated project. Generated file contains a simple `helloWorld` query:

```graphql
type Query {
    helloWorld: String!
}
```

It's a very basic schema of an API that has a single `Query` called `helloWorld` \(which doesn't accept arguments\) and which returns a single output of type `string`. You can query it using GraphQL playground, which available on `/graphql` endpoint or execute next command using CLI:

```graphql
curl \
  -X POST \
  -H "Content-Type: application/json" \
  --data '{ "query": "{ helloWorld }" }' \
  https://api.code.store/{service_url_hash}/graphql
```

Please, replace `service_url_hash` on your service URL hash, which can be found after cs service:info command execution. After `helloWorld` query execution we should get "Hello, World!" response in our terminal:

```graphql
{"data":{"helloWorld":"Hello, World!"}}
```

## Resolvers

Each field, query or mutation, which we specify in `schema.graphql` require resolver. A resolver is a function that's responsible for populating the data for a single field in your schema.

Handler for all queries and mutations, which described in `schema.graphql` file should be placed to `src/resolvers` directory. Each resolver file of your query or mutation should be named the same, as it declared in `graphql.schema` and placed the appropriate directory `src/resolvers/queries` for queries and  `src/resolvers/mutations` for mutations.

For example, in generated service template you can find, that query `helloWorld` in `schema.graphql` have resolver `src/resolvers/queries/helloWorld.ts`

```graphql
import { logger, Resolver } from 'codestore-utils';

const resolver: Resolver = async (parent, args, context, info) => {
  logger.log('This is a helloWorld resolver!', 'helloWorld');
  return 'Hello, World!';
};

export default resolver;

```

{% hint style="info" %}
code.store platform simplifies the process of creating GraphQL resolvers and their handlers using flexible configuration and provides an ability to generate it using **cs generate:resolver** command. 
{% endhint %}

### Context

Each resolver can optionally accept four positional arguments:

`parent` returns value of the previous resolver in the resolver chain for this field's parent

`args` an object that contains all GraphQL arguments provided for this field. For example, when executing a query: `query{ user(id: "4") }`, the args object passed to the user resolver is `{ "id": "4" }`.

`context` an object shared across all resolvers that are executing for a particular operation and has `ResolverContext` type. 

```graphql
export interface ResolverContext {
    db: {
        connection: Connection;
    };
    request: Request;
    [key: string]: any;
}
```

As you can see, context allows receiving database `connection` and provide access to `request` object, which includes such objects as `headers`, `method`, `url`...

`info` contains information about the operation's execution state, including the field name, the path to the field from the root, and more.





## 











