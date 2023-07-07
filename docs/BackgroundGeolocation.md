---
layout: default
title: "Background Geolocation Collection"
lead: ""
description: ""
keywords: "datasdk"
permalink: /back_geo
lang: "en"
---
# Background Geolocation Collection

Background Geolocation Collection extends your App's data collection capabilities by tracking user locations even when your App is running in the background. This feature offers a deeper understanding of user behaviors, enabling you to create more personalized and strategically engaging experiences.

## Expanding Data Collection Beyond In-App

While standard Data SDK events capture user actions within the App, Background Geolocation Collection goes a step further. It collects data beyond the confines of active App usage, providing a more comprehensive understanding of user behaviors.

## Accuracy Level: Balancing Data Collection and Battery Usage

The effectiveness of Background Geolocation Collection is influenced by its accuracy level, which in turn affects the frequency and duration of data collection. App publishers can choose from three accuracy levels:

### - High Accuracy
Provides detailed and frequent location data but uses more battery. Suitable for Apps requiring comprehensive location tracking, such as outdoor adventure or exploration Apps.

### - Mid Accuracy
Strikes a balance between data collection frequency and battery usage. Ideal for Apps that benefit from, but don't heavily rely on, granular location data, like general travel or shopping Apps.

### - Low Accuracy
Uses the least battery power and collects data less frequently. Appropriate for Apps where a general understanding of users' location behavior patterns is sufficient.

Your choice of accuracy level should consider your App's functionality, the role of location data in enhancing user experiences, and the potential impact on battery life. To set the accuracy level, refer to our SDK Integration Guide [iOS]({% link docs/iOS.md %}), [Android]({% link docs/Android.md %}) .

## Key Considerations and Best Practices

### - User Consent
Always secure explicit user consent before initiating data collection.

### - Battery Usage
Strive to find a balance between data accuracy and battery life.

### - Store Submission Review
Adhere to the guidelines of both the App Store and Google Play Store on background geolocation data collection. For more information, refer to [App Submission]({% link docs/AppSubmission.md %}) .

### - Notification and User Experience
Using the Background Geolocation Collection feature triggers system-generated location notifications that cannot be disabled. These notifications, such as "App_Name is actively using your location," might impact the user experience due to their frequency. It is, therefore, crucial to inform users clearly in the prompt and privacy policy about the feature's use.

## Case Study: Travel in Taipei App

The Travel in Taipei App illustrates effective utilization of Background Geolocation Collection

#### Trigger Points
The App begins collecting geolocation data when a user engages in specific activities, such as selecting a tour or exploring attractions.
#### Frequency Setting
The App employs a Mid Accuracy level, achieving a balance between data accuracy and battery usage.
Leveraging this feature, the App has significantly improved itinerary planning and enhanced user engagement and personalization.

For a detailed guide on how to request and handle permissions and prepare your App for submission, refer to our [Permissions]({% link docs/Permission.md %}) and [App Submission]({% link docs/AppSubmission.md %}) pages.
