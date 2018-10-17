---
title: Frequently asked questions| Groove Services
description: View answers to the most frequently asked questions about developing for the Grove API
keywords: groove music, groove api, groove faq
author: sakley
ms.assetid: efff8209-3f96-786d-0bec-bdd942294238
---

#FAQ
- [I'm developing a Universal Windows App, I created my app on Apps.dev.microsoft.com and registered it to the Groove API Program but I can't access the API. What am I doing wrong?](#1)
- [I have my application Client ID and Secret but the authentication fails. What am I doing wrong?](#2)
- [Can I use the same Client ID and Secret for more than one application?](#3)
- [How long does the API access token last? ](#4)
- [Should I actually keep the application Secret secret?](#6)
- [How can I link to Groove from my application or website?](#7)
- [Can I deep link to the native Groove app Windows, Windows Phone, and related platforms without going through a browser?](#8)
- [What is the revenue share of the affiliate program?](#10)
- [Can I become an affiliate without using the APIs? Can I use the API and not become an affiliate?](#11)
- [Can I put advertising in my application or website if I'm using the data from the API? Can I sell my application?](#12)
- [Can I cache the content retrieved from the API or save it locally?](#13)
- [I want to stream music, but I can't because I need to log in a Groove user. What should I do?](#14)
- [I want to access a Groove user's collection, but I can't because I need to log in a Groove user. What should I do?](#15)
- [I'm coding a game. Can I use the Groove API?](#16)
- [I keep receiving 4xx/5xx HTTP error codes in response to my requests to the API. What am I doing wrong?](#17)
- [May I download audio files with my application and provide a download feature to my application users?](#18)
- [Where did the Pilot program go?](#20)

### <a name="1"> </a>I'm developing a Universal Windows App, I created my app on Apps.dev.microsoft.com and registered it to the Groove API Program but I can't access the API. What am I doing wrong?
When developing a Windows UWA, you need to provision your application from Visual Studio first. Then the Application ID and secret will show up on your (Apps Registration Portal) [https://apps.dev.microsoft.com/#/appList] and you can use it for access to our API from your UWA app.

### <a name="2"> </a>I have my Application ID and Secret but the authentication fails. What am I doing wrong?  
Subscribe to the Groove API on the Developer Center [here](https://developer.microsoft.com/groove/signup).  
Also make sure that all parameter values in your authentication POST request are properly encoded.  

###<a name="3"> </a>Can I use the same Application ID and Secret for more than one application?
No, you should register an application in the Developer Center for every application or website that will use the Groove API. Every application should use its assigned Application ID and Secret. Also, make sure the details of your application are accurate.

###<a name="4"> </a>How long does the API access token last?
It lasts for 24 hours, so you will need to refresh it before it expires. This can be done asynchronously for better performance within your app or server-side code. The expiration time is given in the response along with the token.

### <a name="6"> </a>Should I actually keep the application Secret secret?
Yes, the Secret provided by the Applications portal should be kept secret. If you're running a website, the recommended implementation is to run the authentication code server side to prevent the secret from being visible in client-side code or on the network.

### <a name="7"> </a>How can I link to Groove from my application or website?
Most of the API calls return a "Link" item in the response. That Link is an HTTP link designed to automatically redirect to the most appropriate Groove application on the target platform. For example, if you're adding a link to a website, and the user is on a Windows 8 machine, the click from Internet Explorer will open the Groove Native application on Windows 10 (with a browser redirection).

### <a name="8"> </a>Can I deep link to the native Groove app Windows, Windows Phone, and related platforms without going through a browser?
No, you currently need to open a browser. See [examples](https://github.com/Microsoft/Groove-API-documentation/blob/master/Using-the-Groove-RESTful-Services/Deep-Link.md).

###<a name="10"> </a> What is the revenue share of the affiliate program?
Details of the affiliate program can be found [here](http://www.microsoftaffiliates.com/).

### <a name="11"> </a>Can I become an affiliate without using the APIs? Can I use the API and not become an affiliate?
Yes, the Groove API and affiliation are independent. The API is free to use for everyone, and gives you access to the features of Groove. There is no need to become an affiliate.  

If you'd like to earn revenue when linking to Groove from your application, then you should register with the Affiliate program.
More details are available [here](http://www.microsoftaffiliates.com/).  

You do not need to use the APIs to become a Microsoft affiliate.

### <a name="12"> </a>Can I put advertising in my application or website if I'm using the data from the API? Can I sell my application?
Please refer to [Guidelines].

###<a name="13"> </a>Can I cache the content retrieved from the API or save it locally?
Please refer to [Guidelines].

###<a name="14"> </a>I want to stream music, but I can't because I need to log in a Groove user. What should I do?
Some features of the APIs require that you authenticate a Groove user.
Please refer to the [User Authentication] documentation.

###<a name="15"> </a>I want to access a Groove user's collection, but I can't because I need to log in a Groove user. What should I do?
Some features of the APIs require that you authenticate a Groove user.
Please refer to the [User Authentication] documentation.

###<a name="16"> </a>I'm coding a game. Can I use the Groove API?
Please refer to [Guidelines].

### <a name="17"> </a>I keep receiving 4xx/5xx HTTP error codes in response to my requests to the API. What am I doing wrong?
Look at the response body. It often contains an [Error](Groove-service-REST-Reference/JSON-Error.md) object with a precise description of the error case.

### <a name="18"> </a>May I download audio files with my application and provide a download feature to my application users?
No, this is not allowed according to the TOUs of the APIs. The audio may be provided only in the form of streams. This applies to all of your users, even premium users.  

Please refer to [Guidelines].

###  <a name="20"> </a>Where did the Pilot program go?
There is no need for a Pilot program anymore. You can integrate Groove in your application without even notifying us!

[Guidelines]: Using-the-Groove-RESTful-Services/Guidelines.md
[User Authentication]: Using-the-Groove-RESTful-Services/User-Authentication.md
