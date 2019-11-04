---
description: >-
  The CLI makes it easy to create and configure the service, add a data schema
  and custom functions as well as deploy the service.
---

# code.store CLI

## Overview

Generally, code.store CLI provides same features as the UI of the website, i.e. all the actions and the configuration performed on the website can also be performed via CLI and vice versa.

The CLI provides the tools to create/modify/update your local version of the service and keep it up to date with the modifications performed through the website UI. It can also be included in your own CI/CD pipelines in order to build and deploy the service.

### Installation

Install the CLI globally:

```bash
$ npm install -g codestore
```

{% hint style="info" %}
The CLI can be accessed through two commands: _**codestore**_ or its shorter version _**cs**_
{% endhint %}

Once installed, perform a quick  test to ensure that it was installed properly:

```bash
$ codestore -v
```

### Usage

In order to use the CLI  you have to authenticate first:

```bash
$ cs login # this command will guide you through the authentication options
```

Once authenticated, you can create your first project:

```text
$ cs init MyFirstProject
```

{% hint style="info" %}
Most of the commands accept some specific arguments which can be provided while invoking the command in a long or short formats:

* Long format: `$ cs command --argumentName argumentValue`
* Short format: `$ cs command -a argumentValue`

Use  `$ cs help` to know more about its commands and their arguments.
{% endhint %}

