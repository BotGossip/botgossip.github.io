---
title: "Clients"
weight: 2
---

Clients are, fundamentally, HTTP servers that allow data exchange between nodes in a Gossip network.

Gossip clients shall have four operating capabilities:

- Receiving Lookups from clients (inbound GET)
- Sending Lookups to clients (outbound GET)
- Receiving Notifies from clients (inbound POST/PUT)
- Sending Notifies to clients (outbound POST/PUT)

Clients are encouraged to support all above modes, however a client may only implement those that are necessary to the client’s operation. Of specific note, however, is that a client that supports receiving Notifies MUST additionally support receiving Lookups.
