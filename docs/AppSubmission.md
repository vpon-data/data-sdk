---
layout: default
title:          "App Submission"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /app_submission
lang:           "en"
---

# App Submission
## Guidelines for Integrating Data SDK

To successfully integrate our Data SDK into your App and prepare for submission, here's a comprehensive guide:

| **Index** | **Step Name** | **Details** |
|:--------:|:-------------:|:-------------:|
|1| Explore the Data SDK | Get familiar with the wide range of features our Data SDK offers, designed to enhance your App's performance.|
|2| Master Store Guidelines | Understand the rules and comply with [App Store](https://developer.apple.com/app-store/review/guidelines/) and [Google Play](https://play.google.com/about/developer-content-policy/) to ensure a smooth App submission process.|
|3| Manage Permissions Effectively | Navigate to our Data SDK [Permissions](./docs/Permission.md) Page for setting up the required permissions in your App accurately.|
|4| Clear Communication | Use easy-to-understand prompts when requesting user permissions, explaining why your App needs certain data.|
|5| Clarify Privacy Practices | Disclose in your App's privacy policy how data is collected, used, and the role our Data SDK plays in these processes.|
|6| Create Comprehensive Documentation | Develop thorough documentation outlining why your App collects specific data.|


## Guidelines for Integrating Background Geolocation Collection
If your App involves the Background Geolocation Collection feature, follow these extra steps:

| **Index** | **Step Name** | **Details** |
|:--------:|:-------------:|:-------------:|
|1| Meet Specific Requirements | Both the App Store and Google Play have distinct guidelines for Apps using background geolocation:<br>   - **App Store:** Describe location usage in your App's privacy policy and `Info.plist` file. [Learn more](https://developer.apple.com/documentation/corelocation/handling_location_updates_in_the_background)<br>  - **Google Play:** Declare background location use in your App listing and the `Permissions Declaration Form`. [Learn more](https://support.google.com/googleplay/android-developer/answer/9799150?hl=en)|
|2| Request for Permissions | Create clear prompts to request user consent for collecting background geolocation data.|
|3| Update your Privacy Policy | Ensure your App's privacy policy incorporates information about the Background Geolocation Collection feature.|



Remember, it's crucial as an App publisher to effectively communicate the need for Data SDK's functionalities, including background geolocation, to your users and the App platforms.

For any additional assistance, feel free to refer to our complete Data SDK Integration Guide [iOS]({% link docs/iOS.md %}), [Android]({% link docs/Android.md %}) .






