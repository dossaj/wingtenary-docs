# Dashboard Service

The dashboard service is essentially a persisted view of flight information. It is not responsible for managing flights, just to expose the information to other parties and accept subscriptions on a flight record. It also has the responsibility to provide a front end to display on ticker boards.

### Requirements

- The service MUST provide a list of upcoming departures
- The service MUST provide data over a Web API
- The service MUST be accessible via public internet
- The service MUST be scalable for large volumes
- The service MUST provide a dashboard front end.
- The service MUST allow for client to subscribe to flight changes.
- The service MUST support push notifications.

### Web API

#### Departure Endpoint

The departure endpoint is designed to retrieve the flight information. This essentially has a flat data model and queries a database. The endpoint exposes the ability to page the data, potentially OData, and is accessible anonymously.

An example request

```text
GET /api/v1/departures?$skip=0&$take=10
```

with an example data model

```js
[
    {
        "id": 1,
        "airline": "Air New Zealand",
        "flightNumber": "NZ0001",
        "departureTime": "2019-01-01T12:00:00Z",
        ...
    }
]
```

#### Subscription Endpoint

The subscription endpoint is designed to allow a client to register for notifications on a specific flight.

The dashboard service will store this record and on the update of the flight status drop a message onto the bus to send out the notification by the specified means.

An example request

```text
PUT /api/v1/departure/{id}/subscribe/
```

with an example data model

```js
[
    {
        "token": "4sfsf334534534dfsfsdfsdfs",
        ...
    }
]
```

### Technologies

Since this service is relatively small, could be called a micro service, the tech stack is relatively small and could use a number of different techs to achieve its purpose. The following has been chosen but could be changed easily. Backend stack is defined in the overview.

#### Database

A NoSQL database like MongoDB has been selected, as this service is not a source of truth for data, it also does not need to have relationships, plus lightweight, fast and schema-less can have a powerful advantage. The ability to scale is key for this server.

#### Front-End

This could be any front-end web tech. Suggested is React or Angular.

### Data Model

Data models here are essentially flat and only two are defined. See the example data models for further details.
