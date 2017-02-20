#How to insert leads via the Dezrez Core API

In order to use the leads functionality via the Dezrez core API, you need to first register with us so that you can have access codes sent to you.
For further information about the registration process, please see [How To Register](https://github.com/dezrez/DezrezCoreAPI/blob/master/HowToRegister.md)

##Some information to take into consideration
* Requests received must be in JSON format
* Dates must be formatted in accordance with the ISO 8601 standards.
* Only leads relating to a property can be submitted with the Rezi role id specified

##What is the URL end point we have to send data to?
* LIVE: https://api.dezrez.com/api/inboundlead/create
* TEST: https://core-api-uat.dezrez.com/api/inboundlead/create

##What types of lead requests can we submit?
Viewing -	"RequestType": {"SystemName": "Viewing"}  
Valuation - "RequestType": {"SystemName": "Valuation"}
Phone Call Back - "RequestType": {"SystemName": "PhoneCall"} 
Brochure Request - "RequestType": {"SystemName": "BrochureRequest"} 
General	"RequestType": {"SystemName": "General"}

##What does a sample call look like?
```json
{ 
  "People": [ 
    { 
      "Title": "Mr", 
      "FirstName": "Michael", 
      "LastName": "McElhatton" 
    } ], 
    "Email": "m.mcelhatton@ntlworld.com", 
    "DateSubmitted": "2016-08-02T12:13:42.727581Z", 
    "Address": "Ethos, Kings Road, Swansea", 
    "Postcode": "SA1 8AS", 
    "Country": "UK", 
    "PhonePrimary": "01478569321", 
    "PhoneMobile": "01478569321", 
    "DPAFlag": true, 
    "PropertyToSell": false, 
    "PropertyToRent": false, 
    "Comment": "Test comment", 
    "FinancialAdvice": false, 
    "PartExchange": false, 
    "SourceType": {"SystemName": "Rightmove"}, 
    "RequestType": {"SystemName": " BrochureRequest"}, 
    "PropertyMarketingRoleIds": [12345,67890]
}
```

##Once you have developed the specification please:
* Tell us when you are ready to test
* Request your Authorisation Access Token & source type ID/Name
* Provide us a suitable date you would like to start testing lead system
