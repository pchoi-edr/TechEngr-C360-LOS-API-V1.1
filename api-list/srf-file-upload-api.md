# SRF File Upload API

Services performed on collateral properties typically result
in documentation (_e.g._ reports, legal paperwork, affidavits,
_etc._). These documents are ordinarily uploaded to--or
otherwise made available through--the Collateral 360 system.

This API is responsible for uploading the documents that
are associated with a service performed on a collateral
property. It does not support service
requests that are still in the "draft" status.

## Available Endpoints

The following endpoints are available as part of this API:

### <span style="background-color: #ebb747; font-weight: bold; color: #ffffff; padding: 3px 10px; border-radius: 14px;">POST</span> **File Upload**

```text
/api/v1.1/files/upload/locationId/:locationId/uploadedBy/:uploadedBy
```

This endpoint is accessible via the HTTP `POST` method. A
successful invocation will return the contents of the file
in the response body.

The files uploaded can be downloaded within C360 within the File Manager UI.

#### Request

##### Path Parameters

| Path Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| :locationId | Integer | Yes | The ID of uploaded file. |
| :uploadedBy | string | Yes | The email address of file uploader. |

##### Body Parameters

| Body Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| file | Integer | Yes | The ID of uploaded file. |
| preparedBy | string | No | The email address of file uploader. |
| reportTitle | string | No | Title of the Report |
| reportDate | string | No | Report Date |
| displayFileName | string | No | The File Name if you do not want to display original file name |
| serviceGroups | string | No | Stringified Array or Objects that contain the Service Groups |
| serviceTypes | string | No | Stringified Array or Objects that contain the Service Types |
| documentTypes | string | No | Stringified Array or Objects that contain the Document Types |
| documentStatus | string | No | Stringified Objects that contain the Document Status |

##### Query String Parameters

This endpoint does not accept any query string parameters.

#### Response

##### Expected HTTP Response Code

When operating normally, this API endpoint will return
an HTTP response code of `200` ("OK").

##### Expected HTTP Response Body Content

Unlike most other LOS API responses, the HTTP body content
will vary depending on whether the requested file could be
successfully retrieved and sent to the client:

  * If an error occurs, then the body content will be a
    typical JSON-encoded error response. The `responseCode`
    field will contain the corresponding HTTP response code
    that would be indicated by the specific error condition
    (but the actual HTTP response code of the response will
    still be `200`).

  * For a successful invocation, the body content will be
    the binary content of the requested file.

##### Determining If a File Was Successfully Uploaded

Client applications should **not** attempt to determine if an
error occurred by examining whether the response body content
is structured like a JSON error response. Instead, the presence
of the `Content-Disposition` HTTP header with a case-insensitive
value of `attachment` should be used for this purpose.

The `Content-Disposition` header can contain optional
parameters in its value, but these parameters should be ignored
when attempting to determine if its value indicates that a file
was successfully retrieved. The following algorithm can be used
to determine if a file download was successful or not:

  1) Determine if the `Content-Disposition` header is present.
     If this is not present, then the response is an error
     response. No further steps in this algorithm need to
     be performed.

  2) Obtain the textual value of the case-insensitive
     `Content-Disposition` HTTP header.

  3) If at least one semicolon (";") is present in the value
     of the `Content-Disposition` header, then strip the text
     from the first semicolon (inclusive) to the end of the
     string.

  4) Trim all whitespace from the beginning and the end of the
     resultant value:

     * Space
     * Horizontal tab
     * Carriage return
     * Line feed

  5) Perform a case-insensitive comparison to determine if the
     remaining value is equal to "attachment" (using the
     seven-bit ASCII encoding).

  6) If the strings are equal (case-insensitively), then the
     file download was successful, and the response should be
     interpreted as the binary contents of the downloaded file.
     If not, then an error condition has occurred, and the
     response should be interpreted as a JSON error response.

##### The Content-Type Header

Note that, if the download request is successful, then the
`Content-Type` header will reflect the content type of the
downloaded file (instead of the usual content type indicating
a JSON API response).

As is typical, an unknown content type will be returned as
`binary/octet-stream` (indicating the content is a stream
of eight-byte bytes whose structure is unknown).
