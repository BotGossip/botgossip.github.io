---
title: "Cases"
weight: 5
---

ℹ️ This page needs to be moved to the API Reference, and rewritten according to the new route standards

Cases are actions tied to a specific user.

They include some standardised properties as well as permitting for some freeform data to be stored in JSON format.

A case object looks like the following:

| Field         | Type      | Description                                               |
|---------------|-----------|-----------------------------------------------------------|
| `id`          | snowflake | The unique identifier for this case                       |
| `app_id`      | snowflake | The application which created this case                   |
| `type`        | string    | The type of case                                          |
| `target_id`   | snowflake | The identifier of the targeted user                       |
| `target_name` | string    | The name of the targeted user                             |
| `mod_id`      | snowflake | Unique identifier for the moderator who created this case |
| `mod_name`    | string    | Name of the moderator who created this case               |
| `detail`      | string    | Free-form (and human-readable) description of the case    |
| `expires`     | int?      | Timestamp of expiry for the case                          |
| `extra`       | json      | Extra freeform JSON data on the case                      |

There are several API endpoints used for modifying cases.

{{< route method="POST" route="/guilds/{guild_id}/mod/cases/{member_id}" >}}

Create a new case for a member

{{< route method="GET" route="/guilds/{guild_id}/mod/cases/{member_id}" >}}

Fetch all cases for a member

{{< route method="GET" route="/guilds/{guild_id}/mod/case/{case_id}" >}}

Fetch a specific case by ID

{{< route method="PATCH" route="/guilds/{guild_id}/mod/case/{case_id}" >}}

Update an existing case by ID

{{< route method="DELETE" route="/guilds/{guild_id}/mod/case/{case_id}" >}}

Delete an existing case by ID
