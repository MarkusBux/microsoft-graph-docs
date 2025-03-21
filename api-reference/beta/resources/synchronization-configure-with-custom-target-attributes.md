---
title: "Configure synchronization with custom target attributes"
description: "Customize your synchronization schema to include custom attributes that are defined in the target directory."
ms.localizationpriority: medium
doc_type: conceptualPageType
author: "ArvindHarinder1"
ms.prod: "applications"
ms.date: 07/20/2022
---

# Configure synchronization with custom target attributes

Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

You can customize your synchronization schema to include custom attributes that are defined in the target directory. This article describes how to customize a Salesforce subscription by adding a new field called `officeCode`. You set up synchronization from Azure Active Directory (Azure AD) to Salesforce, and for each user, you will populate the `officeCode` field in Salesforce with the value from the `extensionAttribute10` field in Azure AD.

This article assumes that you have already added an application that supports synchronization to your tenant through the [Azure Portal](https://portal.azure.com), that you know the application display name, and that you have an authorization token for Microsoft Graph. For information about how to get the authorization token, see [Get access tokens to call Microsoft Graph](/graph/auth/).

## Find the service principal object by display name

The following example shows how to find a service principal object with the display name Salesforce.

```http
GET https://graph.microsoft.com/beta/servicePrincipals?$select=id,appId,displayName&$filter=startswith(displayName, 'salesforce')
Authorization: Bearer {Token}

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#servicePrincipals(id,appId,displayName)",
    "value": [
    {
        "id": "167e33e9-f80e-490e-b4d8-698d4a80fb3e",
        "appId": "cd3ed3de-93ee-400b-8b19-b61ef44a0f29",
        "displayName": "Salesforce"
    },
    {
        "id": "8cbbb70b-7290-42da-83ee-89fa3517a977",
        "appId": "b0f2e3b1-fe31-4658-b216-44dcaeabb63a",
        "displayName": "salesforce 1"
    },
    {
        "id": "60443998-8cf7-4e61-b05c-a53b658cb5e1",
        "appId": "79079396-c301-405d-900f-e2e0c2439a90",
        "displayName": "Salesforce Sandbox"
    }
    ]
}
```

The `{servicePrincipalId}` is `167e33e9-f80e-490e-b4d8-698d4a80fb3e`.


## List synchronization jobs in the context of the service principal 

The following example shows you how to get the `jobId` that you need to work with. Generally, the response returns only one job.

```http
GET https://graph.microsoft.com/beta/servicePrincipals/60443998-8cf7-4e61-b05c-a53b658cb5e1/synchronization/jobs
Authorization: Bearer {Token}

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#servicePrincipals('60443998-8cf7-4e61-b05c-a53b658cb5e1')/synchronization/jobs",
    "value": [
        {
            "id": "SfSandboxOutDelta.e4bbf44533ea4eabb17027f3a92e92aa",
            "templateId": "SfSandboxOutDelta",
            "schedule": {},
            "status": {}
    }
    ]
}
```

The `{jobId}` is `SfSandboxOutDelta.e4bbf44533ea4eabb17027f3a92e92aa`.


## Get the synchronization schema
The following example shows how to get the synchronization schema.


# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_synchronizationschema_2"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/beta/servicePrincipals/{servicePrincipalId}/synchronization/jobs/{jobId}/schema
Authorization: Bearer {Token}
```

# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-synchronizationschema-2-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-synchronizationschema-2-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-synchronizationschema-2-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-synchronizationschema-2-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [PowerShell](#tab/powershell)
[!INCLUDE [sample-code](../includes/snippets/powershell/get-synchronizationschema-2-powershell-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [PHP](#tab/php)
[!INCLUDE [sample-code](../includes/snippets/php/get-synchronizationschema-2-php-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---

>**Note:** The response object shown here might be shortened for readability. All the properties will be returned in an actual call.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.synchronizationSchema"
} -->
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "directories": [
	    {
		      "id": "66e4a8cc-1b7b-435e-95f8-f06cea133828",
		      "name": "Azure Active Directory",
		      "objects": [
			    {
		            "attributes": [
			            {
			              "anchor": true,
			              "caseExact": false,
			              "defaultValue": null,
			              "metadata": [],
			              "multivalued": false,
			              "mutability": "ReadWrite",
			              "name": "objectId",
			              "required": false,
			              "referencedObjects": [],
			              "type": "String"
			            },
			            {
			              "anchor": false,
			              "caseExact": false,
			              "defaultValue": null,
			              "metadata": [],
			              "multivalued": false,
			              "mutability": "ReadWrite",
			              "name": "streetAddress",
			              "required": false,
			              "referencedObjects": [],
			              "type": "String"
			            }
					],
					"name": "User"
				}
			 ]
		},
		{
		      "id": "8ffa6169-f354-4751-9b77-9c00765be92d",
		      "name": "salesforce.com",
		      "objects": []
		}
  ],
 "synchronizationRules": [
	    {
	      "editable": true,
	      "id": "4c5ecfa1-a072-4460-b1c3-4adde3479854",
	      "name": "USER_OUTBOUND_USER",
	      "objectMappings": [
		        {
			        "attributeMappings": [
				            {
				              "defaultValue": "True",
				              "exportMissingReferences": false,
				              "flowBehavior": "FlowWhenChanged",
				              "flowType": "Always",
				              "matchingPriority": 0,
				              "source": {
				                "expression": "Not([IsSoftDeleted])",
				                "name": "Not",
				                "parameters": [
				                  {
				                    "key": "source",
				                    "value": {
				                      "expression": "[IsSoftDeleted]",
				                      "name": "IsSoftDeleted",
				                      "parameters": [],
				                      "type": "Attribute"
				                    }
				                  }
				                ],
				                "type": "Function"
				              },
				              "targetAttributeName": "IsActive"
				            }
			         ],
			        "enabled": true,
			        "flowTypes": "Add, Update, Delete",
			        "name": "Synchronize Azure Active Directory Users to salesforce.com",
			        "scope": null,
			        "sourceObjectName": "User",
			        "targetObjectName": "User"
			}]
		}]
}
```

## Add a definition for the officeCode attribute and a mapping between attributes

Use a plain text editor of your choice (for example, [Notepad++](https://notepad-plus-plus.org/) or [JSON Editor Online](https://www.jsoneditoronline.org/)) to:

1. Add an [attribute definition](synchronization-attributedefinition.md) for the `officeCode` attribute. 

	- Under directories, find the directory with the name salesforce.com, and in the object's array, find the one named **User**.
	- Add the new attribute to the list, specifying the name and type, as shown in the following example.

2. Add an [attribute mapping](synchronization-attributemapping.md) between `officeCode` and `extensionAttribute10`.

	- Under [synchronizationRules](synchronization-synchronizationrule.md), find the rule that specifies Azure AD as the source directory, and Salesforce.com as the target directory (`"sourceDirectoryName": "Azure Active Directory",   "targetDirectoryName": "salesforce.com"`).
	- In the [objectMappings](synchronization-objectmapping.md) of the rule, find the mapping between users (`"sourceObjectName": "User",   "targetObjectName": "User"`).
	- In the [attributeMappings](synchronization-attributemapping.md) array of the **objectMapping**, add a new entry, as shown in the following example.

```json
{  
    "directories": [
    {
        "id": "8ffa6169-f354-4751-9b77-9c00765be92d",
            "name": "salesforce.com",
            "objects": [
            {
                "attributes": [
                        {
                            "name": "officeCode",
                            "type": "String"
                        }
                ],
                "name":"User"
            }]
    }
    ],
    "synchronizationRules": [
        {
        "editable": true,
        "id": "4c5ecfa1-a072-4460-b1c3-4adde3479854",
        "name": "USER_OUTBOUND_USER",
        "objectMappings": [
            {
            "attributeMappings": [
            	{
                    "source": {
							"name": "extensionAttribute10",
							"type": "Attribute"
                    	},
                    "targetAttributeName": "officeCode"
                }
            ],
            "name": "Synchronize Azure Active Directory Users to salesforce.com",
            "scope": null,
            "sourceObjectName": "User",
            "targetObjectName": "User"
            }
        ],
    "priority": 1,
        "sourceDirectoryName": "Azure Active Directory",
        "targetDirectoryName": "salesforce.com"
    }
	]
}
```

## Save the modified synchronization schema

When you save the updated synchronization schema, make sure that you include the entire schema, including the unmodified parts. This request will replace the existing schema with the one that you provide.

```http
PUT https://graph.microsoft.com/beta/servicePrincipals/{servicePrincipalId}/synchronization/jobs/{jobId}/schema
Authorization: Bearer {Token}
{
    "directories": [..],
    "synchronizationRules": [..]
}

HTTP/1.1 201 No Content
```

If the schema was saved successfully, on the next iteration of the synchronization job, it will start re-processing all the accounts in your Azure AD, and the new mappings will be applied to all provisioned accounts.
<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79 
2015-10-25 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "Get the synchronization schema",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": [
  ]
}-->
