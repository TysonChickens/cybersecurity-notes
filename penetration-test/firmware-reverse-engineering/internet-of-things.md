# Internet of Things

## Objectives

* [ ] &#x20;Explain the Internet of Things, why it is important, and if there should be worried about their danger.
* [ ] Understand the different between IoT-specific protocol and other network service protocols.
* [ ] Understand what a publish/subscribe model and how it interacts with IoT devices.
* [ ] Analyze and exploit the behavior of vulnerable IoT device.

## What is the Internet of Things?

The Internet of Things (IoT) defines a categorization of devices interconnected and rely on heavy communication to achieve a device's objectives. Examples include thermostats, web cameras, and smart fridges and more...

* The term is best described as "a device that sends and receives data to communicate with other devices and systems."
* Devices often involve no human interaction.
* Designed to be interconnected to be used on all the same protocols.
* Security is often a secondary objective and not securing devices could be a fatal weakness overlooked or less important.

## Introduction to IoT Protocols

Any protocol used by an IoT device for machine-to-machine, machine-to-gateway, or machine-to-cloud communication.

* IoT protocol's objective should be efficient, reliable, and secure data communication.

There are two types of IoT protocols. Both are used to communicate data. They are different on how and where the communication occurs:

* IoT data protocol: Relies on the TCP/IP (Transmission Control Protocol/Internet Protocol) model.
  * Similar to network services such as HTTP, SMB, FTP, and others. HTTP can be used as the backbone for other IoT protocols.
* IoT network protocol: Relies on wireless technology for communication.
  * Network or wireless protocol maintains the same goals as data protocols but using wireless technology such as Wi-Fi, Bluetooth, Zigbee, and Z-Wave to transfer data and communicate between entities.

### Messaging Protocols and Middleware

Data communication is the primary objective of IoT data protocols as a form of **messaging protocols -** Helps sending and receiving of message or payload between two parties.

* Messaging protocols communicate between two devices through an independent server (middleware) or negotiate communication amongst themselves.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/495796497ee8356484689b008de96184.png" alt=""><figcaption></figcaption></figure>

A brief overview of popular messaging protocols used by IoT devices:

