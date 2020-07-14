---
description: >-
  Did you ever play Command & Conquer? No? Continue, comrade... and you will
  find yourself on the floor, with Kukov! ☭
---

# Commands

To download and install CLI, [follow the instructions here](code-store-cli.md).

### Synopsis

To get a list of all commands, call `codestore help`:

```bash
codestore help
```

### Basic usage

{% hint style="info" %}
Most of the commands accept some specific arguments which can be provided while invoking the command in a long or short formats:

* Long format: **`codestore command --argumentName argumentValue`**
* Short format: **`codestore command -a argumentValue`**

Use **`codestore help command`** to know more about the specific command and its arguments.
{% endhint %}

#### Global and Local workflows

CLI commands of code.store can be invoked from anywhere in your system, even if you don't have a copy of a service locally, this is what we call a **global workflow.** The advantage of this workflow is that you can quickly get the status of your services without cloning them, or by invoking CLI commands from the outside of your working directory. The disadvantage is that it requires you to pass more arguments to every CLI command.

Another way of working with CLI is to call it from the local copy of the service, in that case, our CLI will automatically deduct the context \(service, project, etc\).

### Authentication

```bash
$ codestore help auth
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
codestore auth:login
```

`codestore login` will try to authenticate through the browser \(it is going to open the default browser in your system\).

At any time you can check under which user you are being authenticated:

```bash
codestore auth:whoami
```

In order to finish your session and logout use the following command:

```bash
codestore auth:logout
```

You can also use short aliases of the above commands: `codestore login`, `codestore whoami` and `codestore logout`.

### Services

```bash
$ codestore service help
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

The `codestore service:list` command that can be shortened to `codestore service:ls`, and is used to provide a list of your [services](../getting-started/core-concepts.md#service) along with information about them.

```bash
codestore service:list
```

By default, without any context set, this command will list all [services](../getting-started/core-concepts.md#service). In case when a [project](../getting-started/core-concepts.md#project) context is set, it will list only [services](../getting-started/core-concepts.md#service-instance) inside that project. You can always list all services by adding `-all` option:

```bash
codestore service:list --all
```

You can also list services for another project by providing `--project-id` argument:

```bash
codestore service:list --project-id [project ID]
```

### \[WIP\] Projects

In order for your [Services](../getting-started/core-concepts.md#service) to be published, they have to be added to [Projects](../getting-started/core-concepts.md#project). Projects can be created and managed either by using the web-site or via CLI.

```bash
$ codestore project help
```

Get a list of all your projects \(you can also use a shorthand alias `codestore project:ls`\):

```bash
codestore project:list
```



