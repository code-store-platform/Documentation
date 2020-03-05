# Commands

To download and install CLI, [follow the instructions here](code-store-cli.md).

{% hint style="info" %}
You can invoke code.store CLI either by using the full **`codestore`** command, or by using the short version **`cs`**.
{% endhint %}

### Synopsis

To get a list of all commands, call `cs --help`:

```bash
cs --help
```

### Basic usage

{% hint style="info" %}
Most of the commands accept some specific arguments which can be provided while invoking the command in a long or short formats:

* Long format: **`cs command --argumentName argumentValue`**
* Short format: **`cs command -a argumentValue`**

Use **`cs help`** to know more about its commands and their arguments.
{% endhint %}

#### Global and Local workflows

CLI commands of code.store can be invoked from anywhere in your system, even if you don't have a copy of a service locally, this is what we call a **global workflow.** The advantage of this workflow is that you can quickly get status of your services without cloning them, or by invoking CLI commands from the outside of your working directory. The disadvantage is that it requires you to pass more arguments to every CLI command.

Another way of working with CLI is to call it from the local copy of the service, in that case our CLI will automatically deduct the context \(service, project, etc\).

### Authentication

To be able to use the CLI you have to login into your code.store account. To do that use the following command:

```bash
cs login
```

At any time you can check under which user you are being authenticated:

```bash
cs whoami
```

In order to finish your session and logout use the following command:

```bash
cs logout
```

### Switching the context

In order to simplify the DX and reduce the number of arguments you are passing to the CLI, it is possible to set the _context,_ i.e. the service or a project.

```bash
cs context:project [project-id]
cs context:service [service-id]
```

After setting the context, you no longer have to pass the arguments `--project-id` or `--service-id` when invoking the commands from outside of your project directory.

{% hint style="warning" %}
Note, that the context of the working directory will always take precedence over the global context.
{% endhint %}

### Services

#### List

The `cs service:list` command that can be shortened to `cs service:ls`, and is used to provide a list of your services along with information about them.

```bash
cs service:list
```

By default, without any context set, this command will list all services. In case when a project context is set, it will list only services inside that project. You can always list all services by adding `-all` option:

```bash
cs service:list --all
```

You can also list services for another project by providing `--project-id` argument:

```bash
cs service:list --project-id [project ID]
```

