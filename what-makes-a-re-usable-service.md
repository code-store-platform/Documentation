# ?? What makes a re-usable service ?

When starting a new project you should consider what parts of it may be re-used later for other projects or clients, but also how well isolated those parts are from the rest of your project.  

What size should a service be? When developing a service, size shouldn't be the important point. Instead, the important point should be to create loosely coupled services so you have autonomy of development, deployment, and scale, for each service. Of course, when identifying and designing services, you should try to make them as small as possible as long as you don't have too many direct dependencies with other services. More important than the size of the service is the internal cohesion it must have and its independence from other services.

### Let's take some examples

Imagine you won the creation of the next digital platform for a large international hotels chain. You have to develop a B2C site where users can search and book hotel rooms, and manage their check-in and check-outs. 

Let's see what kind of re-usable services you may put on code.store.

### Horizontal & vertical growth of services

The first would be the search for available rooms. You might create a service where users can declare their properties \(rooms, size, type, description\) and search for available rooms for a given number of persons and time ranges. Immediately you can see that this service is strongly coupled with the booking process itself. So it might be interesting to add booking user stories. 

You can then take two paths to your service roadmap : 

* Vertical : you implement everything needed within hospitality industry. Including B2B travellers, travel managers, options to the bookings, cross-sells and up-sells. Pushing automatically unsold rooms on booking.com...
* Horizontal : you want to make the most generic search & book engine, making it usable for hotel rooms, meeting rooms, massage sessions or co-working places. You need then reduce the number of features, making existing ones highly configurable \(book for 20 minutes or for 6 months, book  2 available ressources or 2000...\)

### Wrappers and connectors

The second type of services that are good candidates for reuse are wrappers and connecters. Let's take two examples again : 

National Weather governmental organization have a paid service providing with accurate weather forecasts entreprises. But to use their services the process is extremely painful : you need to contact them, sign a contract and ultimately you get their data trough SOAP or, worse, SFTP and XML. For many reasons it's might be possible you cannot touch your legacy systems or processes. 

You can then create a wrapper code.store service that takes as input data from your legacy systems and presents them as  a modern GraphQL based service, you can easily sell on a pay as you go or subscription.

Some clients may also need for a connecter between 2 applications and find Zappier too limitative. You can then create a highly configurable services connecting the 2 applications and sell it based on the volume of data exchanged. 

### What makes a good, re-usable service ?

A good, re-usable micro-service should be

1. **Isolated** : your service must being able to work alone, providing a real value for the end user. It should not depend on other services, out of code.store
2. **Configurable** : each time you'll use it on a project, you should be able to adapt it's behaviour, without touching your code to concrete needs of your project.
3. **UX friendly** : your service will be probably called by a mobile application or a ReactJS web-app, so you should think first about from a usage prospective rather than from your data structure point of view.
4. **Documented** : it's important than other members of your organization immediately understand what your service is doing. Do no describe your internal mechanics, but input and output, data structure and provide test data. Do not assume that specific business vocabulary is understood by your audience. Use examples !
5. **Generic** : Your service will be re-used 







