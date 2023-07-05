---
layout: default
title:          "App Submission"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /app_submission
lang:           "en"
---

# App Submission Guide
## Guidelines for Integrating Data SDK

To successfully integrate our Data SDK into your App and prepare for submission, here's a comprehensive guide:

1. Explore the Data SDK: Learn about the expansive features of our Data SDK that are designed to augment your App's capabilities.

2. Master Store Guidelines: Make sure to comply with the rules set by the App Store and Google Play for a smooth App submission process.

3. Manage Permissions Effectively: Utilize our Data SDK [Permissions]({% link docs/Permission.md %})  Page to set up the required permissions for your App accurately.

4. Clear Communication: Make it easy for users to understand why your App needs certain data. Use clear prompts when requesting permissions

5. Clarify Privacy Practices: Use your App's privacy policy to disclose how data is collected, used, and the role our Data SDK plays in it.

6. Create Comprehensive Documentation: Prepare extensive documentation outlining the reasons why your App collects specific data.

## Guidelines for Integrating Background Geolocation Collection
If your App involves the Background Geolocation Collection feature, follow these extra steps:

1. Meet Specific Requirements: The App Store and Google Play have unique rules for Apps that use background geolocation:
    1. App Store: Describe location usage in your App's privacy policy and `Info.plist` file. [Learn more](https://developer.apple.com/documentation/corelocation/handling_location_updates_in_the_background)
    2. Google Play: Declare background location use in your App listing and in the `Permissions Declaration Form`. [Learn more](https://support.google.com/googleplay/android-developer/answer/9799150?hl=en)

2. Request for Permissions: Design clear prompts to ask users for their consent to collect background geolocation data.

3. Update your Privacy Policy: Make sure your App's privacy policy includes information about the Background Geolocation Collection feature.

Remember, it's crucial as an App publisher to effectively communicate the need for Data SDK's functionalities, including background geolocation, to your users and the App platforms.

For any additional assistance, feel free to refer to our complete Data SDK Integration Guide [iOS]({% link docs/iOS.md %}), [Android]({% link docs/Android.md %}) .






