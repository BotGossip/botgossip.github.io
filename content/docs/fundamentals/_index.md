---
title: "Fundamentals"
weight: 1
---

Gossip, at a very high level, is a specification for an API that allows different bots to talk to each other in a simple and predictable way. The specification is flexible and customizable to allow for developers to customize implementations to suit their needs while also ensuring standards to allow bots of any caliber to work with each other. The specification is loosely inspired by [SCIM](http://www.simplecloud.info/).

Gossip allows bot developers to:
- Create an arbitrary network of bots capable of exchanging information
- Pull information from other clients in a network (“lookups”)
- Push information to other clients in a network (“notifies”)
- Implement and expect a common set of extensible schemas
- Extend or create schemas for application-specific use cases, such as IPC

The Gossip specification follows a federated model where clients (generally bots) will directly communicate with each other. While clients are generally bots, persistent datastores known as “brokers” may be present in any given Gossip network.
