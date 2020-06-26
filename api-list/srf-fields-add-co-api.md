# SRF Fields Add Collateral API

The Add Collateral Fields API will return a schema that describes the
fields available for entry when adding collateral to an existing loan. The
response will be formatted according to the JSON Schema
specification, which is documented here:

    http://json-schema.org/

Client applications should use the returned JSON schema to
format API requests for the creation and modification of requests
to add collateral to an existing loan.

> During the initial testing phase of the LOS API, the field
> list returned by this endpoint will be substantially complete,
> but some fields may not be present. These fields will be
> added to the schema as integration with client customizations
> to EDR's Add Collateral functionality continues.
>
> Any Add Collateral fields not included in the JSON schema must be entered
> manually via the Collateral 360 web application.

The schema returned by this endpoint will contain basic data
type validation rules. More specific validation rules (_e.g._
data formatting for complex data types) will be added over time
in order to assist client application developers in providing
improved user experiences in their applications. Client
applications should be tolerant of additions to the schema.

## Add Collateral Fields vs Service Request Fields

For the most part, the JSON Schema and JSON Templates will not deviate from _Service Request Fields_. The main differences are two:

1. Add Collateral Fields will not contain the transaction data because it is only adding a new collateral to an existing loan.
2. The only required fields will be the _**updatedBy**_ and _**processAsWarnings**_ fields in the meta object.

In addition to specifying the _**updatedBy**_ and _**processAsWarnings**_ fields, the _**collaterals**_ object must also be provided.

## The JSON Schema Model

The following example JSON Schema represents the minimal data
requirements and the required fields. String values ending with
ellipses ("`...`") represent metasyntactic descriptions of the
contents of their containing elements, and should not be
considered literal examples of the data in these elements.

```json
{
  "$id": "service-request-form",
  "type": "object",
  "$schema": "http://json-schema.org/draft-07/schema#",
  "properties": {
    "meta": {
      "$id": "/properties/meta",
      "type": "object",
      "properties": {
        "updatedBy": {
          "$id": "/properties/meta/properties/updatedBy",
          "type": "string",
          "title": "The Updated By Schema",
          "minLength": 1,
          "format": "email"
        },
        "processAsWarnings": {
          "$id": "/properties/meta/properties/processAsWarnings",
          "type": "boolean",
          "title": "The ProcessAsWarnings Schema",
          "minLength": 1,
          "default": true,
          "enum": [
              true,
              false
          ]
        }
      },
      "required": [
          "updatedBy",
          "processAsWarnings"
      ],
      "additionalProperties": false
    },
    "data": {
      "$id": "/properties/data",
      "type": "object",
      "properties": {
          "collaterals": {
            "$id": "/properties/collaterals",
            "type": "array",
            "items": {
              "$id": "/properties/collaterals/items",
              "type": "object",
              "properties": {
                "Collateral Properties as Objects..."
              },
              "dependencies": {
                "propertyType": ["propertySubType"],
                "propertySubType": ["propertyType"]
              },
              "definitions": {
                "propertyTypes": {
                  "$id": "/properties/collaterals/items/definitions/propertyTypes",
                  "type": "object",
                  "items": {
                    "$id": "/properties/collaterals/items/definitions/propertyTypes/items",
                    "type": "object",
                    "properties": {

                    }
                  }
                }
              },
              "required": [
                "Required Collateral Fields..."
              ]
            }
          }
      }
    }
  },
  "definitions": {
    "services": {
      "$id": "/definitions/services",
      "type": "object",
      "default": "",
      "enum": [
        "Services as Objects..."
      ]
    },
  }
}
```

******
<P style="page-break-before: always" />

## Available API Endpoints

The following endpoints are defined by this API subsystem:

### <span style="background-color: #72b566; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">GET</span> **Add Collateral Fields**

```text
/api/v1.1/addCollateral/fields
```

Accessing this endpoint via an HTTP `GET` method will return a
representation of the fields available as part of your Add Collateral.

The fields will broadly be delineated into two groups, each under their
own data element:

