# Versioning

## Overview

The bigger your system grows and the more libs or packages you integrate into your project, the more likely you are to face such a problem as dependency hell. 

As a solution, code.store platform suggests relying on a simple set of rules and requirements that govern how version numbers are assigned and incremented. There are many approaches to software versioning  and their interfaces, the choice is always up to the developer.

{% hint style="info" %}
code.store platform doesn't enforce any standard on how you need to version your services, but we **highly** **recommend** looking at a standard like [semver](https://semver.org) 

[semver](https://semver.org)'s  approach can solve most of the versioning issues
{% endhint %}

When you create a new service, by default, it deployed into  **private** and **demo** [environment](environments.md) and it's version is `0.0.1`

## Which version currently deployed?

To find out which version is in use execute `cs service:info` CLI command and select the service. You will find which versions deployed on **private** and **demo** environments.

```text
> cs service:info

              Private                                                         Demo                                                            
version       0.0.2                                                           0.0.1                                                           
deployed      8/5/2020, 10:37:21 PM                                           8/5/2020, 10:38:58 PM                                           
developer key null                                                                                                                            
url           https://api.code.store/a6203d238a744492bf1bf33833c3ebf6/graphql https://api.code.store/a858e12ddd2c47f5b381bef9d98dc7a9/graphql 
```

On example above on the **private** environment deployed service with `0.0.2` version and `0.0.1` on the **demo**. 

If you already include service to project, you can execute `cs project:service:info` CLI command, select project and service to display.  

```text
> cs project:service:info

              Development                                                     Staging                                                         Production                                                      
version       0.0.3                                                           0.0.2                                                           0.0.2                                                           
deployed      8/5/2020, 10:39:22 PM                                           8/5/2020, 10:39:23 PM                                           8/5/2020, 10:39:21 PM                                           
developer key                                                                                                                                                                                                 
url           https://api.code.store/8ddc603ea9dd4a669755bf2125bdca24/graphql https://api.code.store/bb2eae903e924bdeb3f6fe9627055d93/graphql https://api.code.store/efe4caaf5584497599728f3785e8fc7d/graphql 
```

On example above deployed on three environments deployed next versions:

| environment | version |
| :--- | :--- |
| development | 0.0.3 |
| staging | 0.0.2 |
| production | 0.0.2 |

## Create a new service version

To create a new version just push your changes using `cs push` CLI command. More information about pushing changes can be found in [Services](services/) section. After pushing changes - a new version will be available on the **private** [environment](environments.md).

It's very important to increment service version after making changes to service. Actual service version is always available at `package.json` file.

{% hint style="info" %}
By default, code.store platform will automatically increment path \(x.y.**Z**\) version of your code after each push, if you follow [semver](https://semver.org/) specification. 
{% endhint %}

## Publish a new service version

After creating a new service version using `cs push` command - changes will be available only on the **private** [environment](environments.md). 

**demo** [environment](environments.md) - is the only place, where developed changes can be published. Changes from demo environment is available for including to the project or public [access](access-and-authorization.md). 

To make a new version available - execute `cs promote` CLI command. This command will deploy changes from **private** to **demo** environment and makes a new version available for update/include into projects. Promoted version to demo environment is marks as `LATEST`

```text
cs promote
```

## Manage service version inside project

When you include a new service to the [project](projects.md) - version from **demo** [environment](environments.md) will be deployed. This allows adhering to the concept of public release of new versions to avoid unexpected system behavior. More information about including services to projects can be found in [Projects](projects.md) section.

### Move service version per environment

After including service to the project - it's deployed only to **development** [environment](environments.md). To move service version to another environment use `cs project:service:promote` CLI command. It allows you to move already deployed version to another environment.

```text
cs project:service:promote
```

For example, if your project includes some service - you can promote only already deployed service version to another environments.

### Update service version to latest

To update project service to latest version execute `cs project:service:roll` CLI command, where you can select project, environment where will be applied changes, service and version. 

Select `latest` version if you need a latest available service version.

```text
cs project:service:roll
```

### Rollback service version

To rollback service version use the same command `cs project:service:roll` and just select needed version and environment where to deploy needed version.



