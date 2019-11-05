# Utility: Document Status API


The Document Status API is used primarily with the [File Upload API](../srf-file-upload-api.md). Although the File Upload API `documentStatus` parameter isn't mandatory, you can use this API to populate the acceptable status.

### <span style="background-color: #72b566; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">GET</span> **Document Status**

```text
/utility/documentStatus
```

The returned data looks like the following

```json
{
  "meta": {...},
  "data": {
    "documentStatus": [
      {
          "typeID": 98,
          "typeName": "Draft Report",
          "orderIndex": 1
      },
      {
          "typeID": 99,
          "typeName": "Final Report",
          "orderIndex": 2
      },
      {
          "typeID": 100,
          "typeName": "Invoice",
          "orderIndex": 3
      },
      {
          "typeID": 101,
          "typeName": "Supporting Documentation",
          "orderIndex": 4
      }
    ]
  }
}
```

The usage is you select the Document Status you need and use the stringified version of it.

```json
{
  "typeID": 98,
  "typeName": "Draft Report",
  "orderIndex": 1
}
```

```text
{"typeID":98,"typeName":"Draft Report","orderIndex":1}
```

As we add further functionality to LOS API's, the functional usage may differ. Currently, only the [File Upload API](../srf-file-upload-api.md), requires that the data used be stringified, but other API's usage may not and may require you submit data as an Object.