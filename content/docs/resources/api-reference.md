---
title: "API Reference"
date: 2021-02-16T18:56:15Z
draft: true
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

## Rate Limits

- Content TBD

## Routes

The basic route format for API routes is `/{version}/{topic}/{resource}`. All routes detailed below assume that `/{version}` is used as the base URL and hence does not include that. The current API version is `v1`, though the version used by a server may differ from the latest version.

### Miscellaneous Routes

{{< route method="GET" route="/details" >}}

⚠️ This is **not** a versioned endpoint and should not be prefixed with `/{version}`

This endpoint details information about the server including it's capabilities and API version.

Return Body:

|Field|Type|Description|
|---|---|---|
|version|string|The server's API version.|
|capabilities|json|A `capabilities` object detailing the server's capabilities.|
|meta|json|Any extra data the server wants to give about itself.|

Example Body:

```json
{
  "version":"1",
  "capabilities":{},
  "meta":{
    "host":{
      "language":"Python",
      "library":"Gossipy-Server",
      "os":"Linux/Debian"
    }
  }
}
```

### Message Routes

{{< route method="POST" route="/core/messages/new/{event_type}" >}}

This endpoint creates a new message with the event type of `event_type` which will be POSTed to clients who have registered webhooks for that event.

Request Body:

|Field|Type|Description|
|---|---|---|
|data|json|The JSON data of the event.|

Example Body:

```json
{
  "data":{
    "type":"member_join",
    "guild":810932869862129664,
    "member":{
      "id":297045071457681409,
      "name":"vcokltfre",
      "discriminator":6868
    }
  }
}
```

When this endpoint is called it will create a POST request to all listeners of that event with the following data structure:

Post Body:

|Field|Type|Description|
|---|---|---|
|event|string|The event type of the message.|
|data|json|The JSON data of the event.|

Example Body:

```json
{
  "event":"log",
  "data":{
    "type":"member_join",
    "guild":810932869862129664,
    "member":{
      "id":297045071457681409,
      "name":"vcokltfre",
      "discriminator":6868
    }
  }
}
```

{{< route method="POST" route="/core/messages/register/{event_type}" >}}

This endpoint registers a new message listener webhook for event messages. If no `event_type` is passed it will be sent all events which it is authorized to receive. It is possible to register multiple events to a single webhook, therefore as previously detailed an `event` attribute is sent in the event POST.

Request Body:

|Field|Type|Description|
|---|---|---|
|url|string|The webhook URL that events should be posted to.|

Example Body:

```json
{
  "url":"https://gossip.vcokltf.re/event"
}
```
