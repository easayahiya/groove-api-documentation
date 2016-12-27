---
title: Register for the Groove music service | Groove Services
description: Register your application with the Groove Music API to gain a authentication token, which is necessary for using all functions in the Groove API.
keywords: groove api, groove api developer, groove access token, groove developer registration
author: sakley
ms.assetid: eb59a521-e5de-6913-0b71-019c0cb94726
---

# Obtaining a Developer Access Token
Developer authentication is mandatory for all functions in the Groove API. All the functions share a common mandatory query parameter, accessToken, in which a valid authentication token must be passed.   

 [Dev Center Signin]: site-images/dev-center-signin.png
 [Dev Center Signin Account]: site-images/dev-center-signin-account.png
 [Groove Dev Center]: site-images/groove-dev-center.png
 [Groove signup]: site-images/groove-signup.png
 [Register your app]: site-images/register-your-app.png [SignIn]: https://i-msdn.sec.s-msft.com/dynimg/IC702605.png
 [Registration]: https://i-msdn.sec.s-msft.com/dynimg/IC702606.png
 [Accept ToU]: https://i-msdn.sec.s-msft.com/dynimg/IC702607.png
 [Login Azure]: https://i-msdn.sec.s-msft.com/dynimg/IC702608.png
 [my account]: https://i-msdn.sec.s-msft.com/dynimg/IC702611.png
 [Registered applications]: https://i-msdn.sec.s-msft.com/dynimg/IC702609.png
 [Register your app]: https://i-msdn.sec.s-msft.com/dynimg/IC702612.png
 [Registeredapp2]: https://i-msdn.sec.s-msft.com/dynimg/IC702613.png  
 [SignUp]: https://i-msdn.sec.s-msft.com/dynimg/IC702614.png

