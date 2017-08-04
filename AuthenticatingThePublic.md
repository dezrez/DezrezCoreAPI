# Authenticating end users
There are many use cases in which an estate agent will want to authenticate thier customers.  The primary example is where the website delivers additional features for vendors and applicants; the vendor or applicant will need to log in somehow, in order to prove they are who they say they are, and to show them thier related properties.

In both the examples below, the client (in this case, the website) is asserting the identity of the user, not dezrez/core API.  The website makes an assertion that because the user has access to the email address, the user owns that email address; and that if the user owns that email address, they must be the person in the core API that is registered with that email address.  These assertions have risk, and these risks should be fully understood before considering using email addresses in this way.

Below is a brief overview to how a website/server process can authenticate using a third party user system, either managed direct locally, or managed by a third party such as facebook:

| **SELF-MANAGED MANAGE USER ACCOUNTS** | **THIRD PARTY MANAGED USER ACCOUNTS**                          |
|----------------------------------------|----------------------------------------------------------------|
| User  logs in                          | USER LOGS INTO SITE  VIA FACEBOOK                              |
| site confirms email                    | SITE CALLS API TO CHECK IF ANY USER HAS THIS FACEBOOK IDENTITY |
| site calls findusersbyemail            | NO MATCH                                                       |
| SITE PICKS BEST MATCH                  | SITE CALLS FINDUSERSBYEMAIL \*using email provided by facebook |
| SITE SETS IDENTITY                     | SITE PICKS BEST MATCH                                          |
|                                        | SITE SETS USER IDENTITY                                        |
| SITE ASSERTS WHO PERSON IS           | SITE ASSERTS WHO PERSON IS                                   |

Endpoint locations

Find users by email:

<https://core-api-dev.dezrez.com/Help/Api/GET-api-people-findbyemail_emailAddress>

Find person by identity:

<https://core-api-dev.dezrez.com/Help/Api/GET-api-people-findbyidentity_issuer_nameidentifier>

Add identity to person:

<https://core-api-dev.dezrez.com/Help/Api/POST-api-identity-Add_personId>
