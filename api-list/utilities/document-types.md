# Utility: Document Types API

The `Document Types` API provides a comprehensive list of `Document Types` that can be used to distinguish a document or API.

### <span style="background-color: #72b566; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">GET</span> **Document Types**

```text
/utility/documentTypes
```

The returned data looks like the following

```json
{
  "meta": {...},
  "data": {
    "documentTypes": [
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
      },
      ...
    ]
  }
}
```

The usage for [File Upload API](../srf-file-upload-api.md) is you select the Document Types you need and use the stringified version of it.

```json
[
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
```

```text
[{"typeID":98,"typeName":"Draft Report","orderIndex":1},{"typeID":99,"typeName":"Final Report","orderIndex":2},{"typeID":100,"typeName":"Invoice","orderIndex":3},{"typeID":101,"typeName":"Supporting Documentation","orderIndex":4}]
```

As we add further functionality to LOS API's, the functional usage may differ. Currently, only the [File Upload API](../srf-file-upload-api.md), requires that the data used be stringified, but other API's usage may not and may require you submit data as an Object of Arrays