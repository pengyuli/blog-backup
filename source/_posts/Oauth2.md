---
title: Oauth2
date: 2020-09-12 11:40:59
categories: Network
tags: Oauth2
---
# Oauth2

## Roles 
* Resource Owner: User
* Client: Application The client is the application that wants to access the user’s account. Before it may do so, it must be authorized by the user, and the authorization must be validated by the API.
* Resource Server: hosts the protected user account informations
* Authorization Server: verifies the identity of the user then issues access tokens to the application.

Example: Resource Owner(me) want to login to RubyChina(client) use my github account(Resource and Authorization server)

## Protocol Flow
![Protocol flow](/images/Oauth2_flow.png)

## Application Registration
Before Application(client) want to use Oauth2, must register application with the service. This is done through a registration form in the “developer” or “API” portion of the service’s website, where you will provide the following information (and probably details about your application):

* Application Name
* Application Website
* Redirect URI or Callback URL

When App is registered, service will assign 

* Client ID 
* Client Secret

to Application.The Client ID is a publicly exposed string that is used by the service API to identify the application, and is also used to build authorization URLs that are presented to users. The Client Secret is used to authenticate the identity of the application to the service API when the application requests to access a user’s account, and must be kept private between the application and the API.

## Authorization Grant
In the Abstract Protocol Flow above, the first four steps cover obtaining an authorization grant and access token. The authorization grant type depends on the method used by the application to request authorization, and the grant types supported by the API. OAuth 2 defines four grant types, each of which is useful in different cases:

* Authorization Code: used with server-side Applications
* Implicit: used with Mobile Apps or Web Applications (applications that run on the user’s device)
* Resource Owner Password Credentials: used with trusted Applications, such as those owned by the service itself
* Client Credentials: used with Applications API access

More details about grant type can be find 
https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2#authorization-grant