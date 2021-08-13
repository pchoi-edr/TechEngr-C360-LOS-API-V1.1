# Service Request - Add Collateral API - POST

### <span style="background-color: #5493dc; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">POST</span> **Add Collateral(s) to Service Request**

```text
/api/v1.1/serviceRequest/addCollateral/loanID/:loanID
```
```text
/api/v1.1/serviceRequest/addCollateral/locationID/:locationID
```

The `Add Collateral` request contains a collection of collaterals and LOS attempts to add them to an existing loan. There are two ways to use the `Add Collateral` API:
- If the `/loanID` path is used, LOS looks up the loan by the loan ID specified in the path.
- If the `/locationID` path is used, LOS looks up the loan that the location is associated to.

### Request

#### Path Parameters

| Path Parameter | Required | Type | Description |
| :--- | :--- | :--- | :--- |
| :locationID | Yes | Integer | The locationID to associate specified collateral. |
| :loanID | Yes | Integer | The loanID to associate specified collateral. |

Either the `locationID` or the `loanID` **_must_** be present in the request. Additionally, the value that is present must be valid.

#### Body Parameters

The API request body conforms to the standard API request
format (_i.e._ a `meta` and a `data` element), per the
[API Data Structures](../request-response-structure.md)
section of this document.

##### Metadata Field Definitions

The following fields should be included in the API request's
top-level `meta` element:

| Metadata Field | Required | Type | Description |
| :--- | :--- | :--- | :--- |
| updatedBy | Yes | String | The email address of the user who is issuing the request. This must be an email address associated with an appropriate user account in Collateral 360. |
| processAsWarnings | Yes | Boolean | **_TRUE_** processes Add Collateral regardless of form errors.<br>**_FALSE_** On process errors, doesn't add collateral to the ServiceRequest and outputs all errors.<br><span style="font-size: 12px;">**NOTE:** exception to processAsWarnings = true, is when data is submitted that violates database field integrity. (i.e. a string submitted when data column indicates an integer)</span> |

##### Data Field Definitions

The request's top-level `data` element should contain the
following element, each of which must conform to the
requirements described above.

* `collaterals`

##### Example JSON Request

```json
{
  "meta": {
    "updatedBy": "string",
    "processAsWarnings": "boolean"
  },
  "data": {
    "collaterals": [
      {
        "services": [],
        "LocationPropertyId": "string",
        "PropertyType": {
          "PropertyType": "string",
          "PropertySubType": "string"
        },
        "PropCountry": "string",
        "PropAddress": "string",
        "SecondaryStreetAddress": "string",
        "PropUnit": "string",
        "PropCity": "string",
        "PropState": "string",
        "PropZip": "string",
        "PropCounty": "string",
        "PropLatitude": "string",
        "PropLongitude": "string",
        "PropertyNumbers": "string",
        "ContactCompany": "string",
        "ContactName": "string",
        "ContactPhone": "string",
        "ContactEmail": "string",
        "ContactAltPhone": "string",
        "Comments": "string",
        "Purpose": {
          "Purpose": "string",
          "TransactionType": "string"
        },
        "OtherTextApr": "string",
        "AppraisalPriority": "string",
        "ofsiReportReview": "boolean",
        "PropInterest": [],
        "ValuationPremise": [],
        "PurposeEnv": {
          "PurposeEnv": "string",
          "TransactionTypeEnv": "string"
        },
        "OtherTextEnv": "string",
        "CurrentLienBalance": "number",
        "EnvironmentalPriority": "string",
        "ContactType": "string",
        "ContactTypeOther": "string",
        "NumBuildings": "number",
        "BuildingSize": {
          "BuildingSize": "string",
          "BuildingSizeUnits": "string"
        },
        "BuildingSizeAlt": {
          "BuildingSizeAlt": "string",
          "BuildingSizeAltUnits": "string"
        },
        "BuildingSizeCompleted": {
          "BuildingSizeCompleted": "string",
          "BuildingSizeCompletedUnits": "string"
        },
        "BuildingSizeCompletedAlt": {
          "BuildingSizeCompletedAlt": "string",
          "BuildingSizeCompletedAltUnits": "string"
        },
        "LandSize": {
          "LandSize": "string",
          "LandSizeUnits": "string"
        },
        "LandSizeAlt": {
          "LandSizeAlt": "string",
          "LandSizeAltUnits": "string"
        },
        "ExcessLand": "boolean",
        "YearBuilt": "number",
        "LastRenovated": "number",
        "Tenancy": "string",
        "Occupancy": "string",
        "TenantsThirdPartyLeasePct": "string",
        "Tenants": "number",
        "HasRenovation": "boolean",
        "RenevationDesc": "string",
        "Zoning": "string",
        "PropertyStatus": [],
        "LocationPropertyQuality": "string",
        "HasUseChange": "boolean",
        "ProposedUse": "string",
        "HasGroundLease": "boolean",
        "GroundLeaseDesc": "string",
        "IsForSale": "boolean",
        "IsForSaleBrokerageFirm": "string",
        "ListPrice": "number",
        "HasRecentSale": "boolean",
        "RecentSaleBrokerageFirm": "string",
        "SalePrice": "number",
        "SaleDate": "string",
        "PropertyDescription": "string",
        "PropInterestOther": "string",
        "ValuationPremiseOther": "string"
      }
    ]
  }
}
```

##### Query String Parameters

This endpoint does not accept any query string parameters.

### Response

#### Expected HTTP Response Code

When operating normally, this API endpoint will return
an HTTP response code of `200` ("OK"). This indicates that the request has been processed by the system. .

#### Pre-Processing Validation

##### LoanId/LocationId Validation

If the identifier in the path is invalid or the identifier cannot be found in the system, the following error will be returned:

``` json
{
    "description": "The location id you are trying to use does not exist",
    "field": ""
}
```

##### Concurrent Request Validation

This endpoint currently only allows one request per loan to process at any given time. There is a validation step that ensures there is not already a request processing against the loan that is specified in the request. In the event that there is already a request in process, the following error will occur:

``` json
{
    "description": "There is already an api call in progress for this SRF",
    "field": ""
}
```

##### Collateral Limit Validation

The Add Collateral endpoint restricts the maximum of collaterals on a single loan to 50. If the request has more than 50 Collaterals or the number of Collaterals in the request would cause the total number of collaterals to be greater than 50 on the loan, the request will fail. An example of the error is as follows:

``` json
{
    "description": "This SRF already has 5 collaterals from a maximum of 50 and you want to add 50",
    "field": ""
}
```

##### Request Validation

The API will validate the data from the request against the schema returned in the AddCollateral Fields API.

##### User Validation

If the `meta.updatedBy` is not present or is empty, the API will fail. If the email address in `meta.updatedBy` is not valid or does not have access to the logged in company or the loan specifically, the API will return an error. Examples of those errors are as follows:

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

##### Completed Loan Validation

If the collateral is attempting to be added to a loan that has been marked `completed`, the following error will be returned:

``` json
{
  "description": "This loan can't be updated since it's marked as complete.",
  "field": ""
}
