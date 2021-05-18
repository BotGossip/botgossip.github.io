---
title: "Standard Routes"
weight: 7
---

### Cases

{{< route method="POST" route="/gossip/v1/cases" >}}

This endpoint notifies the server of a new case

Request Body:

| Field      | Type.       | Description                                                          |
| ---------- | ----------- | -------------------------------------------------------------------- |
| `guild`    | snowflake   | Guild ID where the case took place.                                  |
| `user`     | snowflake   | User ID where the action was taken.                                  |
| `actioner` | snowflake   | User ID that created the case. Might be bot ID if it was automated.  |
| `action`   | case_action | Type of action taken.                                                |
| `duration` | long.       | Milliseconds for duration. 0 if permanent                            |
| `reason`   | string.     | Reason for action, might be empty                                    |


Where `case_action` is one of (`BAN`, `KICK`, `MUTE`, `WARN`)

Example Body:

```json
{
  "data":{
    "guild":810932869862129664,
    "user": 297045071457681409,
    "actioner": 427045071457681409,
    "action": "BAN",
    "duration": 3600,
    "reason": "Spamming all channels with rickrolls"
  }
}
```

{{< route method="GET" route="/gossip/v1/cases" >}}

This endpoint gets all cases you have access to, with optional filters and pagination

Request Body:
 
| Field       | Type.       | Description                                                          |
| ----------- | ----------- | -------------------------------------------------------------------- |
| `user`     | snowflake   | Filter for a specific user.                                          |
| `guild`     | snowflake   | Filter for a specific guild.                                         |
| `actioner`  | snowflake   | Filter for a specific actioner.                                      |
| `page_size` | int         | Max page size, implementors can set their own max                    |
| `page`      | int         | Page to return, starts on 1                                          |

None, one or multiple filters can be set

Example request:

`/gossip/v1/cases?user=1234567&page=2`

Example return:
```json
{
  "page_size": 200,
  "current_page": 1,
  "total_pages": 20
  "data": [
    {
      "guild":810932869862129664,
      "user": 297045071457681409,
      "actioner": 427045071457681409,
      "action": "BAN",
      "duration": 3600,
      "reason": "Spamming all channels with rickrolls"
    }
  ]
}
```
