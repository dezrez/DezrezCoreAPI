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
There is an important distinction between these types of flow.
