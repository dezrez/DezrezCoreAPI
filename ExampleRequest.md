#Making a Request to the API

Here is an example request to the API, which creates a new group.

POST https://core-api-uat.dezrez.com/api/group/addgroup?agencyId=4&branchId=31901

Content-Type: application/json
Rezi-Api-Version: 1

Authorization: Bearer ejY345-09830948v10458vc901348n5c093248n5vc092348n5.3245c3245c8n0234.2345c2345c3...

{
    "Name":"Mr and Mrs Dendle",
    "Members":[
        {
        "Person":
        {
            "Gender":{"SystemName":"Male"},
            "Title":"Mr",
            "FirstName":"Matthew",
            "LastName":"Dendle",
            "ContactItems":[
                {
                    "Type":{"SystemName":"Email"},
                    "Value":"matthewDOTdendle@dezrez.com",
                    "Notes":"Added via postman"
                }
                ]
        },
        "RelationshipType":{"SystemName":"PrimaryGroupMember"}
    }],
    "GroupType":{"SystemName" : "Individual"}
}
