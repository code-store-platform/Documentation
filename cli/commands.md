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

#### Global and Local workflows

CLI commands of code.store can be invoked from anywhere in your system, even if you don't have a copy of a service locally, this is what we call a **global workflow.** The advantage of this workflow is that you can quickly get status of your services without cloning them, or by invoking CLI commands from the outside of your working directory. The disadvantage is that it requires you to pass more arguments to every CLI command.

Another way of working with CLI is to call it from the local copy of the service, in that case our CLI will automatically deduct the context \(service, project, etc\).

### Authentication

```bash
$ cs help auth
Authenticate at code.store platform

USAGE
  $ cs auth:COMMAND

COMMANDS
  auth:login   Authenticate at code.store platform
  auth:logout  Clears user credentials and invalidates local session
  auth:whoami  Displays currently logged in user
```

To be able to use the CLI you have to login into your code.store account. To do that use the following command:

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

### Switching the context

```bash
$ cs context help                                                                                                                                            537ms  Wed Mar 11 18:12:23 2020
Manage global Project and Service contexts

USAGE
  $ codestore context:COMMAND

COMMANDS
  context:list     List all globally set contexts
  context:project  Manage global project context
  context:service  Manage global service context
```

In order to simplify the developer experience and reduce a number of arguments you are passing to the CLI, it is possible to set the _context,_ i.e. the _service_ or a _project_:

```bash
cs context:project [project-id]
cs context:service [service-id]
```

After setting the context, you no longer have to pass the arguments `--project-id` or `--service-id` when invoking the commands from the outside of your project directory.

{% hint style="warning" %}
Note, that the context of the working directory will always take precedence over the global context.
{% endhint %}

Get the information about the currently set context:

```bash
cs context:list
```

To clear the context use `--clear` flag:

```bash
cs context:project --clear
cs context:service --clear
```

### \[WIP\] Services

```bash
$ cs service help
```

#### List

The `cs service:list` command that can be shortened to `cs service:ls`, and is used to provide a list of your [services](../getting-started-1/getting-started.md#service) along with information about them.

```bash
cs service:list
```

By default, without any context set, this command will list all [services](../getting-started-1/getting-started.md#service). In case when a [project](../getting-started-1/getting-started.md#project) context is set, it will list only [services](../getting-started-1/getting-started.md#service-instance) inside that project. You can always list all services by adding `-all` option:

```bash
cs service:list --all
```

You can also list services for another project by providing `--project-id` argument:

```bash
cs service:list --project-id [project ID]
```

### \[WIP\] Projects

In order for your [Services](../getting-started-1/getting-started.md#service) to be published, they have to be added to [Projects](../getting-started-1/getting-started.md#project). Projects can be created and managed either by using the web-site or via CLI.

```bash
$ cs project help
```

Get a list of all your projects \(you can also use a shorthand alias `cs project:ls`\):

```bash
cs project:list
```



