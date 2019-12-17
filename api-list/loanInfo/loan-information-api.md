# SRF Loan Information - Collateral Overview API

This API provides an overview of Collateral Overview information for a locationID.

If a location ID is specified, then the results will be
limited to only that single location. No other locations
will be present in the data structure returned to the client.

## Available Endpoints

The following endpoints are made available by this API, depending on
the desired identifier used to query the server:

### <span style="background-color: #72b566; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">GET</span> **Collateral Overview**

```text
/api/v1.1/loan/information/collateralOverview/:locationID
```

The API endpoints are accessible via the HTTP `GET` method.

#### Request

##### Path Parameters

| Path Parameter | Required | Type | Description |
| :--- | :--- | :--- | :--- |
| :locationID | Integer | Yes* | A location ID. |


##### Body Parameters

This endpoint does not accept and HTTP body parameters.

#### Response

##### Expected HTTP Response Code

When operating normally, this API endpoint will return
an HTTP response code of `200` ("OK").

##### Example JSON Response

```json
{
  "meta": {
    "date": "2018-04-28 12:23:23",
    "function": "get",
    "responseCode": 200,
    "responseID": "e3733640-789c-11e8-9dfc-81c439846400",
    "success": true,
    "warnings": []
  },
  "data": {
    "transaction": {
      ...
    },
    "callateral": {
      ...
    }
  }
}
```

Transaction & Collateral data varies from company to company and is company specific.
