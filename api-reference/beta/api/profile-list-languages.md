---
title: "List languages"
description: "Retrieve a list of languageProficiency objects."
ms.localizationpriority: medium
author: "kevinbellinger"
ms.prod: "people"
doc_type: "apiPageType"
---

# List languages

Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Retrieve a list of [languageProficiency](../resources/languageproficiency.md) objects from a user's [profile](../resources/profile.md).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

| Permission type                        | Permissions (from least to most privileged)                                      |
|:---------------------------------------|:---------------------------------------------------------------------------------|
| Delegated (work or school account)     | User.Read, User.ReadWrite, User.ReadBasic.All, User.Read.All, User.ReadWrite.All |
| Delegated (personal Microsoft account) | User.Read, User.ReadWrite, User.ReadBasic.All, User.Read.All, User.ReadWrite.All |
| Application                            | User.ReadBasic.All, User.Read.All, User.ReadWrite.All |

## HTTP request

<!-- { "blockType": "ignored" } -->

```http
GET /me/profile/languages
GET /users/{id | userPrincipalName}/profile/languages
```

## Optional query parameters

This method supports the following OData query parameters to help customize the response. For general information, see [OData query parameters](/graph/query-parameters).

|Name            |Value    |Description                                                                                                                                                                 |
|:---------------|:--------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|$filter         |string   |Limits the response to only those objects which contain the specified criteria.                                                                                             |
|$orderby        |string   |By default the objects in the response are sorted by their createdDateTime value in a query. You can change the order of the of the response using the *$orderby* parameter.|
|$select         |string   |Comma-separated list of properties to include in the response. For optimal performance, only select the subset of properties needed.                                        |
|$skip           |int      |Skip the first n results, useful for paging.                                                                                                                                |
|$top            |int      |Number of results to be returned.                                                                                                                                           |

## Request headers

| Name           |Description                  |
|:---------------|:----------------------------|
| Authorization  | Bearer {token}. Required.   |

## Request body

Do not supply a request body for this method.

## Response

If successful, this method returns a `200 OK` response code and a collection of [languageProficiency](../resources/languageproficiency.md) objects in the response body.

## Examples

### Request

The following is an example of the request.

# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_languages"
}-->

```msgraph-interactive
GET https://graph.microsoft.com/beta/me/profile/languages
```

# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-languages-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-languages-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-languages-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-languages-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [PowerShell](#tab/powershell)
[!INCLUDE [sample-code](../includes/snippets/powershell/get-languages-powershell-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [PHP](#tab/php)
[!INCLUDE [sample-code](../includes/snippets/php/get-languages-php-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---

### Response

The following is an example of the response.

> **Note:** The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.languageProficiency",
  "isCollection": true
} -->

```http
HTTP/1.1 200 OK
Content-type: application/json

{
  "value": [
    {
      "id": "0fb4c1e3-c1e3-0fb4-e3c1-b40fe3c1b40f",
      "allowedAudiences": "organization",
      "inference": null,
      "createdDateTime": "2020-07-06T06:34:12.2294868Z",
      "createdBy": {
        "application": null,
        "device": null,
        "user": {
          "displayName": "Innocenty Popov",
          "id": "db789417-4ccb-41d1-a0a9-47b01a09ea49"
        }
      },
      "lastModifiedDateTime": "2020-07-06T06:34:12.2294868Z",
      "lastModifiedBy": {
        "application": null,
        "device": null,
        "user": {
          "displayName": "Innocenty Popov",
          "id": "db789417-4ccb-41d1-a0a9-47b01a09ea49"
        }
      },
      "source": null,
      "displayName": "Norwegian Bokmål",
      "tag": "nb-NO",
      "spoken": "nativeOrBilingual",
      "written": "nativeOrBilingual",
      "reading": "nativeOrBilingual"
    }
  ]
}
```


