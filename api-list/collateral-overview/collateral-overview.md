# Collateral Overview - Patch API

This API provides an overview of Collateral Overview patch API for a locationID.

If a location ID is specified, then the results will be
limited to only that single location. No other locations
will be present in the data structure returned to the client.

## Available Endpoints

The following endpoints are made available by this API, depending on
the desired identifier used to query the server:

### <span style="background-color: #0095ff; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">PATCH</span> **Collateral Overview**

```text
/api/v1.1/collateralOverview/:locationID
```

The API endpoints are accessible via the HTTP `PATCH` method.

#### Request

##### Path Parameters

| Path Parameter | Required | Type | Description |
| :--- | :--- | :--- | :--- |
| :locationID | Integer | Yes* | A location ID. |


##### Body Parameters

In order to update a loan, a JSON body must be sent.
The most basic JSON body is:

```json
{
    "meta": {
        "updatedBy": "email@email.com"
    },
    "data": {
	"transaction": {
	},
	"collaterals":  [
		{}
	]
    }
}
```

The updatedBy in the meta object has to be a user who has access to the loan, and we will log in the history entries that this user made the changes
Based on what fields you want to update, you can either add specific fields in the transaction / collaterals object or all of them.

Only the fields that are different will be updated. That means if you add LoanAmount as 4000, and the LoanAmount is currently 4000, that field wont get updated (no history entry will exist, and no emails will be sent)

In the **_Transaction_** & **_Collaterals_** object, you can update one valid field or all.

A more complex JSON body would look like the following:

```json
{
  "meta": {
    "updatedBy": "emailUser@domain.com"
  },
  "data": {
    "transaction": {
      "ProjectName": "LOS NON-DRAFT single test update CO done",
      "LoanNumber": "222",
      "LoanAmount": 333,
      "BorrowerName": "Jack Bauer done",
      "ecid": 444,
      "CostCenter": "909102",
      "RequesterAID": "fake_399fa74e-086@chase.com",
      "AccountOfficerAID": "fake_399fa74e-086@chase.com",
      "CompanyNumber": "0001",
      "LendingGroup": "BUSINESS BANKING WEST",
      "TeamLeadAID": [
        "fake_399fa74e-086@chase.com"
      ],
      "ClosingDate": "12/31/2019",
      "DesiredReviewDeliveryDate": "12/30/2019",
      "LoanCurrentBalance": 555,
      "LoanNewMoney": 666,
      "IsSbaLoan": false,
      "PartnerBusinessName": "test business name done",
      "AltPartnerBusinessName": "alt business name done",
      "IsParticipationLoan": true,
      "ParticipationLoanAmount": 100000,
      "ParticipationLenderShare": 50000,
      "IsAgentBank": true,
      "OtherBanks": "other bank text done",
      "PriorJob": "Not done",
      "isPortfolio": true
    },
    "collaterals": [
      {
        "PropertyType": {
          "PropertyType": "Land",
          "PropertySubType": "Land - Office"
        },
        "PropCountry": "US",
        "PropAddress": "501 South Vincent Avenue",
        "PropUnit": "unit text done",
        "PropCity": "West Covina",
        "PropState": "CA",
        "PropZip": "91793",
        "ContactCompany": "Contact company name done",
        "PropCounty": "LOS ANGELES",
        "ContactName": "test name",
        "PropLatitude": "34.066491",
        "PropLongitude": "-117.928287",
        "ContactPhone": "7777",
        "ContactEmail": "test1234@edrnet.com",
        "ContactAltPhone": "8888",
        "PropertyNumbers": "9999",
        "Comments": "comments text done",
        "availableReports": "not available done",
        "Purpose": "New Loan to JPMC",
        "AppraisalPriority": "High Priority",
        "ofsiReportReview": false,
        "PropInterest": [
          "Leasehold",
          "NotSure"
        ],
        "ValuationPremise": [
          "AsCompleted"
        ],
        "PurposeEnv": "OREO",
        "OtherTextEnv": "other text content",
        "EnvironmentalPriority": "High Priority",
        "ContactType": "Broker",
        "ContactTypeOther": "other contact",
        "NumBuildings": 1,
        "BuildingSize": {
          "BuildingSize": "1",
          "BuildingSizeUnits": "SF"
        },
        "improvementsizeAsIs": {
          "improvementsizeAsIs": "2",
          "improvementsizeAsIsUnits": "SM"
        },
        "improvementsizeAsIsAlt": {
          "improvementsizeAsIsAlt": "3",
          "improvementsizeAsIsAltUnits": "Sites"
        },
        "BuildingSizeCompleted": {
          "BuildingSizeCompleted": "4",
          "BuildingSizeCompletedUnits": "SM"
        },
        "improvementsizeAsCompletedAlt": {
          "improvementsizeAsCompletedAlt": "5",
          "improvementsizeAsCompletedAltUnits": "Slips"
        },
        "LandSize": {
          "LandSize": "6",
          "LandSizeUnits": "Sites"
        },
        "ExcessLand": false,
        "YearBuilt": 2000,
        "LastRenovated": 2001,
        "Tenancy": "Multi-Tenant Investor",
        "Occupancy": "10",
        "TenantsThirdPartyLeasePct": "20",
        "Tenants": 30,
        "HasRenovation": true,
        "RenevationDesc": "renovated description done",
        "Zoning": "zone text",
        "PropertyStatus": [
          "Vacant Land"
        ],
        "HasUseChange": true,
        "ProposedUse": "proposed use done",
        "HasGroundLease": true,
        "GroundLeaseDesc": "ground lease description done",
        "IsForSale": true,
        "ListedSaleBrokerCnt": "2",
        "ListPrice": 200,
        "HasRecentSale": true,
        "PendingSaleBrokerCnt": "300",
        "SalePrice": 400,
        "SaleDate": "1/1/2019",
        "PropertyDescription": "property description text done",
        "PropInterestOther": "other interest",
        "ValuationPremiseOther": "valuation premise other"
      }
    ]
  }
}
```

The fields that you can use are present in the fields API located at this URL: /api/v1.1/collateralOverview/fields

**NOTE:** if you use fields that are not present in the transaction / collateral of the loan, they wont get used an no error will be returned about them

#### Response

##### Expected HTTP Response Code

When operating normally, this API endpoint will return
an HTTP response code of `200` ("OK").

##### Example JSON Success Response

```json
{
  "meta": {
    "date": "2018-04-28 12:23:23",
    "function": "patch",
    "responseCode": 201,
    "responseID": "e3733640-789c-11e8-9dfc-81c439846400",
    "success": true,
    "warnings": []
  },
  "data": {
    "updated": true
  }
}
```

##### Example JSON Failed Response

```json
{
  "meta": {
    "date": "2019-12-11T13:58:59Z",
    "errors": [
      {
        "description": "Collateral Tab -  Pending/Sold must be a value in the following list: Yes, No",
        "field": ""
      }
    ],
    "function": "patch",
    "reason": "Bad Request",
    "responseCode": 400,
    "responseID": "6124e9a0-1c1e-11ea-aa1b-2fa4ba7c3e9d",
    "success": false,
    "warnings": []
  },
  "data": {}
}
```