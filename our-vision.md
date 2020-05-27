---
description: "If you have nothing else to do, you can read this long piece of art about our vision of the future of the world \U0001F926‍♀️"
---

# Our vision

### ♻️ Reusability

We created **code.store** because we believe the way software is being built today is not adapted to the pace of the modern world. We think that you should not spend time on problems that have been already solved in the past.

![From custom-built monolith to software editor powered monoliths to re-usable API components](.gitbook/assets/image%20%281%29.png)

Software started with fully custom-built monoliths. Large mono-repository projects where teams coded absolutely everything. Then came frameworks and software editor solutions \(Magento, Drupal, Wordpress, Salesforce, SAP...\), providing vertical monoliths for common needs \(CRM, e-commerce, ERP, DAM, PIM, ...\). Usually, clients of software editor solutions end overpaying for features they don't use \(a client uses only 30% of features on average\), and they still have an ever-growing budget for maintenance of a massive monolith. 

Today it's time to build software in a new way: re-using small building blocks solving a unique functional problem, like using lego bricks.

‌Modules, packages, DLLs, JARs, servlets, there has always been a desire for reusability, but there were always many barriers to reusability: technological stack, support & maintenance, integration, compatibility, and size of each component, the coupling between UX and back-end.

**So why it would be different with code.store?**

In the past years, the world of web-development saw several profound changes in the way we build software that makes out code.store idea reasonable:

* **Headless and decoupled approaches**: with robust and stable frontend frameworks like Angular, React, and Vue, it is now easy to build genuinely decoupled applications. It is important because the strongest barrier to reusability is frontend and UX. With decoupling, we can focus on API reusability.
* **GraphQL**: it offers a lot of flexibility to frontend developers. Previously, each time an application needed a product listing presented in a slightly different way, we would either have to load all the unnecessary data from a single REST endpoint or ask backend developers to provide a new "lighter" endpoint.
* **Serverless is widely accepted**: you want to reuse live, running, supported, and functional code. That means you accept that the module/service/lego brick you reuse might run somewhere and you do not care if it handles traffic and provides good SLAs.
* **Microservices are mainstream**: you already do "microservices" without knowing it, when you implement external APIs on your projects like Google Maps, Stripe or Facebook Connect . Call them nano/micro/macro/mini services, but your project is already patchwork of small, isolated, and autonomous services glued together by your frontend application.

### 💰Revenues

When independent developers, companies, or digital agencies build software for others, they usually bill time they spent on it. It's therefore complicated to re-use components from one project to another, and almost impossible to share funding, specifically when you mix hosting and support. We wanted to change that paradigm by providing a new way for billing projects.

For each service on code.store, you may activate metered or monthly billing and sell them to your clients. We take care of retrieving funds and take a small cut of only 10%. The recurring revenues cover your initial development time, hosting resources, our platform, and the time you spent on the support and maintenance of your service. 

Nowadays, « Every company is a tech company », but being a software editor is not easy. Initial technological stack, marketing, R&D investments, ROI roadmap management, indirect distribution are complex and inaccessible for most companies.

We bet that by providing a common platform and reducing the software to « bite » sized, running, live service, we’ll enable re-usability, sharing and, ultimately, billing trough direct sales or marketplace.

### 🦄 Simplicity

There are too many ways to create software today. We created code.store in a way that you can focus only on your code, while we take care of the rest \(some of the features in the list are still in the roadmap, but we are working hard to deliver them to you as soon as possible\):

* containerization
* database modeling and management
* security
* GDPR
* performance
* continuous integration and deployment
* automated tests
* monitoring
* H24 support
* instant re-use

**code.store** is a rather opinionated platform, which means we have made a certain number of choices for you to simplify the development. However, we want it to be a platform built by developers for developers, and we are open to suggestions and would be really happy to hear from you in our community chat  [https://spectrum.chat/code-store](https://spectrum.chat/code-store) !

PS: If you read it all, please [tweet](https://www.twitter.com) about us!

