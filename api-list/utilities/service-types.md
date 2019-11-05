# Utility: Service Types API

The `Service Types` API provides a comprehensive list of `Service Types` for your company. This list is more comprehensive than the list in the JSON Schema Fields API.

### <span style="background-color: #72b566; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">GET</span> **Service Types**

```text
/utility/serviceTypes
```

The returned data looks like the following

```json
{
  "meta": {...},
  "data": {
    "serviceGroups": [
      {
          "featureID": 81,
          "serviceGroup": "Environmental Services"
      },
      {
          "featureID": 87,
          "serviceGroup": "Valuation Services"
      }
    ],
    "serviceTypes": [
      {
        "serviceType": "ACMInv",
        "displayName": "ACM Investigation",
        "featureID": 81,
        "featureName": "Procure New Services",
        "serviceGroupID": 72,
        "serviceGroup": "Environmental Services",
        "isExternal": 1,
        "type": "RFP",
        "reportID": 74204,
        "categoryID": 1,
        "subCategoryID": "4",
        "showOnSRF": 0
      },
      {
        "serviceType": "Aerial",
        "displayName": "EDR Aerial Photo Package",
        "featureID": 81,
        "featureName": "Procure New Services",
        "serviceGroupID": 72,
        "serviceGroup": "Environmental Services",
        "isExternal": 1,
        "type": "EDR",
        "reportID": 74215,
        "categoryID": 1,
        "subCategoryID": "5",
        "showOnSRF": 0
      },
      {
        "serviceType": "Agency",
        "displayName": "Agency File Review",
        "featureID": 81,
        "featureName": "Procure New Services",
        "serviceGroupID": 72,
        "serviceGroup": "Environmental Services",
        "isExternal": 1,
        "type": "RFP",
        "reportID": 74226,
        "categoryID": 1,
        "subCategoryID": "6",
        "showOnSRF": 0
      },
      ...
    ]
  }
}
```

What makes this API unique is that it contains both `Service Groups` and `Service Types`. You will use both the `Service Groups` and `Service Types` in the [File Upload API](../srf-file-upload-api.md).

The usage is you select the Service Types you need and use the stringified version of it.

```json
[
  {
    "serviceType": "Aerial",
    "displayName": "EDR Aerial Photo Package",
    "featureID": 81,
    "featureName": "Procure New Services",
    "serviceGroupID": 72,
    "serviceGroup": "Environmental Services",
    "isExternal": 1,
    "type": "EDR",
    "reportID": 74215,
    "categoryID": 1,
    "subCategoryID": "5",
    "showOnSRF": 0
  },
  {
    "serviceType": "Agency",
    "displayName": "Agency File Review",
    "featureID": 81,
    "featureName": "Procure New Services",
    "serviceGroupID": 72,
    "serviceGroup": "Environmental Services",
    "isExternal": 1,
    "type": "RFP",
    "reportID": 74226,
    "categoryID": 1,
    "subCategoryID": "6",
    "showOnSRF": 0
  }
]
```

```text
[{"serviceType":"Aerial","displayName":"EDR Aerial Photo Package","featureID":81,"featureName":"Procure New Services","serviceGroupID":72,"serviceGroup":"Environmental Services","isExternal":1,"type":"EDR","reportID":74215,"categoryID":1,"subCategoryID":"5","showOnSRF":0},{"serviceType":"Agency","displayName":"Agency File Review","featureID":81,"featureName":"Procure New Services","serviceGroupID":72,"serviceGroup":"Environmental Services","isExternal":1,"type":"RFP","reportID":74226,"categoryID":1,"subCategoryID":"6","showOnSRF":0}]
```

As we add further functionality to LOS API's, the functional usage may differ. Currently, only the [File Upload API](../srf-file-upload-api.md), requires that the data used be stringified, but other API's usage may not and may require you submit data as an Object of Arrays