---
description: >-
  Did you ever play Command & Conquer? No? Continue, comrade... and you will
  find yourself on the floor, with Kukov! ☭
---

# Commands

To download and install CLI, [follow the instructions here](code-store-cli.md).

{% hint style="info" %}
You can invoke code.store CLI either by using the full **`codestore`** command, or by using the short version **`cs`**.
{% endhint %}

### Synopsis

To get a list of all commands, call `cs help`:

```bash
cs help
```

### Basic usage

{% hint style="info" %}
Most of the commands accept some specific arguments which can be provided while invoking the command in a long or short format:

* Long format: **`cs command --argumentName argumentValue`**
* Short format: **`cs command -a argumentValue`**

Use **`cs help command`** to know more about the specific command and its arguments.
{% endhint %}

### Authentication

```bash
$ cs help auth
Authentication commands, login, logout, whoami

USAGE
  $ codestore auth:COMMAND

COMMANDS
  auth:login   Authenticate at code.store platform
  auth:logout  Clears user credentials and invalidates local session
  auth:whoami  Display the currently logged in user
```

To be able to use the CLI you have to login into your **code.store** account. To do that use the following command:

```bash
cs auth:login
```

`cs login` will try to authenticate through the browser \(it is going to open the default browser in your system\).

At any time you can check under which user you are being authenticated:

```bash
cs auth:whoami
```

In order to finish your session and logout use the following command:

```bash
cs auth:logout
```

You can also use short aliases of the above commands: `cs login`, `cs whoami` and `cs logout`.

### Services

```bash
$ cs service help
Manage your services

USAGE
  $ codestore service:COMMAND

COMMANDS
  service:create    Create new service
  service:dev       Launch your service locally
  service:info      Displays detailed information about a service
  service:list      List services in your organization
  service:logs      Print the logs for your services
  service:promote   Promotes service from private env to demo
  service:pull      Download an existing service
  service:push      Push local changes to Private environment
  service:remove    Remove a service
```

#### List

