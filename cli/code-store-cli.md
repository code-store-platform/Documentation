---
description: >-
  code.store CLI provides a set of commands that allow you to manage your
  services and projects. This section contains the installation steps, a typical
  workflow and a description of main commands.
---

# Getting started

### Installation

{% hint style="success" %}
We are iterating really fast in order to bring the best user experience and some great features to our product, that's why please check for updates in our CLI! 
{% endhint %}

#### macOS

```bash
brew tap code-store-platform/brew && brew install codestore
```

### Other installation methods

#### NPM

This installation method is not recommended as it does not auto-update.

```bash
npm install -g codestore
```

#### Standalone tarballs

These are available in gzip compression:

* [macOS](https://s3.code.store/codestore-darwin-x64.tar.gz)
* [Linux \(x64\)](https://s3.code.store/codestore-linux-x64.tar.gz)
* [Windows \(x64\)](https://s3.code.store/codestore-win32-x64.tar.gz)
* [Windows \(x86\)](https://s3.code.store/codestore-win32-x86.tar.gz)
* PalmOS \(just kidding\)

### Verifying the installation

To verify that the CLI has been correctly installed, use the `codestore --version` command:

```bash
codestore --version
```

You should see "codestore x.y.z darwin-X node-vX.Y.Z" output.

{% hint style="info" %}
The CLI can be accessed through two commands: _**codestore**_ or its shorter version _**cs**_
{% endhint %}

### Staying up to date

The **code.store** CLI will keep itself up to date automatically, unless you installed it via `npm install`. In that case use `npm update codestore` in order to upgrade the package to the latest version.

{% hint style="info" %}
Most of the commands accept some specific arguments which can be provided while invoking the command in a long or short formats:

* Long format: **`cs command --argumentName argumentValue`**
* Short format: **`cs command -a argumentValue`**

Use **`cs help`** to know more about its commands and their arguments.
{% endhint %}

### Service directory structure

For each service, the **code.store** CLI is generating a directory structure that resembles the following:

```bash
# Example of the directory structure of a Service
./
├── src/
│		├── data/ # contains generated TypeORM entities
│		├── resolvers/
│		│		├── mutations/
│		│				└── mutationExample.js|ts
│		│		├── queries/
│		│				└── queryExample.js|ts
│		└── schema.graphql # GraphQL definition of your service's API
├── .build # temporary directory
├── package.json # standard NPM configuration file
└── codestore.yaml # main configuration file
```

Read more about the [anatomy of the service directory here](../getting-started/quick-start/quick-start-with-cli.md#the-anatomy-of-a-service).

