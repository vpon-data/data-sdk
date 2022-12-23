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
---
Debug Mode provides a check mechanism to help App publishers understand the integration status. When an App integrates Vpon Data SDK with Debug Mode enabled, App publishers can see the checking messages on the developer console.

Debug Mode checks SDK integration in 3-steps: ***SDK Initialization***, ***SDK Info Collection***, and ***Endpoint Connection***.

When start running App, the ***SDK Initialization*** step will check the SDK initialization status and display the device's essential information in the developer console shown as follows.

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

***SDK Info Collection*** and ***Endpoint Connection*** examine the status when an App event occurs or triggers. The messages are shown as follows in the developer console:
```
[VponData] Checking triggered event data...
[VponData] --Collect Time: 2020-11-01 17:20:45 UTC+0
[VponData] --Event Type: Launch
[VponData] Checking Vpon endpoint status... 
[VponData] Succeed in sending data to Vpon endpoint. Endpoint response code: 200.
[VponData] Pass all SDK integration tests.
```
However, App publishers may see error messages shown as follows if an inappropriate setting occurs:

```
[VponData] Start SDK integration tests...
[VponData] Checking SDK and device status...
[VponData] License key is invalid. 
[VponData] Fail to initialize SDK. Please check the required settings in Vpon Data SDK: https://datasdk.vpon.com/
```
These error messages indicate that the License key is invalid, which reminds App publishers to check the License key setting when calling SDK functions.

```
[VponData] Fail to receive Vpon endpoint’s feedback. Endpoint response code : 0(-1009, The Internet connection appears to be offline.). Please make sure your network connection is stable and check Vpon’s endpoint connection again.
```

The above error messages indicate that the device is not connected to the network or is unstable.

If some errors keep unsolved, App publishers can collect all the messages that start with **[VponData]** in the developer console, and then send the messages to Vpon Contact for further supports.
