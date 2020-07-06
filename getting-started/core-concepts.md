---
description: >-
  This page is all about definitions and vocabulary to get you on board as fast
  as possible.
---

# Core concepts

### 🧱 Service

Service is the most crucial concept in code.store. It is a stand-alone web-service that can be \(re\)used in [projects](core-concepts.md#project). What defines a service:‌

* **GraphQL** [**Schema**](/@code-store/s/docs/getting-started/core-concepts#schema-or-graphql-schema): you start by defining a GraphQL API describing types, queries and mutations of your service
* **Code**: actual code that is invoked when your GraphQL API is called. There is a specific structure and naming convention for your files which we describe in our Quick Start guide.
* **Database**: based on your GraphQL schema, there is a [database](core-concepts.md#database) where you can store your data. We take care of its creation, updates and whole management including automatic migrations in case of any change in your [GraphQL schema](core-concepts.md#schema-or-graphql-schema).
* **Documentation**: when you create a new service you need to explain what functional problem your service solves, how does it solve it and what is its functional domain \(e-commerce, content management, logistics, etc.\). You can also add some free \#tags to help users search for your service.

What makes a perfect **code.store** service :

* **Independent**: it does not rely on anything else to function \(no external APIs or services or software is required to use it\).
* **Isolated**: by all means, it should avoid communication with external systems \(except for connectors\)
* **Autonomous**: it's shipped with a database and file storage if any of those are required.
* **Solving one functional problem**: we do not limit services by size, but it must solve a real functional problem and only one. 
* **Accessible only through GraphQL**: yes, the only way to access your service and its data, is through its GraphQL API. 

Some examples of what we call service : ‌

* Shopping cart of an e-commerce site
* Meeting rooms booking system 
* Email sending service
* Credit card payment
* Promotions code management for an e-commerce site
* Client view service presenting complete information about a client gathering parts from SAP, Magento and Salesforce.

Each service has 2 [environments](core-concepts.md#environment): `private` - used by service [maker](core-concepts.md#maker) for their development and tests, and `demo`, used by developers to test the service 

### 🚧 Project

A project is a particular app or website, where you reuse your existing services. It might be your e-commerce project or a logistics mobile application or business web-app. Because you pay us only when we help you save money, we bill you only for live [services](core-concepts.md#service-instance) \(those that are included in Projects\).

Each time you add a service to a project, we create a separate, isolated instance of your [service](core-concepts.md#service-instance). Each service reused in a project has its own [environments](core-concepts.md#environment), [databases](core-concepts.md#database), logs, and billing. 

### ♻️ Service instance

A service reused in a [project](core-concepts.md#project) is an instance of a [service](core-concepts.md#service) you've created. Each time you add a service to a project, you create a service instance. Each instance of a service is isolated, runs its own set of 3 [environments](core-concepts.md#environment) \(`dev`, `stage`, `prod`\) and is accessible through its GraphQL [endpoint](core-concepts.md#endpoint).

### ⚛ Schema or GraphQL Schema

A schema or [GraphQL schema](core-concepts.md#schema-or-graphql-schema) defines and describes your [service](core-concepts.md#service). It uses [GraphQL](https://graphql.org/) [SDL](https://graphql.org/learn/schema/) with some additional directives. You have to define 3 main things:

* [**Types**](graphql-schemas.md#graphql-types): they describe objects your service are manipulating \(Product for a cart, Meeting Room for rooms booking engine or Client for a CRM service\).
* [**Queries**](graphql-schemas.md#graphql-queries-execution): at its simplest, GraphQL is about asking for specific fields on objects. It's a shorthand syntax where we omit both the query keyword and the query name, but in production apps, it's useful to use these to make our code less ambiguous. 
* **Mutations**: most discussions of GraphQL focus on data fetching, but any complete data platform needs a way to modify server-side data as well. So mutations offer your API consumers a way to create and update objects manipulated by your service \(i.e., addToCart\(productSKU\)\)

### 📁 Model

A model is a description of the way your service's database is structured. You cannot directly modify your service's model, which is generated based on the GraphQL schema of your service. We generate TypeORM entities in your service files directories here: /src/models/

‌ You can access the structure of your database or model through the web-UI data viewer too.

### 🛢Database

Each [service](core-concepts.md#service) has a managed database related to its [GraphQL schema](core-concepts.md#schema-or-graphql-schema). Each time you add, remove or update a type or a field, we automatically update and migrate your service's database. We use PostgreSQL to run your service's database, and we generate TypeORM entities to help you access your data from your service's code. You can also access your database, through ou data viewer web-UI.

### 🍱 Environment

An _environment_ is an isolated, running copy of your service. Your [service](core-concepts.md#service) is automatically shipped with 2 environments: `private` and `demo`. `Private` is visible only to you, the service [maker](core-concepts.md#maker), while `demo` is used to test the service by anyone in your [organization](core-concepts.md#organization) willing to use it on their [projects](core-concepts.md#project). It's also `demo` environment which is used in web-UI service page where users within your [organization](/@code-store/s/docs/~/drafts/-M8VZKsTXFD524H5zY8_/getting-started/core-concepts#organization) can use the playground to experiment with your service.

As soon as you reuse a [service](core-concepts.md#service) in a [project](core-concepts.md#project), you create a [service instance](core-concepts.md#service-instance) and 3 environments for this particular service in this particular [project](core-concepts.md#project): `dev`, `stage` and `prod`. Each environment has its own [endpoint](core-concepts.md#endpoint), [database](core-concepts.md#database), logs and other stuff. Be careful though, only `prod` environment is suitable to be used, well... in production, others \(`dev`, `stage`, `private`, `demo`\) have quotas and limitations and are not scalable.

Of course, you are not obliged to use any of those environments, and you can push your service to prod as soon as it's ready. However, first of all, it is not considered to be a good practice, and secondly, you may want to match the environment of your service with that of your front-end.

### 👷‍♀️Maker

If you read this documentation, you're a developer. We needed to distinguish developers who create [services](core-concepts.md#service) from those who use them in [projects](core-concepts.md#project). It's not a role or hard distinction, and you can be both consumer and maker of services within your [organization](core-concepts.md#organization). So to make it clear, we call maker the developer who created a [service](core-concepts.md#service).

### 🤷‍♂️Client

When you enable billing on your [services](core-concepts.md#service), you're prompted to invite a client to your [project](core-concepts.md#project). So on code.store, a client is an [organization](core-concepts.md#organization) who pays for [services](core-concepts.md#service) used in a project. It's entirely optional to have clients. If you don't sell your services and use them internally, you will not need to deal with clients.

### 🏢Organization

It's an entity where projects, services and users are attached to. All services you create as a maker are visible to all users within your organization. Each user of code.store is always attached to an organization.

### ⚓ Endpoint

It's the URL you need to call to connect to your [service](core-concepts.md#service) and execute [GraphQL](core-concepts.md#schema-or-graphql-schema) queries. There is an endpoint for each [environment](core-concepts.md#environment) of your [service](core-concepts.md#service). There are endpoints used to test a service before using it \(`private` and `demo` [environments](core-concepts.md#environment) attached to each service created by your [organization](core-concepts.md#organization)\), and there are 3 endpoints for each [service-instance](core-concepts.md#service-instance) inside each [project](core-concepts.md#project): `dev`, `stage` and `prod`.

