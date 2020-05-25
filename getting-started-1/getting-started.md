---
description: >-
  This page is all about definitions and vocabulary. Just to make sure we
  understand each other when we talk about services, databases, projects, and so
  on.
---

# Core concepts

Modern web development is really complex and it's not becoming any easier, quite the opposite. That's why code.store provides the instruments that help you concentrate on your main goals: providing value to your clients and writing a state-of-the-art code.

With code.store you are getting:

* [GraphQL](getting-started.md#schema-or-graphql-schema)-first, fully scalable serverless API;
* Managed [database](getting-started.md#database) and storage;
* Logging and debugging tools;
* The Command Line Interface and the code.store Console that provide advanced service management capabilities and allow grouping of multiple services into projects;
* Billing for your services that allows to monetize on the internal developments.

### Vocabulary

It's important to share a common language, let's see how we name things at code.store :  

#### Service

A service is the most important concept in code.store. It is basically a stand-alone web-service that can be \(re\)used in [projects](getting-started.md#project). What defines a a service : 

* **GraphQL** [**Schema**](getting-started.md#schema-or-graphql-schema) : you start by defining a GraphQL API describing types, queries and mutations of your service
* **Code** : actual code that will be invoked when your GraphQL API is called. There is a specific structure and naming convention for your files. Don't worry we generate them for you.
* **Database** : based on your GraphQL schema, there is a database, where you can store any data you'll need. Don't worry, we take care of its creation, updates and whole management including automatic migrations in case of any change in your GraphQL schema.

What makes a perfect code.store service :

* **Independent** : it does not rely on anything else to function \(no external APIs or services or software is required to use it\).
* **Isolated** : by all means it should avoid communication with external systems \(except for connectors\)
* **Autonomous** : it's shipped with a database and file storage, if any of those are required.
* **Solving one functional problem** : we do not limit services by size, but it must solve real functional problem and only one. 
* **Accessible only through GraphQL**  : yes, the only way to access your service and its data, is trough its GraphQL API. 

Some examples of what we call service : 

* Shopping cart of an e-commerce site
* Meeting rooms booking system  
* Email sending service
* Credit card payement
* Promotions code management for an e-commerce site
* Client view service presenting complete information about a client gathering parts from SAP, Magento and Salesforce.

Each service has only 2 available [environnements](getting-started.md#environment) : dev and demo. 

#### Project

A project is a concrete app or website, where you re-use your existing services. It might be your e-commerce project, or a logistics mobile application or business web-app. Because you pay us only when we help you save money, we bill you only for services that are included in real projects. 

Each time you add a service to a project, we create a separate, isolated instance of your [service](getting-started.md#service). Each service re-used in a project will have it's own [environnements](getting-started.md#environment), [databases](getting-started.md#database), logs, and billing. 

#### Service instance \(?\)

A service re-used in a [project](getting-started.md#project) is an instance of a [service](getting-started.md#service) you've created.  Each time you add a service to a project, you actually create a service instance. Each instance of a service is isolated, runs its own set of 3 [environnements](getting-started.md#environment) \(dev, stage, production\) and is accessible through its own GraphQL endpoint.

#### Schema or GraphQL Schema

A schema or [GraphQL schema](graphql-schemas.md) defines and describes your [service](getting-started.md#service). It uses [GraphQL](https://graphql.org/) [SDL](https://graphql.org/learn/schema/) with some additional decorators. You will have to define 3 main things :

* \*\*\*\*[**Types**](graphql-schemas.md#graphql-types) : it describes objects your service will manipulate \(Product for a cart, Meeting Room for a rooms booking engine or Client for a CRM service\).
* \*\*\*\*[**Queries**](graphql-schemas.md#graphql-queries-execution) : At its simplest, GraphQL is about asking for specific fields on objects. It's a shorthand syntax where we omit both the query keyword and the query name, but in production apps it's useful to use these to make our code less ambiguous. 
* **Mutations** : Most discussions of GraphQL focus on data fetching, but any complete data platform needs a way to modify server-side data as well. So mutations offer your API consumers a way to create and update objects manipulated by your service \(ie.: addToCart\(productSKU\)\)

#### Model

A model is the description of they way your service's database is structured. You cannot directly modify your service model, which is generated based on your GraphQL schema. We generate TypeORM entities in your service files directories here :  `/src/models/`

#### Database

Each [service](getting-started.md#service) has a managed database related to its [GraphQL schema](getting-started.md#schema-or-graphql-schema). Each time you add, remove or update a `type` or a `field`, we automatically update and migrate your service's database. We use PostgreSQL to run your service's database and we generate TypeORM entities to help you access your data from your service's code. You can also access your database, through ou data viewer web-ui.

#### Environment

An environnement is an isolated, running copy of your service. Your [service](getting-started.md#service) is automatically shipped with 2 environnements : Dev and Demo. Dev is visible only to you,  service [maker](getting-started.md#maker), while Demo is used to test the service by anyone in your [organization](getting-started.md#organization) willing to use it on their [projects](getting-started.md#project).

As soon as you re-use a [service](getting-started.md#service) in a [project](getting-started.md#project), you create a service instance and 3 environnements for this particular service in this particular [project](getting-started.md#project) : Dev, Stage and Production.  Each environment has it's own [endpoint](getting-started.md#endpoint), [database](getting-started.md#database), logs, etc... Be careful, only Production environnement is suitable to be used, well.... in production, others \(dev, stage, demo\) have strong quotas and limitations and are not scalable.

#### Maker

If you read this documentation, you're a developer. We needed to distinguish developers who create [services](getting-started.md#service) from those who use them. It's not a role or hard distinction, you can be both consumer and maker of services within your [organization](getting-started.md#organization). So to make it clear : we call maker the developer who created a [service](getting-started.md#service).

#### Client

#### Organization

#### Endpoint







