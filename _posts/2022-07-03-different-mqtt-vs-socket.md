---
title: What is different between mqtt and socket ?
author: Youngjin Kwak
date: 2022-07-02 00:24:00 +0800
categories: [Backend]
tags: [backend]
---
# What is mqtt?
MQTT stands for Message Queuing Telemetry Transport. MQTT is a simple messaging protocol, designed for constrained devices with low bandwidth. So, it’s the perfect solution to exchange data between multiple IoT devices.

## Features
2. MQTT clients are very small, require minimal resources so can be used on small microcontrollers.
3. It is publish-subscribe, machine to machine network protocol.
4. MQTT message headers are small to optimize network bandwidth.
5. It allows for messaging between device to cloud and cloud to device. This makes for easy broadcasting messages to groups of things.
6. It is good for connecting with millions of IoT devices.
7. It is message based unlike socket (session based)
8. (QoS) Quality of service. It defines priority for data flow

## Publish-Subscribe Architecture
![mqtt-architecture](https://mqtt.org/assets/img/mqtt-publish-subscribe.png)

### Note
1. MQTT Client -> MQTT Broker (Publish)
2. MQTT Broker -> Other MQTT Clients (Publish)
3. MQTT Clients <- MQTT Broker (Subscribe)

# What is different between Mqtt and Socket
## Comparing table

| MQTT                                                                                                          | Socket                                                                                                                                                         |
|:--------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MQTT is a typical pub/subsystem, and they are majorly used in small devices.                                  | Mainly works in an environment that supports pub/sub-architectures.                                                                                            |
| Having the facility to set priority.                                                                          | No feature available for setting the priority.                                                                                                                 |
| Majorly used in client and server applications.                                                               | Full push/pull communications.                                                                                                                                 |
| minimal overhead during communication.                                                                        | A lot of overhead when we have a lot of IOT devices during communication.                                                                                      |
| Specifically designed for IOT devices with an aim to reduce the bandwidth and provides assurance of delivery. | Full-duplex/bidirectional communication channels.                                                                                                              |
| High-level protocol.                                                                                          | Low-level protocol.                                                                                                                                            |
| Multiples parties can be able to subscribe and publish messages.                                              | Designed mainly for point to point communication.                                                                                                              |
| Message based                                                                                                 | Session based                                                                                                                                                  |
| Layer 4                                                                                                       | Layer 3 (and you have to design your own RYO layer 4 protocol)                                                                                                 |
| Defines how different machines can talk to each other, they can talk to the same channel                      | Able to send messages to clients/groups of clients. They are always open channel for bidirectional data transfer without request for open and close like HTTP. |

## So when we do not need to use Mqtt
1. Large data communication
2. Authentication
3. Browser support
4. Chat system

### Note
For browser support, we need web-socket

# Conclusion
Let's use Mqtt in proper place


# References
- https://mqtt.org/
- https://en.wikipedia.org/wiki/MQTT
- https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=changbab&logNo=221565552533
- https://randomnerdtutorials.com/what-is-mqtt-and-how-it-works/
- https://tigoe.github.io/mqtt-examples/mqtt-vs-websockets.html
- https://forums.raspberrypi.com/viewtopic.php?t=203192
