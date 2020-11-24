# GraphQL

## Overview

code.store platform supports GraphQL and allows you to setup your GraphQL API in the quickest way. To make developers life easier code.store platform:

* by default runs GraphQL Apollo Server
* provides an opportunity to generate database entities based on `graphql.schema`
* generate resolvers for your queries and mutations
* secure your GraphQL API from massive complex requests and DDoS attacks, and allows you to configure GraphQL query costs

Basic information about GraphQL can be found in [Recipes - GraphQL](../../recipes/graphql-schemas.md) section.

## Endpoint

By default, code.store platform runs [Apollo Server](https://www.apollographql.com/docs/apollo-server/) and GraphQL playground available via `/graphql` endpoint. 

### Schema

When you create a new service, we code.store platform generating it with default `schema.graphql` file, which contains services GraphQL schema. You can find it in `src` directory of generated project. Generated file contains a simple `helloWorld` query:

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

Please, replace `service_url_hash` on your service URL hash, which can be found. After `helloWorld` query execution we should get "Hello, World!" response in our terminal:

```graphql
{"data":{"helloWorld":"Hello, World!"}}
```

## Resolver

Each field, query or mutation, which we specify in `schema.graphql` require resolver. A resolver is a function that's responsible for populating the data for a single field in your schema.

code.store platform simplifies the process of creating GraphQL resolvers and their handlers using flexible configuration and provides an ability to generate a couple of entities.

## 











