---
description: >-
  Code.store CLI provides a set of commands that allow you to manage your
  services and projects. This section contains the installation steps, a typical
  workflow and a description of main commands.
---

# Getting started

Generally, code.store CLI provides same features as the UI of the website, i.e. all the actions and the configuration performed on the website can also be performed via CLI and vice versa.

### Installation

#### macOS

```bash
brew tap codestore/brew && brew install codestore
```

#### Ubuntu 16+

```text
sudo snap install --classic codestore
```

#### Windows

```text
choco install codestore
```

### Other installation methods

#### NPM

This installation method is not recommended as it does not autoupdate.

```bash
npm install -g codestore
```

{% hint style="info" %}
The CLI can be accessed through two commands: _**codestore**_ or its shorter version _**cs**_
{% endhint %}

#### Standalone tarballs

These are available in gz compression:

* macOS
* Linux \(x64\)
* Windows \(x64\)
* Windows \(x86\)

### Verifying the installation

To verify that the CLI has been correctly installed, use the `codestore --version` command:

```bash
codestore --version
```

You should see "codestore x.y.z" output.

### Staying up to date

The code.store CLI will keep itself up to date automatically, unless you installed it via `npm install`. In that case use `npm update codestore` in order to upgrade the 

Continue to read about CLI Commands:

{% page-ref page="commands.md" %}



{% hint style="info" %}
Most of the commands accept some specific arguments which can be provided while invoking the command in a long or short formats:

* Long format: **`cs command --argumentName argumentValue`**
* Short format: **`cs command -a argumentValue`**

Use **`cs help`** to know more about its commands and their arguments.
{% endhint %}

### Service directory structure

For each service, the Code.Store CLI is generating a directory structure that resembles the following:

```bash
# Example of the directory structure of a Service
./
├── codestore.yaml # main configuration file
├── env.yaml|json # environmental variables
├── src/
│		├── models/ # can be used to override default generated model
│		│		├── example.model
│		│		└── another_example.model
│		├── schema/
│		│		└── example.graphql
│		├── functions/
│		│		├── exampleFunctionOne/
│		│		│		├── index.js
│		│		│		├── tests/
│		│		│		│		└── testExampleFunctionOne.js|ts
│		│		└── exampleFunctionTwo/
│		│				└── index.js
└── .build
```



