# Dezrez Core API
##Who are we?
Dezrez is an independent software vendor based in Wales, UK.  We develop software for the property industry, and at the heart of all of our latest product offerings is the Dezrez Core API.

##What is the Dezrez Core API?
The Dezrez Core API is the backbone to all of our latest product offerings, and is a programmatic interface to all operations that can be performed across all of these products.

It is based on JSON, and is secured using OAuth2.

##What can I do with it?
People use our API primarily to deliver apps that deliver some value for Estate Agents, thier customers, or partners.

For example - many people use the API to deliver the very best online experiences for Vendors - allowing them to run thier own marketing, manage thier own viewings and even negotiate thier own sales.

We also have a basic integration option for websites, where we can supply a simple search function for getting Estate Agents properties on thier website.

If you want to get started, you just need to register your application with us, as below.

##Getting access to the Dezrez Core API - Registering your application
In order to use the Dezrez core API, you need to first register with us so that you can have access codes sent to you.

Send an email to developer.registration@dezrez.com requesting that your client be registered for access, and tell us a bit about it.

###Information we need for your registration

####Tell us what type of app it is
Web App? Native mobile app? Back end server app?

This will dictate which ‘OAuth2 Flow’ to use – implicit, code or client being the main choices.

If dezrez users will log into your app/system, its going to be 'Code' or 'Implicit'.
If you want to have your back-end servers talking to our API, its most likely 'Client' that you'll need.

If you are using a Web App, you have to make sure you do not leak the security token to the end user, as this could pose a security risk.

####What access rights will your app need? 
We can help answer this question, but what we need to know is what types of things in the API will you interact with, and how you will interact with them.  E.g. Update properties, read people data, book appointments etc.

####Do you want offline access?

This basically means that you get a Refresh Token from the Authorisation Server after authentication, which you can use to get new Access Tokens in the future. The refresh token lifetime is usually much longer than the access token, up to a year in fact, but users can choose this in the consent screen.

####Tell us what redirect URLs that you want to use
We don’t send security tokens just anywhere; the client developer must tell us which URLs they want to redirect to.

##API Environments
We have two environments for use by third parties - the first is the UAT environment, where clients are tested.  Then, there is our LIVE production environment.

Both of these environments have Swagger documents available, as well as having Swagger UI available.
However, you will not be able to make calls using Swagger UI on the production environment.

The URL for UAT is:
https://core-api-uat.dezrez.com/swagger/ui/index

And for LIVE:
https://api.dezrez.com/swagger/ui/index

NOTE: All Email and SMS communications instigated from the UAT environment are routed through to Dezrez internally for security reasons. Should this need to be changed for testing purposes, please submit a request through this GitHub site.

##White Papers
We demonstrate some of the advantages of having an API through a series of white papers, available here:
[Dezrez Core API white papers](https://github.com/dezrez/DezrezCoreAPI/blob/master/WhitePapers.md)

##Learning resources
To help you understand how to use our API, we have compiled several resources that aim to bring you up to speed on what you need to know, quickly.

###The Dezrez Core Platform Domain Model
[Dezrez Core Platform Domain Model](https://dezrezservices-my.sharepoint.com/personal/matthew_dendle_dezrez_com/_layouts/15/guestaccess.aspx?guestaccesstoken=wG26X6xJQpVALwVHGuzxMIvEDcpVUB%2fnOenxMxBrCxY%3d&docid=03c2d6f52b51747f4b7bd2562de2f2cec)

###Dezrez Core API Overview (also covers authentication)
[Dezrez Core API Overview](https://dezrezservices-my.sharepoint.com/personal/matthew_dendle_dezrez_com/_layouts/15/guestaccess.aspx?guestaccesstoken=lwhdlgb3j7Y91GmaXpXjrX6cSn5iLZfzrPPtrReNinA%3d&docid=06036c1316bb14d5a8b4c4e6012d1889f)

###Authenticating third parties against people in dezrez###
Please see this brief overview:

[Authenticating estate agent customers](https://github.com/dezrez/DezrezCoreAPI/blob/master/AuthenticatingThePublic.md)

