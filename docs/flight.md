# Flight Service

The flight service is essentially flight management system, for scheduling flights and any other related information. It also has the responsibility to provide a front end to for airlines to logon to and update flight information. This service is again spilt into a backend API and front-end site.

### Requirements

- The service MUST publish flight changes to the service bus
- The service MUST provide authentication
- The service MUST provide authorization per airline
- The service MUST not be accessible via public internet
- The service MUST provide a management front end.

### Technologies

Since this service is larger and more complex, the tech stack has been tweaked to follow a more domain driven design. The following has been chosen but could be changed based on more complex requirements. Backend stack is defined in the overview as before.

#### Database

A relational database like SQL Server has been selected, as this service is a source of truth for data and has a more complicated domain model. Scalability if required could be handled by an elastic pool or other services.

#### Front-End

This could be any front-end web tech. Suggested is React or Angular. This is very dependant on team knowledge and familiarity with the chosen tech.

### Data Model

![service](/static/images/architecture.data-model.svg)
