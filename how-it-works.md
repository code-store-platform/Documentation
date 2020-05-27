---
description: >-
  A short guide explaining the whole code.store on a single page. Don't say
  thanks ;)
---

# How it works?

![Not ideal, but clear way to understand code.store](.gitbook/assets/image%20%283%29.png)

First you need a code.store account, you can create one here.

### Create your service & GraphQL Schema

You need then create your first [service](getting-started/core-concepts.md#service). We generate a structure of files containing your schema and code. You can use your favorite source control system to follow changes and updates to your service's code and schema.

Each time you change your [GraphQL schema](getting-started/graphql-schemas.md#what-is-graphql), we update and migrate your service database, no worries there.

### Promote your service to demo environment

When you're ready you can push your changes using our [CLI](cli/commands.md) to our platform. code.store will check your code, containerize it and deploy to a dev [environment](getting-started/core-concepts.md#environment).  You can then promote your service to demo environment. Demo environment is used to let every developer in your [organization](getting-started/core-concepts.md#organization) play with you [service](getting-started/core-concepts.md#service) and check if it corresponds to the needs of their [project](getting-started/core-concepts.md#project).

### Add a service to a project

Once created, your [service](getting-started/core-concepts.md#service) cannot be used per se in a production application or site, you need to add it to a [project](getting-started/core-concepts.md#project). Projects represent applications or sites where your [service](getting-started/core-concepts.md#service) is used. Each service can be used in as many projects as you wish. You can use our web UI or [CLI](cli/commands.md) to add you service to any of your projects. Every developer in your organization can create projects and add services to them. A [service-instance](getting-started/core-concepts.md#service-instance) is created when you add a service to a [project](getting-started/core-concepts.md#project). It's a completely **isolated** version of your service : it has it's own environnements, database, API keys and logs.

### Sell your work to your clients for a monthly fee, if you want

For each [service-instance](getting-started/core-concepts.md#service-instance) in a [project](getting-started/core-concepts.md#project) you can define a rate-plan, so you can bill your clients monthly per service usage \(price per call\) or as a subscription. The core idea is to bundle together costs of building the service, its maintenance, support and hosting in a single simple fee, your client would pay. Up to today you can sell and bill services to your clients only, but we'll be launching a public marketplace as soon as we have on-boarded enough service [makers](getting-started/core-concepts.md#maker).

 







