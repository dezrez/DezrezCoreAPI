# Webhooks API

## Overview
The Dezrez Core API has built-in webhooks available for a wide range of events that happen in the system.

Each of these events has a specific data contract associated with them, and API clients can register webhooks in order to be notified when these events happen.

When an event happens, the specific trigger data contract is sent to the URL specified in the webhoook, in real time.

### Webhook Triggers
A list of webhook triggers can be obtained by an authenticated API client by calling the endpoint *GET api/workflow/triggers*.

This will return a list of events that webhooks can be used with, along with the list of properties that the actual event data contract will contain.

Below is an example of one of the items in the list of triggers from the call to *GET api/workflow/triggers*:

```javascript
 {
        "TriggerSystemName": "PersonChangedSubscriptionNotification",
        "TriggerDescription": "This trigger occurs when anything regarding a person changes.",
        "TriggerProperties": [
            {
                "ContentPropertyName": "PersonId",
                "ContentPropertyDataType": "System.Int64",
                "IsPropertyFilter": true
            },
            {
                "ContentPropertyName": "RootEntityId",
                "ContentPropertyDataType": "System.Int64",
                "IsPropertyFilter": false
            },
            {
                "ContentPropertyName": "AgencyId",
                "ContentPropertyDataType": "System.Int64",
                "IsPropertyFilter": false
            },
            {
                "ContentPropertyName": "BranchId",
                "ContentPropertyDataType": "System.Int64",
                "IsPropertyFilter": false
            },
            {
                "ContentPropertyName": "Occurred",
                "ContentPropertyDataType": "System.DateTime",
                "IsPropertyFilter": false
            },
            {
                "ContentPropertyName": "ChangedByPersonId",
                "ContentPropertyDataType": "System.Int64",
                "IsPropertyFilter": false
            },
            {
                "ContentPropertyName": "ChangeType",
                "ContentPropertyDataType": "System.String",
                "IsPropertyFilter": false
            }
        ]
}
```
    
Remember - The above json simply *describes* the JSON that will be sent to you.  The *actual* json that will be sent to the webhook URL in the above case will be:
```javascript
{
  "PersonId": 1234,
  "RootEntityId": 1234,
  "AgencyId": 1234,
  "BranchId": 1234
  "Occurred":"2017-10-26T11:48:22.597Z"
  "ChangedByPersonId": 1234
  "ChangeType": "Updated"
}
```

### Creating a webhook
Webhooks can be created by POSTing to **api/webhook/create/<TriggerSystemName>**, and the body of the post contains the callback URL.
 
For example, to create a webhook that listens for changes to documents, calling back to [request bin](https://requestb.in) (really handy service for webhook testing!) here is the request to make (all headers including auth headers are ommited for brievity):
 
 **POST https://api.dezrez.com/api/webhook/create/DocumentChangedSubscriptionNotificationDataContract**
 ```javascript
 {
	"WebhookUrl":"https://requestb.in/p53z0up5"
}
 ```
