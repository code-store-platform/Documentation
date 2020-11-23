# Logging

## Overview

From time to time becomes necessary to monitor the status and progress of a deployed application, look at the current application activity, or debug an error. 

code.store platform provides an interface for working with report **logs**. By default logs contain information about the exceptions that the deployed application produces, service bootstrap and other things that the developer considered necessary to add as logs.

On backstage, as a log storage code.store platform used [elasticsearch](https://www.elastic.co/elasticsearch/) database, which allows to organize a quick search through the logs. 

{% hint style="info" %}
Note: logs are stored on the platform for a month.
{% endhint %}

## Service logs

To reach service logs navigate to your service **directory** and execute **cs service:logs** command, or specify service ID using `-s` flag. Below is an example of listing **demo\_app** service logs, where demo\_app is an id of [service](services/).

```typescript
> cs logs -s demo_app

Displaying logs for environment private, service demo_app
2020-11-17T14:02:49.243Z [GqlLoader] Loaded queries: helloWorld
2020-11-17T14:02:49.338Z [RestLoader] Loaded REST handlers:
2020-11-17T14:02:49.341Z [RestLoader] -> /name - GET
2020-11-17T14:02:49.341Z [Bootstrap] -> [GET] http://localhost:3002/rest/name
2020-11-17T14:02:49.341Z [Bootstrap] REST endpoints are available on:
2020-11-17T14:02:49.341Z [Bootstrap] GraphQL is available on: http://localhost:3002/graphql
```

{% hint style="info" %}
Logs for **private** [environment](environments.md) will be displayed, if environment is not specified manually.
{% endhint %}

By default, command display only 20 of the most recent log lines, to increase output lines count use `-n` flag. Below is an example of listing **demo\_app** service logs, where output lines count are set to **1000**

```typescript
> cs logs -s demo_app -n 1000
```

## Project and environment logs

### Project logs

To access full [project](projects.md) logs you should specify project ID using `-p` flag. 

{% hint style="info" %}
To list your available project execute **cs project:service:list** command. Learn more on the [**Projects**](projects.md) section.
{% endhint %}

```typescript
> cs logs -p my_project
```

After command execution logs from all deployed services on all \(development, staging, production\) environments will be [displayed](environments.md).

### Environment logs

To filter environments just specify environment name using `-e` flag. Below is an example of displaying **logs** of all deployed services on **development** [environment](environments.md) of **my\_project** [project](projects.md).

```typescript
> cs logs -p my_project -e development
```

Also, you can display service logs from **demo** and **private** [environment](environments.md). To display these logs specify environment name using `-e`  and service id using `-s` flag.

```typescript
> cs logs -s demo_app -e demo
```

## Logger

### Overview

code.store platform read full **stdout** log and store, you may use any convenient logger. But, to make developers life easier - code.store platform provides a built-in **logger**, which can be imported from `codestore-utils`.

```typescript
import { logger } from 'codestore-utils';
```

Built-in logger provides default method for logging and map each log for future text search. Logger provides default logging methods, such as:

* `log` - informational logs that might make sense to system administrators, and highlight the progress of the application
* `error` - error logs of considerable importance that will prevent normal program execution, but might still allow the application to continue running
* `warn` - potentially harmful situations of interest that indicate potential problems - 
* `debug` - information that is diagnostically helpful to people more than to system administrators
* `verbose` - verbose information about any thing which may be useful

### Usage

By default, any log method consume three params: `message`, `context` and `data`.

```typescript
public log(message: any, context = '', data?: any): void
public warn(message: any, context = '', data?: any): void
public debug(message: any, context = '', data?: any): void
public verbose(message: any, context = '', data?: any): void
```

`message` - is a message, which will be logged

`context` \(empty by default\) - is a prefix of message, which usually indicated where method was executed \(method, or constructor name for example...\). This param are .

`data` \(optional\) - is an optional object, which will be stringify and append to the `message`

Example of usage:

```typescript
import { logger } from 'codestore-utils';


logger.log('User received a new achievement', `${this.constructor.name}`, { achievement: { name: 'STAR', level: 3 }});
```

An exception to the rule is an `error` method that has a slightly different signature:

```typescript
public error(error: string | Error, trace = '', context = '', data?: any): void
```

This method usually used to log a handled exception. You can just pass an error object as first argument and **logger** will format a message to valid format. For example:

```typescript
import { logger } from 'codestore-utils';


try {
    throw new Error('This is an error...');
} catch(e) {
    logger.error(e);
}

```



