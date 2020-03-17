# Service Request Form API - POST

### <span style="background-color: #5493dc; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">POST</span> **Add Service(s) to Service Request**

```text
/api/v1.1/serviceRequest/:locationId/services
```

The `Add Service` request contains a collection of service types and LOS attempts to add them to an existing loan specified by the `locationId` in the path. Internally, the processing is done asychronously via a job. Consequently, the information regarding the result of the processing will be sent in an email when the job has completed. However, if the request does not pass the initial validation, the user would see an error message in the response from the endpoint.

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

#### Post-Processing Email Notification

##### All Services Successful

If all services are added successfully, an email notification will be sent to the user that requested the services to be added (in the `meta.updatedBy` section of the request). It will list the services that were added successfully and indicate the address of the property that the services were added to.

##### All Services Failed

If all services fail to be added, an email notification will be sent to the user that requested the services to be added (in the `meta.updatedBy` section of the request). It will list the services that failed and indicate that no properties were affected.

##### Partial success and partial failure

If only some of the services are added successfully and the rest of them fail, an email notification will be sent to the user that requested the services to be added (in the `meta.updatedBy` section of the request). It will list the services that were added successfully and indicate the address of the property that the services were added to. The email will also list the services that were not able to be added.
