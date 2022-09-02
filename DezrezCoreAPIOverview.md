# Dezrez Core API Overview - Developers Guide
This document is aimed at familiarizing a developer with the dezrez Core API

# Introduction to the Dezrez Core API
## Audience
This document’s intended audience have a development background, and are interested in working with the dezrez Core API.

This document’s function is to familiarise the reader with resources to learn about the API functions, and to guide developers through the process of authentication and authorisation of their systems to the core API.
## The Core API
The Core API (a.k.a Dezrez Core Platform) is the platform on which rezi is built.  

Rezi is a single page application (SPA) that uses the Core API to perform functions.  All functions in the Rezi SPA are fulfilled via the API, and as such **you can do anything the rezi SPA can do, using the API.**
## Development Environments - UAT and Live
At dezrez, we maintain several development environments that are isolated from one another.

As an external developer, you can request access to the UAT (User acceptance testing) and LIVE (Production) environments.

Note: UAT normally has features that are yet to make it to the LIVE environment.
## Things you need to know before using the API
- It’s based on **JSON**
- It’s secured using **OAuth2**
- It’s **versioned** based on request header values

By far, the most issues that developers have with the API is adopting OAuth2, and this document aims to help you use the API by explaining in detail how to work with OAuth2.
### Already familiar with OAuth2?
If you are already familiar with OAuth2, here’s what you need to know to get started straight away:

- To register your client with us, email <developer.registration@dezrez.com> with the following information:
  - Company Name (if any)
  - Project Name and Description
    - This is just to give us an idea of what access scopes to grant you
  - Environment (UAT/LIVE)
- OAuth2 Authorisation endpoint:
  - UAT: <https://dezrez-core-auth-uat.dezrez.com/Dezrez.Core.Api/oauth/authorize/>
  - LIVE: <https://auth.dezrez.com/Dezrez.Core.Api/oauth/authorize/>
- OAuth2 Token Endpoint:
  - UAT: <https://dezrez-core-auth-uat.dezrez.com/Dezrez.Core.Api/oauth/token/>
  - LIVE: <https://auth.dezrez.com/Dezrez.Core.Api/oauth/token/>
- API Surface documentation:
  - <https://api.dezrez.com/help>.
  - <https://api.dezrez.com/swagger>
- Every request must specify the API version that is being targeted using a request header
  - Rezi-Api-Version: 1.0
# OAuth2 implementation in detail
All requests to the Dezrez Core API (apart from OPTIONS CORS pre-flight requests) that are made to the Core API must contain an Authorization header, using the bearer scheme, containing a string called a JSON Web Token (JWT).

This JWT header value is obtained using a standard called OAuth2, detailed below.
## OAuth2 Spec
For extremely detailed information on OAuth2, you can visit the OAuth2 spec at the following location

<http://tools.ietf.org/html/rfc6749>
## OAuth2 Vocabulary
Here are some terms that are important in the realm of OAuth2, Authorisation and Authentication.  Defining them here will help you fully understand this area.

- **Client**
  - The system or app that customers will be using. 
  - Any system/app that makes calls to the core API on the users behalf
- **Consent**
  - The act of a user granting a system/app access to the core API on their behalf
- **Consent Screen**
  - A UI that the **Authorisation Server** uses to ask the user if they want to grant specific permissions to the **Client**.  If the client is registered to support **Offline Access**, the user is also asked how long they would like to grant the client access.  This is used to set the lifetime of the issued **Refresh Token**.
- **Flow**
  - One of the OAuth2 mechanisms for performing the authentication
  - Most common are ‘implicit’ and ‘code’
  - Implicit favoured for embedded apps
  - Code favoured for web apps (as the actual access token isn’t ‘leaked’ to the user agent – I.e. it doesn’t appear in the URL bar, as it would with Implicit flow)
- **Application**
  - The Core API
  - Don’t confuse with a client
- **Access Token**
  - Used by clients to prove to the Application that they have been granted access to protected resources
  - In the case of the core API, this is a JWT token.
  - Limited lifetime (they expire)
  - Obtained from the Token Endpoint
- **Refresh token**
  - A longer-lived token (normally weeks, could be forever)
  - Used to get new Access Tokens when they expire
  - Exchanged with a new Access Token at the Token Endpoint
- **Authorisation endpoint**
  - The UI that captures the users credentials, and displays the consent screen.
- **Authorisation Server**
  - A server that controls Client access, the scopes which clients can request, and refresh tokens.
- **Identity Server**
  - An IdP
  - Also an STS
  - Where users credentials are stored
