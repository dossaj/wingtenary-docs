# Overview

## Table of Contents

1. [Overview](overview.md)
2. [Architecture](architecture.md)
3. [Dashboard Service](dashboard.md)
4. [Flight Service](flight.md)

## Deliverables

1. Data modeling is provided with each service component in their appropriate sections.
2. System architecture is covered in the architecture section.
3. Requirements are covered in this section.
4. Time estimate for the project will be covered in this section.

## Requirements

Will be covered by each service component in the appropriate sections.

## Technologies

This section will cover the choice of high-level technologies.

#### .NET Core

.NET Core provides a large level of flexibility and with the power of a high-level language like C#. It has a large support base as well as libraries and tooling. Some advantages are:

- It provides cross platform support.
- Performance is good.
- Large choice of development tools
- Widely adopted
- Excellent libraries like Castle, NServiceBus, EF etc
- Support for modern web tools including Angular and React

#### Containerization

The use of docker containers would be used for ease of deployments and flexibility based on the environment being deployed to. Containers provide the ability to deploy a number of different services in the cloud or on premise. App services, Azure Container Instances, Amazon ECS, Kubernetes etc.

## Assumptions

The assumptions here are applied to all sections

- The product will have a certain level of infrastructure/platform provided, whether this is through cloud services or on-premise hosting.
- Service Bus - A form of messaging service, whether this is provided by Azure, AWS, RabbitMQ or MSMQ etc.
- Identity - An OIDC/OAuth compliant service allowing for the issuing of *id_tokens* and *access_tokens*.
- Shielding - An appropriate IDS is in place, to protect against DOS and D-DOS attempts, whether it be RedShield, Palo-Alto etc.
- Security - All applications are deployed in the correct network security groups. Publicly accessible web servers are in different network security groups etc.
- Notification service is out of scope.
- This design does not cover auditing, logging and analytics.
- This design assumes all tooling is provided.
- The services should be scalable and be able to run in HA.
- Not accessible to the internet, is assumed to mean not publicly accessible, and that the hosting can still be provided over an internet connection, for example, a VPN.
- Mobile application is not in scope.
- User registration is not in scope.

## Testing

The testing strategy is defined into the categories of unit tests, integration tests and UI tests, with the goal of automating as much of the testing as possible, that align with the company's acceptance of risk.

Unit tests are the primary line of defence with the use of XUnit, all services and logic is tested to a standard. Unit tests run on every merge request. A TDD approach should be used.

The integration tests are coved using BDD. Using SpecFlow and Gherkin. These cover the API's versioning and provide confidence the nothing is broken for the connecting client. These tests can check security but are not designed to test business logic, just the expected behavior.

UI tests ensure the front-end functions as expected and will use a combination of Selenium and SpecFlow. Along with the integration tests these tests should run as often as possible and within reason.

## Continuous Delivery

The design assumes the product would include setup of a CI/CD pipeline, with automated deployments to different environments. Each deployment should be triggered at different stages of development. This includes merges, manual intervention etc.

The pipeline is assumed to have the appropriate approvals based on the organizational requirements.

## Time Estimates

Time estimates are given as if each service was being built from scratch. Ideally libraries that do the boiler plate setup would be created and each subsequent service will be quicker to build.

Times assume the UI is designed and drawn up ready to go.

Estimates consider a fully production ready system. Also, hours include full development time, with a highly focused and capable team of seniors and no distractions. So, its probably optimistic :). Team sizing would need to be performed.

Time is given in hours as the number of team members can vary.

#### Dashboard Service

- Project setup                        - 20 hours
- Web API                              - 40 hours
- Logic Layer                          - 40 hours
- Eventing                             - 20 hours
- Data Access Layer                    - 40 hours
- Front End                            - 80 hours
- CI Setup                             - 20 hours
- CD Setup                             - 80 hours

Sub-Total                              - 340 hours

#### Flight Service

- Project setup                        - 20 hours
- Web API                              - 80 hours
- Logic Layer                          - 80 hours
- Eventing                             - 20 hours
- Data Access Layer                    - 40 hours
- Front End                            - 160 hours
- CI Setup                             - 20 hours
- CD Setup                             - 80 hours

Sub-Total                              - 500 hours

Total                                  - 840 hours
