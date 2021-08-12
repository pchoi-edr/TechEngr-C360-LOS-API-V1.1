# Service Request - Add Services API - POST

### <span style="background-color: #5493dc; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">POST</span> **Add Service(s) to Service Request**

```text
/api/v1.1/serviceRequest/addService/:locationID
```

The `Add Service` request contains a collection of service types and LOS attempts to add them to an existing loan specified by the `locationID` in the path. Internally, the processing is done asychronously via a job. Consequently, the information regarding the result of the processing will be sent in an email when the job has completed. However, if the request does not pass the initial validation, the user would see an error message in the response from the endpoint.

#### Request

##### Path Parameters

| Path Parameter | Required | Type | Description |
| :--- | :--- | :--- | :--- |
| :locationID | Integer | Yes | The locationID to associate specified services. |


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
		"updatedBy": "fake_efbae2a5-1e6@example.com"
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
an HTTP response code of `200` ("OK"). This indicates that the request has been received by the system and is in process.

#### Pre-Processing Validation

##### Request Validation

The API will validate basic information from the request before it passes the data to the job for processing.

###### User Validation

If the `meta.updatedBy` is not present or empty, the API will fail. If the email address in `meta.updatedBy` is not valid or does not have access to the logged in company or the loan specifically, the API will return an error. Examples of those errors are as follows:

``` json
{
    "description": "The requester's user account is unknown.",
    "field": "meta.updatedBy"
},
{
    "description": "The requester does not have access to the collateral you want to patch.",
    "field": "meta.updatedBy"
}
```

###### Services Validation

There are a couple layers of pre-validation on the services as well. If the services are empty in the request, the following error will be returned:

``` json
{
    "description": "At least one service must be defined.",
    "field": "data.services"
}
```

If one or more services in the request are not valid for the logged in company, the API will return the following error where `::List Of Valid Services::` is a complete list of the services that are able to be added for the `locationID` in the request:

``` json
{
    "description": "The following services have invalid names: FakeServiceName. They must be a value in the enumeration: [::List Of Valid Services::]",
    "field": "data.services.*.serviceType"
}
```

#### Post-Processing Email Notification

##### All Services Successful

If all services are added successfully, an email notification will be sent to the user that requested the services to be added (in the `meta.updatedBy` section of the request). It will list the services that were added successfully and indicate the address of the property that the services were added to.

##### All Services Failed

If all services fail to be added, an email notification will be sent to the user that requested the services to be added (in the `meta.updatedBy` section of the request). It will list the services that failed and indicate that no properties were affected.

##### Partial success and partial failure

If only some of the services are added successfully and the rest of them fail, an email notification will be sent to the user that requested the services to be added (in the `meta.updatedBy` section of the request). It will list the services that were added successfully and indicate the address of the property that the services were added to. The email will also list the services that were not able to be added.
