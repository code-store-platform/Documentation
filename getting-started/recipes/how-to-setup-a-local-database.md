---
description: >-
  To help you with local development of you services you'll need a local Postgre
  database.
---

# Setup a local database with your service

You know that we care about your time, so we created a local launcher for your services. But you also know that your services have a local database to store your objects.  Let's setup a local Postgre database.

{% hint style="info" %}
This tutorial covers postgre setup for mac. Follow [postgre site](https://www.postgresql.org/download/) instruction for other OS.
{% endhint %}

I love working with their simplest version: postgreapp. Go [there and download it.](https://postgresapp.com/downloads.html)

Launch the application. You have your local postgre database. You should see a small icon of postgre in your menu top bar.

Now you can go in any of your services folders and and edit codestore.yaml file. You should see something like that :

```yaml
serviceId: 145
localConfiguration:
  database:
    port: 5432
    database: database
    password: password
    username: username
    host: localhost
  application:
    port: 3000
```

 Change the database name, password, and username to the ones from [postgre configuration.](https://stackoverflow.com/questions/12720967/postgresql-how-to-change-postgresql-user-password)

To test your connection, nothing more simple : execute in the root folder of your service `cs dev` command. You should see something like that : 

```yaml
cs dev
2020-09-11T10:10:00.638Z [NPM] Installing dependencies
2020-09-11T10:10:05.359Z [TypeScript] Compiling typescript code
2020-09-11T10:10:13.745Z [GraphQL] Validating schema
2020-09-11T10:10:13.767Z [GraphQL] Validating queries and mutations
2020-09-11T10:10:17.168Z [INFO] Starting development server
2020-09-11T10:10:17.168Z [Bootstrap] Start bootstrapping the application
2020-09-11T10:10:17.168Z [Database] Connecting to database
2020-09-11T10:10:17.316Z [Database] Successfully connected
2020-09-11T10:10:17.441Z [Database] Migrations ran
2020-09-11T10:10:17.443Z [GqlLoader] Loaded queries: load
2020-09-11T10:10:17.462Z [Bootstrap] Graphql is available on: http://localhost:3000/graphql
```





