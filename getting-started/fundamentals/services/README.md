# Services

## Overview

**Services** - is the main entity that you operate on when working with the [**code.store** ](https://app.code.store) platform. These are backends that you, members of your organization, or public users of the [**code.store** ](https://app.code.store) platform creates.

One of the key features of our platform is the reuse of services. Since the service doesn't belong to any specific project, you can reuse the services that are available to you.

For convenience, the [**code.store** ](https://app.code.store) platform provides the ability to develop your services in various languages:

* TypeScript

Currently, we are actively working on adding support for different languages and frameworks, such as: Go, PHP, Python, Java, C\#... so soon you will be able to see support for your particular technology.

Using the CLI or web interface - you can _create/edit/update/add to projects/delete_ your services. Below are examples of how this can be done.

When service is created - the platform automatically deploys it to **private** and **demo** environments. For more information on environments, see the [**Environments**](../environments.md) section.

**private** environment - created exclusively for you, with the purpose of developing and testing your service, when the **demo** - is a public environment, in the context of your organization \(or marketplace, if you wish to publish your service in mass and make some money on it\)

## New Service Creation

In order to create a new service, you must have an account on the [**code.store** ](https://app.code.store) platform

### Web interface

You can create a new service using the web interface by going to [https://app.code.store/services](https://app.code.store/services) by clicking on the “**create service**” button located at the bottom of the screen. Fill out the service creation form and click on the **CREATE** button. After that, the service will be available on the general list on the services page.

It takes some time for the service to be available, in general, the creation process takes less than a few minutes, during which we create a working instance of your future service, collecting an image for you, and deploying it in one of the k8s clusters. _We are actively working on the platform and in the future, the process of creating service will take no more than 10 seconds._

### CLI

In general, creating a service through the web interface or through the CLI is no different, except for the visual design. Perhaps, as a developer, the way of creating a service using the CLI will be more comfortable for you, since at the stage of creation you will receive more information about what is happening “under the hood”

In order to create a new service, you need to have a pre-installed CLI and be authorized on the [**code.store** ](https://app.code.store)platform _\(see_ [_**Getting started**_](https://app.gitbook.com/@code-store/s/docs/~/drafts/-MLmAW2NQT_EaWuncaRq/cli/code-store-cli) _guide\)_

First, go to the directory where the folder with the initialization template for your service will be created, for example, let it be your home directory.

```text
cd ~
```

Then, just execute [service creation command](https://app.gitbook.com/@code-store/s/docs/~/drafts/-MLmAW2NQT_EaWuncaRq/cli/commands#services): 

```text
cs service:create 
```

Using the **cs service: create** command, we initiate the process of creating a service, during which it will be necessary to answer the following questions:

* ? Service name: 
* ? What problem are you solving?: 
* How do you solve it?: 
* Select business domain using arrow keys
* Specify hashtags

After that, you will see the progress of creating a new service, during which we copy the starting project template, build the image, and deploy it to our k8s cluster.

We are actively working on the platform and in the future, the process of service creation will take only a few seconds.

After successfully creating the service, you will receive a message with links and secrets. Here an example of the output:

```text
Use developer key for private environment: d72e1217-28e8-44bf-9a31-9b220f2e29fc
Your service on private environment is available by this url: https://api.code.store/50de255b0812453e9ae3cec6ee7e8b83/graphql
Your service on demo environment is available by this url: https://api.code.store/ffc8b48e5c1d45e2b48d5c7b91ca6748/graphql

YOUR_SERVICE_NAME
├── codestore.yaml
├── package.json
└── src
    ├── data
    │   ├── entities
    │   └── migrations
    ├── resolvers
    │   ├── mutations
    │   ├── queries
    │   │   └── helloWorld.ts
    │   └── resolvers.ts
    └── schema.graphql
```

You can check its performance by following the links that you received when creating the service. These links lead to the GraphQL playground, which is available by default for every new service.

Please note that your service was deployed on two **private** and **demo** environments at once. For more information on environments, see the [**Environments**](../environments.md) **section.**

You also receive a _developer key_ for your **private** environment. This key must be used each time when you call your service in a **private** environment, just by adding HEADER **“x-user-authorization”.** In order to restrict access to a service that is under active development, you should use an authorization. The built-in mechanism for accessing and authorizing your services can be found in the [**Access and Authorization**](../access-and-authorization.md) section.

After creating the service - the code is available at the same dir, where you execute **cs service:create** command, in a new folder, which has the name of your service, that you specified while creating.

## File Structure

The root directory contains two files and one folder:

* `codestore.yaml` – the file that contains the configurations of your service, you can learn more about the settings on the service [**configuration**](configuration-1.md) page
* `package.json` – it is a standard NPM configuration file. Feel free and add any NPM packages you like using `npm install {packageName}`;
* `src/` – this is where all the source code lives.

Let's dive into the `src/` directory:

* `schema.graphql` – contains a [GraphQL](../../quick-start/core-concepts.md#schema-or-graphql-schema) schema of your service;
* `data/` – folder that contains entities, which required to work with the database. 
* `data/entities` – this directory contains TypeORM entities. You can automatically generate TypeScript classes for your database tables using **`cs generate:models -p src/data`** command;
* `data/migrations` – this directory contains SQL migrations for your service;
* `resolvers/` – this is where your business logic lives. 
* `resolvers/query`  and`resolvers/mutation`  – resolvers and mutations serve two purposes: connect your GraphQL objects to data in the database and is a place where you implement any additional business logic. 

Most of the things for working with the database, such as migrations, typeorm entities, can be generated using the generator built into the CLI. The principles of models and migrations generation can be found in  [**Generation**](../generation/) section.

## Local development

To simplify the local launch of the service - available simple command: **cs dev .**After execution this command on the backstage will be installed all dependencies \(npm i\), compiled typescript code \(tsc\), validating GraphQL schema, queries and mutations and applied [**middlewares**]().

Note, if the service uses a database, you need to provide the credentials \(login, password, database, port, host\) for the database object in the [**services.yaml**](configuration-1.md) file. Here an example of local configuration of services.yaml:

```text
# ./codestore.yaml

localConfiguration:
 database:
   port: 5432
   database: my-local-database
   password: password
   username: postgres
   host: localhost
```

Running this command will install all the necessary dependencies with package.json, compile the code \(for this we use tsc\), validated GraphQL schema.

After successful execution of the command, the service will be available at the link: **http://localhost:3000/grpahql** Please, make sure that **3000** port is free, before launching command.

Below is as an example of successful execution **cs dev** command

```text
2020-11-02T20:27:34.930Z [NPM] Installing dependencies 
2020-11-02T20:28:00.848Z [TypeScript] Compiling typescript code 
2020-11-02T20:28:04.570Z [GraphQL] Validating schema 
2020-11-02T20:28:04.589Z [GraphQL] Validating queries and mutations 
2020-11-02T20:28:05.856Z [INFO] Starting development server 
2020-11-02T20:28:05.856Z [Bootstrap] Start bootstrapping the application 
2020-11-02T20:28:05.864Z [Database] Connecting to database 
2020-11-02T20:28:05.983Z [Database] Successfully connected 
2020-11-02T20:28:05.985Z [GqlLoader] Loaded queries: helloWorld 
2020-11-02T20:28:05.997Z [RestLoader] Loaded REST handlers: 
2020-11-02T20:28:05.999Z [Bootstrap] GraphQL is available on: http://localhost:3000/graphql 
```

## Service update

### Create a new version

Each service from time to time has to roll our a new updates. After changes have been made to your service code - we can roll updates to the [**private** environment](../environments.md). To publish a new version you have to use **cs push** command.

{% hint style="info" %}
If you roll a new updates and don't update your version at your **packgaje.json**, we will automatically increment the path version \(x.y.**Z**\). We recommend follow [**semver**](https://semver.org/) standard and update your service version each time, when you push updates. 
{% endhint %}

Displayed service version will taken from **package.json** file.

Following our environments concept, by default, the service will be updated on the **private** environment.

Using the **cs push** command - you publish your changes. When executing this command, you will specify release notes, which will serve as information about what exactly changes have been made. Below is as an example of  successful execution **cs push** command:

```text
 Please enter release notes (semicolon separated)
 Notes: note

✔ Compiling your code
✔ Validating schema
✔ Preparing the service code for upload
```

As you can see, on the backstage we compiling your code using tsc, and validating the schema, so you can be sure that changes you made is valid. If something went wrong - you will see error message and pushing will be interrupted.

In general, working with the **cs push** command can be thought of as a git command with validation and pre-compilation of your code. In the future, we will provide access to your code through the GIT repository, but at the moment, you need to take care of this by yourself.

### Promote new version to demo environment

## Handlers

{% hint style="info" %}
You can generate your handlers using **cs generate:handler** command
{% endhint %}



