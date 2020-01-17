# Service & Project Lifecycle

Management and deployment of microservices can be a tedious task. At code.store we continuously invest into simplification of these tasks to make the process of creation and management of APIs in the cloud as simple as possible.

When you create a new service it is created in a _Repository_ and is not publicly exposed. Each Service in a _Repository_ has three environments at its disposal: Dev, Stage and Public Playground. The Public Playground environment is going to be used as a source of API and Data for a Playground displayed on a public service page.

_Repository_ environments are restricted in terms of resources and you will have to create a _Project_ in order to use the service in the real world. Project is a way to group services used for the same client \(or a group of clients\), can have its own billing and provides four environments per service: Dev, Stage, PreProd and PROD.

The typical development workflow of a service would be:

* create a Service in a _Repository_;
* develop your Service on Dev and test on Stage;
* once the Service development is finished and you are ready to release a new version, the Service is deployed to Public Playground;
* you need to use the Service for some of your clients and you create a Project dedicated to this client and add a Service to this Project;
* inside the Project, your Service has four instances \(also called environments\): Dev, Stage, PreProd and Prod, which can be integrated into your typical development workflow.

