# Architecture

The following sections cover the overall architecture as well as how each service is structured.

## System Architecture

The following diagram illustrates the components of the system.

![architecture](/static/images/architecture.system.svg)

#### 1. Authentication and Authorization

Supports the login of the users as well as the issuing of tokens for each user. User are associated with claims that include the airline for authorization. An example would be something like **read:airline:airnz**. This service is out of scope for this design also, along with user registrations and user management.

#### 2. Service Bus

The system is agnostic to the service bus provider. A technology like NService Bus handles different transports. This means the service selection could be anything. Ideally the configuration is pushed as part of the continuous delivery.

#### 3. Notification Service

Since this service is not a direct necessity for MVP it is out of scope. It provides the ability to have multiple types of notifications allows for extensibility, as well as provides a smaller service component, which can handles the different providers, templates and translations etc. Push notifications and additional systems like email, text message can easy be supported. Service components can drop messages on to the bus, or make API calls, to trigger notifications.

#### 4. Dashboard Service

The dashboard service is broken out to a public facing service providing an API and a front end to display the ticker. The dashboard service holds a *persisted view* of flight and is cut down to be as thin as possible. This service is front facing and scalable quickly for load. It also provides the subscription endpoint.

This service is covered in more detail [here](dashboard.md).

#### 5. Flight Service

The flight service is a backend component for airlines to manage their flight schedule it is also broken down into an API and web portal front end. The flight service is the main service providing the airline functionality required. The flight service is responsible for managing the flight, as well as publishing events and notifications of changes.

The usage on this system would be a lot less and can be built for maintainability over performance.

This service is covered in more detail [here](flight.md).

## Service Architecture

The service architecture is design to keep clean separation of layers.

The service is abstracted from it's host to allow the service within different processes based on necessity. Along with the standard flexibly of each layer.

![service](/static/images/architecture.service.svg)
