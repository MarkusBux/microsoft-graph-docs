---
description: "Automatically generated file. DO NOT MODIFY"
---

```go

//THE GO SDK IS IN PREVIEW. NON-PRODUCTION USE ONLY
graphClient := msgraphsdk.NewGraphServiceClient(requestAdapter)

headers := abstractions.NewRequestHeaders()
headers.Add("Prefer", "outlook.timezone=\"Pacific Standard Time\"")

requestParameters := &graphconfig.MeEventsRequestBuilderGetQueryParameters{
	Select: [] string {"subject","body","bodyPreview","organizer","attendees","start","end","location"},
}
configuration := &graphconfig.MeEventsRequestBuilderGetRequestConfiguration{
	Headers: headers,
	QueryParameters: requestParameters,
}

result, err := graphClient.Me().Events().Get(context.Background(), configuration)


```