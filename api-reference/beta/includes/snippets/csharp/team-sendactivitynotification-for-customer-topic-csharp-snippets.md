---
description: "Automatically generated file. DO NOT MODIFY"
---

```csharp

var graphClient = new GraphServiceClient(requestAdapter);

var requestBody = new Microsoft.Graph.Beta.Users.Item.Teamwork.SendActivityNotification.SendActivityNotificationPostRequestBody
{
	Topic = new TeamworkActivityTopic
	{
		Source = TeamworkActivityTopicSource.Text,
		Value = "Deployment Approvals Channel",
		WebUrl = "https://teams.microsoft.com/l/message/19:448cfd2ac2a7490a9084a9ed14cttr78c@thread.skype/1605223780000?tenantId=c8b1bf45-3834-4ecf-971a-b4c755ee677d&groupId=d4c2a937-f097-435a-bc91-5c1683ca7245&parentMessageId=1605223771864&teamName=Approvals&channelName=Azure%20DevOps&createdTime=1605223780000",
	},
	ActivityType = "deploymentApprovalRequired",
	PreviewText = new ItemBody
	{
		Content = "New deployment requires your approval",
	},
	TemplateParameters = new List<KeyValuePair>
	{
		new KeyValuePair
		{
			Name = "deploymentId",
			Value = "6788662",
		},
	},
};
await graphClient.Users["{user-id}"].Teamwork.SendActivityNotification.PostAsync(requestBody);


```