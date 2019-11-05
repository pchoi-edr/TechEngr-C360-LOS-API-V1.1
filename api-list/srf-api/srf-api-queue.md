# Service Request Form API - Submission Queue Processing

The Non-Draft Service Request process uses Queue Jobs Processing to handle various tasks which would otherwise be too process intensive.

So the initial Service Request Submission returns the serviceRequestID's and locationID's, where this are assets to be used with further downstream functionality such as [File Upload API](../srf-file-upload-api.md).

Everything else that does not require immediate assets to be returned, will be run in a Queue Jobs Processing.

Here is a list of all the Queue Jobs Processing that happens when an SRF is created

  * Email notifications: Emails notifications that are configured to trigger when SRF is created
  * Routing rules: Routing rules that assign a primary and secondary assignees on Services added on SRF
  * Access Rules: Some companies have access rules that limit access to loan files when they are created
  * Prescreen:  Environmental prescreen is run on every collateral

