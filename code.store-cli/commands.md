# Commands

To download and install CLI, [follow the instructions here](code-store-cli.md).

{% hint style="info" %}
You can invoke code.store CLI either by using the full **`codestore`** command, or by using the short version **`cs`**.
{% endhint %}

### Synopsis

To get a list of all commands, call `cs --help`:

```text
cs --help
```

### Basic usage

{% hint style="info" %}
Most of the commands accept some specific arguments which can be provided while invoking the command in a long or short formats:

* Long format: **`cs command --argumentName argumentValue`**
* Short format: **`cs command -a argumentValue`**

Use **`cs help`** to know more about its commands and their arguments.
{% endhint %}

### Authentication

To be able to use the CLI you have to login into your code.store account. To do that use the following command:

```text
cs login
```

At any time you can check under which user you are being authenticated:

```text
cs whoami
```

In order to finish your session and logout use the following command:

```text
cs logout
```

