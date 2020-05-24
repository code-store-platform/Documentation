---
description: >-
  A short guide explaining the whole code.store on a single page. Don't say
  thanks ;)
---

# How it works?

![Not ideal, but clear way to understand code.store](.gitbook/assets/image%20%283%29.png)

First you need a code.store account, you can create one here.

### Create your service & GraphQL Schema

You need then create your first [service](getting-started-1/getting-started.md#service). We generate a structure of files containing your schema and code. You can use your favorite source control system to follow changes and updates to your service's code and schema.

Each time you change your [GraphQL schema](getting-started-1/graphql-schemas.md#what-is-graphql), we update and migrate your service database, no worries there.

### Promote your service to demo environment

When you're ready you can push your changes using our [CLI](cli/commands.md) to our platform. code.store will check your code, containerize it and deploy to a dev environment.  You can then promote your service to demo environment. Demo environment is used to let every developer in your organization play with you service and check if it corresponds to the needs of their [project](getting-started-1/getting-started.md#project).







