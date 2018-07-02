# Webhooks API

## Overview
The Dezrez Core API has built-in webhooks available for a wide range of events that happen in the system.

Each of these events has a specific data contract associated with them, and API clients can register webhooks in order to be notified when these events happen.

When an event happens, the specific trigger data contract is sent to the URL specified in the webhoook, in real time.

** web hooks need to be explicilty enabled by dezrez staff before they can be used.  If this is not done, you will get an error message stating that they need to be enabled **

Dezrez staff need to enable the webhooks 'external provider' in order for them to work.

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
**NOTE - The response will contain a location header that will be used later for deleting the webhook.**

### Deleting webhooks
Webhooks can be deleted by a DELETE call to the location specified in the location header of the webhook create call above.
Example:
**DELETE https://api.dezrez.com/api/webhook/1234**

### Trigger Hierarchy
Triggers have a built-in hierarchy; for example, a PropertyMarketingRoleChanged trigger encompasses all triggers that more specifically describe a change to a property marketing role, I.e.  
PropertyRoleDescriptionChangedSubscriptionNotificationDataContract is a sub trigger of PropertyRoleChangedSubscriptionNotification.

This is helpful if you want to send everything to do with a property changing, but dont want to specify all the trigger names in the MessageTypes parameter.
