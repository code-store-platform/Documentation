# Quick Start with CLI \[WIP\]

This guide will introduce some basic code.store concepts like services and schema generation using CLI. The goal of this quick start is to get you up and running fast, so lets not waste any time and start!🚀 

### Create code.store account

If you haven't done this already, then click on this link.

### Install the code.store CLI

We invite you to follow this guide and install our command line interface:

{% page-ref page="../../cli/code-store-cli.md" %}

### Authenticate and create service

Once you have your account and the CLI is installed, we can finally do some interesting stuff!

In order to work with the CLI, you have to connect it with your account by launching the following command:

```bash
cs auth:login
```

This command is going to launch your default browser and ask for your login details. Once you are authenticated, we can go on and create a new service.

```bash
cs service:create
```

![Creating your first service](../../.gitbook/assets/service-create.gif)

You can check the contents of your new service directory by running `ls -lh ./` Lets take a couple of minutes and study the contents of the directory closer.

First of all, we have a package.json file with some basic NPM packages, service name and version. Feel free and add any NPM packages you like, we are going to install them for you during the deployment of the service.

Next file is codestore.yaml which contains your service ID and will contain more configuration options later.

### Describe your data model

### 4. Add business logic

### 5. Write tests

### 6. Deployment to Code.Store.Cloud

### 7. Generate a Client and access your Service

