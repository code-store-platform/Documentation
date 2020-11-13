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

**private** environment - serves to enable an opportunity to update service and test the changes made in an isolated environment. The API of this service is accessed using a **key** that is generated when the service is created. Access to services, which deployed in this environment, has only the owner \(developer\) of this service. 

**demo** environment - serves to publish changes, after the active development process, from a private environment. demo environment - serves as a starting point for distributing the service, or its new versions, to other projects. demo environment is a public environment that is accessible without any authorization.

You don't need to worry about creating any environment when creating a new project - the code.store platform does this automatically.

More details on how to create a new service can be found in the Projects section. Information on how to deploy updates from private to demo environment is in the Versioning section.

The main concept is as follows: The developer, after he has created a new service \(or a new version of the service\) and checked its performance in a private environment, rolls out a new version of this service to the demo environment, after which the new version becomes publicly available \(for the organization that owns this service \) in order to include it in your projects or update the version of a previously included service in the project.

For services deployed on demo and private environments, a set of restrictions and rules apply. These services do not scale under load and are only available on request. These environments are created solely for the purpose of developing over the service and demonstrating their functionality.

What does it mean "services on demo and private environments are available only on request?" For example, if a service is a few days ago and no requests are received for it, we put it into standby mode. But, as soon as a request comes to it, it becomes active. From this it should be taken into account that the first request to the service, after a long time in standby mode, may take slightly longer than usual. Subsequent requests will run normally.

## Project Environments

In a micro-service architecture, deployment approaches vary greatly, but in general, environments start with development and end with production environments.

We understand how important testing and pre-release preparation is for a project and have added a staging environment. In total, the project includes the following environments: development stagning production

development and staging environments have some limitations in terms of scaling and are intended for active development and testing.

production is a production environment that has a specific set of rules for scalability and resiliency. This environment is always as stable as possible in principle. We guarantee SLA 99.99% of the services that are deployed in a production environment.

You don't need to worry about creating any environment when creating a new project - the code.store platform does this automatically.

For more information on how to create a project, how to include / exclude a service from a project, see the Projects section







