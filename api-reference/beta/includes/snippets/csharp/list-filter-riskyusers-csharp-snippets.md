---
description: "Automatically generated file. DO NOT MODIFY"
---

```csharp

var graphClient = new GraphServiceClient(requestAdapter);

var result = await graphClient.IdentityProtection.RiskyUsers.GetAsync((requestConfiguration) =>
{
	requestConfiguration.QueryParameters.Filter = "riskLevel eq microsoft.graph.riskLevel'medium'";
});


```