---
description: "Automatically generated file. DO NOT MODIFY"
---

```go

//THE GO SDK IS IN PREVIEW. NON-PRODUCTION USE ONLY
graphClient := msgraphsdk.NewGraphServiceClient(requestAdapter)

requestBody := graphmodels.NewActivatePostRequestBody()


user := graphmodels.NewUser()
id := "8cdf25a8-c9d2-423e-a03d-3f39f03c3e97"
user.SetId(&id) 
user1 := graphmodels.NewUser()
id := "ea09ac2e-77e3-4134-85f2-25ccf3c33387"
user1.SetId(&id) 

subjects := []graphmodels.Objectable {
	user,
	user1,

}
requestBody.SetSubjects(subjects)

graphClient.IdentityGovernance().LifecycleWorkflows().WorkflowsById("workflow-id").IdentityGovernanceActivate().Post(context.Background(), requestBody, nil)


```