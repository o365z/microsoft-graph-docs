---
title: "Get serviceHealth"
description: "Read service health overview of a specified service for tenant. The operation returns a [serviceHealth](../resources/servicehealth.md) object."
author: "payiAzure"
localization_priority: Normal
ms.prod: "service communications"
doc_type: apiPageType
---

# Get serviceHealth
Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Retrieve the properties and relationships of a [serviceHealth](../resources/servicehealth.md) object.

This operation is to retrieve health overviews of a specified service for tenant.

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type|Permissions (from least to most privileged)|
|:---|:---|
|Delegated (work or school account)|ServiceHealth.Read.All|
|Delegated (personal Microsoft account)|ServiceHealth.Read.All|
|Application|ServiceHealth.Read.All|

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->

``` http
GET /admin/serviceAnnouncement/healthOverviews('{Service Name}')
```

## Optional query parameters
This method supports some of the OData query parameters to help customize the response. For general information, see [OData query parameters](/graph/query-parameters).

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|

## Request body
Do not supply a request body for this method.

## Response

If successful, this method returns a `200 OK` response code and a [serviceHealth](../resources/servicehealth.md) object in the response body.

## Examples

### Example 1: Get the properties of a [serviceHealth](../resources/servicehealth.md) object

#### Request
<!-- {
  "blockType": "request",
  "name": "get_servicehealth"
}
-->

``` http
GET https://graph.microsoft.com/beta/admin/serviceAnnouncement/healthOverviews('Microsoft 365 suite')
```

#### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.serviceHealth"
}
-->

``` http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#admin/serviceAnnouncement/healthOverviews/$entity",
    "service": "Microsoft 365 suite",
    "status": "falsePositive",
    "id": "OSDPPlatform"
}
```

### Example 2: Include navigation property issues

#### Request
<!-- {
  "blockType": "request",
  "name": "get_servicehealth"
}
-->

``` http
GET https://graph.microsoft.com/beta/admin/serviceAnnouncement/healthOverviews('Microsoft 365 suite')?$expand=issues
```

#### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.serviceHealth"
}
-->

``` http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#admin/serviceAnnouncement/healthOverviews(issues())/$entity",
  "service": "Microsoft 365 suite",
  "status": "FalsePositive",
  "id": "OSDPPlatform",
  "issues@odata.context": "https://graph.microsoft.com/beta/$metadata#admin/serviceAnnouncement/healthOverviews('OSDPPlatform')/issues",
  "issues": [
        {
          "startDateTime": "2020-11-04T00:00:00Z",
          "endDateTime": "2020-11-20T17:00:00Z",
          "lastModifiedDateTime": "2020-11-20T17:56:31.39Z",
          "title": "Intermittently unable to access some Microsoft 365 services",
          "id": "MO226574",
          "impactDescription": "Users may have been intermittently unable to access some Microsoft 365 services.",
          "classification": "Advisory",
          "origin": "Microsoft",
          "status": "ServiceRestored",
          "service": "Exchange Online",
          "feature": "Tenant Administration (Provisioning, Remote PowerShell)",
          "featureGroup": "Management and Provisioning",
          "isResolved": true,
          "highImpact": null,
          "details": [],
          "posts": [
              {
                "createdDateTime": "2020-11-12T07:07:38.97Z",
                "postType": "Regular",
                "description": {
                    "contentType": "Text",
                    "content": "Users may have been intermittently unable to access some Microsoft 365 services. We'll provide an update within 30 minutes."
                  }
              },
              ...
          ]
        },
        ...
    ]
}
```