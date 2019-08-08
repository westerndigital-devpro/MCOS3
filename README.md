[<](../README.md)
![MCHLOGO](./images/wd/WD_my_cloud_home_logo_long.jpg)  

# My Cloud Home / ibi&trade; GETTING STARTED
----
Welcome to the Western Digital SDK Readme for developers wishing to get up and running quickly building apps for the My Cloud Home and ibi&trade; devices. To simplify, we will refer to this platform as the MCH Platform.  MCH Platform supports two app types: Those that run on the device itself, or 'On Device', and those that remotely access the device, called 'Off Device' apps.

On Device Apps live on the device, call the API locally, and run in a Western Digital flavored Android stack.  Off Device apps can live on a mobile device, on a computer in the network, or cloud, and can communicate to the MCH/ibi device with an authentication certificate and REST based API calls.

You might develop Off Device apps using the REST API's, however if your app needs access to the core functions that Android provides, you will want to build an On Device app.  Also, if your app is not connecting to the cloud, you will need to build it On Device.

If you would like more information on developing applications for the MCH devices, please visit the Resources page on the website:

https://developer.westerndigital.com/develop/wd-my-cloud-home/discover/why-develop-for-my-cloud-home.html


## CONTENTS
1. [ARCHITECTURE](#architecture)
2. [REGISTER](#register)
3. [QUICK START](#quick-start)
4. [AUTHENTICATION](#authentication)

## OFF DEVICE CONTENTS
1. [OFF DEVICE OVERVIEW](#off-device-overview)
2. [OFF DEVICE CODE EXAMPLES](#off-device-code-examples)
3. [COMMAND LINE EXAMPLE](#command-line-example)
4. [PYTHON OFF and ON DEVICE EXAMPLES](#python-off-and-on-device-examples)
5. [POSTMAN OFF DEVICE EXAMPLES](#postman-off-device-examples)
6. [JAVASCRIPT OFF DEVICE EXAMPLES](#javascript-off-device-examples)
7. [iOS OFF DEVICE EXAMPLE](#ios-off-device-example)
8. [OFF DEVICE API](#off-device-api)
9. [GET SUPPORT](#get-support)
10. [SUBMIT OFF DEVICE APP](#submit-off-device-app)
11. [USEFUL TIPS](#useful-tips)

## ON DEVICE CONTENTS
1. [ON DEVICE OVERVIEW](#on-device-overview)
2. [GET ON DEVICE SDK](#get-on-device-sdk)
3. [REQUEST DEVICE](#obtain-hardware)
4. [GET SUPPORT](#get-support)
5. [SUBMIT ON DEVICE APP](#submit-off-device-app)
6. [ON DEVICE APP SHOWCASE](#off-device-app-showcase)
----

## ARCHITECTURE
If you haven't done so already, please take a look at the My Cloud Home (MCH) Architecture Diagram:

![arch](./images/wd/mch_architecture_0.png)


***My Cloud Home Device*** Refers to the physical My Cloud Home and or ibi hardware devices. This platform is refer to MCH.

***On Device Apps***
On Device apps live on the device it self, interface with a Device SDK and/or Android API's. See [ON DEVICE OVERVIEW](#on-device-overview) section below for more information. On-Device Apps refer to the apps that run on the MCH device. These applications are distributed through the App catalog of the Services menu in the MCH device mobile or MyCloud.com web app.

***Off-Device Apps***
Off-Device Apps refer to applications that are built by developers using MCH platform endpoints. Off Device apps connect via HTTPS and, once authenticated, can manipulate the MCH REST API. The apps use MCH APIs to access user’s content. Signup and registration are required to obtain app specific assigned authentication keys.

***Cloud Services***
MCH Services provide functionalities such as authentication, sharing, device lookup, and configuration. These can be used by applications to fetch token, share user data, get device information, and retrieve service endpoints.

[^](#contents)

## REGISTER

To get started, you need to decide which type of app you want to build.  In some cases, you may wish to build both types of apps so they can talk to each other. App development can begin without registration, however to publish your app you will be required to sign up and register.  

You may view and edit the SDK samples and view API's for each app flavor without signing up or registering your app, or buying a device. You can download or clone the SDK's, tools, code, API's and sample apps for each type following the instructions below.

Off Device developers can get started quickly by using a temporary trial Client_ID and Secret_ID (CSID).The temporary CSID cannot be used for more than 30 days.  

>***NOTE*** -  This temporary trial CSID is shared active for short internals of time, and changed regularly. It cannot be used as part of your released app and will be disabled without notice.

Off Device app Registration is required to obtain a Client_ID and Secret_ID assigned to your company's Off Device app. Signup is required to register.

To have your On Device app included in the MCH or ibi Catalog, signup, registration, validation and acceptance is also required. Check in advance by registering your On Device app, or reach out to obtain an understanding if your app has the opportunity to be included into the App Catalog for the targeted device(s).

If accepted, we will assist you in setting your MCH device to a development environment device.

The link to sign up is:

[Free Sign Up](https://account.wdc.com/devportal)

You will fill in User Information, Email, and Password, and agree to the WD Terms and Conditions and Privacy Policy.

The Western Digital system will Email a verification. The links to register your device are below:

- [Build OFF DEVICE APP](https://developer.westerndigital.com/develop/wd-my-cloud-home/forms/mchoff/register-app-new-mchoff.html)


- [Build ON DEVICE APP](https://developer.westerndigital.com/develop/wd-my-cloud-home/forms/mchon/register-app-new-mchon.html)

[^](#contents)

## QUICK START

Ready to get started with an Off Device app, link to the Off Device readme in the github [here](./MchOffDevice/README.md).

Follow the steps below to build an Off Device App for My Cloud Home.

The WD SDK provides sample code, steps required to register you as a developer, so you can publish your app.  We show how to perform app authentication using oAuth2.0, with example API prototypes, how get more Developer support, and finally how to submit your app to Western Digital for publishing when done.

[^](#contents)

## AUTHENTICATION
Understanding the different steps in the authorization flow to communicate with the My Cloud Home REST APIs using the proper credentials is key. Developers can get started quickly by using a temporary trial set of credentials, known as the Client_ID and Secret_ID (or 'CSID').

>***NOTE*** -  This temporary trial CSID is shared, and  active for short intervals of time, and changed regularly. It cannot be used as part of your released app and will be disabled without notice.

Registration is required to obtain a full production set of Client_ID and Secret_ID  credentials assigned to your company and Off Device app.

For detailed steps on performing Authentication, visit the authentication web page:

https://developer.westerndigital.com/develop/wd-my-cloud-home/discover/off-device-applications/authentication.html

[^](#contents)

----

# OFF DEVICE OVERVIEW

With Off Device app development, you may use an off-the-shelf My Cloud Home device. You should setup your My Cloud Home or ibi device drive on your local network by adding it to your router. My Cloud home using a CAT5 cable and ibi using WiFi. Follow the instructions in the My Cloud Home / ibi manual for setting up the device.  You need to setup a set of user credentials for this device:

>TIP: At the end of this procedure, you will be using two sets of credentials.  One for logging into the My Cloud Home connected to your local network, and one for the Developer account.  We suggest using different email addresses and credentials for these two accounts so that you may keep them apart.

### Five Step Development Scenario

1. Endpoint lookup
2. Get access token
3. Device Look up
4. Manage content
5. File sharing


## OFF DEVICE CODE EXAMPLES
The following Off Device examples and samples are all located in the [WD-DEVPRO Git Repo](https://github.com/westerndigital-devpro). These apps show how how to connect with and use the MCH API using popular languages. These are not intended to be full-blown apps, merely examples for you to get started.

See the basic info below for each of the sample apps, for more details, refer to the readme in each app repo branch.

>***NOTE*** - The code examples are not intended for production use, but only demonstrate some ways to use the API's

[^](#contents)

## COMMAND LINE EXAMPLE

The following Curl example is the best way to initially connect to your My Cloud Home device and ensure all the credentials are working before building an app, or for debugging.

### CURL AUTHENTICATION TO DEVICE
Open your favorite Terminal and run the following command:

```sh
curl -X POST   https://service.auth0.url/oauth/token   -H 'content-type: application/json'   -d '{
"grant_type": "http://service.auth0.url/oauth/grant-type/password-realm",
"username":"YOUR DEVELOPER EMAIL",
"password":"YOUR DEVELOPER PASSWORD",
"audience":"mycloud.com",
"realm": "Username-Password-Authentication",
"scope":"openid nas_read_only nas_read_write user_read user_write device_read auth_get_userinfo offline_access",
"client_id":"YOUR DEVELOPER SECRET KEY",
"client_secret":"YOUR DEVELOPER CLIENT SECRET"
}'
```
Be sure to include the closing apostrophe to execute the command.

#### CURL AUTHENTICATION RESPONSE
If you have correctly called the device with the proper credentials, you will receive a response similar to the below, with an Access token and Refresh token defined, as well as some profile settings..

```sh
{"access_token":"eyJ0eXAi....
....(a very long unique id string)...
...evnxg","scope":"openid profile email address phone nas_read_write nas_read_only user_read device_read auth_get_userinfo offline_access","expires_in":86400,"token_type":"Bearer"}

```

Once you have successfully communicated to the device, and receive a token set similar to the above, you can make subsequent API calls from your Off Device application.

You may also use the Curl method above for obtaining a Token set to make other API calls either from the command line, or from a tool like Postman.  See below for Postman examples and links to the API.

[^](#contents)

---


## PYTHON ON DEVICE EXAMPLES
>https://github.com/westerndigital-devpro/apidocs/tree/master/MchPlatform/MchOnDevice

This python app is a python script that shows how to:
 - Get auth0 information for a user
 - Get user information
 - Get device information
 - Access device associated with the user account
 - Create folder and files on the device
 - Search content and metadata of file on device
 - Delete file on device

## POSTMAN OFF DEVICE EXAMPLES
>https://github.com/westerndigital-devpro/apidocs/tree/master/MchPlatform/MchOffDevice/ibi-api-postman

This is a set of Postman collections that demonstrate how to talk to Off Device API's.

[See Postman README here](./MchOffDevice/ibi-api-postman/README.md)

[^](#contents)

## JAVASCRIPT OFF DEVICE EXAMPLES

>https://github.com/westerndigital-devpro/apidocs/tree/master/MchPlatform/MchOffDevice/JavascriptExample

This is a Javascript/React sample app that demonstrates how to talk to the Off Device API's, demonstratingLogin, Credentials, Get User Info, Get Device Info, File Search and Display Content in a web browser.

[See Javascript README here](./MchOffDevice/JavascriptExample/app/README.md)

## iOS OFF DEVICE EXAMPLE
>[./MchPlatform/MchOffDevice/IosExamples](./MchOffDevice/IosExample/README.md)

This is an iOS / Swift native sample app that demonstrates how to take media from the iPhone device and store on the My Cloud Home drive device using the Off Device API's.

[See iOS README here](./MchOffDevice/IosExample/README.md)

----

[^](#contents)

## OFF DEVICE API

>[OFF DEVICE API](https://developer.westerndigital.com/develop/wd-my-cloud-home/api.html)

>***NOTE*** - My Cloud server end points:
```

Auth URL: https://wdc.auth0.com
Cloud URL: https://device.mycloud.com

```

For more information on the Off Device API, refer to the the following resource:

>[API FEATURES](https://developer.westerndigital.com/develop/wd-my-cloud-home/discover/off-device-applications/api-features.html)

----
## GET SUPPORT

Send us a message if you need help or have questions.
>[GET SUPPORT](https://developer.westerndigital.com/develop/wd-my-cloud-home/forms/mchoff/support-mchoff.html)


## SUBMIT OFF DEVICE APP

Submit your app for us to qualify & publish in the App Catalog
>[PUBLISH APP](https://developer.westerndigital.com/develop/wd-my-cloud-home/forms/mchoff/submit-app-new-mchoff.html)


## USEFUL TIPS

See the Western Digital Resources page for additional tips and advanced information here:
https://developer.westerndigital.com/develop/wd-my-cloud-home/discover/on-device-applications/useful-tips.html

[^](#contents)

----

# ON DEVICE OVERVIEW

My Cloud On Device application development is described in detail:
https://developer.westerndigital.com/develop/wd-my-cloud-home/discover/on-device-applications/creating-on-device-apps.html.

The ibi&trade; On Device apps SDK and tools are by invitation only. If you feel your On Device app aligns to an ibi Photo / Video use case, please submit details of your On Device app in the 'Register your App' form.

For assistance in acquiring hardware for your project, go here:
https://developer.westerndigital.com/develop/wd-my-cloud-home/forms/mchon.html

>***GETTING STARTED*** - Follow the steps below to build and publish an On Device App for My Cloud Home

1. GET SDK
2. OBTAIN HARDWARE
3. DEVELOP APP - See Hello World Example
4. GET SUPPORT
5. SUBMIT APP

>***TIP*** - The following table provides information on the Android features that are not available on the My Cloud Home platform.

https://developer.westerndigital.com/develop/wd-my-cloud-home/discover/on-device-applications/regular-android-app-vs-device-app.html


## GET ON DEVICE SDK
Download SDK and start building your app:

[ON DEVICE SDK](https://developer.westerndigital.com/develop/wd/sdk.html)

## ON DEVICE EXAMPLES
You will first need a registered Developer Account, and follow the instructions above to download and install the Android Hello World Example, the First Device App Example and a step by step developer tutorial.

Android Hello World Example App, First Device App Example, step by step tutorial and README:

[ON DEVICE EXAMPLES](./MchOnDevice/README.md)

---

## OBTAIN HARDWARE
[Request](https://developer.westerndigital.com/develop/wd-my-cloud-home/forms/mchon/request-hardware-new-mchon.html) developer environment and possibly devices to use during your development activities.

### EXAMPLE APP and LOADING ON DEVICE APP
See the [Android On Device Example App developer Readme](./MchOnDevice/AndroidExamples/androidDev-Pro/README.md).

See the [Python Off Device tool](./MchOnDevice/PythonExamples/MchOnDeviceDemoTool) to learn how to load On Device Apps.


## GET SUPPORT
[Send](https://developer.westerndigital.com/develop/wd-my-cloud-home/forms/mchon/support-mchon.html) us a message if you need help or have questions.


## SUBMIT ON DEVICE APP
[Submit](https://developer.westerndigital.com/develop/wd-my-cloud-home/forms/mchon/submit-app-new-mchon.html) your app for us to qualify & publish in the App Catalog.


## ON DEVICE APP SHOWCASE
Check out apps built for My Cloud OS3 NAS devices: https://www.wd.com/solutions/my-cloud-apps.html

[^](#contents)

----

| Updated  |  Rev       |
|----------|-----------:|
|DA        |v07242019   |
