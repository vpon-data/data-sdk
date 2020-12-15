---
layout: default
title:          "Outline"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /outline
lang:           "en"
---


# Data SDK

**Outline**
1. Introduction
2. Details of Collected Data
3. Data Privacy 
4. Partner Benefits (待Hood補充)
5. Required App User Permission
6. Implement Procedure
7. Integration Guide
8. Debug Interface
10. FAQ


**1. Introduction**

Vpon Data Software Development Kit(Data SDK) is a light data collection toolkit to help you understand your App user's behaviors and insights.

With Data SDK integration into your App, your users' data with the authorization will send to Vpon. You can see your user's insights and explore more business opportunities via dashboards and other services. 

![](/uploads/upload_cf3ff79323dec609abd32ee4412f25d0.png)

Data SDK implements App data collection based on iOS and android APIs. The data will be collected when a particular App event occurs or triggers. You can leverage Data SDK to understand your App users more without worrying any complex API definitions, iterations, and other details. 


**2. Details of Collected Data**

Data SDK collects 5 types of behavioral data, Permission, Device, Geolocation, Wi-Fi, and App related information, automatically. Besides, there are still some other optional data types you can collect if your App fits the requirements. Please contact datasdk.support@vpon.com for further supports.


| Data Category | Data Field          | Description and Permission                                                     | Application                                                                                                                                                          |
| ------------- | ------------------- | ------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Permission    | opt_in              | Users agree to let we, App developer and business partner, collect their data. | To record user's permission. If the user does not "opt-in", we will not collect the sample.                                                                          |
| Permission    | limited_ad_tracking | Users turn on "limit ad tracking" function in the device's privacy settings.   | If the users choose to turn on "limit ad tracking" function, we can not identify the device ID value. Hence, we will not provide personalized contents to the users. |
|Device               |device_ID_type                     |Mobile Advertising ID of the device. IDFA for iOS, ADID (GAID) for Android. Can not identify one person, can only identify the device. If the user did restrict access to the Mobile Advertising ID, which means turning on "limit ad tracking" function, we will not collect the related sample. If the user did reset the Mobile Advertising ID, we will collect the sample of resetted Mobile Advertising ID.|To provide personalized content to the users for better user experience, e.g., based on the user's in-App behavior, provide more relevant contents to the user.|
|Device               |device_ID                     |Value of Mobile Advertising ID, for more details please refer to "device_ID_type".                                                                                |Same as "device_ID_type"                                                                                                                                                                      |
|Device               |device_os                     |User device OS                                                                                |To improve mobile App service, e.g., check software problems by breaking down different OS version results.                                                                                                                                                                      |
|Device               |device_os_version                     |User device OS version number                                                                                |Same as "device_os"                                                                                                                                                                      |
|Device               |sdk_version                     |DMP SDK version number                                                                                |Same as "device_os"                                                                                                                                                                      |
|Geolocation               |gps_timestamp                     |Timestamp when a geolocation record is generated                                                                                |To provide location-enabling service(s) by calculating and providing the geographic location to App developers, device makers and operating systems, when users have opted in and provide permission.                                                                                                                                                                      |
|Geolocation               |horizontal accuracy                     |Location horizontal accuracy (unit: meter)                                                                                |To provide location-enabling service(s) by calculating and providing the geographic location to App developers, device makers and operating systems, when users have opted in and provide permission.                                                                                                                                                                      |
|Geolocation               |vertical_accuracy                     |Location vertical accuracy (unit: meter)                                                                                |Same as "horizontal accuracy"                                                                                                                                                                      |
|Geolocation               |latitude                     |Location latitude (unit: degree)                                                                                |Same as "horizontal accuracy"                                                                                                                                                                      |
|Geolocation               |longitude                     |Location longitude (unit: degree)                                                                                |Same as "horizontal accuracy"                                                                                                                                                                      |
|Geolocation               |altitude                     |Location altitude (unit: meter)                                                                                |Same as "horizontal accuracy"                                                                                                                                                                       |
|Geolocation               |speed                     |Location speed (unit: meter per second)                                                                                |Same as "horizontal accuracy"                                                                                                                                                                       |
|Wi-Fi               |wifi_ssid                     |Connected Wi-Fi hotspot name                                                                                |To provide better location-enabling service(s), when users have opted in and provide permission.                                                                                                                                                                      |
|Wi-Fi               |wifi_bssid                     |Connected Wi-Fi hotspot mac address                                                                                |Same as "wifi_ssid"                                                                                                                                                                      |
|App               |app_list                     | The array of App names based on the installed App list in a device. | To provide personalized content to the users for better user experience, e.g., based on user's in-App behavior, provide more relevant contents to the user, when users have opted in.                                                                         |



