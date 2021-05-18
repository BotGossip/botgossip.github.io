---
title: "API Reference"
weight: 6
---

## Authentication


There are two modes of authentication for routes in Gossip:

1) Header-based authentication using the `Authorization` header.
2) No authentication; anonymous requests.

### Header-based Authentication

For authenticated endpoints the client should pass an `Authorization` header with their bearer token:

```
Authorization: Bearer b3c98d3f
```

The format of that Authorization token its left to the implementor

## Rate Limits

Implementors are free to implement rate limits as needed, the following headers should be sent when a rate limit is active

`X-RateLimit-Limit` Limit on number of calls for the current endpoint
`X-RateLimit-Remaining` Number of calls remaining for the current endpoint
`X-RateLimit-Reset` Unix epoch timestamp in milliseconds for next reset
`X-RateLimit-Retry-After` Only sent after rate limit is active, milliseconds until the client should retry

When a client exceeds the limit, the server MUST send a 429 Too Many Requests status code alongwith a `X-RateLimit-Retry-After` header

## Routes

The basic route format for API routes is `/{namespace}/{version}/{topic}/{resource}`. The version is namespace specific. If the namespace is gossip then the current active version is `v1`.

`gossip` is a reserved namespace, used for gossip standards. Implementors are free to implement custom routes on their own namespace

Both GET and POST should be implemented, POST is used to create a new event, GET to get all events your key has access to (and can be filtered further by the event schema)

### Miscellaneous Routes

{{< route method="GET" route="/details" >}}

{{< tip "warning" >}}
This is **not** a versioned endpoint and should not be prefixed with `/{version}`
{{< /tip >}}

This endpoint details information about the server including it's capabilities and API version.

Return Body:

| Field          | Type   | Description                                                  |
| -------------- | ------ | ------------------------------------------------------------ |
| `version`      | string | The server's API version.                                    |
| `capabilities` | json   | A `capabilities` object detailing the server's capabilities. |
| `meta`         | json   | Any extra data the server wants to give about itself.        |

Example Body:

```json
{
  "version":"1",
  "capabilities":{
    "endpoints": [
      "/gossip/v1/cases",
      "/myBot/v1/counters"
    ]
  },
  "meta":{
    "host":{
      "language":"Python",
      "library":"Gossipy-Server",
      "os":"Linux/Debian"
    }
  }
}
```

### Standard routes

Routes made standard and implemented inside the `gossip` namespace are documented in [Standard Routes](standard-routes.md)
