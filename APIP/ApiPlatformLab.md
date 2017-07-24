Update: July 24, 2017

## 0.1 Introduction

This lab is an extension of the APAC Cloud Test Drive and is about  using API Platform Cloud Service

## 0.2 Objectives

As API Platform Admin / Manager
- Create a new API
- Connect the API to backend services
- Apply policies to API
- Deploy API to Gateway
- Publish API to Developer Portal for search, view, register and consume
- Approve Application Registration

As Application Developer
- Create Application and Generate Application key
- Search and View available API(s)
- Register application to consume API
- View application and API usage

## 0.3 Required Artifacts

- completed APAC Cloud Test Drive Microservice Lab - have the Offer API ready as backend service
- this lab requires an Oracle API Platform Cloud Service account that will either be applied by yourself or supplied by your instructor
- you will also need to use Postman to test the API

# 1. Create API in API Platform Cloud Service

## 1.1 Login to API Platform Cloud Service as API Administrator / Manager

- Use a Web Browser, navigate to API Platform, the URL of API Platform will be provided by your instructor    
  https://{apiplatorm-host-name}/apiplatform/

![](images/001.apipcs.png)

- Enter the credential provided by your instructor and click [**Sign In**] button. After login you will see the API Platform Cloud Service Landing page.

![](images/002.landing.png)

- Click [**Create API**] button and enter the following information   
**Name**: `Partner Offer API`  (if you are using SHARED environment, use `Partner Offer API XX`, where XX is your group number: 01-20)  
**Version**: `1`  
**Description**: `Offer API open to Partner`
- Click [**Create**] button

![](images/003.createapi.png)

- After you clicked the Create button, you will go back to the API main screen. You will now see the API just created. Next, click the API name you just created to EDIT the API.

![](images/004.created.png)

- This is API details you will see after clicking the API

![](images/005.apidetails.png)

- Hover the mouse pointer on [**API Request**], click [**Edit**]

![](images/006.apirequest.png)
