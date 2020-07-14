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
Authenticate at code.store platform

USAGE
  $ codestore auth:COMMAND

COMMANDS
  auth:login   Authenticate at code.store platform
  auth:logout  Clears user credentials and invalidates local session
  auth:whoami  Displays currently logged in user
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

### Switching the context

```bash
$ codestore context help                                                                                                                                            537ms  Wed Mar 11 18:12:23 2020
Manage global Project and Service contexts

USAGE
  $ codestore context:COMMAND

COMMANDS
  context:list     List all globally set contexts
  context:project  Manage global project context
  context:service  Manage global service context
```

In order to simplify the developer experience and reduce the number of arguments you are passing to the CLI, it is possible to set the _context,_ i.e. the _service_ or a _project_:

```bash
codestore context:project [project-id]
codestore context:service [service-id]
```

After setting the context, you no longer have to pass the arguments `--project-id` or `--service-id` when invoking the commands from the outside of your project directory.

{% hint style="warning" %}
Note, that the context of the working directory will always take precedence over the global context.
{% endhint %}

Get the information about the currently set context:

```bash
codestore context:list
```

To clear the context use `--clear` flag:

```bash
codestore context:project --clear
codestore context:service --clear
```

### \[WIP\] Services

```bash
$ codestore service help
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



