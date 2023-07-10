---
layout: default
title: "Events"
lead: ""
description: ""
keywords: "datasdk"
permalink: /events
lang: "en"
---
# Events

Utilize the power of Data SDK's event-based data collection to gain valuable insights into your user's behaviors. The understanding obtained from these events can aid in personalizing the user experience, refining your marketing strategies, and improving your App's overall performance. We provide three main types of event collections: Auto Events, Custom Events, and Events triggered by Background Geolocation Collection.

## 1. Auto Events 
Automatically tracked by the Data SDK, Auto Events capture significant milestones in the user's journey within your App without requiring any additional coding. Here are the Auto Events supported by our SDK:

|Event Name|Trigger Point|
|:---|:---|
|Launch| User launches an App| iOS, Android|
|First Open| User launches an App for the first time|
|App Update| User updates an App|
|OS Update| User updates device OS|
|Foreground| User switches an App to the foreground|
|Background| User changes an App to the background|

These events provide a baseline of data collection, delivering a robust understanding of your app's usage patterns.

## 2. Custom Events

Custom Events offer flexibility, allowing you to track specific actions that are unique and significant to your App. These events might include in-App purchases, user interactions with specific features, or the completion of a level in a game. Utilize Custom Events to collect data on actions beyond what is covered by Auto Events, capturing unique insights into how your users interact with specific features in your App.

## 3. Events Triggered by Background Geolocation Collection 

Our Data SDK supports events triggered by Background Geolocation Collection. This feature enables continuous geolocation data collection, even when your app is running in the background, providing valuable location-based user behavior insights.

Use events triggered by Background Geolocation Collection when understanding the user's location behavior outside of App usage is valuable for your App. For example, a travel guide App could leverage this feature to understand what locations the user visits, thus creating more personalized guides. For more information, please refer to our [Backgroung Geolocation Collection]({% link docs/BackgroundGeolocation.md %}) guide.


## Choosing the Right Events

While Auto Events are universally applicable, the use of Custom Events and events triggered by Background Geolocation Collection should be dictated by your App's specific needs and goals. It's crucial to balance your data collection needs with user privacy considerations. Always secure explicit user consent and comply with all relevant privacy laws and platform guidelines. For more information, please refer to our [Permission]({% link docs/Permission.md %}) and [App Submission]({% link docs/AppSubmission.md %}) guides.

Remember, event-based data collection is a powerful tool for understanding and engaging your App users. Use these events effectively to reap maximum benefits from your Data SDK integration.