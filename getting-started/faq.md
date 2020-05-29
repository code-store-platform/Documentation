---
description: >-
  You'll find all the answers you were looking for since you were born. TL;DR>
  42.
---

# FAQ

## 🏠 Where my services are hosted?

**code.store**  is cloud-agnostic, meaning we can deploy **code.store** on any cloud provider or even on-premises for Enterprise clients.

Services of all other plans are currently hosted on our AWS infrastructure \(Frankfurt region at the moment, other regions are coming soon\).

## 🦄 Who creates services?

You do it. Don't be lazy. [Code](https://code.store). 😈

## 💰How do I monetize my services?

There is no public marketplace yet. When you build new projects for your clients, you can create some part of those [projects](/@code-store/s/docs/~/drafts/-M8VKgZ9kST8_aoru2ZT/getting-started/core-concepts#project) as reusable [services](/@code-store/s/docs/~/drafts/-M8VKgZ9kST8_aoru2ZT/getting-started/core-concepts#service). Then you can sell them to your clients with a subscription or pay-per-use rate plan.

When you add a [service](/@code-store/s/docs/~/drafts/-M8VKgZ9kST8_aoru2ZT/getting-started/core-concepts#service) in a [project](/@code-store/s/docs/~/drafts/-M8VKgZ9kST8_aoru2ZT/getting-started/core-concepts#project), you can set up a different price for each of your [service-instances](/@code-store/s/docs/~/drafts/-M8VKgZ9kST8_aoru2ZT/getting-started/core-concepts#service-instance). You can then invite your client to this [project](/@code-store/s/docs/~/drafts/-M8VKgZ9kST8_aoru2ZT/getting-started/core-concepts#project), providing his billing details. We'll generate the invoice for each client and collect payments for you. Each month you'll receive your combined funds collected from all clients in a single payment from us. Money time!

## 💵 How should I price my services?

You can bundle in a single monthly rate everything: 

* your initial build cost _\(example: the 50 working days used to build the service\)_
* support and maintenance time _\(example: the 5 working days you spend every month on this service\)_
* hosting _\(code.store costs\)_ 
* and provision for new features _\(for example yearly 20 working days used to add new features to your service\)._ 

## 🗣️ What programming languages do you support?

At the moment we support only [_TypeScript_](https://www.typescriptlang.org/) __\(which is the 2nd most loved programming language in the world 🤘 as per [the 2020 Stack Overflow survey](https://insights.stackoverflow.com/survey/2020#technology-most-loved-dreaded-and-wanted-languages-loved)\). If you need a specific language for your [project](/@code-store/s/docs/~/drafts/-M8VKgZ9kST8_aoru2ZT/getting-started/core-concepts#project), drop us a word [here](https://spectrum.chat/code-store).

## 🛢 I need a database for my service, how do I create one?

We provide a managed Postgres database for your services, but you don't have to worry about it as **code.store** creates and updates your [database](/@code-store/s/docs/~/drafts/-M8VKgZ9kST8_aoru2ZT/getting-started/core-concepts#database) based on the [GraphQL schema](/@code-store/s/docs/~/drafts/-M8VKgZ9kST8_aoru2ZT/getting-started/core-concepts#schema-or-graphql-schema) of your [service](/@code-store/s/docs/~/drafts/-M8VKgZ9kST8_aoru2ZT/getting-started/core-concepts#service).

## 🧱 What is a service?

We call a service piece of code running on our platform that is accessed through a GraphQL API. You can learn more about our core concepts here.

## 🖼️ Where should I host my front-end?

We provide a platform to create and host back-end services that are accessed through GraphQL API. So at the moment, we are not focused on this particular feature, especially knowing that there are already many great services that can help host your frontend in the cloud.

However, this is something that is in our roadmap, and you can [drop us a message in our community](https://spectrum.chat/code-store) to help us prioritize it!