* The `meta` group contains descriptions of fields that describe the Add Collateral, but which are not actually visible Add Collateral fields within Collateral 360. These may represent data that are normally handled behind-the-scenes or automatically within Collateral 360, and that therefore may require special consideration by your application.

* The `collaterals` section contains schemata for fields that are entered
  for each collateral property to be associated with the existing loan.

  For example, a property street address would appear here, since each
  real property used to collateralize a loan has its own address.

#### Request

##### Path Parameters

This endpoint does not accept any URL path parameters.

##### Body Parameters

This endpoint does not accept any HTTP body parameters.

#### Response

##### Expected HTTP Response Code

When operating normally, this API endpoint will return
an HTTP response code of `200` ("OK").

##### Example JSON Response (Abbreviated)

A successful invocation of this endpoint should return a
response with a structure similar to the following.
String values ending with ellipses ("`...`") represent
metasyntactic descriptions of the contents of their
containing elements, and should not be considered literal
examples of the data in these elements.

```json
{
  "meta": {
    "date": "2018-04-28T12:23:23Z",
    "function": "get",
    "responseCode": 200,
    "responseID": "5e28d8e0-7984-11e8-adc0-fa7ae01bbebc",
    "success": true,
    "warnings": []
  },
  "data": {
    "model": {
      "jsonSchema": {
        "JSON Object Formatted using JSON Schema Draft-7..."
      },
    },
    "dataTemplates": {
      "json": {"JSON Object Format..."}
    }
  }
}
```

##### Example JSON Response (Full)

For reference, a more complete version of the preceding
example response follows.

```json
{
  "meta": {
      "date": "2018-04-28T12:23:23Z",
      "function": "get",
      "responseCode": 200,
      "responseID": "05da8aac-7985-11e8-adc0-fa7ae01bbebc",
      "success": true,
      "warnings": []
  },
  "data": {
    "model": {
      "jsonSchema": {
        "$id": "service-request-form",
        "type": "object",
        "$schema": "http://json-schema.org/draft-07/schema#",
        "properties": {
          "meta": {
            "$id": "/properties/meta",
            "type": "object",
            "properties": {
              "updatedBy": {
                "$id": "/properties/meta/properties/updatedBy",
                "type": "string",
                "title": "The Updated By Schema",
                "minLength": 1,
                "format": "email"
              },
							"processAsWarnings": {
								"$id": "/properties/meta/properties/processAsWarnings",
								"type": "boolean",
								"title": "The Created By Schema",
								"minLength": 1,
								"default": true,
								"enum": [true, false]
							}
            },
            "required": [
              "updatedBy",
              "processAsWarnings"
            ]
          },
          "data": {
            "collaterals": {
              "$id": "/properties/collaterals",
              "type": "array",
              "items": {
                "$id": "/properties/collaterals/items",
                "type": "object",
                "properties": {
                  "Collateral Properties as Objects..."
                },
                "required": [
                  " Required Collateral Fields..."
                ]
              }
            }
          }
        },
        "definitions": {
          "services": {
            "$id": "/definitions/services",
            "type": "object",
            "default": "",
            "enum": [
              "Services as Objects..."
            ]
          }
        },
        "required": [
          "Required Main Fields..."
        ]
      }
    },
    "dataTemplates": {
      "JSON": {
        "v1.0": {
          "meta": {
            "updatedBy": "email"
          },
          "collaterals": [
            {
              "Collaterals as Array of Objects",
              "services": [
                "Array of Services..."
              ]
            }
          ]
        },
        "v1.1": {
          "meta": {
            "updatedBy": "email",
            "processAsWarnings": true
          },
          "collaterals": [
            {
              "Collaterals as Array of Objects",
              "services": [
                "Array of Services..."
              ]
            }
          ]
        },
      }
    }
  }
}
```

## Service Types

A list of available Service Types is provided in the JSON Schema under the `definitions` object.

The Service Types listed in the JSON Schema is a subset of the full Service Types, which can be retrieved using the Utility API ServiceTypes. This subset list is the Service Types that can be used to create the Service Request Form.

The Service Types in the Utility API is the full list that can be used to augment the Service Request Form.

<div style="page-break-after: always;"></div>
