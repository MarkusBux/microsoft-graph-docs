---
description: "Automatically generated file. DO NOT MODIFY"
---

```csharp

var graphClient = new GraphServiceClient(requestAdapter);

var result = await graphClient.Policies.AppManagementPolicies["{appManagementPolicy-id}"].AppliesTo.GetAsync();


```