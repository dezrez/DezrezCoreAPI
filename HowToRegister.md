#How to register to use the Dezrez Core API

In order to use the Dezrez core API, you need to first register with us so that you can have access codes sent to you.
Send an email to developer.registration@dezrez.com requesting that your client be registered for access, and tell us a bit about it.

##Information we need for your registration

###Tell us what type of app it is

Web App? Native mobile app? Back end server app?

This will dictate which ‘OAuth2 Flow’ to use – implicit, code or client being the main choices.

If dezrez users will log into your app/system, its going to be 'Code' or 'Implicit'. If you want to have your back-end servers talking to our API, its most likely 'Client' that you'll need.

If you are using a Web App, you have to make sure you do not leak the security token to the end user, as this could pose a security risk.

###What access rights will your app need?

We can help answer this question, but what we need to know is what types of things in the API will you interact with, and how you will interact with them. E.g. Update properties, read people data, book appointments etc.

###Do you want offline access?

This basically means that you get a Refresh Token from the Authorisation Server after authentication, which you can use to get new Access Tokens in the future. The refresh token lifetime is usually much longer than the access token, up to a year in fact, but users can choose this in the consent screen.

Tell us what redirect URLs that you want to use

We don’t send security tokens just anywhere; the client developer must tell us which URLs they want to redirect to.
