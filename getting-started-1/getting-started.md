---
description: >-
  code.store is an API-as-a-Service (or Backend-as-a-Service) that provides a
  powerful reuse platform with billing capabilities and marketplace.
---

# Core concepts

Modern web development is really complex and it's not becoming any easier, quite the opposite. That's why code.store provides the instruments that help you concentrate on your main goals: providing value to your clients and writing a state-of-the-art code.

With code.store you are getting:

* GraphQL-first, fully scalable serverless API;
* Managed database and storage;
* Logging and debugging tools;
* The Command Line Interface and the code.store Console that provide advanced service management capabilities and allow grouping of multiple services into projects;
* Billing for your services that allows to monetize on the internal developments.

### Vocabulary

It's important to share a common language, let's see how we name things at code.store :  

#### Service

A service is the most important concept in code.store. It is basically a stand-alone web-service that can be used in projects. What defines a a service : 

* GraphQL Schema : you start by defining a GraphQL API describing types, queries, mutations of your service
* Code : actual code that will be invoked when your GraphQL API is called.
* Database : based on your GraphQL schema, we'll generate a database model, where you can store any data you'll need 



* Independent : it does not rely on anything else to function \(no external APIs or services or software is required to use it\).
* Isolated : by all means it should avoid communication with external systems \(except for connectors\)
* Autonomous : it's shipped with a database and file storage, if any of those are required.
* Solving one functional problem : we do not limit services by size, but it must solve real functional problem and only one. 
* Accessible only trough GraphQL 

Some examples of what we call service : 

* Shopping cart
* Meeting rooms reservation API
* Email sending service
* Credit card payement
* Promotion code management

 

#### Project

A project is a concrete app, where you re-use your existing services. It might be your e-commerce project, or a logistics mobile application. Because you pay us only when we help you save money, we bill you only for services that are included in real projects. 

Each time you add a service to a project, we create a separate, isolated instance of your code. Each service re-used in a project will have it's own environnements, databases, logs, and billing. 

#### Service instance \(?\)

A service re-used in a project is an instance of a service you've created. 

Schema

Environment

Maker

Client