- **Offline Access**
  - This basically means that the client is given **Refresh Tokens** from the **Authorisation Server** during the authentication process.
- **Relying Party**
  - A service or app that relies upon an STS for authentication
- **IdP**
  - **Identity Provider**
  - E.g. Facebook, Google+, Twitter, Rezi Identity Server
- **STS**
  - **Security Token Service**
  - Any service which sends or receives tokens 
- **ClientID**
  - A unique identifier for a client – normally human readable (Dezrez.SPA)
- **ClientSecret**
  - A shared secret between the client and dezrez (Normally a base64 encoded byte array, generated by us)
- **Scope**
  - A string value indicating which rights your application would like to be granted by the user.
## Signing up with dezrez to use the API
Not just anyone can make requests on the API – the requesting party must be granted access as a **client application.**

- Register with dezrez (auth.dezrez.com)
  - Send an email to [developer.registration@dezrez.com](mailto:rezidev@dezrez.com) requesting that your client be registered for access.
  - Tell us what type of app it is
    - Web App?
    - Native mobile app?
    - (This will dictate which ‘OAuth2 Flow’ to use – implicit or code being the main choices)
  - Tell us what access rights you need
    - These aren’t enforced yet, but right now we can just use entity type (Events, People, property)
    - Do you want offline access?
      - This basically means that you get a **Refresh Token** from the **Authorisation Server** after authentication, which you can use to get new **Access Tokens** in the future.  The refresh token lifetime is usually much longer than the access token, up to a year in fact, but users can choose this in the **consent screen.** 
  - Tell us what redirect URLs that you want to use
    - We don’t send security tokens just anywhere; the client developer must tell us which URLs they want to redirect to
- Obtain ClientID and client secret from dezrez (we issue this after we register you)
## Obtaining an Access Token
Depending on which flow you use (in our case, Implicit Flow or Code Flow), you may need only to make one request, or two.
### Implicit Flow
Your app shows the Authorisation Endpoint UI in a web browser by constructing a URL with everything that is needed for the Authorisation Server to process the request.

The base of the URI is our Authorisation Servers **authorise endpoint.** Currently:

<https://auth.dezrez.com/Dezrez.Core.Api/oauth/authorize/> (LIVE)

<https://dezrez-core-auth-uat.dezrez.com/Dezrez.Core.Api/oauth/authorize/> (UAT)

The components of this URL are as follows:

- **client\_id**
  - The ID that the client was assigned by the dezrez registration process
- **scope**
  - A list of scopes that the client is asking for, separated by spaces
- **redirect\_uri**
  - The URL that the Authorisation Endpoint should redirect to
  - **Must be SSL! (start with https)**
  - Don’t forget to URL Encode it (after all, it is in a URL!)
- **response\_type**
  - **Token** for implicit flow
- **State**
  - A random string used to prevent certain attack vectors from faking requests

Example final URL:

<https://auth.dezrez.com/Dezrez.Core.Api/oauth/authorize/?client_id=SomeRegisteredClient&scope=property_read&redirect_uri=https%3A%2F%2Flocalhost%2F&response_type=token&state=435jk344g3467>

Once this URL is followed, and the user successfully logs in, and decides to grant your app the requests access (scopes), the redirect URL is followed, with extra parameters stuck on the end – one being the access\_token (the thing you need to call the core API), one being the refresh\_token, and another representing the expiry time of the issued token.
### Code Flow
To use Code Flow, everything is the same as the Implicit Flow, with three exceptions:

1. The response\_type is now **code** and not **token**.
1. Once the redirect\_uri is followed, you don’t get an **access\_token**, you get a **code**
1. Once you have the code, you need to exchange it for an **access\_token** at the token endpoint (Covered below - Exchanging a code for an access token)
### Client Flow
This flow involves the client authenticating as itself, and is only used in a small set of circumstances.

The Client flow involves making one call to the token endpoint as below:

POST https://dezrez-core-auth-uat.dezrez.com/Dezrez.Core.Api/oauth/token

Authorization: Basic <Base64 of clientId:ClientSecret>

Content-Type: application/json

{ grant\_type:'client\_credentials', scope:’impersonate\_web\_user’}

Tokens obtained in this fashion do not have an implicit link to a single agency ID.  For this reason, when calling the API with the resulting token, you **must** add and agencyId parameter to the URL in every request.
### Resource Owner Flow
The resource owner password credentials grant type is suitable in cases where the resource owner has a trust relationship with the client, such as the device operating system or a highly privileged application. The authorization server should take special care when enabling this grant type and only allow it when other flows are not viable.
###
This grant type is suitable for clients capable of obtaining the resource owner’s credentials (username and password, typically using an interactive form). It is also used to migrate existing clients using direct authentication schemes such as HTTP Basic or Digest authentication to OAuth by converting the stored credentials to an access token.

