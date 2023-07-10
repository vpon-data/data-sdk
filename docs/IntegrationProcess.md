---
layout: default
title:          "Integration Process"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /integration_process
lang:           "en"
---

# Integration Process
---

The Integration Process guides you through integrating the Data SDK into your App, offering detailed instructions tailored for both iOS and Android platforms. It covers a range of essential steps, from initial setup to release, ensuring you have the tools you need for a successful integration.


![](/docs/images/integration_process_5.png) 

| Step | Role        | Task                                                                                                    | Duration          |
|------|-------------|---------------------------------------------------------------------------------------------------------|-------------------|
| Application    | App publisher | a. Fill out the [Business Request Form](https://airtable.com/shr0Mts1aMzUlzEIm) with your App's information and submit.        |         1 day          |
|      | Vpon        | b. Vpon confirms the pre-inquiry and sends the SDK license key.                                | 2 days            |
| Installation| App publisher | a. Download and import the Data SDK for your platform ([iOS]({% link docs/iOS.md %}) or [Android]({% link docs/Android.md %}), then follow the step-by-step integration guide provided by Vpon for initializing the Data SDK. |          2 days         |
|      | App publisher   | b. Optionally, set up [Custom Events]({% link docs/Event.md %}#2-custom-events) based on your App's requirements, or enable the optional feature of [Background Geolocation Collection] ({%link docs/BackgroundGeolocation.md %}). | 2-5 days |
| Testing    | App publisher | a. Enable [Debug Mode]({% link docs/DebugMode.md %}) and test your App in a simulation environment. | 5-8 days          |
|      | App publisher| b. Email the Debug Mode log to Vpon's support team for review.                               |         0.5 day          |
|      | Vpon        | c. Vpon evaluates the integration and provides feedback. Address common issues and solutions if needed. | 2 days            |
| Release    | App publisher | a. After successful testing, disable Debug Mode, and submit your App to the relevant App marketplaces. Review the [App Submission]({% link docs/AppSubmission.md %}) guidelines before submitting.|     0.5 day               |
|      | App publisher  | b. Monitor your App's status during the platform review process (iOS: 1-7 days, Android: 1-3 days).     | Varies by platform |

Note: The duration estimates provided are for reference only and may vary based on individual circumstances.


If you encounter any issues or have questions during the process, please do not hesitate to contact us via email for assistance. Our support team is here to help and will gladly assist you with any concerns you may have. The contact email can be found in the footer of our website.

##  More Guides
The Integration Process is comprised of various related pages, each addressing a crucial aspect of integration:

| Documentation | Description |
| -------------- | ------------ |
| [iOS SDK]({% link docs/iOS.md %}) | Provides detailed steps for embedding Data SDK in your iOS App, along with code settings for optimal functionality. |
| [Android SDK]({% link docs/Android.md %}) | Offers specific instructions for integrating Data SDK into your Android App, with code settings for ideal performance. |
| [Permission]({% link docs/Permission.md %}) | Guidelines for setting App permissions effectively, ensuring user privacy and trust. |
| [App Submission]({% link docs/AppSubmission.md %})| Explains the submission process and requirements for iOS and Android platforms, assisting in a smooth app review process. |
| [Debug Mode]({% link docs/DebugMode.md %}) | Details how to use the real-time event log for debugging in the developer console. |
| [Event]({% link docs/Event.md %}) | Comprehensive information on the three main types of event collections (Auto Events, Custom Events, and Background Geolocation Collection) and guidelines on when to use optional features. |
| [Background Geolocation Collection]({% link docs/BackgroundGeolocation.md %})| Specifics of this optional feature, its benefits, and the process of its integration. |
