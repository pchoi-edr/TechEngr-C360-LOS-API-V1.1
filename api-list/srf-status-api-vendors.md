# SRF Status API - Engagement Vendors

In version 1.1, EDR has released Vendor information in the Status API. For the end user, nothing needs to be provided. Vendor information will be provided as part of the GET Status call. If Engagement Vendor details are available, vendor details will now be provided as part of the status response package.

#### Response

##### Additional Data Objects

1. `hasEngagedVendor` which can be:
    -  `"hasEngagedVendor": "Yes"`
       - Yes is when we have an engaged vendor, or for 3rd party services
  or
    - `"hasEngagedVendor": "No"`
       - No when there is no vendor engaged, and it's not a 3rd party service
2. `vendor` which is an object
    ```json
    "vendor": {
        "accountId": 12345,
        "companyName": "Test Vendor Company",
        "name": "Tony Vendor",
        "emailAddress": "fake_7441723a-68d@example.com",
        "rating": {
            "quality": "3/5",
            "service": "4/5",
            "performance": "2/5",
            "total": "9/15"
        },
        "hasValidLicense": "Yes",
        "license": {
            "number": "553.001360",
            "expiration": "09/30/2021"
        }
    },

    ```
    - Each field can be either blank or have a value
    The ratings have the format: `X/5` and the total is `X/15` OR they can be blank
    - If the vendor has a valid license, then `hasValidLicense` will be Yes, and the `license` key will be an array with data, but if it's No, then the license key is an empty array
    - if it's a 3rd party service the `vendor` key will look like this
    ```json
    "vendor": {
        "accountId": "",
        "companyName": "3rd Party Vendor",
        "firstName": "",
        "lastName": "",
        "emailAddress": "",
        "rating": {
            "quality": "",
            "service": "",
            "performance": "",
            "total": ""
        }
    },
    ```
    - The ratings have the format: `X/5` and the total is `X/15` OR they can be blank the rest of the response is all blank, except the companyName which will always be 3rd Party Vendor
3. `participatingVendors` which is also an array
    ```json
    "participatingVendors": [
        {
            "vendorID": 1,
            "companyName": "Test Vendor Company",
            "email": "fake_e81ab9da-68d@example.com",
            "name": "Test Vendor",
            "contribution": "Authored"
        }
    ]
    ​
    ```

    - this key can be either an empty array, or have data as above an example response

##### Example JSON Response

Sample of a full JSON response from Status API

  ```json
  {
  "meta": {
    "reason": "OK",
    "responseCode": 200,
    "responseID": "9a376460-e459-11e9-bfb2-69a10751705e",
    "errors": null,
    "warnings": null,
    "function": "",
    "success": true
  },
  "data": {
      "serviceRequestID": 774487,
      "loanID": 1271932,
      "draft": false,
      "locations": [
        {
          "locationID": 1900556,
          "jobNumber": "19-000910-0003",
          "complete": false,
          "address": {
            "street1": "7 Humphrey",
            "street2": "unit text",
            "city": "Oak Park",
            "state": "IL",
            "postalCode": "60302",
            "country": "US",
            "latitude": 41.887195,
            "longitude": -87.776514
          },
          "services": [
            {
              "serviceType": "MoldInv",
              "name": "Mold Investigation",
              "serviceGroup": "Environmental",
              "locationServiceID": 1752,
              "jobNumber": null,
              "status": "New",
              "currency": null,
              "fee": null,
              "primaryAssignee": null,
              "secondaryAssignees": [],
              "startDate": null,
              "dueDate": null,
              "completionDate": null,
              "created": "2019-09-24T11:53:59Z",
              "updated": null,
              "hasEngagedVendor": "No",
              "vendor": [],
              "participatingVendors": []
            },
            {
              "serviceType": "Appraisal",
              "name": "External Appraisal Report",
              "serviceGroup": "Valuation",
              "locationServiceID": 1753,
              "jobNumber": null,
              "status": "Accepted",
              "currency": "USD",
              "fee": 123,
              "primaryAssignee": null,
              "secondaryAssignees": [],
              "startDate": "2019-09-24T11:55:55Z",
              "dueDate": "2019-10-31T13:00:00Z",
              "completionDate": null,
              "created": "2019-09-24T11:54:37Z",
              "updated": "2019-09-26T13:25:09Z",
              "hasEngagedVendor": "Yes",
              "vendor": {
                "accountId": 54321,
                "companyName": "Test Vendor Company",
                "name": "John Vendor",
                "emailAddress": "fake_997b4d9b-68d@example.com",
                "rating": {
                  "quality": 5,
                  "service": 4,
                  "performance": 4,
                  "total": 13
                },
                "hasValidLicense": "Yes",
                "license": {
                  "number": "553.001360",
                  "expiration": "09/30/2021"
                }
              },
              "participatingVendors": [
                {
                  "vendorID": 2,
                  "companyName": "Vendor Company Test",
                  "email": "fake_5ab4639f-68d@example.com",
                  "name": "Test L Vendor",
                  "contribution": "Performed"
                },
                {
                  "vendorID": 3,
                  "companyName": "Company Vendor Test",
                  "email": "fake_d612c868-68d@example.com",
                  "name": "Mike Vendor",
                  "contribution": "Authored"
                },
                {
                  "vendorID": 4,
                  "companyName": "Vendor Company Test Name",
                  "email": "fake_688e7cb6-68d@example.com",
                  "name": "Guido Vendor",
                  "contribution": "Other"
                }
              ]
            },
            {
              "serviceType": "ExtCompliRevw",
              "name": "External Compliance Review",
              "serviceGroup": "Valuation",
              "locationServiceID": 1754,
              "jobNumber": null,
              "status": "Accepted",
              "currency": "USD",
              "fee": 555,
              "primaryAssignee": null,
              "secondaryAssignees": [],
              "startDate": "2019-09-30T12:38:56Z",
              "dueDate": "2019-10-31T00:00:00Z",
              "completionDate": null,
              "created": "2019-09-24T11:54:37Z",
              "updated": "2019-09-30T12:48:12Z",
              "hasEngagedVendor": "Yes",
              "vendor": {
                "accountId": 12345,
                "companyName": "Test International",
                "name": "William Vendor",
                "emailAddress": "fake_7441723a-68d@example.com",
                "rating": {
                  "quality": "",
                  "service": "",
                  "performance": "",
                  "total": ""
                },
                "hasValidLicense": "No",
                "license": []
              },
              "participatingVendors": [
                {
                  "vendorID": 5,
                  "companyName": "Testing Vendor Co.",
                  "email": "fake_e81ab9da-68d@example.com",
                  "name": "Michele Vendor",
                  "contribution": "Authored"
                }
              ]
            }
          ]
        }
      ],
      "created": "2019-09-16T15:44:15Z"
    }
  }

  ```
