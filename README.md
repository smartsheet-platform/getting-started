# Introduction
The [Smartsheet](https://www.smartsheet.com/) REST API allows you to programmatically access and manage your organization's Smartsheet data and account information. 

You call the API using standard HTTP commands (GET, POST, PUT, and DELETE) and all data is passed in JSON format.

The REST URL structure follows typical resource-oriented conventions. For example, to get a list of sheets, use:

 `GET https://api.smartsheet.com/2.0/sheets`
 
 This will return a list of Sheet objects, where each Sheet will have an “id” attribute. To get details on the sheet with id 123456, use:
 
 `GET https://api.smartsheet.com/2.0/sheets/123456`

 If you don't want to make raw HTTP calls, we also have SDKs which provide a higher level interface for [C#](https://github.com/smartsheet-platform/smartsheet-csharp-sdk), [Java](https://github.com/smartsheet-platform/smartsheet-java-sdk), [Python](https://github.com/smartsheet-platform/smartsheet-python-sdk) and [Node.js](https://github.com/smartsheet-platform/smartsheet-javascript-sdk) code. However, it is still helpful to understand the underlying messages.
  
# Getting started
To use the Smartsheet API, you should be familiar with the [Smartsheet product](https://www.smartsheet.com/) and have a basic understanding of programming concepts.

## Authentication and authorization
The Smartsheet API uses OAuth 2.0 for Authentication and Authorization. An HTTP header containing an Access Token is required to authenticate each request. 

If you want to get started quickly, or are developing a standalone application that can run with your credentials, you can generate an Access Token through the UI.
Open the Account/Personal Settings form and select the "API Access" tab. Click the "Generate new access token" button to obtain an access token.

If your application requires users to be able to login with their own account, you will need to implement the full OAuth flow. See the documentation for [Third party apps](http://smartsheet-platform.github.io/api-docs/#third-party-app-development) and [Developer Registration](https://www.smartsheet.com/developers/register).

The access token must be sent with every API call in an HTTP authorization header.

## Making your first API call
Before you write any code, try executing API requests using a tool like [cURL](https://curl.haxx.se/) or [Postman](https://www.getpostman.com/). By taking your code out of the equation, you can isolate troubleshooting to the raw Request and Response.

You will need your access token from the instructions above. In the examples below, replace "MY_ACCESS_TOKEN" with your actual token value.

To get a list of all your sheets, try the following command:

`curl -X GET -H "Authorization: Bearer MY_ACCESS_TOKEN" "https://api.smartsheet.com/2.0/sheets"`

In Postman, it would look like this:

![Postman screen shot](https://raw.githubusercontent.com/smartsheet-platform/getting-started/master/assets/postman-sample.png?token=AFTWAEH4a4ccHGAJXdh-mIMQRf-3f9iBks5Y0YeHwA%3D%3D)

The result should look something like this (after formatting):
```json
{
    "pageNumber": 1,
    "pageSize": 100,
    "totalPages": 1,
    "totalCount": 2,
    "data": [{
            "id": 6141831453927300,
            "name": "My first sheet",
            "accessLevel": "ADMIN",
            "permalink": "https://app.smartsheet.com/b/home?lx=8enlO7GkdYSz-cHHVus33A",
            "createdAt": "2016-01-28T22:02:35Z",
            "modifiedAt": "2016-08-09T17:50:06Z"
        },
        {
            "id": 6141831453927300,
            "name": "Sheet shared to me",
            "accessLevel": "VIEWER",
            "permalink": "https://app.smartsheet.com/b/home?lx=8enlO7GkdYSz-cHHVus33A",
            "createdAt": "2016-01-28T22:02:35Z",
            "modifiedAt": "2016-08-09T17:50:06Z"
        }
    ]
}
```

# Documentation
Complete documentation of all objects, endpoints, and errors is here:
https://smartsheet-platform.github.io/api-docs/

# Samples and SDKs (language bindings)
We provide SDKs providing a higher level interface for the several languages.

|Language|SDK|Sample application|
|:---|:---|:---|
|C#|[smartsheet-csharp-sdk](https://github.com/smartsheet-platform/smartsheet-csharp-sdk)|[csharp-read-write-sheet](https://github.com/smartsheet-samples/csharp-read-write-sheet)|
|Java|[smartsheet-java-sdk](https://github.com/smartsheet-platform/smartsheet-java-sdk)|[java-read-write-sheet](https://github.com/smartsheet-samples/java-read-write-sheet)|
|Python|[smartsheet-python-sdk](https://github.com/smartsheet-platform/smartsheet-python-sdk)|[python-read-write-sheet](https://github.com/smartsheet-samples/python-read-write-sheet)|
|Node.js|[smartsheet-javascript-sdk](https://github.com/smartsheet-platform/smartsheet-javascript-sdk)|(Coming soon)|


# Support
Questions, problems - please post on [StackOverflow](https://stackoverflow.com/questions/tagged/smartsheet-api) using the "smartsheet-api" tag. Or contact us directly with questions or any other feedback at api@smartsheet.com. 

If you find errors or have suggestions for this document, please [file an issue](https://github.com/smartsheet-platform/getting-started/issues/new) or submit a PR.

## API FAQ
* __Is there a fee to use the API?__

    No. The use of the API is free to all Smartsheet customers, regardless of plan, and third party application developers.

* __How do I access the API?__

    If you are a Smartsheet customer, you can use the API to directly access your data and integrate your Smartsheet account with other systems or applications. Simply go to your Personal Settings > API Access to generate an access token.

    If you are an application developer, we are committed to making it easy to build on top of Smartsheet - whether you are developing a solution for your organization or creating an app for the Smartsheet customer community at large. Use standard OAuth2 authentication and authorization to safely access Smartsheet data on behalf of your users without requesting or storing their usernames or passwords. To get the ball rolling, sign up for a [Smartsheet developer account](https://www.smartsheet.com/developers/register) and register your app to get and app key and secret.

* __Can I use the API to transfer data between Smartsheet and XYZ (another service or product)?__

    The Smartsheet API provides a way to programmatically access and manage your Smartsheet data.  In order to transfer data between Smartsheet and another service, please first make sure that the other service also provides a way to access and manage its data, via an API or another method - if it does, an integration is likely possible.  Please keep in mind, however, in order to create an integration you will need the help of a software developer who is familiar with the standards underlying the Smartsheet API (REST, JSON, etc.).

* __Where can I find examples of code interacting with the API?__

    For every API method listed in our [API documentation](http://smartsheet-platform.github.io/api-docs/) we provide example requests in multiple languages and an example (JSON) response.  

    Complete sample applications are available in these Github collections: [smartsheet-samples](https://github.com/smartsheet-samples) and [smartsheet-platform](https://github.com/smartsheet-platform).

* __How can my program know when data in Smartsheet has changed?__

    [Webhooks](http://smartsheet-platform.github.io/api-docs/#webhooks) provide a mechanism for Smartsheet to notify your application when sheet data changes. They provide a more efficient alternative to polling.

* __How do I get support?__

    If you build on our API, we will do our best to support you and quickly respond to all your questions. We would also love to hear your feedback, and promise to give it serious considerations. Questions, problems - please post on StackOverflow using the "smartsheet-api" tag. Or contact us directly with these or any other feedback at api@smartsheet.com. 
    
    For news and updates, please subscribe to developer updates [here](https://www.smartsheet.com/developers/register) and follow us on Twitter at @SmartsheetDev.

* __What are the legal terms and conditions of the Smartsheet Developer Program?__

    The Smartsheet developer program is governed by the [Smartsheet Developer Program Agreement](https://www.smartsheet.com/sites/default/files/SmartsheetDeveloperProgramAgreement20150630.pdf)
 