In order to obtain an access token when the username and password have been obtained, we need to send the raw credentials over to the token endpoint.  The client must authenticate this request by using HTTP Basic Auth, the ClientID being the username, and the client secret being the password.

The base URI of our Authorisation Servers token endpoint is currently: 

<https://auth.dezrez.com/Dezrez.Core.Api/oauth/token/> (LIVE)      

<https://dezrez-core-auth-uat.dezrez.com/Dezrez.Core.Api/oauth/token/> (UAT)      

- **grant\_type**
  - value muse be “password”
- **username**
  - The username value
- **password**
  - The password
- **scope**
  - A space separated list of scopes that the client is requesting.
### Checking the state
The redirect that was issued that contains the code, will also contain a state parameter.  Check to make sure that this is the same value you set state parameter that you send with your original request.
### Exchanging a code for an access token
Once you have the code, you need to call the token endpoint with a call that is made using HTTP basic auth, containing the code.  The username for basic auth is the ClientID, and the password is the Client Secret. 

The components of this URL are as follows:

- **grant\_type**
  - authorization\_code
- **code**
  - The authorization code received from the authorization server
- **redirect\_uri**
  - The URL that the Authorisation Endpoint should redirect to
  - **Must be SSL! (start with https)**
  - Don’t forget to URL Encode it (after all, it is in a URL!)
  - **Must match the redirect URI used in the initial request!**

The above data must be POSTed to the URL, using the “application/json” format, (If using JSON) or "application/x-www-form-urlencoded" format.

The response body will contain the access\_token, token\_type, expires\_in and a refresh\_token value (the refresh\_token value will only be included if your client has registered for them).
### Exchanging a refresh token for an access token
When your access token expires, you don’t want to have to force the user to log in again.  The access token lifetime is (at the time of writing) 2 hours, and it would be a pain if the user was kicked out every two hours.  So, this is where the **Refresh Token** comes in.

Provided that your client has been registered for **Offline Access**, your client would have been given a **Refresh Token** during the authentication process, and your client should have held onto it for future use.  You can use this refresh token to get a new access token, by POSTing to the token endpoint, as described below.

The base URI of our Authorisation Servers token endpoint is currently: 

<https://auth.dezrez.com/Dezrez.Core.Api/oauth/token/>

The components of this URL are as follows:

- **grant\_type**
  - must be **refresh\_token**
- **refresh\_token**
  - The refresh token as issued by the **Authorisation Server** during the authentication process

The above data must be POSTed to the URL, using the “application/json” format, (If using JSON) or "application/x-www-form-urlencoded" format.

HTTP Basic Auth must be used for all requests to this endpoint; the username is your client\_id, and the password is your client secret.  So, as per HTTP Basic Auth, you’d add a header called “Authorization” with a string value of “basic <*BASE64(CLIENT\_ID:CLIENT\_SECRET)*>.

Example: “Authorization: basic SW5zZXJ0WW91ckNsaWVudElkSGVyZTpJbnNlcnRDbGllbnRTZWNyZXRIZXJl “

The response body will contain the access\_token, token\_type, expires\_in and a refresh\_token value.
## Using the access\_token
You use the access token in every request to the dezrez core API.  You can authenticate requests by adding the access\_token value in an Authorization header, with the bearer scheme, as below

Authorization: bearer *ey054mhpo45jkvbij5pvy54m9b7yj6mbypio5v6yjkl54rjt6vy0n8954uyjpbi46jbyio5656bh56bh5v4h54v6j7mi67im6y*
## Scopes
This is a list of scopes that are currently in use in the dezrez core API.  Please note that these are correct at time of printing, but might be modified or extended subsequently.

**property\_read**

Access to read all information about a property or a property marketing role

**property\_write**

Access to update any aspect of a property or property marketing role

**people\_read**

Access to read full people information

**people\_basic\_read**

Access to read basic people information

**people\_write**

Access to write full people information

**event\_read**

Access to read full event information

**event\_write**

Access to write full event information

**property\_basic\_read**

Access to read basic property information

**impersonate\_user**

Access to fully impersonate the end user – reserved for applications for which we have full trust (internal)

**document\_read**

Access to read full document information

**document\_write**

Access to write full document information

**lead\_sender**

Access to send a lead into your system

**impersonate\_web\_user**

Impersonates the web user/system account

**impersonate\_any\_agency**

Impersonate any agency – reserved for applications for which we have full trust
