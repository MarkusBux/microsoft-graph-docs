---
description: "Automatically generated file. DO NOT MODIFY"
---

```go

//THE GO SDK IS IN PREVIEW. NON-PRODUCTION USE ONLY
graphClient := msgraphsdk.NewGraphServiceClient(requestAdapter)

requestBody := graphmodels.NewComplianceChange()
additionalData := map[string]interface{}{
content := graphmodels.New()
catalogEntry := graphmodels.New()
id := "6b7e60db-a8e4-426a-9aed-bd12b5c0b9d4"
catalogEntry.SetId(&id) 
	content.SetCatalogEntry(catalogEntry)
	requestBody.SetContent(content)
deploymentSettings := graphmodels.New()
	requestBody.SetDeploymentSettings(deploymentSettings)
schedule := graphmodels.New()
startDateTime := "String (timestamp)"
schedule.SetStartDateTime(&startDateTime) 
gradualRollout := graphmodels.New()
endDateTime := "String (timestamp)"
gradualRollout.SetEndDateTime(&endDateTime) 
	schedule.SetGradualRollout(gradualRollout)
	requestBody.SetSchedule(schedule)
}
requestBody.SetAdditionalData(additionalData)

result, err := graphClient.Admin().Windows().Updates().UpdatePoliciesById("updatePolicy-id").ComplianceChanges().Post(context.Background(), requestBody, nil)


```