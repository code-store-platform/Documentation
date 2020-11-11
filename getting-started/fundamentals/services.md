# Services

## Overview

**Services** - is the main entity that you operate on when working with the [**code.store** ](https://app.code.store) framework. These are backends that you, members of your organization, or public users of the [**code.store** ](https://app.code.store) platform creates.

One of the key features of our platform is the reuse of services. Since the service doesn't belong to any specific project, you can reuse the services that are available to you.

For convenience, the [**code.store** ](https://app.code.store) platform provides the ability to develop your services in various languages:

* TypeScript

Currently, we are actively working on adding support for different languages and frameworks, such as: Go, PHP, Python, Java, C\#... so soon you will be able to see support for your particular technology.

Using the CLI or web interface - you can _create/edit/update/add to projects/delete_ your services. Below are examples of how this can be done.

When service is created - the platform automatically deploys it to **private** and **demo** environments. For more information on environments, see the [**Environments**](environments.md) section.

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

Please note that your service was deployed on two **private** and **demo** environments at once. For more information on environments, see the [**Environments**](environments.md) **section.**

You also receive a _developer key_ for your **private** environment. This key must be used each time when you call your service in a **private** environment, just by adding HEADER **“x-user-authorization”.** In order to restrict access to a service that is under active development, you should use an authorization. The built-in mechanism for accessing and authorizing your services can be found in the [**Access and Authorization**](access-and-authorization.md) section.

After creating the service - the code is available at the same dir, where you execute **cs service:create** command, in a new folder, which has the name of your service, that you specified while creating.

## File Structure

The root directory contains two files and one folder:

* `codestore.yaml` – contains your service ID and will contain more configuration options in later versions;
* `package.json` – it is a standard NPM configuration file. Feel free and add any NPM packages you like using `npm install {packageName}`;
* `src/` – this is where all the source code lives.

Let's dive into the `src/` directory:

* `schema.graphql` – one of the most \(if not the most\) important files. It contains a [GraphQL](../quick-start/core-concepts.md#schema-or-graphql-schema) schema of your service;
* `data/` – this directory contains TypeORM entities. You can automatically generate TypeScript classes for your database tables using **`cs generate:models -p src/data`** command;
* `resolvers/` – this is where your business logic lives. Resolvers serve two purposes: connect your GraphQL objects to data in the database and is a place where you implement any additional business logic.





