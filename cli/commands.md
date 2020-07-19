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
Most of the commands accept some specific arguments which can be provided while invoking the command in a long or short formats:

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
  service:delete    Remove service
  service:generate  Generate entities and migrations
  service:list      List your services
  service:promote   Promotes service from private env to demo
  service:pull      Download an existing service
  service:push      Push local changes to Private environment
```

#### List

The `cs service:list` command that can be shortened to `cs service:ls`, and is used to provide a list of your [services](../getting-started/core-concepts.md#service) along with information about them.

```bash
cs service:list
```

#### Create

Create a new service by calling `cs service:create` which will display a wizard and ask for some necessary information in order to create a service.

```bash
$ cs service:create
```

#### Delete

Deletes the service. Deletes it for real, so please make sure that you are sure about what you are doing.

```bash
$ cs service:delete
```

#### Generate

Generates the entity models and database migrations for your GraphQL types and puts them into `src/entities`.

```bash
$ cs service:generate
```

{% hint style="warning" %}
Entity and database generation functionalities are still in alpha version. We are iterating fast to bring the best features as soon as possible. We would be happy to hear from you about what do you think about it in our community chat here: [https://spectrum.chat/code-store](https://spectrum.chat/code-store) 
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

In order for your [Services](../getting-started/core-concepts.md#service) to be published, they have to be added to [Projects](../getting-started/core-concepts.md#project). Projects can be created and managed either by using the web-site or via CLI.

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
  project:service:add      Adds and existing service to your project
  project:service:list     Lists services in your project
  project:service:promote  Promotes service inside the project between Development, Stating and Production environments
  project:service:remove   Exclude service from project. This is a potentially destructive operation that might result in a loss of data.
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



