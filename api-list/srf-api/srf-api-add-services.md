# Service Request Form API - POST

### <span style="background-color: #5493dc; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">POST</span> **Add Service(s) to Service Request**

```text
/api/v1.1/serviceRequest/:locationId/services
```

#### Request

##### Path Parameters

| Path Parameter | Required | Type | Description |
| :--- | :--- | :--- | :--- |
| :locationId | Integer | Yes | The locationId to associate specified services. |


##### Body Parameters

The API request body conforms to the standard API request
format (_i.e._ a `meta` and a `data` element), per the
[API Data Structures](../request-response-structure.md)
section of this document.

The request's top-level `data` element should contain the
following elements, each of which must conform to the
requirements described above.

* `services`


##### Example JSON Request

``` json
{
	"meta": {
		"updatedBy": "fake_efbae2a5-1e6@chase.com"
	},
	"data": {
		"services": [
			{
				"serviceType": "IntValRevReport",
			},
			{
				"serviceType": "Screening",
			},
			{
				"serviceType": "HumanHealth",
			}
		]
	}
}
```

##### Query String Parameters

This endpoint does not accept any query string parameters.

#### Response

##### Expected HTTP Response Code

When operating normally, this API endpoint will return
an HTTP response code of `202` ("ACCEPTED"). This indicates that the request has been received by the system and is in process.