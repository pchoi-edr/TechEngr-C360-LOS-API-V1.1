# Service Request Fields API - 5 Tab Version

In LOS API v1.1, the JSON template structure has more complex needs like having related field objects that needs to be have data provided for it with additional requirements like Required and Dependency relationships or multiple tab implementations.

Currently, Service Request Form, only supported 2 tab implementations, but with this current release, support for 5 tab implementation has been added.

The impact to this change will affect the JSON Schema Model. The biggest impact is in the 'data' object within the JSON Schema. Whereas in the previous implementation there was only 'transation' and 'collaterals', 5 Tab adds 'lenderInformation' to the 'data' object.

Before:

```json
{
  "$id": "service-request-form",
  "type": "object",
  "$schema": "http://json-schema.org/draft-07/schema#",
  "properties": {
    "meta": {
      "$id": "/properties/meta",
      "type": "object",
      "properties": {...}
    "data": {
       "$id": "/properties/data",
      "type": "object",
      "properties": {
        "transaction": {
          "$id": "/properties/transaction",
          "type": "object",
          "properties": {
             "Transaction Properties as Objects..."
          }
        },
        "collaterals": {
          "$id": "/properties/collaterals",
          "type": "array",
          "items": {
            "$id": "/properties/collaterals/items",
            "type": "object",
            "properties": {
              "Collateral Properties as Objects..."
            },
          }
        }
      }
    }
```

Current:

```json
{
  "$id": "service-request-form",
  "type": "object",
  "$schema": "http://json-schema.org/draft-07/schema#",
  "properties": {
    "meta": {
      "$id": "/properties/meta",
      "type": "object",
      "properties": {...}
    "data": {
       "$id": "/properties/data",
      "type": "object",
      "properties": {
        "transaction": {
          "$id": "/properties/transaction",
          "type": "object",
          "properties": {
             "Transaction Properties as Objects..."
          }
        },
        "lenderInformation": {
          "transaction": {
          "$id": "/properties/lenderInformation",
          "type": "object",
          "properties": {
             "Lender Information Properties as Objects..."
          }
        },
        "collaterals": {
          "$id": "/properties/collaterals",
          "type": "array",
          "items": {
            "$id": "/properties/collaterals/items",
            "type": "object",
            "properties": {
              "Collateral Properties as Objects..."
            },
          }
        }
      }
    }
```

For the most part, the addition of the 'lenderInformation' object is the biggest change to the 5 Tab implementation. However, there are additonal minor changes to the JSON Schema and JSON templates.

  1. Services
  2. JSON template for version 1.0
  3. JSON template for version 1.1

## Services

For 5 Tab implementation, the service list has been extended to support

  - DesiredDeliveryDate
  - NoOfHardCopies

in addition to

  - serviceType
  - displayName
  - featureID
  - featureName

```json
{
  "properties": {
    "serviceType": { "type": "string" },
    "displayName": { "type": "string" },
    "featureID": { "type": "number" },
    "featureName": { "type": "string" },
    "DesiredDeliveryDate": { "type": "string" },
    "NoOfHardCopies": { "type": "number" }
  }
}
```

## JSON Templates

The JSON templates reflect what the JSON Schema is therefor both 1.0 and 1.1 versions of the JSON Template will be modified according to the JSON Schema 'lenderInformation' object schema.
