<!-- markdownlint-disable MD041 -->

```csharp
// GET https://graph.microsoft.com/v1.0/me/messages/{message-id}?$expand=attachments

string messageId = "AQMkAGUy...";
var message = await graphClient.Me.Messages[messageId]
    .GetAsync( requestConfig => requestConfig.QueryParameters.Select = new string[] { "attachments" });
```
