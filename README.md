# Dezrez Core API
## Who are we?
Dezrez is an independent software vendor based in Wales, UK.  We develop software for the property industry, and at the heart of all of our latest product offerings is the Dezrez Core API.

## What is the Dezrez Core API?
The Dezrez Core API is the backbone to all of our latest product offerings, and is a programmatic interface to all operations that can be performed across all of these products.

It is based on JSON, and is secured using OAuth2.

## What can I do with it?
People use our API primarily to deliver apps that deliver some value for Estate Agents, thier customers, or partners.

For example - many people use the API to deliver the very best online experiences for Vendors - allowing them to run thier own marketing, manage thier own viewings and even negotiate thier own sales.

We also have a basic integration option for websites, where we can supply a simple search function for getting Estate Agents properties on thier website.

If you want to get started, you just need to register your application with us, as below.
## Learning resources
To help you understand how to use our API, we have compiled several resources that aim to bring you up to speed on what you need to know, quickly.

### Before you call our API
[Authentication and Authorisation Basics - PLEASE READ](https://github.com/dezrez/DezrezCoreAPI/blob/master/AuthorisationBasics.md)

### API Environments
We have two environments for use by third parties - the first is the UAT environment, where clients are tested.  Then, there is our LIVE production environment.

Both of these environments have Swagger documents available, as well as having Swagger UI available.
However, you will not be able to make calls using Swagger UI on the production environment.

The URL for UAT is:
https://core-api-uat.dezrez.com/swagger/ui/index

And for LIVE:
https://api.dezrez.com/swagger/ui/index

NOTE: All Email and SMS communications instigated from the UAT environment are routed through to Dezrez internally for security reasons. Should this need to be changed for testing purposes, please submit a request through this GitHub site.

### Getting access to the Dezrez Core API - Registering your application
Please register by following this [guide](https://github.com/dezrez/DezrezCoreAPI/blob/master/HowToRegister.md#how-to-register-to-use-the-dezrez-core-api "Registering your application").

### An example request to the API
[Create a Group](https://github.com/dezrez/DezrezCoreAPI/blob/master/ExampleRequest.md) 

### Guide explaining some basic concepts of our data model:
[Dezrez Core Platform Domain Model](https://dezrezservices-my.sharepoint.com/personal/matthew_dendle_dezrez_com/_layouts/15/guestaccess.aspx?guestaccesstoken=wG26X6xJQpVALwVHGuzxMIvEDcpVUB%2fnOenxMxBrCxY%3d&docid=03c2d6f52b51747f4b7bd2562de2f2cec)

### Webhook functionality
The Dezrez Core API supports webhooks - a [brief guide](https://github.com/dezrez/DezrezCoreAPI/blob/master/webhooks.md) is available.

## Further Reading
To cover more advanced topics, please read these articles and white papers.

Also, feel free to check out our starter kits for web applications that call the Dezrez Core API.  They may be helpful if you plan to write an app for our API.  These starter kits are available as public repositories under our [Dezrez Organisation Page](https://github.com/dezrez)

### White Papers
We demonstrate some of the advantages of having an API through a series of white papers, available here:
[Dezrez Core API white papers](https://github.com/dezrez/DezrezCoreAPI/blob/master/WhitePapers.md)

### Authenticating third parties against people in dezrez
Please see this brief overview:

[Authenticating estate agent customers](https://github.com/dezrez/DezrezCoreAPI/blob/master/AuthenticatingThePublic.md)

