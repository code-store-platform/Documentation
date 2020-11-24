# Configuration

## Overview

Each service has a default configuration file, which available by default, after new service creation. This configuration file named `codestore.yaml` and located in the root of service dir. 

{% hint style="info" %}
**codestore.yaml** is required, without it, the service will not be launched. Please, don't remove this file.
{% endhint %}

This file contains service configuration and used to:

* enable/disable PostgreSQL database
* enable/disable Redis database
* setup configuration for local development
* contains internal code.store's serviceId

## Variables

`serviceId` internal code.store's service id

`serviceConfiguration` remote service configuration, which allows and contains next flags:

* `skipDatabase` _\(false by default\)_ boolean flag, allows to enable or disable PostgreSQL database
* `enableRedis` _\(false by default\)_ boolean flag, allows to enable or disable Redis database 

`localConfiguration` configuration, which allows to run local development service using `cs dev` CLI command and . Local configuration contains service, database \(Redis, PostgreSQL\) configurations which required if databases in `serviceConfiguration` are enabled. `localConfiguration` is contains next properties:

* `application` 
  * `port` port where an application will runs
* `database` PostgreSQL connection config
  * `port`  port, where Postgres server launched, usually it's 5432
  * `username` your Postgres user
  * `password` password for your Postgres user
  * `host` PostgreSQL host \(for example localhost or 127.0.0.0\)
  * `database` name of the database 

{% hint style="info" %}
**localConfiguration** applies only during local development process and have no impact  on deployed application
{% endhint %}

## Configuration versions

{% hint style="info" %}
In future, code.store platform will support different **codestore.yaml** configuration versions for backward compatibility. 
{% endhint %}

## Enable/Disable PostgreSQL

By default, PostgreSQL - enabled. To disable PostgreSQL set skipDatabase`: true` of the `serviceConfiguration`object and push changes using **cs push** command. 

## **Enable/Disable Redis**

By default, Redis - disabled. To enable Redis set `enableRedis: true` of the `serviceConfiguration`object and push changes using **cs push** command. 

## 



