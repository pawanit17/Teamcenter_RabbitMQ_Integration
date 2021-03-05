# RabbitMQ

RabbitMQ is a messaging service that is quite popular. It also supports clustering for fault tolerance and scalability.

Has centralized / broker architecture unlike Kafka, which is decentralized.

Messaging Protocols that are popular:

STOMP - Simple Text Oriented Messaging Protocol
- Does not have the concept of queues/topics
- SENDs message to a DESTINATION string

MQTT - Message Queue Telemetry Transport
- IoT connectivity protocol
- Publish-subscribe model
- Specifically designed for resource-constrained devices like Mobile and IoT.

AMQP - Advanced Message Queueing Protocol
- Routing, security with publish-subscribe.

![image](RabbitMQ_Overview.png)

# Usecases

- Real time feed of constantly updating information
- Want to connect different softwares together
- Message delivery after the destination comes online etc..

# Core
Main participants in RabbitMQ
- Producer
- Exchanges - Messages from Producer are sent to Exchanges. Takes the incoming message, applies the routing algorithm ( bindings ) and sends them to one or more queues.
Default, Fanout, Topic, Headers are the exchange types.
- Routing
- Queue - Consumers only know about the Queues. Bindings are done from Exchange to Queue. Durable vs Non-Durable queues. Exclusive and Auto-Delete options.
- Topics - Are simply the subject part of the messages.
- Bindings - Queues are bound to exchanges using Bindings. These are responsbile for routing messages. May have an optional routing key attribute used by some exchange types.
- Consumer

In RabbitMQ, messages for which there are no consumers can be configured to be dropped or returned to the producer.

Exchange -----> Bindings ------> Queues

# Launching

RabbitMQ could be launched with the help of Docker. Use the below command to spawn a Docker container containing RabbitMQ.

```docker run -d --name some-rabbit -p 5672:5672 -p 5673:5673 -p 15672:15672 rabbitmq:3-management```

With this, the portal is accessible via http://localhost:15672/

More one Docker [here](https://github.com/pawanit17/learn_docker).

# Teamcenter_RabbitMQ_Integration

Here, I integrate Teamcenter ( a datasource ) with RabbitMQ ( a messaging queue ).

Teamcenter is a Product Lifecycle Management software and RabbitMQ is a messaging queue. A PLM software would hold the master data in any manufacturing topology and that means that there would be downstream applications where such data is to be replicated to. Examples of these downstream applications include ERP systems like SAP, Analytics softwares like SAP HANA, Reporting softwares like TIBCO Spotfire or to huge data processing softwares like Splunk, you name it.

So this scheme can be applied to any datasource ( say, your home grown Java application that needs to have a certain activity processed in the back end - you could just leverage RabbitMQ to drop a message to the intended backend application that registered with RabbitMQ to do such a processing!.