| <p>Protocol<br></p>                                   | <p>Communication Method<br></p> | <p>Description<br></p>                                                                                                     |
| ----------------------------------------------------- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| <p>MQTT (Message Queuing Telemetry Transport)<br></p> | <p>Middleware<br></p>           | <p>A lightweight protocol that relies on a publish/subscribe model to send or receive messages.<br></p>                    |
| <p>CoAP (Constrained Application Protocol)<br></p>    | <p>Middleware<br></p>           | <p>Translates HTTP communication to a usable communication medium for lightweight devices.<br></p>                         |
| <p>AMQP (Advanced Message Queuing Protocol)<br></p>   | <p>Middleware<br></p>           | <p>Acts as a transactional protocol to receive, queue, and store messages/payloads between devices.<br></p>                |
| <p>DDS (Data Distribution Service<br></p>             | <p>Middleware <br></p>          | <p>A scalable protocol that relies on a publish/subscribe model to send or receive messages. <br></p>                      |
| <p>HTTP (Hypertext Transfer Protocol)<br></p>         | <p>Device-to-Device<br></p>     | <p>Used as a communication method from traditional devices to lightweight devices or for large data communication.<br></p> |
| <p>WebSocket <br></p>                                 | <p>Device-to-Device<br></p>     | Relies on a client-server model to send data over a TCP connection.                                                        |

## Functionality of Publish/Subscribe Model

Messaging protocols commonly use a publish/subscribe model with MQTT protocol. This model relies on a broker to negotiate "published" messages and "subscription" queries.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/9af9a374b9401e1f61d200240752c012.png" alt=""><figcaption><p>Publish/Subscribe Model</p></figcaption></figure>

1. A publisher sends their message to a broker.
2. The broker continues relaying the message until a new message is published.
3. A subscriber can attempt to connect to a broker and receive a message.

A broker can store multiple message from different publishers by using **topics** to avoid using multiple brokers for multiple devices.

* A topic is a value pre-negotiated by the publisher and subscriber and sent along with a message. The format of a topic commonly looks like `<name>/<id>/<function>`

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/bc178e6c7cf7ad59bafa6029a4dc006e.png" alt=""><figcaption><p>Two publishers sending different messages with topics.</p></figcaption></figure>

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/a8df1ae7f4eafc5aee7cec79e195c71d.png" alt=""><figcaption><p>Several subscribers receiving messages from separate topics of a broker.</p></figcaption></figure>

A publish/subscribe model is helpful for any data maintained asynchronously or received by several different devices from one publisher.

* Example of a publish/subscribe model could be a thermostat publishing its current temperature. Several thermostats can publish to one broker, and several devices can subscribe to the thermostat they want data from.

MQTT is lightweight, with a small footprint and minimal bandwidth.

## Are IoT Protocols Vulnerable?

Similarly to HTTP vulnerabilities, IoT protocols are not inherently vulnerable.

Data should follow CIA (Confidentiality, Integrity, and Availability) as close as possible. The data should not be read or manipulated by unauthorized sources.

* Best practices, authentication and authorization should be implemented to prevent potentially bad actors from compromising any principle of the CIA triad.
* If best practices are ignored, risk is dependent on the behavior of the device where an attacker could send a malicious message to perform unintended actions (modify thermostat's temperature).

Note the difference between insecure and vulnerable; an insecure implementation may allow an attacker to exploit a vulnerability, but does not mean the implementation is inherently vulnerable.

## Abusing Device Behavior

An attacker can discover device behavior from communication sniffing, source code analysis, or documentation.

* **Communication** sniffing can reveal protocol used, middleware or broker address, and the communication behavior.
* **Source Code analysis** can provide direct insight on how a device parses sent data and how it is being used. Analysis can identify similar information to communication sniffing but is more reliable and definite source of information.
* **Documentation** provides with a clear understanding of the standard functionality of a device or endpoint.
  * Disadvantage is may leave out sensitive topics, or other information not relevant to a normal user an attacker would want.

Once a behavior is identified, clients can be used to interact with devices and send malicious messages/payloads.

Most IoT devices have a Device ID to identify themselves to other devices and other devices can use to identify the target device.

* Devices must exchange this device ID before any other communication can occur.
* An attacker can target specific topics or message formats knowing the device ID and behavior of the target device.

## Interacting with MQTT

Different IoT protocols will have different libraries or other means of interacting with them. MQTT commonly used libraries are **Paho** and **Mosquitto**.

* Paho is a python library that offers support for all features of MQTT.
* Mosquitto is a suite of MQTT utilities including a broker and publish/subscribe clients from the command line.

### Subscribe to a Topic (mosquitto\_sub)

Use the mosquitto\_sub client utility to subscribe to an MQTT broker.

* Connecting to a localhost and subscribing to the topic, device/ping: `mosquitto_sub -t device/ping`
* Connect to a remote broker: `mosquitto_sub -h example.com -t device/thm`

### Publish to a Topic (mosquitto\_pub)

Use the mosquitto\_pub client utility to publish to an MQTT broker.

* Publish a message to a topic with `-m` or `-message` flag to denote the message/payload. `mosquitto_pub -h example.com -t device/info -m "This is an example"`

For both clients, optional flags that will be helpful:

* `-d`: Enables debug messages.
* `-i` or `—id`: Specifies the id to identify the client to the server.
* `-p` or `—port`: Specifies the port the broker is using. Defaults to port `1883`.
* `-u` or `—username`: Used to specify the username for authentication.
* `-P` or `—password`: Used to specify the password for authentication.
* `—url`: Used to specify username, password, host, port, and topic in one URL.
