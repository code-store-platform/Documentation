# Environments

## Overview

**Environments** are created for those cases when it is necessary to create a set of independent services, with own databases, which interacted with each other, in order to isolate the environment for development, testing, and release of service groups.

In service deployment, **environments** are a kind of isolation medium. Each **environment** unites certain sets of rules which describe components that it includes, namely: services, their versions, databases, routing traffic rules... 

For convenience, we on the code.store platform creates several environments at once for the purpose of comfortable development and rolling out updates.

For example, when you creating a new project, we automatically create three environments: **development**, **staging**, **production** \(hereinafter: **Project Environments**\). 

These environments are completely isolated from each other and are separate namespaces in our k8s cluster. When we include a new service in project, we deploy a copy of a container with different databases in all three environments. 

In case when we create a new service, we deploy it on its own, isolated environments - **private** and **demo** \(hereinafter: **Service Environments**\)

## Service Environments

When we create a new service, it is automatically deployed in two environments, which called: **private** and **demo**.

### Private Environment

Private environment - serves to enable an opportunity to update service and test the changes made in an isolated environment. The API of this service is accessed using a **key** that is generated when the service is created. Access to services, which deployed in this environment, has only the owner \(developer\) of this service. 

### **Demo environment**

**demo** environment - serves to publish changes, after the active development process, from a **private** environment. **demo** environment - serves as a starting point for distributing the service, or its new versions, to other projects. demo environment is a public environment, where any person who has a link - can access service without any authorization.

You don't have to worry about creating any environment when creating a new project - code.store platform does it for you automatically.

More details on how to create a new service can be found in [**Projects**](projects.md) section. Information on how to deploy updates from **private** to **demo** environment is in the [**Versioning**](versioning.md) section.

### Concept

Developer, after new service creation, may test it and roll updates using cs push command on the **private** environment. 

When changes were made and ready to publish - a new service version can be rolled up to **demo** environment using **cs promote** command.

After promotion service to **demo** environment - a new version becomes publicly available. "Public" version - is an exact version, which will be rolled, when you include a new service in the project. 

{% hint style="info" %}
Services are available only for the owner \(person who created a service\) and the organization, which he belongs
{% endhint %}

For services deployed on **demo** and **private** environments, a set of restrictions and rules apply. These services do not scale under load and available only when requested. 

{% hint style="info" %}
What does it mean "**services on demo and private environments are available only when requested?**" For example, if service doesn't receive any HTTP requests for a long time - code.store platform will transfer it to standby mode. As soon, as a request comes to it - service container becomes active. The first request to the service, after a long time in standby mode, may take slightly longer than usual. Subsequent requests will run normally.
{% endhint %}

**private** and **demo** environments are created only for the purpose of developing service, demonstrating their functionality, and acts as a point for distributing updates.

## Project Environments

In a micro-service architecture, deployment approaches are different, but in general, environments start with **development** and **production** environments.

We understand how important testing and pre-release preparation for projects and added a **staging** environment. So, each project on the code.store platform includes the following environments: 

* development
* staging
* production

**development** and **staging** environments have some limitations in terms of scaling and intended for active development and testing.

**production** environment has a specific set of rules for scalability and availability. We guarantee SLA \(Service Level Agreement\) **99.9%** of the services deployed to the **production** environment.

You don't have to worry about creating any environment when creating a new project - the code.store platform does it automatically.

For more information on how to create a project, how to include or exclude a service from a project, see the [**Projects**](projects.md) section.