The `cs service:list` command that can be shortened to `cs service:ls`, and is used to provide a list of your [services](../getting-started/quick-start/core-concepts.md#service)  along with their status.

```bash
$ cs service:list # or cs service:ls
Service ID         Name                Status
amazing-service-1  Amazing service #1  ACTIVE
amazing-service-2  Amazing service #2  ACTIVE
```

#### Create

Create a new service by calling `cs service:create` which will display a wizard and ask for some necessary information in order to create a service.

```bash
$ cs service:create
```

#### Info

Displays more detailed information about the service:

```bash
$ cs service:info
         Private                     Demo
version  0.0.3                       0.0.2
deployed 8/31/2020, 10:01:44 PM      8/31/2020, 2:48:30 PM
url      ...                         ...
```

#### Delete

Deletes the service. Deletes it for real, so please make sure that you are sure about what you are doing.

```bash
$ cs service:delete
```

#### Dev

Launches a service locally. Requires PostgreSQL and configuration in codestore.yaml.

```bash
$ cs service:dev # or cs dev
```

#### Generate

{% hint style="warning" %}
This command has been moved to **`cs generate:models`**
{% endhint %}

#### List

List the services in your organization. You can also use a short version of this command: `cs service:ls.` 

**Note:** don't be surprised to see some services when you just created an account as those may be the services created by the colleagues in your organization.

```bash
$ cs service:list
```

#### Logs

Print out the logs of your service. Available options are:

```bash
$ cs service:logs --help
Print the logs for your services

USAGE
  $ codestore service:logs

OPTIONS
  -e, --env=(private|demo|development|staging|production)  [default: development] Project environment.
  -f, --follow                                             Specify if the logs should be streamed.
  -n, --num=num                                            [default: 20] Number of most recent log lines to display.
  -p, --projectId=projectId                                Project ID
  -s, --serviceId=serviceId                                Service ID

ALIASES
  $ codestore logs
```

#### Promote

Pushes your service from Private to Demo environment.

```bash
$ cs service:promote [ID] --help
Promotes service from private env to demo

USAGE
  $ codestore service:promote [SERVICEID]

ARGUMENTS
  SERVICEID  An (optional) Service ID
```

{% hint style="info" %}
When launched without the optional Service ID argument, the command will look for `codestore.yaml` file and will promote the current service.
{% endhint %}

#### Pull

Downloads a service to the current directory.

```bash
$ cs service:pull --help
Download an existing service

USAGE
  $ codestore service:pull [SERVICEID]

ARGUMENTS
  SERVICEID  An (optional) Service ID

ALIASES
  $ codestore pull
```

{% hint style="info" %}
hen launched without the optional Service ID argument, the command will look for `codestore.yaml` file and will promote the current service.
{% endhint %}

#### Push

Push local changes to Private environment.

```bash
$ cs service:push --help
Push local changes to Private environment

USAGE
  $ codestore service:push

ALIASES
  $ codestore push
```

### Projects

In order for your [Services](../getting-started/quick-start/core-concepts.md#service) to be published, they have to be added to [Projects](../getting-started/quick-start/core-concepts.md#project). Projects can be created and managed either by using the web-site or via CLI.

```bash
$ cs project --help
🚧 A project is a particular app or website, where you can (re)use your existing services. It might be your e-commerce project or a logistics mobile application or business web-app. Each time you add a service to a project, we create a separate, isolated instance of your service. Each service reused in a project has its own environments, databases, logs, and billing

USAGE
  $ codestore project:COMMAND

COMMANDS
  project:create   Creates a new project, where you can add services
  project:delete   Removes project (only if there are no more services inside)
  project:list     List projects in your organization
  project:service  Adds and existing service to your project
```

#### Create

Launches a project creation dialogue:

```bash
$ cs project:create
? What is your project's name? Test project
? Please add a short description of your project (255 chars max): Project description
? Is everything ok, can I create this project? Yes
⠹ Creating Project Test project
```

#### Delete

Deletes the project but only if there are **no existing** services inside it. Make sure that you remove all services from the project before removing the project itself. 

```bash
$ cs service:delete --help
Removes the project (only if there are no more services inside)

USAGE
  $ codestore project:delete [PROJECTID]

ARGUMENTS
  PROJECTID  ID of the Project that should be removed
```

#### List

Get a list of all your projects \(you can also use a shorthand alias `cs project:ls`:

```bash
cs project:list
```

### Services inside the Project

In order to manage services inside your project, you can use `cs project:service` sub-commands. Most of the commands are quite similar to those of `cs service`.

```bash
$ cs project:service --help
Manage services inside your project

USAGE 
  $ codestore project:service:COMMAND
  
COMMANDS 
  project:service:add Adds and existing service to your project
  project:service:info Displays detailed information about project's service
  project:service:list Lists services in your project
  project:service:promote Promotes service inside the project between Development, Stating and Production environments
  project:service:remove Exclude service from project. This is a potentially destructive operation that might result in a loss of data.
```

#### Add

Adds an existing service to a project. Requires a Project ID as an argument.

```bash
$ cs project:service:add --help
Adds and existing service to your project

USAGE
  $ codestore project:service:add [SERVICEID]

ARGUMENTS
  SERVICEID  Id of the service

OPTIONS
  --project-id=project-id  (required) Id of the project
```

#### List

Lists services in your project:

```bash
$ cs project:service:list --help
Lists services in your project

USAGE
  $ codestore project:service:list PROJECTID

ARGUMENTS
  PROJECTID  (required) Project ID

ALIASES
  $ codestore project:service:ls
```

#### Info

Displays detailed information about project's service, in a similar way to `cs service:info`.

```bash
cs project:service:info {PROJECT} {SERVICE}
```

#### Promote

Promotes your service inside the project between Development, Staging and Production environments.

```bash
$ cs project:service:promote --help
Promotes service inside the project between Development, Stating and Production environments

USAGE
  $ codestore project:service:promote [SERVICEID]

ARGUMENTS
  SERVICEID  ID of the service

OPTIONS
  --project-id=project-id  (required) ID of the project
```

#### Remove

Removes the service from the project.

{% hint style="danger" %}
This is a destructive operation that might result in the loss of data! Please make sure that you definitely want to remove the service from the project.
{% endhint %}

```bash
$ cs project:service:remove --help
Exclude service from project. This is a potentially destructive operation that might result in a loss of data.

USAGE
  $ codestore project:service:remove [SERVICEID]

ARGUMENTS
  SERVICEID  ID of the service

OPTIONS
  --project-id=project-id  (required) ID of the project
```

### Generate

This group of commands generate scaffolding \(templates\) of some important files.

```bash
$ cs generate
Generates scaffolding (templates) of some important files

USAGE
  $ codestore generate:COMMAND

COMMANDS
  generate:handler   Generates auth.handler or context.handler
  generate:models    Generates database entities and migrations
  generate:resolver  Generates a GraphQL resolver
  generate:rest      Generates a REST API handler
```

#### Handler

Generates **`auth`** and **`context`** handlers.

```bash
$ cs generate:handler --help
Generates auth.handler or context.handler

USAGE
  $ codestore generate:handler

OPTIONS
  -f, --force                     Force overwrite file if it already exists
  -t, --handlerType=context|auth  Handler type, can be one of: context, auth.
```

Read more about the usage of those handlers in our [dedicated tutorial here](../getting-started/recipes/authentication.md).

#### Models

Generates the entity models and database migrations for your GraphQL types and puts them into `src/entities`.

```bash
$ cs generate:models
```

{% hint style="warning" %}
Entity and database generation functionalities are still in alpha version. We are iterating fast to bring the best features as soon as possible. We would be happy to hear from you about what do you think about it in our community chat here: [https://spectrum.chat/code-store](https://spectrum.chat/code-store) 
{% endhint %}

#### Resolver

Generate a template of a GraphQL resolver:

```bash
$ cs generate:resolver --help                                                                                              12.18.3
Generates a GraphQL resolver

USAGE
  $ codestore generate:resolver

OPTIONS
  -f, --force                        Force overwrite file if it already exists
  -n, --name=name                    Resolver name
  -t, --resolverType=query|mutation  Resolver type, one of: 'query' or 'mutation'
```

#### REST

Generates a template of a REST API endpoint handler:

```bash
$ cs generate:rest --help                                                                                            3s   12.18.3
Generates a REST API handler

USAGE
  $ codestore generate:rest

OPTIONS
  -f, --force                       Force overwrite file if it already exists
  -m, --method=get|post|put|delete  HTTP method, one of: get, post, put, delete
  -n, --name=name                   REST endpoint name
```

