---
description: "\U0001F5A5"
---

# Quick Start with CLI \[WIP\]

This guide will introduce some basic code.store concepts like services and schema generation using CLI. The goal of this quick start is to get you up and running fast, so let's not waste any time and start!

### Create code.store account

If you haven't done this already, then click on this link.

### Install the code.store CLI

We invite you to follow this guide and install our command line interface:

{% page-ref page="../../cli/code-store-cli.md" %}

### Authenticate and create service

Once you have your account and the CLI is installed, we can finally do some interesting stuff!

In order to work with the CLI, you have to connect it with your account by launching the following command:

```bash
cs auth:login
```

This command is going to launch your default browser and ask for your login details. Once you are authenticated, we can go on and create a new service.

```bash
cs service:create
```

![Creating your first service](../../.gitbook/assets/service-create.gif)

### The anatomy of a service

You can check the contents of your new service directory by running `ls -lh ./` 

```bash
# Example of the directory structure of a Service
./
├── src/
│		├── models/ # contains generated TypeORM entities
│		├── resolvers/
│		│		├── mutations/
│		│				└── mutationExample.js|ts
│		│		├── queries/
│		│				└── queryExample.js|ts
│		└── schema.graphql # GraphQL definition of your service's API
├── .build # temporary directory
├── package.json # standard NPM configuration file
└── codestore.yaml # main configuration file
```

Let's get into the details of each file and directory.

Root directory contains two files and one folder:

* `package.json` – it is a standard NPM configuration file. Feel free and add any NPM packages you like, we are going to install them for you during the deployment of the service;
* `codestore.yaml` – contains your service ID and will contain more configuration options in later versions;
* `src/` – this is where all the source code lives.

Let's dive into `src/` directory:

* `schema.graphql` – one of the most \(if not the most\) important files. It contains a GraphQL schema of your service;
* `models/` – this directory contains generated TypeORM entities. We automatically generate TypeScript classes for your database tables, that's why you should not edit the files in this directory \(even if you will, they will be re-generated automatically\);
* `resolvers/` – this is where your business logic lives. Resolvers serve two purposes: connect your GraphQL objects to data in the database and is a place where you implement any additional business logic.

### Basic API schema and resolver

When you create a new service, we are generating it with default `schema.graphql` which contains the following code:

```graphql
type Query {
    helloWorld: String!
}
```

It is a very basic schema of an API that has a single `Query` called `helloWorld` \(which doesn't accept arguments\) and which returns a single output of type `string`.

{% hint style="info" %}
If you are not comfortable with GraphQL syntax, we are inviting you to read [our GraphQL quick-start guide first.](../graphql-schemas.md)
{% endhint %}

We can test this query by running the following curl command in your terminal:

```bash
curl https://api.code.store/{service_id}/{environment_id}/graphql?{helloWorld}
```

Hopefully, we should get "Hello, World!" message in our terminal 🤞

Let's take a look at the resolver \(business logic\) for this query which is located at the file `src/resolvers/queries/helloWorld.ts`:

```typescript
export default async (parent, args, context, info) => {
    return 'Hello, World!';
};
```

{% hint style="info" %}
When starting the service, code.store loads all files from `src/resolvers/mutations` and `src/resolvers/queries` directories and passes them to the GraphQL server. The filename of the resolver must be equal to the name of _query_ or a _mutation_. Each query and mutation in the `schema.graphql` file must have a corresponding _resolver_ in the filesystem.
{% endhint %}

This should give you a basic understanding of how GraphQL schema and resolvers work together and let's write something more meaningful in the next chapter.

### Blog-post example

We can finally write something more or less meaningful! For the sake of simplicity, we decided to implement a well-beaten example of a Blog-post.

First of all we should modify our `schema.graphql` file:

```graphql
# API schema for a simple Blog-post service

type Post {
    id: ID!
    createdAt: String!
    title: String!
    body: String!
    author: Author!
}

type Author {
    id: ID!
    name: String!
}

type Query {
    allPosts: [Post]
}
```

{% hint style="info" %}
Every GraphQL schema has a _query_ type and may or may not have a _mutation_ type. Read more about [GraphQL in our quick start guide here](../graphql-schemas.md), or in the official [GraphQL documentation](https://graphql.org/learn/schema/#object-types-and-fields).
{% endhint %}

We have added two types and two queries in the schema and we can now go on and add the resolvers. Let's begin with the query allPosts: create a file `src/resolvers/queries/allPosts.ts` and initialize it with the following code:

```typescript
export default async (parent, args, context, info) => {
    return [
        {
            id: 1,
            createdAt: '2020-06-30',
            title: 'Test post',
            body: 'Test body',
            author: {
                id: 1,
                name: 'Test author'
            }
        }
    ];
}
```

{% hint style="info" %}
Each GraphQL _query_ or _mutation_ must be mapped to a resolver. In order to find a resolver for a _query_/_mutation_, **code.store** is using a file structure mapping to find a corresponding resolver.

Thus, all _queries_ should be placed into `src/resolvers/queries/{queryName}.ts` files, all _mutations_ into `src/resolvers/mutations/{mutationName}.ts`. For example, resolver for a _mutation_ `createUser` should be placed into `src/resolvers/mutations/createUser.ts` file.
{% endhint %}

Here we go, this is our first test resolver which is not yet connected to anything but which already can return the data! You can deploy and test the application by running `cs push.`

Until now we were not using any database at all and it is the time to create one. The cool thing is that code.store generates the database automatically based on the GraphQL schema you provided! CONTINUE.

* add resolvers
* add mutation
* generate & push

### Deploy to code.store

Here is a structure of the `resolvers/` directory:

* `mutations/` – 
* `queries/` – 
* `resolvers.js` – 

TODO:

* resolvers chains

