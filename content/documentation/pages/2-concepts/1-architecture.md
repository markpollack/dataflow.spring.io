---
path: 'concepts/architecture/'
title: 'Architecture'
description: 'Introduction to Data Flow\'s Architecture'
---

# Architecture

Data Flow has two main components, The Data Flow Server and the Skipper Server.
The main entry point to access Data Flow is through the Web API of the Data Flow Server.
The Web Dashboard is served from the Data Flow Server and a separate Data Flow Shell applications both communicate through the web API.
The servers can be run on several platforms: Cloud Foundry, Kubernetes, or on your Local machine.
Each server stores state in a relational database.
A high level view of the Architecture and the paths of communication are shown below.

![Spring Cloud Data Flow Architecture Overview](images/architecture-overview.png)

The Data Flow Server is responsible for

- Parsing the Stream and Batch Job definitions using the Domain Specific Language (DSL).
- Validating and persisting Stream, Task, and Batch Job definitions
- Registering artifacts such as .jar and docker images to names used in the DSL.
- Deploying Batch Jobs to one or more platforms.
- Creating Skipper packages Delegating Stream Deployment to Skipper.
- Add properties to Stream applications that configure messaging inputs and outputs, monitoring labels.
- Auditing actions.
- Querying detailed Task and Batch Job execution history.
- Delegating Job scheduling to a platform.
- Providing Stream and Batch Job DSL tab-completion features.

The Skipper Server is responsible for:

- Deploying Streams to one or more platforms.
- Upgrading and rolling back deployed applications on one or more platforms using a State Machine based blue/green update strategy.
- Store the history of each application's manifest file that represents the final description of what has been deployed.

## Tooling

The Dashboard and Shell are the main ways you interact with Data Flow.
You can also hit the Web API using curl or write an applications that uses the Java client library which in turn calls the Web API.
The next section introduces the features of the Dashboard and the Shell.

### Dashboard

Spring Cloud Data Flow provides a browser-based GUI called the dashboard to manage the following information:

- _Apps_: The Apps tab lists all available applications and provides the controls to register/unregister them.
- _Runtime_: The Runtime tab provides the list of all running applications.
- _Streams_: The Streams tab lets you list, design, create, deploy, and destroy Stream Definitions.
- _Tasks_: The Tasks tab lets you list, create, launch, schedule and, destroy Task Definitions.
- _Jobs_: The Jobs tab lets you perform batch job related functions.

### Shell

### REST API

## Security

## System Requirements

**Java:** Data Flow uses Java 8.

**Database:** The Data Flow Server and Skipper Server need to have an RDBMS installed.
By default, the servers use an embedded H2 database.
You can easily configure the servers to use external databases.
The supported databases are H2, HSQLDB, MySQL, Oracle, Postgresql, DB2, and SqlServer.
The schemas are automatically created when each server starts.

**Messaging Middleware:** Deployed stream applications communicate via messaging middleware
product.
We provide prebuilt stream applications that use [RabbitMQ](https://www.rabbitmq.com) or
[Kafka](https://kafka.apache.org).
However, other [messaging middleware products](https://cloud.spring.io/spring-cloud-stream/#binder-implementations)
such as
[Kafka Streams](https://kafka.apache.org/documentation/streams/),
[Amazon Kinesis](https://aws.amazon.com/kinesis/),
[Google Pub/Sub](https://cloud.google.com/pubsub/docs/)
[Solace PubSub+](https://solace.com/software/)
and
[Azure Event Hubs](https://azure.microsoft.com/en-us/services/event-hubs/)
are supported.
