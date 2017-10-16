# ORACLE Cloud Test Drive #
-----
## 401: Create MBE (Mobile Back End) for mobile applications ##

### Introduction ###
This tutorial demonstrates how to create a MBE (Mobile Back End) to support the mobile applications. Mobile backends are server-side groupings of APIs (Platform & Custom APIs) and other resources that you create to support a specific set of applications.

![](../../common/images/mobile/long/mcsgs_dt_015_mobile_bkend.png)

### About the Exercise Today ###
In this exercise, you will create your MBE for a mobile application called "Cafe Supremo" to support APIs for loyalty management and mobile client. By doing this, Cafe Supremo mobile application interacts with the created MBE to get offer push, query offer details and accept or reject the offer.

### Prerequisites ###
- Oracle Public Cloud Service account for Mobile Cloud Service (Check with instructor if you don't have one)
- Please open a JSON file called "Mobile_App_Settings_Sample.json" using a text editor to replace some properties such as "baseUrl", "backendId" and "anonymousToken" in below step called "6. Check".

----

#### Create MBE (Mobile Back End) for Cafe Supremo application ####

1. Sign in to Mobile Cloud Service by provided **Mobile Cloud Service \(MCS\)** identity domain Id and credential in the Access Document. Using the dashboard open the Mobile Cloud Service Console.

2. In the dashboard screen, click on "Mobile Environment Service".

![](../../common/images/mobile/long/400-MobileEnvService.png)

3. In the service details screen, click on "Service Instance URL".

![](../../common/images/mobile/long/400-MCS_ServiceInstanceURL.png)

4. Click on the hamburger icon located at the left top corner of the service introduction page. From the navigation bar, select “Applications” -> “Mobile Backends” and click on the “+ New Mobile Backend” green button.

![](../../common/images/mobile/long/400-New_MBE.png)

5. Configure MBE with the following parameters:
+ **Name**: `LoyaltyMgmt_MBE0X` (0X is the sequence number assigned to you by instructor.)
+ **Description**: `LoyaltyMgmt_MBE0X` (Any value is okay.)

![](../../common/images/mobile/long/400-New_MBE_name_desc.png)

6. Check

The Mobile Backend is now created and it will bring you to the “Settings” tab of the newly created MBE where you will see the mobile backend ID, etc., which you will need to use when interacting with the MBE. Click on the two “Show” links to see the “Anonymous Key”.

![](../../common/images/mobile/long/400-MBE_settings.png)

Please open a JSON file called "Mobile_App_Settings_Sample.json" using a text editor. **Copy the values of "Mobile Backend ID", "Anonymous Key" and "Base URL", and replace values of properties like "backendId", "anonymousToken" and "baseUrl" in the JSON file with copied values respectively.** And save the JSON file for later use. You are going to use it in the "404: Set up Push Notification and Test Push Notification to mobile app" to create a QR code for the setting of Cafe Supremo mobile application.

```
{
      "baseUrl": "https://mcs-<YOUR_MCS_DOMAIN_NAME>.mobileenv.us2.oraclecloud.com:443",
            --> Replace the vaue inside double quotes with the value of "Base URL".
      "applicationKey": "9722de7f-4ecf-443f-8e0e-714b2f6e0f9c",
      "backendId": "2879cc11-97de-485a-bced-8476b91196f3",
            --> Replace the value inside double quotes with the value of "Mobile Backend ID".
      "anonymousToken": "R1NFMDAwMTE2NzhfTUNTX01PQklMRV9BTk9OWU1PVVNfQVBQSUQ6Smk3cXBld3lrczlfbmI=",
            --> Replace the value inside double quotes with the value of "Anonymous Key".
      "API":"LoyaltyManagementAPI",
      "senderID":"925757644219"
}

```


You have finished this lab section.

[Procced to Next - 402: Create Connectors for external services](402-MobileLab.md)

or

[Back to Mobile Serivce and Application Home](README.md)
