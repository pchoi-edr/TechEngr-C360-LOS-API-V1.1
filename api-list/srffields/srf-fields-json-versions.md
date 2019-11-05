# Service Request Fields API - JSON Template Versions

In LOS API v1.1, the JSON template structure has more complex needs like having related field objects that needs to be have data provided for it with additional requirements like Required and Dependency relationships.

To provide for _**v1.0**_ and _**v1.1**_ the Service Request Fields API has been modified to provide both _**v1.0**_ and _**v1.1**_ versions of the API's JSON template.

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
        ...
      }
    },
    "dataTemplates": {
      "JSON": {
        "v1.0": {
          "meta": {
            "cabinet": "string",
            "currency": "USD",
            "requestedBy": "email"
          },
          "transaction": {
            "Transaction Fields as Objects"
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
            "cabinet": "string",
            "currency": "USD",
            "requestedBy": "email",
            "createdBy": "email",
            "srfAction": "PROCURE",
            "processAsWarnings": true
          },
          "transaction": {
            "Transaction Fields as Objects"
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
```

The JSON structure has not changed up to the

> data -> dataTemplates -> JSON

Has not changed at all.

However, the contents of the JSON object no longer holds the default JSON template but now has two sub-object keys

* "v1.0"
* "v1.1"

Depending on which version of the Service Request Form API you want to submit to, select the appropriate version key _**"v1.0"**_ or _**"v1.1"**_ to get the latest JSON Template.

Submit _**"v1.0"**_ to the v1.0 API's with /api/v1/*

Submit _**"v1.1"**_ to the v1.1 API's with /api/v1.1/*