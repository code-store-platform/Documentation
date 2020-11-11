# Secret management

## Overview

Managing sensitive strings such as passwords, API keys, and secret credentials  — is just one of the steps in the quest for increasing security in a project. We understand this like no one else and provide an extremely easy and secure way of managing secret variables.

All secret variables are stored in [Vault](https://www.vaultproject.io/) \(secret storage from [HashiCorp](https://www.hashicorp.com/) organization\), which provides a high-security level thanks to its architecture and secret engines.

## Service Secrets

For convenience, all variables that we specify for the service are available as environment variables. In order to add a new variable for the service, you can use the CLI interface, which can be found on [Commands section](../../cli/commands.md).

{% hint style="info" %}
Please note, that each operation with a secret \(create, update, remove…\) will trigger container reboot. Currently, we are working on improving the current secret delivery solution. Soon, secrets variables will deliver to your services on the fly.
{% endhint %}

Let's add the **FOO** variable with the **BAR** value to the existing service with ID: **MY\_SERVICE**. For clarity, we will use a service that is deployed in a **demo** environment.  


## Project and Environment Secrets



## Inheritance

There are cases when we need to specify only one secret variable for all services, that includes in the whole project. In this case, we can just execute **cs secret:add** command without **-e** \(environment\) and **-s** \(service flags\).