+ [Authentication token](#authentication-token)
+ [Using valid tokens from Azure Marketplace](#using-valid-tokens-from-azure-marketplace)
+ [Create a developer account on Azure Marketplace](#create-a-developer-account-on-azure-marketplace)
+ [Register your application with Azure Marketplace](#register)
+ [Sign up](#sign-up)
+ [Make an HTTP POST request to the token service](#httppost)
+ [Using the access token](#accesstoken)
+ [Protecting the client's secret value](#protectclient)
+ [Calling the Groove Music API with the token](#callapi)
+ [Renewing the token before it expires](#renew)
+ [Sample code](#sample-code)

## Authentication token
There are two distinct use cases depending on the API you are using. If your API calls are user authenticated, follow instructions on
[Groove User Authentication](User-Authentication.md).

The authentication token is based on the Simple Web Token (SWT) format. It contains a list of name-value claims that identify the client application and validity period of the token; it also contains a signature to prevent malicious users from modifying the contents of the token. For more information about SWT, see Simple Web Token on MSDN.  

This authentication token is obtained from the Live authentication endpoint, and it should be considered opaque and be passed as-is in requests to the Groove Service; the only change necessary is to prefix the token with "Bearer", a standard prefix for OAuth tokens.   

The tokens have a validity period of 24 hours, and there is a mechanism for renewing tokens described in Renewing the token before it expires, later in this topic.   

## Using valid tokens 
In order to be able to use the Groove Music API, a third-party developer must first create a developer account on [Microsoft Developer Center](https://developer.microsoft.com/groove)  and then sign up to the Groove Music API program (for free).   

Once properly subscribed, the third-party app should obtain authentication tokens from the Live service by using the procedure in this section; the scope to use is ``` app.music.xboxlive.com``` . The tokens have a validity   
period of 24 hours and must be renewed after they expire—or ideally, before they expire.   

You must obtain an access token to use the Groove Music API. The access token is passed with each API call and is used to authenticate your access to the Groove Music API. It provides a secure access to the Groove Music API and allows the API to associate your application's requests to the Groove Service with your account on the Developer Center.   

Microsoft provides methods to obtain access tokens safely, repeatedly, and easily. To obtain an access token, complete the steps in the following procedure; each step links to a subsection in this topic that describes the step in more detail.


## Create a developer account on Microsoft Developer Center
Subscribe to the Groove Music API on Microsoft Developer Center. Subscriptions are free.  

### To subscribe to the Groove Music API  
1. Visit <https://developer.microsoft.com/groove>. 
2. Click **Sign In** in the upper right corner.   
 ![SignIn]

3. Register with the Microsoft account of your choice.  
If you don't have a Microsoft Account, you'll need to create a new one.  
 ![Registration]  
3. On <https://developer.microsoft.com/groove>, click the **Sign up** link ![Groove Dev Center] or visit <https://developer.microsoft.com/dashboard/groove>.

4. Fill in the correct details about you carefully - we'll need your valid email address to contact you. ![Groove signup] 

5. Read the [Terms Of Use](groove-api-terms-of-use.md) and accept them. Then click on **Subscribe to Groove Music API Program**.


You are now a member of the Groove Music API Program!

You will now need to associate Applications to your account.

<a name="register">
## Register your application for the Groove Music API.
</a>
After subscribing to the Groove Music API, you must associate your application to your program.

### Create an application 

To register your app to connect with Groove, you'll need a Microsoft account.

1. Go to the [Microsoft Application Registration Portal](https://account.live.com/developers/applications)
2. When prompted, sign in with your Microsoft account credentials.
3. Find My applications and click Add an app.
4. Enter your app's name and click Create application.
5. Scroll to the bottom of the page and check the Live SDK support box.

After you've completed these steps, an application ID and application secret are created for your app and displayed on your new app's properties page.

**Important** Treat the value of client secret the same as you would a user's password. The secret represents the key to your application and, if made available, can be used to impersonate your application.

Under the Platforms header, configure details about your app. By default a new app is created as a web app and needs one or more redirect URIs. To enable native client flows for your app as well, click the Add Platform button and choose Mobile.

### Allow this application to access Groove Music API

1. When signed-in to the developer center, on <https://developer.microsoft.com/groove>, click the **Sign up** link or visit <https://developer.microsoft.com/dashboard/groove>.
2. Follow the instructions on the page. You'll need to obtain an authentication token [see also below](#httppost) ![Register your app]
3. Enter the obtained authentication token in the field and click on Register.
**TODO: include sample**
4. You can register up to **xx** apps. You can manage them on this page. 
**TODO: include screenshot with dashboard rempli**


<a name="httppost">
## Make an HTTP POST request to the token service  
</a>
In order to register your application or afterwards to call our unauthenticated API, make a POST request to the token service to obtain the access token. The parameters for the token request are URL-encoded and passed in the HTTP request body. Table 1 lists the mandatory input parameters and their descriptions.   

**Table 1. Token request input parameters**  

| Parameter name  | Value  | Description                                                                              |
|:---------------|:------|:----------------------------------------------------------------------------------------|
| *grant_type*    | string | Use "client" as value for application token authentication. |
| *client_id*     | string | Your Application ID as displayed on your application page on the [Microsoft Application Registration Portal](https://account.live.com/developers/applications) |
| *client_secret* | string | Your Application Secret as displayed on your application page on the [Microsoft Application Registration Portal](https://account.live.com/developers/applications). The value needs to be URL encoded. |
| *scope*         | string | The scope your application requires. For application access to the Groove API the scope is "app.music.xboxlive.com" |

The response for the token request contains the access token that you can use to access the Groove Music API. The response is JSON-encoded and includes the output properties shown in Table 2.   

**Table 2. Token request output properties**  

|Property|Description|
|:------|:------|
|accessToken|The access token that you can use to authenticate you access to the Groove Music API.|
|token_type|The type of the token.|
|expires_in|The number of seconds for which the access token is valid.|


<a name="accesstoken">
## Using the access token
</a>
As mentioned earlier in this topic, you must obtain an access token to use the Groove Music API. To use authenticated API, please refer to the [dedicated page](user-authentication.md).
The access token is secure, OAuth standard compliant, and flexible. The value of access token can be used for subsequent calls to the Groove Music API. The access token expires after 24 hours.  

It is always better to check elapsed time between the time at which the token was issued and the current time. If the elapsed time exceeds 24 hours, renew the access token by following the procedure for obtaining the access token.  

Remember the following points about using the access token:   

+ Either pass the 24 hours token you obtain as the parameter accessToken, or use the value of the accessToken property as the Authorization header to the calls to the Groove Music API. In either case, use the prefix "Bearer ".
+ The access token is valid for 24 hours. If the access token expires, you need to generate a new access token. The sample code in C#, linked at the end of this topic , can generate a new access token prior to exceeding the 24 hours period.

<a name="protectclient">
## Protecting the client's secret value
</a>
The tokens are obtained from Azure Marketplace in exchange for a client ID and secret value, obtained during the subscription. If possible, these should be secured and used in such a way that cannot be intercepted on the client machine.  

If the application has a server component, then the server should be responsible for storing the client ID and secret value, and the server should obtain the tokens on behalf of the client component so that the secret value cannot be intercepted on the client machines.

<a name="callapi">
## Calling the Groove Music API with the token
</a>
Once it is in possession of a valid authentication token, a third-party application may call the Groove Music API and provide the OAuth token in one of the following two ways:  

+ As the value of the URI query parameter, accessToken; be sure to encode the token for incorporation into a URL.
+ As the value of the **Authorization** HTTP header; however, we discourage the use of the **Authorization** header for developer authentication in favor of the query parameter instead, because the **Authorization** header will be used for user authentication in the functions that require it.  

  >**Note**
The standard OAuth prefix "Bearer " must be prepended to the contents of the actual retrieved token.  

**TODO: Update? **
<a name="renew">
## Renewing the token before it expires
</a>
Because the access tokens are only valid for 24 hours, they must be refreshed by sending a second request to the Live service (located at <https://login.live.com/accesstoken.srf>). We recommended that your code refresh them proactively before the end of the period in order to avoid having a period of time when the Groove Service can't be used.  

This 24 hours duration may change in the future. You should not hardcode it, but rather rely on the validity duration returned in the response by Azure Datamarket along with the access token.  

## Sample code
+  [Getting Started with the Groove SDK](../getting-started.md)

**TODO: Update Groove SDK**