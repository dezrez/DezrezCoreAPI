#Authentication and Authorisation Basics

One of the first problems that developers face is using OAuth2 with thier application.

There are many different types of application; some with no UI (back end server apps), some that power a website (vendor login area etc.) and some that dezrez users log into directly (Mobile apps).  Depending on which application you are writing, upon registration you'll be set up with a different OAuth2 flow.

Flows are an OAuth2 concept, they are descriptions of the interactions between a client, a user and an authorization server to request access tokens.

Here are the OAuth 2 flows that we support, and who thier uses:
End users, with a UI "User OAuth2 Flows":
* Code
* Implicit
* Resource Owner

Back end servers, web servers, with no users logging in "Userless OAuth2 Flows"
* Client
* Assertion

##User and Userless OAuth2 flows
There is an important distinction between these types of flow.  If you are using a "User OAuth2 Flow" to get your access token, when you call the API, you wont need to use an AgencyID url parameter - as we already know the agency that the user belongs to.

However, if your application uses one of the "Userless OAuth2 Flows", then you will need tell us which agencyId you are intending to call, by using the AgencyId parameter.

##Supplying branch context
In "User OAuth2 Flows", the users default branch is already known to us, as we just use the users home branch.  However, this is just a default setting; A user can perform actions in any branch - so if you need to change the branch that an action is performed under, just ad a BranchId URL parameter, with the ID of the branch you'd like to perform the action in.

