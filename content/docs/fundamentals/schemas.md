---
title: "Schemas"
weight: 3
---

## Tier I - Core Attributes

All Schemas contain a core set of required data known as Core Attributes. Any client capable of reporting information of this schema type MUST include all Core Attributes. Core Attributes MAY be null depending on the type of data, but the field values must be present.

## Tier II - Extended Attributes

Schemas may contain an extended set of in-specification data values. This data MAY be provided by clients if available, but clients SHALL NOT expect this data to be present. Optional Extended Data MAY be null or missing entirely.

## Tier III - Client-Specific Attributes

Schemas may contain Client-Specific Attributes, which are to be considered an extension of a Schema. Client-Specific Attributes MAY be provided by clients if available. Clients SHOULD be aware of extra data although processing of this data is not required. These attributes are not defined in the specification.