**3. Data Privacy**

Please refer to Privacy Policy of Vpon Official Website.
https://www.vpon.com/en/privacy-policy/

**4. Partner Benefits**

**5. Permission**

Vpon Data SDK requires very limited permissions from App users. Based on the collected data type, all we need are geolocation and network permissions. 

![](/uploads/upload_87e473699fd34a76ee917e5f2b676b67.png)

The details are shown as follows:
Android:
* geolocation: 
    * ACCESS_COARSE_LOCATION or ACCESS_FINE_LOCATION
* network:
    * ACCESS_NETWORK_STATE
    * ACCESS_WIFI_STATE
    * CHANGE_WIFI_STATE
    * READ_PHONE_STATE

iOS:
* geolocation:
  * Need Location Authority
  * Add LocationUsageDescription: 
    * +NSLocationAlwaysAndWhenInUseUsageDescription
    * +NSLocationUsageDescription
    * +NSLocationWhenInUseUsageDescription
* network:
  * Add LocationUsageDescription: 
    * +NSLocationAlwaysAndWhenInUseUsageDescription
    * +NSLocationUsageDescription
    * +NSLocationWhenInUseUsageDescription
  * Enable "Access WiFi Information" in ProjectSetting on iOS 12 and later versions"


**6. Implement Procedure**

![](/uploads/upload_063f2c1789b09d91146991807e189c73.png)
1. Apply to Vpon Contact for Data SDK license registration  
2. Start to integrate Data SDK according to website instructions and then check the integration results and data transmission status with Vpon Contact. We also provide a Debug Interface for SDK integration diagnosis. 
3. Submit your App to Marketplaces (Apple Store or Google Play) and notify Vpon Contact when your App is available on marketplaces
4. Start to collect and explore your App users’ data

Vpon Contact: datasdk.support@vpon.com

**7. Integration Guide**

![](/uploads/upload_78666ffc8378425a9b4d89537a8ee183.png)
Wait for MI to update....
* android
* iOS


**8. Debug Interface**

Debug Interface provides a check mechanism to help App publishers understand the integration status. When Vpon Data SDK is integrated with debug_mode enabled, App publishers can see the checking messages on the developer console.

Debug Interface checks SDK integration in 3-steps: ***SDK Initialization***, ***SDK Info Collection***, and ***Endpoint Connection***.

When start running App, ***SDK Initialization*** step will check SDK initialization status and display the device basic information in the developer console shown as follows.
```
[VponData] Start SDK integration tests...
[VponData] Checking SDK and device status...
[VponData] --SDK Version: iOS V2.0.0
[VponData] --License key: XXXXXXXX
[VponData] --CustomID: YYYYYYYY
[VponData] --Device Model Name: iPhone 12,3
[VponData] --Device OS: iOS 13.5.1
[VponData] --Device Limited_Ad_Tracking: False
[VponData] Succeed in initializing SDK. 
```

***SDK Info Collection*** and ***Endpoint Connection*** examine Send Event status when an App event occurs or triggers. The messages are shown as follows in the developer console:
```
[VponData] Checking triggered event data...
[VponData] --Collect Time: 2020-11-01 17:20:45 UTC+0
[VponData] --Event Type: Launch
[VponData] Checking Vpon endpoint status... 
[VponData] Succeed in sending data to Vpon endpoint. Endpoint response code : 200.
[VponData] Pass all SDK integration tests.
```
However, App publishers may see error messages if inappropriate setting occurs shown as follows:
```
[VponData] Start SDK integration tests...
[VponData] Checking SDK and device status...
[VponData] License key is invalid. 
[VponData] Fail to initialize SDK. Please check the required settings in Vpon Data SDK website. 
```
These error messages indicate that License key is invalid, which remind App publishers to check License key setting when calling SDK API.

```
[VponData] Fail to receive Vpon endpoint’s feedback. Endpoint response code : 0(-1009, The Internet connection appears to be offline.). Please make sure your network connection is stable and check Vpon’s endpoint connection again.
```
These above error messages indicate that the device is not connected to network or the network is not stable. 


If some errors keep unsolved, App publishers can collect all the messages with [VponData] header in developer console and send them to Vpon Contact: datasdk.support@vpon.com for further supports.

***Reminder: If everything goes well, App publishers have to disable debug_mode manually before submitting App to marketplaces.***


**9. FAQ**

