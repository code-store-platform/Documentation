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

Here is a structure of the `resolvers/` directory:

* `mutations/` – 
* `queries/` – 

TODO:

* resolvers chains

### Describe your data model

### Add business logic

### Deploy to code.store

