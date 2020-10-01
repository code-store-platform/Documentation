---
description: "\U0001F5A5\U0001F914⌨️\U0001F44F\U0001F680"
---

# Quick Start with CLI

This guide will introduce some basic **code.store** concepts like services and schema generation using CLI. The goal of this quick start is to get you up and running fast, so let's not waste any time and start!

### Create code.store account

If you haven't done this already, then [click on this link](https://app.code.store/).

### Install the code.store CLI

We invite you to follow this guide and install our command-line interface:

{% page-ref page="../../cli/code-store-cli.md" %}

### Authenticate and create service

Once you have your account and the CLI is installed, we can finally do some interesting stuff!

In order to work with the CLI, you have to connect it with your account by launching the following command:

```bash
codestore login
```

This command is going to launch your default browser and ask for your login details. Once you are authenticated, we can go on and create a new [service](../core-concepts.md#service).

```bash
codestore service:create
```

### The anatomy of a service

You can check the contents of your new service directory by running `ls -lh ./` 

```bash
# Example of the directory structure of a Service
./
├── codestore.yaml # main configuration file
├── package.json # standard NPM configuration file
└── src
    ├── data # contains generated TypeORM entities
    │   ├── entities
    │   └── migrations
    ├── resolvers # contains GraphQL resolvers 
    │   ├── mutations # mutations as used to create new objects  
    │   ├── queries # queries are used to retrieve objects
    │   │   └── helloWorld.ts
    │   └── resolvers.ts
    └── schema.graphql # GraphQL definition of your service's API
```

Let's get into the details of each file and directory.

The root directory contains two files and one folder:

* `package.json` – it is a standard NPM configuration file. Feel free and add any NPM packages you like using `npm install {packageName}`;
* `codestore.yaml` – contains your service ID and will contain more configuration options in later versions;
* `src/` – this is where all the source code lives.

Let's dive into the `src/` directory:

* `schema.graphql` – one of the most \(if not the most\) important files. It contains a [GraphQL](../core-concepts.md#schema-or-graphql-schema) schema of your service;
* `data/` – this directory contains generated TypeORM entities. We automatically generate TypeScript classes for your database tables, that's why **you should not edit the files in this directory** \(even if you will, they will be re-generated automatically\);
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
If you are not comfortable with GraphQL syntax, we are inviting you to read [our GraphQL quick-start guide first](../graphql-schemas.md) and if you want to go deeper into that rabbit-hole 🐰then the official GraphQL documentation [https://graphql.org/learn/](https://graphql.org/learn/).
{% endhint %}

We can test this query by running the following curl command in your terminal:

```bash
curl \
  -X POST \
  -H "Content-Type: application/json" \
  --data '{ "query": "{ helloWorld }" }' \
  https://api.code.store/{service_url_hash}/graphql
```

Hopefully, we should get "Hello, World!" response \(something looking like that `{"data":{"helloWorld":"Hello, World!"}}`\) in our terminal 🤞

Let's take a look at the resolver \(business logic\) for this query which is located in the file `src/resolvers/queries/helloWorld.ts`:

```typescript
// src/resolvers/queries/helloWorld.ts

import { logger, Resolver } from 'codestore-utils';

const resolver: Resolver = async (parent, args, context, info) => {
  logger.log('This is a helloWorld resolver!', 'helloWorld');
  return 'Hello, World!';
}

export default resolver;
```

This is a basic code which does few things:

* we are importing a logger module which is going to output messages to the local console or to our cloud log storage;
* we are importing a Resolver, which is an Interface for a function type; it is not a necessary step but it is a useful one if you want to see type hints in your IDE;
* if your code editor cannot find 'codestore-utils' then simply run `npm install` in the service directory root.

{% hint style="info" %}
When starting the service, code.store loads all files from `src/resolvers/mutations` and `src/resolvers/queries` directories and passes them to the GraphQL server. The filename of the resolver must be equal to the name of _a query_ or _a_ _mutation_. Each query and mutation in the`schema.graphql` file must have a corresponding _resolver_ in the filesystem.
{% endhint %}

This should give you a basic understanding of how GraphQL schema and resolvers work together and let's write something more meaningful in the next chapter.

### Local development

{% hint style="warning" %}
The local development workflow is still in early beta and we are working hard to bring you the most stable and comfortable local development experience. If you notice any issues, please ping us in our [community](https://spectrum.chat/code-store). 
{% endhint %}

Local development comes in handy if you don't want to launch `codestore push` after each modification and then wait until it finishes.

In order to use local development workflow:

* install PostgreSQL database locally; you can do it quite easily either [https://postgresapp.com/](https://postgresapp.com/) or via [Docker](https://hub.docker.com/_/postgres);
* configure your local settings in codestore.yaml:

```yaml
# ./codestore.yaml

localConfiguration:
 database:
   port: 5432
   database: my-local-database
   password: my-secure-password
   username: my-db-username
   host: localhost
 application:
   port: 3000
```

* launch a local development server by running `codestore dev`
* `codestore dev` will try to run "npm install" to make sure that the dependencies of your service are installed but you can also launch it manually if you wish.

After launching `codestore dev` you should see the following output:

```bash
$ codestore dev
✔ Installing dependencies
✔ Compiling code
2020-08-10T16:12:18.250Z Starting development server
2020-08-10T16:12:18.251Z [bootstrap] Start bootstrapping the application
2020-08-10T16:12:18.251Z [DatabaseConnector] Connecting to database
2020-08-10T16:12:18.279Z [DatabaseConnector] Successfully connected to database my-local-database
2020-08-10T16:12:18.279Z [DatabaseConnector] Running migrations
2020-08-10T16:12:18.289Z [DatabaseConnector] Loaded entities:
2020-08-10T16:12:18.735Z [GraphqlLoader] Loaded queries: helloWorld
2020-08-10T16:12:18.749Z [bootstrap] Server is running on http://localhost:3000
2020-08-10T16:12:18.749Z [bootstrap] Graphql is available on http://localhost:3000/graphql
```

Voila ! Let's try and test our local server:

```bash
curl \
  -X POST \
  -H "Content-Type: application/json" \
  --data '{ "query": "{ helloWorld }" }' \
  http://localhost:3000/graphql
```

You should get a "Hello, World!" message if everything works properly 🤞

{% hint style="info" %}
We are using lots of `curl` commands to query the web-services in this Quick Start, however, you can also GraphQL Playground by clicking on the link of the service, i.e. http://localhost:3000/graphql for the local environment, or https://api.code.store/{service URL hash}/graphql for remote environments.
{% endhint %}

### Blog-post example

We can finally write something more or less meaningful! For the sake of simplicity, we decided to implement a well-beaten example of a Blog-post. We are going to be using the local development server during this example, so make sure that you have a PostgreSQL database ready. 

First of all, we should modify our `schema.graphql` file:

```graphql
# src/schema.graphql

# API schema for a simple Blog-post service

type Post {
    id: ID!
    createdAt: String!
    title: String!
    body: String!
    authorName: String!
}

type Query {
    allPosts: [Post]
}
```

{% hint style="info" %}
Every GraphQL schema has a _query_ type and may or may not have a _mutation_ type. Read more about [GraphQL in our quick start guide here](../graphql-schemas.md), or in the official [GraphQL documentation](https://graphql.org/learn/schema/#object-types-and-fields).
{% endhint %}

We have added two types and two queries in the schema and we can now go on and add the resolvers. Let's begin with the query `allPosts`: create a file `src/resolvers/queries/allPosts.ts` and initialize it with the following code:

```typescript
// src/resolvers/queries/allPosts.ts

import { logger, Resolver } from 'codestore-utils';

const resolver: Resolver = async (parent, args, context, info) => {
    logger.log('This is a allPosts resolver!', 'allPosts');
    return [
        {
            id: 1,
            createdAt: '2020-06-30',
            title: 'Test post',
            body: 'Test body',
            authorName: 'Test author',
        }
    ];
}

export default resolver;

```

{% hint style="warning" %}
Each GraphQL _query_ or _mutation_ must be mapped to a resolver. In order to find a resolver for a _query_/_mutation_, **code.store** is using a file structure mapping to find a corresponding resolver.

The rules are simple:

* all _queries_ should be placed into `src/resolvers/queries/{queryName}.ts` files, 
* all _mutations_ into `src/resolvers/mutations/{mutationName}.ts` 

For example, resolver for a _mutation_ `createUser` should be placed into `src/resolvers/mutations/createUser.ts` file.
{% endhint %}

Here we go, this is our first test resolver which is not yet connected to anything but which already can return the data! One last step before running the deployment command - we have to remove `src/resolvers/queries/helloWorld.ts` or simply rename it to `helloWorld.ts_`. And that's it, you can now run your application locally via `codestore dev` and test it via CURL: 

```bash
curl \
  -X POST \
  -H "Content-Type: application/json" \
  --data '{ "query": "{ allPosts { id title authorName } }" }' \
  http://localhost:3000/graphql
```

{% hint style="warning" %}
GraphQL queries and mutations in your `schema.graphql` should match 1-to-1 the queries and migrations in the file system, i.e. if you have a query _"test"_ in a schema and you don't have in the file system, the service will throw an error. The same in the opposite order, if you have a resolver in the file system but not in the schema.
{% endhint %}

Until now we were not using any database at all and the time has come to ~~grab a beer~~ create one. The cool thing is that **code.store** generates the database automatically based on the GraphQL schema you provided! In order to generate the entities locally, we should run `codestore generate` command.  As soon as it finishes the generation, let's modify our resolver and add some database queries:

```typescript
// src/resolvers/queries/allPosts.ts

import { logger, Resolver } from 'codestore-utils';
import Post from '../../data/entities/Post';

const resolver: Resolver = async (parent, args, context, info) => {
    logger.log('This is a allPosts resolver!', 'allPosts');
    const postRepository = context.db.connection.getRepository(Post);
    
    return postRepository.find();
}

export default resolver;

```

{% hint style="info" %}
For every type in your GraphQL schema, **code.store** performs two operations:

* it generates database migrations \(using [TypeORM](https://typeorm.io/)\)
* it generates [TypeORM entities](https://typeorm.io/#/entities) which it stores in `src/data/entities/{TypeName}.ts`
{% endhint %}

Few things have changed here:

* we are importing [TypeORM Repository](https://typeorm.io/#/working-with-repository) and our generated Post entity
* we are initializing the repository and performing a [find query](https://typeorm.io/#/find-options) for our Post entity

As soon as we run the application with `codestore dev` , we can test it again and see that it's returning an empty array as we haven't created anything yet 🤦🏽‍♀️. 

```bash
curl \
  -X POST \
  -H "Content-Type: application/json" \
  --data '{ "query": "{ allPosts { id title authorName } }" }' \
  http://localhost:3000/graphql
```

Time to add the first mutation.

First of all, modify your schema.graphql to look like the following:

```graphql
# src/schema.graphql

# API schema for a simple Blog-post service

type Post {
    id: ID!
    createdAt: String!
    title: String!
    body: String!
    authorName: String!
}

type Query {
    allPosts: [Post]
}

type Mutation {
    createPost(title: String!, body: String!, authorName: String!): Post
}
```

This is what has changed, we added a type Mutation to our GraphQL schema containing a mutation  `createPost`. Now we can implement our resolver:

```typescript
// src/resolvers/mutations/createPost.ts
import { logger, Resolver } from 'codestore-utils';
import Post from '../../data/entities/Post';

const resolver: Resolver = async (parent, args, context, info) => {
    logger.log('creating a new Post', 'createPost');
    
    const post = new Post();
    post.title = args.title;
    post.authorName = args.authorName;
    post.body = args.body;
    post.createdAt = new Date().toISOString();

    logger.log(post, 'createPost');

    // Getting a database connection
    const repository = context.db.connection.getRepository(Post);
    
    // Saving our first post entity
    return await repository.save(post);
}

export default resolver;
```

Now launch `codestore dev` again and run some queries \(we are going to be using a [http](https://httpie.org/) command which is similar to cURL but provides a better output\):

```bash
# Create a couple of new posts
$ curl 'http://localhost:3000/graphql' \
    -X POST \
    -H 'Content-Type: application/json' \
    --data '{"query":"mutation createPost($title:String!, $body:String!, $authorName:String!) { createPost(title:$title, body:$body, authorName:$authorName) { id title body authorName } }","variables":{"title":"Our First Article","body":"Body","authorName":"Arthur Conan Doyle"}}'

# And you will get output like this, meaning post successfully created
{"data":{"createPost":{"id":"1","title":"Our First Article","body":"Body","authorName":"Arthur Conan Doyle"}}}

# Create another one
$ curl 'http://localhost:3000/graphql' \
    -X POST \
    -H 'Content-Type: application/json' \
    --data '{"query":"mutation createPost($title:String!, $body:String!, $authorName:String!) { createPost(title:$title, body:$body, authorName:$authorName) { id title body authorName } }","variables":{"title":"Our Second Article","body":"Body","authorName":"Arthur Conan Doyle"}}'

# Output  
{"data":{"createPost":{"id":"2","title":"Our Second Article","body":"Body","authorName":"Arthur Conan Doyle"}}}


# Let's retrieve the posts now
$ curl \
  -X POST \
  -H "Content-Type: application/json" \
  --data '{ "query": "{ allPosts { id title authorName } }" }' \
  http://localhost:3000/graphql
  
# All posts that we created for now
{"data":{"allPosts":[{"id":"1","title":"Our First Article","authorName":"Arthur Conan Doyle"},{"id":"2","title":"Our Second Article","authorName":"Arthur Conan Doyle"}]}}

# Or if we format the JSON for more readability
{
  "data": {
    "allPosts": [
      {
        "id": "1",
        "title": "Our First Article",
        "authorName": "Arthur Conan Doyle"
      },
      {
        "id": "2",
        "title": "Our Second Article",
        "authorName": "Arthur Conan Doyle"
      }
    ]
  }
}
```

### Finalizing

So now we have a working service on our local machine and it would be great to have it deployed somewhere in the cloud. Let's do exactly that and deploy the service to the private environment by running `codestore push` command. As soon as finished, you can launch the queries in your private environment! 

### **Conclusion**

Not sure if it was quick 😉 but we hope that after this guide you have a good understanding of how code.store works. Feel free to check the rest of the documentation and contact us in the community chat if you will have any questions!

Happy coding and may the force be with you! 🦾

