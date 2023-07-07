---
layout: default
title:          "Debug Mode"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /debug_mode
lang:           "en"
---

# Debug Mode

Debug mode is an essential feature of our Data SDK, designed to assist App publishers in validating their SDK integration. This guide will walk you through using debug mode to test all Data SDK features such as Auto Events, Custom Events, and Background Geolocation Collection.

## Prerequisites
Before starting with the debug mode, ensure:

- You have completed the SDK integration with your App.
- Debug mode is enabled in your App.

For both prerequisites, please refer to our SDK Integration Guide [iOS]({% link docs/iOS.md %}), [Android]({% link docs/Android.md %}) .

Next, this guide describes the overall [Debug Mode Flow](#debug-mode-flow) and the logs related to [Background Geolocation Collection](#background-geolocation-collection), offering examples of both successful and unsuccessful logs. At the end, it provides a comprehensive [Debug Mode Example](#debug-mode-example), detailing the Debug mode with the App setup and operations.

## Debug Mode Flow
The debug mode comprises three main steps:

### 1. SDK Initialization

When the App is launched, this step ensures that the SDK has been initialized successfully with accurate parameters. It verifies the SDK version, license key, custom ID, device model name, device operating system, and the status of limited ad tracking.

A successful initialization log will look like this:
```
[VponData] Start SDK integration tests...
[VponData] Checking SDK and device status...
[VponData] --SDK Version: iOS V2.0.5
[VponData] --License key: your_license_key_here
[VponData] --CustomID: 
[VponData] --Device Model Name: iPhone 12,3
[VponData] --Device OS: iOS 15.1
[VponData] --Device Limited_Ad_Tracking: True
[VponData] Succeed in initializing SDK.
```
Error Message Example:
```
[VponData] Start SDK integration tests...
[VponData] Checking SDK and device status...
[VponData] License key is invalid. 
[VponData] Fail to initialize SDK. Please check the required settings in Vpon Data SDK: https://datasdk.vpon.com/
```

This error message indicates that the License key is invalid, which reminds App publishers to check the License key setting when calling SDK functions.

### 2. SDK Info Collection

This step checks that the SDK is correctly collecting events data. It checks each triggered event, its collect time, and event type.

The SDK logs information based on the events that occur within the application. These events include Auto Events (occur automatically), Custom Events (defined by App publishers), and the `continuous_geo` event (part of the Background Geolocation Collection feature).

A successful collection of event data can be verified by the following log:
```
[VponData][event_id] Checking triggered event data...
[VponData][event_id] --Collect Time: 2023-06-10 17:21:08 UTC+0
[VponData][event_id] --Event Type: auto
```

### 3. Endpoint Connection

This step confirms that the collected data is successfully sent to the Vpon endpoint and receives a positive response.

```
[VponData][event_id] Checking Vpon endpoint status...
[VponData][event_id] Succeed in sending data to Vpon endpoint. Endpoint response code : 200.
```
Error Message Example:
```
[VponData][event_id] Fail to receive Vpon endpoint’s feedback. Endpoint response code: 0(-1009, The Internet connection appears to be offline.). Please make sure your network connection is stable and check Vpon’s endpoint connection again.
```
This error message indicates that the device is not connected to the network or the network connection is unstable.

## Background Geolocation Collection
Background Geolocation Collection allows the SDK to collect geolocation data while the App is running in the background. The logs related to this feature can be divided into three parts:

### 1. Initialization
Upon enabling the Background Geolocation Collection, the SDK checks its status, including whether it's enabled and the collection frequency setting.
```
[VponData] Checking background geolocation collection status...
[VponData] Background geolocation collection is currently enabled.
[VponData] The collection frequency setting for background geolocation is set to high.
[VponData] Background geolocation collection status check completed.
```

### 2. Periodic Collection
When the feature is active, it periodically logs `continuous_geo` events. These events are timestamped, collected, and sent to the Vpon endpoint.
```
[VponData][event_id] Checking triggered event data...
[VponData][event_id] --Collect Time: 2023-06-10 17:21:08 UTC+0
[VponData][event_id] --Event Type: continuous_geo
[VponData][event_id] Checking Vpon endpoint status...
[VponData][event_id] Succeed in sending data to Vpon endpoint. Endpoint response code : 200.
```

### 3. Disabling Collection
Upon disabling the Background Geolocation Collection, the SDK checks and confirms the feature has been correctly disabled.

```
[VponData] Checking background geolocation collection status...
[VponData] Background geolocation collection is currently disabled.
[VponData] Background geolocation collection status check completed.
```

## Debug Mode Example
Let's consider an example. Assume that we have an App named **Travel in Taipei** which integrates Data SDK.

### Actions set up by App Publisher using Data SDK
1. Set up 1 custom event named `change language`.
2. Integrated the background geolocation collection feature, which:
    1. Triggers the feature when users click `Start Tracking`.
    2. Disables the feature when users click `Stop Tracking`

### Actions taken by App Tester
1. Launches the App **Travel in Taipei**
2. Changes the language from English (EN) to Japanese (JP)
3. Clicks `Start Tracking`
4. Opens another App (which sends **Travel in Taipei** to the background)
5. Returns to the **Travel in Taipei** App(which bring it to the foreground) after a while
6. Clicks `Stop Tracking`

Given the tester's actions, the debug mode logs may appear as follows:

```
// SDK Initializes
[VponData] Start SDK integration tests...
[VponData] Checking SDK and device status...
[VponData] --SDK Version: iOS V2.0.5
[VponData] --License key: your_license_key
[VponData] --CustomID: your_custom_id
[VponData] --Device Model Name: iPhone 12,3
[VponData] --Device OS: iOS 15.1
[VponData] --Device Limited_Ad_Tracking: True
[VponData] Succeed in initializing SDK.

// App Launches
[VponData][9B2A6CD1] Checking triggered event data...
[VponData][9B2A6CD1] --Collect Time: 2023-06-10 17:20:00 UTC+0
[VponData][9B2A6CD1] --Event Type: auto
[VponData][9B2A6CD1] Checking Vpon endpoint status...
[VponData][9B2A6CD1] Succeed in sending data to Vpon endpoint. Endpoint response code: 200.

// Change language from EN to JP
[VponData][8F3DA2E6] Checking triggered event data...
[VponData][8F3DA2E6] --Collect Time: 2023-06-10 17:20:10 UTC+0
[VponData][8F3DA2E6] --Event Type: change_language
[VponData][8F3DA2E6] Checking Vpon endpoint status...
[VponData][8F3DA2E6] Succeed in sending data to Vpon endpoint. Endpoint response code: 200.

// Start Tracking
[VponData] Checking background geolocation collection status...
[VponData] Background geolocation collection is currently enabled.
[VponData] The collection frequency setting for background geolocation is set to high.
[VponData] Background geolocation collection status check completed.

// 1st continuous_geo
[VponData][C1E5D7F4] Checking triggered event data...
[VponData][C1E5D7F4] --Collect Time: 2023-06-10 17:25:10 UTC+0
[VponData][C1E5D7F4] --Event Type: continuous_geo
[VponData][C1E5D7F4] Checking Vpon endpoint status...
[VponData][C1E5D7F4] Succeed in sending data to Vpon endpoint. Endpoint response code: 200.

// 2nd continuous_geo
[VponData][F3D2E6A7] Checking triggered event data...
[VponData][F3D2E6A7] --Collect Time: 2023-06-10 17:30:10 UTC+0
[VponData][F3D2E6A7] --Event Type: continuous_geo
[VponData][F3D2E6A7] Checking Vpon endpoint status...
[VponData][F3D2E6A7] Succeed in sending data to Vpon endpoint. Endpoint response code: 200.

// App goes to the background
[VponData][B6C5D7F1] Checking triggered event data...
[VponData][B6C5D7F1] --Collect Time: 2023-06-10 17:32:00 UTC+0
[VponData][B6C5D7F1] --Event Type: auto
[VponData][B6C5D7F1] Checking Vpon endpoint status...
[VponData][B6C5D7F1] Succeed in sending data to Vpon endpoint. Endpoint response code: 200.

// App returns to foreground
[VponData][E6A7F8D9] Checking triggered event data...
[VponData][E6A7F8D9] --Collect Time: 2023-06-10 17:35:30 UTC+0
[VponData][E6A7F8D9] --Event Type: auto
[VponData][E6A7F8D9] Checking Vpon endpoint status...
[VponData][E6A7F8D9] Succeed in sending data to Vpon endpoint. Endpoint response code: 200.

// Stop Tracking
[VponData] Checking background geolocation collection status...
[VponData] Background geolocation collection is currently disabled.
[VponData] Background geolocation collection status check completed.

```

Before submitting your App, you're required to collect all messages beginning with `[VponData]` from your developer console. These debug mode logs should then be sent to Vpon's support team, which is a crucial step for us to validate your SDK integration, provide necessary assistance, and ensure seamless data collection and transmission in your App.

The support team's email can be found in the footer of our website. If you encounter any issues or persistent errors during the testing process, please make sure to include these in the logs you send us. Our team is always here to provide support and help troubleshoot any issues.