---
description: "Automatically generated file. DO NOT MODIFY"
---

```csharp

var graphClient = new GraphServiceClient(requestAdapter);

var requestBody = new TokenLifetimePolicy
{
	Definition = new List<string>
	{
		"definition-value",
	},
	DisplayName = "displayName-value",
	IsOrganizationDefault = true,
};
var result = await graphClient.Policies.TokenLifetimePolicies["{tokenLifetimePolicy-id}"].PatchAsync(requestBody);


```