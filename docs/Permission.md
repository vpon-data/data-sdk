---
layout: default
title:          "Permission"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /permission
lang:           "en"
---

# Permission
 
Simplify App permissions with the Vpon Data SDK to maximize potential and protect user privacy. This guide walks you through setting up Network and Geolocation Data permissions, including Background Geolocation, for your iOS and Android Apps. 

As responsible publishers, it's crucial to craft user-friendly location permission prompts. By ensuring the right permissions, you provide a seamless experience while adhering to iOS and Android guidelines. Adapt permissions to your App's needs and respect user privacy. Let's effortlessly navigate App permissions to unlock your App's full potential and build trust with users.

## iOS
Setting up your iOS App involves adjusting permissions in your `info.plist` and project settings.

| Type of Permission       | Required Adjustments                                                                                             |
|--------------------------|-----------------------------------------------------------------------------------------------------------------|
| Network Permissions      | 1. Insert these keys in your App's `info.plist`with corresponding descriptions: <br> - NSLocationAlwaysAndWhenInUseUsageDescription <br> - NSLocationUsageDescription <br> - NSLocationWhenInUseUsageDescription <br> 2. Enable the “Access WiFi Information” capability in your project settings for iOS 12 and later versions. |
| Geolocation Permissions | 1. Verify that your App has the necessary Location Authority. <br> 2. Insert these keys in your App's `info.plist` with corresponding descriptions: <br> - NSLocationAlwaysAndWhenInUseUsageDescription <br> - NSLocationUsageDescription <br> - NSLocationWhenInUseUsageDescription |
| Background Geolocation   | 1. Enable the "Background Modes - Location updates" capability in your project settings. <br> 2. In your App source code, set `allowsBackgroundLocationUpdates` to `true`. |
| Advertising Identifier (IDFA)      | Follow instructions in our [IDFA guide](https://wiki.vpon.com/ios/idfa/) |

### Note to iOS Developers: 
Proper setup of the `info.plist` descriptions is crucial. If not done correctly, your Apps may encounter crashes or face App Store submission rejections. Make sure to double-check your descriptions to prevent any issues.

For more detailed integration steps, please refer to the [iOS]({%link docs/iOS.md %})page.

## Android
For your Android App, specific permissions need to be added to your `AndroidManifest.xml` file.

| Type of Permission       | Required Adjustments                                                                                             |
|--------------------------|-----------------------------------------------------------------------------------------------------------------|
| Network Permissions      | 1. Include these permissions: <br> - INTERNET <br> - ACCESS_NETWORK_STATE <br> - ACCESS_WIFI_STATE <br> - CHANGE_WIFI_STATE  <br> 2. Depending on your target Android API level, include either: <br> - READ_PHONE_STATE for `API-1` <br> - READ_BASIC_PHONE_STATE for `API-33 and up` (`Android-13 and beyond`) |
| Geolocation Permissions | Add either of these permissions: <br> - ACCESS_COARSE_LOCATION <br> - ACCESS_FINE_LOCATION |
| Background Geolocation   | 1. Include the - ACCESS_BACKGROUND_LOCATION permission. <br> 2. Setup prompt <br> For `Android 10` devices: When your App requests runtime-permissions, a dialog will be presented with the option to "Allow all the time". <br> For `Android 11 and beyond`: Users must be guided to the App's settings to allow background location permissions. The dialog will not present the "Allow all the time" option, so users need to manually select "Always allow" (or a similar option, depending on language settings) in the App settings. |

For more detailed integration steps, please refer to the [Android]({%link docs/Android.md %}) page.