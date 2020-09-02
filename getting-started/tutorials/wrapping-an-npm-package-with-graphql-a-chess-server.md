---
description: 'Let''s have fun : create a GraphQL chess server !'
---

# Wrapping an NPM package with GraphQL: a chess server

In some projects you'll need to include some NPM packages and run them as a service. Let's take an example and create a chess server using [chess.js](https://github.com/jhlywa/chess.js/blob/master/README.md)

We consider that you're familiar with **code.store** CLI, you have an account and you know how to create a new service. If not, follow our [quick start guide](../quick-start/quick-start-with-cli.md). 

## Step 1: Create a new service

Check that you're authenticated :

```text
cs whoami
```

If you receive following error message, that means you're not authenticated and you'll need to execute `codestore auth:login` command.

```text
Seems that you're not logged in. Please execute  codestore login  command to sign-in again.
```

Let's create a new service :

```text
cs service:create

 What is your service name?
 It should be the shortest meaningful name possible, for example:
        Meeting-rooms booking
 Service name: Chess Server

 Describe what functional problem are you solving with your service?
 It's optional and here is an example:
        My service manages meeting rooms and their booking by users
 What problem are you solving?: Let consumers play chess using GraphQL

 Describe how you solve it? It's optional too and should look something like:
        This service provides an API to create, update and delete rooms and
        another set of queries to manage bookings, cancellations, and search for available rooms.
 How you solve it?: Wrapping chess.js into a GraphQL endpoint

 What is the most relevant business domain of your service?
 Use up/down arrows to navigate and hit ENTER to select.
 Please select 'Other' as last option
 Business domain: Content_Management

 Now, the last thing, enter free-hashtags describing your service.
 Up to 5, comma-separated, no need to add #.
 Example:
        hospitality, booking, meeting-rooms, office
 Hashtags: games,chess,play,fun
```

You should get something like that : 

```text
✔ Created service with ID: chess-server
✔ Private and demo environment containers were built
✔ Deployed to private and demo environments
✔ Downloading service template 
Your service on private environment is available by this url: https://api.code.store/121066bcd3ae4a049a326c99639e26bc/graphql
Your service on demo environment is available by this url: https://api.code.store/858f86742a234d0b91be456a59089adb/graphql
```

## Step 2: Chess game schema

As we created our service, the first thing we need to do is to modify the default GraphQL schema by adding a new Type: Game. Players will interact with our API to play chess, games will be stored in our database. Inside your service, you'll need to edit the `/src/schema.graphql` file.







