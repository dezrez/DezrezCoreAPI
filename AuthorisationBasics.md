# Authentication and Authorisation Basics

One of the first problems that developers face is using OAuth2 with their application.  We've got a guide to help you with this, available here:
[Dezrez Core API Overview](https://dezrezservices-my.sharepoint.com/:w:/g/personal/matthew_dendle_dezrez_com/ETHBNmCxa1pNi0xOYBLRiJ8B5o_v__Wizn2m8RW6bdz2gA?e=IUZyO6)

## Once you've got your access token
### Protect it!
The access tokens you obtain should never be exposed to the public.  ESPECIALLY if your token is a back end token.  The reason being that if anyone were to intercept it, they would have full access to the agency's data via the API.

An example of bad token security:
A web development company wants to call the API directly from the client, using a single page app.  The web application itself calls the token endpoints to get a new token.  As the website is public, anyone can use the web app.  A hacker uses the web app, checks the network traces using debugging tools, and grabs the access token.
The hacker then proceeds to call the API directly, deleting applicants, property data and documents!
Please don't let this be you!

*KEEP THE ACCESS TOKEN SAFE*

If you are in any doubt as to the security of your application, please get in touch and we can discuss this with you.

### Understanding the different types of "OAuth2 Flow"
There are many different types of application; some with no UI (back end server apps), some that power a website (vendor login area etc.) and some that dezrez users log into directly (Mobile apps).  Depending on which application you are writing, upon registration you'll be set up with a different OAuth2 flow.

Flows are an OAuth2 concept, they are descriptions of the interactions between a client, a user and an authorization server to request access tokens.

Here are the OAuth 2 flows that we support, and who their uses:
End users, with a UI "User OAuth2 Flows":
* Code
* Implicit
* Resource Owner

Back end servers, web servers, with no users logging in "Userless OAuth2 Flows"
* Client
* Assertion

## User and Userless OAuth2 flows
There is an important distinction between these types of flow.  If you are using a "User OAuth2 Flow" to get your access token, when you call the API, you wont need to use an AgencyID url parameter - as we already know the agency that the user belongs to.

However, if your application uses one of the "Userless OAuth2 Flows", then you will need tell us which agencyId you are intending to call, by using the AgencyId parameter.

## Supplying branch context
In "User OAuth2 Flows", the users default branch is already known to us, as we just use the users home branch.  However, this is just a default setting; A user can perform actions in any branch - so if you need to change the branch that an action is performed under, just ad a BranchId URL parameter, with the ID of the branch you'd like to perform the action in.

