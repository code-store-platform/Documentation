---
description: "A short guide explaining the whole code.store in a single page. Don't say thanks! \U0001F44A"
---

# How it works?



![Schema is not perfect but represents quite well code.store. ](.gitbook/assets/image%20%284%29.png)

### Create your service & GraphQL Schema

The [service](getting-started/core-concepts.md#service) you are building is going to be consumed by your clients \(real clients or frontend teammates\) via an API \(GraphQL\), which your service is exposing. That is why we believe in the schema-first approach, where you are required to define an [API \(or a schema\)](getting-started/core-concepts.md#schema-or-graphql-schema) first and then develop a backend that provides data for this schema \(as opposed to a code-first approach where the schema is generated from the code you write\). [GraphQL schema](getting-started/core-concepts.md#schema-or-graphql-schema) \(or API\) IS YOUR PRODUCT! That is why everything starts with a [schema](getting-started/core-concepts.md#schema-or-graphql-schema) at code.store.

### Database generation

We strive to simplify your life, and so we are taking the complexity of database management from your shoulders and are g[enerating database tables](getting-started/core-concepts.md#database) automatically from your schema. Whenever you add a new type, field, or modify the existing ones, our platform _generates_ migrations and[ TypeORM Entities \(also called models\),](getting-started/core-concepts.md#model) which you can use to write business logic in resolvers.

{% hint style="info" %}
_At the moment, we are supporting Typescript/JS services, thus the generation of TypeORM models. We are going to support other programming languages as well, with PHP being the next one._
{% endhint %}

### Promote your service to _a_ private environment

When ready, push your changes to our cloud using the [CLI](cli/commands.md) to our platform. code.store will check your code, containerize it, and deploy _it_ to a private [environment](getting-started/core-concepts.md#environment).  You can then promote your service to the Demo environment, which is used to let every developer in your [organization](getting-started/core-concepts.md#organization) experiment with your [service](getting-started/core-concepts.md#service) and check if it corresponds to the needs of their [project](getting-started/core-concepts.md#project).

### Add a service to a project

Once created, your [service](/@code-store/s/docs/~/drafts/-M8Li-hHXy6npg1jgtmS/getting-started/core-concepts#service) cannot be used per se in a production application or site, you need to add it to a [project](/@code-store/s/docs/~/drafts/-M8Li-hHXy6npg1jgtmS/getting-started/core-concepts#project). Projects represent applications or sites where _your_ [service](/@code-store/s/docs/~/drafts/-M8Li-hHXy6npg1jgtmS/getting-started/core-concepts#service) is used. Each service can be used in as many projects as you wish. You can use our web UI or [CLI](/@code-store/s/docs/~/drafts/-M8Li-hHXy6npg1jgtmS/cli/commands) to add you service to any of your projects. Every developer in your organization can create projects and add services to them. A [service-instance](/@code-store/s/docs/~/drafts/-M8Li-hHXy6npg1jgtmS/getting-started/core-concepts#service-instance) is created when you add a service to a [project](/@code-store/s/docs/~/drafts/-M8Li-hHXy6npg1jgtmS/getting-started/core-concepts#project). It's an entirely **isolated** version of your service: it has its dedicated environments, database, and logs.

### Sell your work to your clients for a monthly fee, if you want 💰

For each [service-instance](/@code-store/s/docs/~/drafts/-M8Li-hHXy6npg1jgtmS/getting-started/core-concepts#service-instance) in a [project](/@code-store/s/docs/~/drafts/-M8Li-hHXy6npg1jgtmS/getting-started/core-concepts#project), you can define a rate-plan so that you can bill your clients monthly per service usage \(price per call\) or as a subscription. The core idea is to bundle together costs of building the service, its maintenance, support, and hosting in a single simple fee that your client pays. Up to today, you can sell and bill services to your clients only, but we'll be launching a public marketplace as soon as we have _enough on-board service_ [makers](/@code-store/s/docs/~/drafts/-M8Li-hHXy6npg1jgtmS/getting-started/core-concepts#maker).

