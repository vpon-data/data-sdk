---
layout: default
title: "SDK-iOS"
lead: ""
description: ""
keywords: "datasdk"
permalink: /ios
lang: "en"
---

# iOS SDK

Dive into the world of Data SDK integration with this comprehensive guide!

Here, we break down how to supercharge your App with key features such as Auto Events, Custom Events, and Background Geolocation Collection. Follow these simple steps:

1. [Check the Prerequisites](#check-the-prerequisites)
2. [Download Data SDK](#download-data-sdk)
3. [Initialize Data SDK](#initialize-data-sdk)
4. [Set up Background Geolocation Collection](#set-up-background-geolocation-collection) (Optional)
5. [Set up Custom Events](#set-up-custom-events) (Optional)
6. [Test in Debug Mode](#debug-mode)

Upon completing first three steps, you'll have fulfilled the minimum requirements and enabled [Auto Events]({% link docs/Event.md %}#1-auto-events) tracking in your App.

Step 4 involves the optional setup of [Background Geolocation Collection]({% link docs/BackgroundGeolocation.md %}). This powerful feature allows continuous gathering of geolocation data from users, even when your App runs in the background, to provide more personalized experiences and services.

Step 5 allows you to set up [Custom Events]({% link docs/Event.md %}#2-custom-events) according to your App's design and user needs. While optional, we highly recommend creating suitable custom events to obtain a comprehensive view of your App users.

Lastly, in step 6, use the [Debug Mode]({% link docs/DebugMode.md %} ) to verify your integration status. Debug Mode facilitates testing of all SDK configurations, including Background Geolocation Collection, Auto & Custom events, before launching your App on various platforms. We recommend enabling Debug Mode to ensure everything is functioning as expected, and then disabling it before your App's publication.

This guide is designed to make the integration process intuitive and efficient, letting you focus on building and enhancing your App.
## Check the Prerequisites 
Ensure that your App supports iOS version `10.0 or later` before proceeding with the Data SDK integration.

## Download Data SDK
Start by downloading the Data SDK [HERE](#download). Once downloaded, unzip and include the `VponDataAnalytics.xcframework` folder in your project.

## Initialize Data SDK
Initialize Data SDK in your `AppDelegate.swift` or `AppDelegate.h` file, within the application `didFinishLaunchingWithOptions` method. This ensures the [Auto Events]({% link docs/Event.md %}#1-auto-events) feature operates correctly.

You'll also manage the [License Key](#license-key), [Opt-in](#opt-in), and [Debug Mode](#debug-mode) in this step.

### License Key
Upon approval of your application, you'll receive a unique license key. If you encounter any issues or haven't received your key, please refer to the [Integration Process]({% link docs/IntegrationProcess.md %}) for further details or email Vpon’s support team for additional support.


### Opt-in
Data SDK respects user privacy by only collecting data with the user's explicit consent, meaning data is gathered only when a user agrees to your App's terms of use or privacy policy.

To help you manage this consent effectively, Data SDK offers three Opt-In options: `DEFAULT`, `CONSENT`, and `NOCONSENT`.
- `DEFAULT`: neither granted nor declined
- `CONSENT`: granted
- `NOCONSENT`: declined

We recommend setting the user consent status in the application `didFinishLaunchingWithOptions` method, then updating the Opt-In option and forwarding it to Data SDK depending on the latest permission status. If Opt-In is set to either `NOCONSENT` or `DEFAULT`, warning messages will display on the developer console.

Here's a setup example of License Key and Opt-in:
{% tabs lic-ios %}
{% tab lic-ios Swift %}
```
config.setLicenseKey("testKey", withCustomID: "testCustomID", withOptIn: .CONSENT)
```
{% endtab %}

{% tab lic-ios Objective-C%}
```
[config setLicenseKey:@"testKey" withCustomID:@"testCustomID" withOptIn:VDAOptInCONSENT];
```
{% endtab %}

{% endtabs %}

### Debug Mode
Debug Mode allows you to interactively test your App events, including Auto, Custom, and Background Geolocation Collection.

We recommend enabling Debug Mode and providing the Debug Mode log to Vpon’s support team before submitting your App to various marketplaces, ensuring correct integration settings. If everything is working as expected, disable Debug Mode before publishing your App.

For more detailed information, you can refer to the sections on [Debug Mode]({% link docs/DebugMode.md %}) and [Integration Process]({% link docs/IntegrationProcess.md %}).

Here's how to toggle Debug Mode:

{% tabs debug-ios %}

{% tab debug-ios Swift %}
```
// Turn Debug Mode on
config.setDebugMode(true)

// Turn Debug Mode off
config.setDebugMode(false)
```
{% endtab %}

{% tab debug-ios Objective-C%}
```
// Turn Debug Mode on
[config setDebugMode:YES];

// Turn Debug Mode off
[config setDebugMode:NO];
```
{% endtab %}

{% endtabs %}

Here's a complete example that demonstrates how to initialize the Data SDK:
{% tabs allexample-ios %}

{% tab allexample-ios Swift %}

```
import VponDataAnalytics

// Opt-In options: 
// .DEFAULT 
// .CONSENT
// .NOCONSENT

// Debug Mode options: true/false

// Configure Opt-In as .CONSENT when a user gives consent
// Turn Debug Mode on 
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions:      
    [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        let config = VDAConfiguration.sharedInstance
        config.setLicenseKey("testKey", withCustomID: "testCustomID", withOptIn: .CONSENT)
        config.setDebugMode(true)
        config.initialize()
}

// Configure Opt-In as .NOCONSENT when a user refuses to give consent
// Turn Debug Mode off 
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions:      
    [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        let config = VDAConfiguration.sharedInstance
        config.setLicenseKey("testKey", withCustomID: "testCustomID", withOptIn: .NOCONSENT)
        config.setDebugMode(false)
        config.initialize()
}
```
{% endtab %}

{% tab allexample-ios Objective-C%}
```
#import <VponDataAnalytics/VponDataAnalytics.h>

// Opt-In options: 
// VDAOptInDEFAULT 
// VDAOptInCONSENT
// VDAOptInNOCONSENT

// Debug Mode options: YES/NO

// Configure Opt-In as VDAOptInCONSENT when a user gives consent
// Turn Debug Mode on
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    VDAConfiguration *config = [VDAConfiguration sharedInstance];
    [config setLicenseKey:@"testKey" withCustomID:@"testCustomID" withOptIn:VDAOptInCONSENT];
    [config setDebugMode:YES];
    [config initialize];
}

// Configure Opt-In as VDAOptInNOCONSENT when a user refuses to give consent
// Turn Debug Mode off
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    VDAConfiguration *config = [VDAConfiguration sharedInstance];
    [config setLicenseKey:@"testKey" withCustomID:@"testCustomID" withOptIn:VDAOptInNOCONSENT ];
    [config setDebugMode:NO];
    [config initialize];
}
```
{% endtab %}
{% endtabs %}

## Set up Background Geolocation Collection
Background Geolocation Collection is a powerful feature that allows continuous geolocation data collection, even when your App is running in the background. However, it's essential to respect user privacy and adhere to Apple's guidelines when implementing this feature.

Before using this function, ensure that your project settings and permissions are properly set up. You can refer to the [Background Geolocation Collection]({% link docs/BackgroundGeolocation.md %}) and [Permission]({% link docs/Permission.md %}) sections for more details on this.

To integrate the Background Geolocation Collection feature into your iOS App, follow these steps:

1. Initialization: Make sure the Data SDK is properly initialized in your App before you start using the background geolocation collection feature.

2. Start/Stop Interface: Data SDK provides an interface that allows App developers to easily call and control the geolocation tracking. When calling the `startBackgroundLocationUpdate` method to begin collecting geolocation data, remember to set up the frequency for data collection as needed. Use the `stopBackgroundLocationUpdate` method to stop the data collection when it's no longer required.

3. Accuracy Level Configuration: The SDK allows you to set the level of accuracy for geolocation data collection. There are three options available: `high`, `mid`, and `low` accuracy respectively. Note that the accuracy level and the frequency of updates may affect the App's battery usage, so choose your settings carefully.

Here is a sample code snippet to use these methods:

{% tabs setup-background-ios %}

{% tab setup-background-ios Swift %}
```swift
// to start or stop geolocation collection with mid accuracy
let config = VDAConfiguration.sharedInstance
config.startBackgroundLocationUpdate(frequency: .mid)

// to stop geolocation collection
config.stopBackgroundLocationUpdate()

// three accuracy options: high/mid/low
// high accuracy 
config.startBackgroundLocationUpdate(frequency: .high)
// mid accuracy
config.startBackgroundLocationUpdate(frequency: .mid)
// low accuracy
config.startBackgroundLocationUpdate(frequency: .low)
```
{% endtab %}

{% tab setup-background-ios Objective-C%}
```objc
// to start geolocation collection with mid accuracy
VDAConfiguration *config = [VDAConfiguration sharedInstance];
[config startBackgroundLocationUpdateWithFrequency:VDAFrequencyMid];

// to stop geolocation collection
[config stopBackgroundLocationUpdate];

// three accuracy options: high/mid/low
// high accuracy
[config startBackgroundLocationUpdateWithFrequency:VDAFrequencyHigh];
// mid accuracy
[config startBackgroundLocationUpdateWithFrequency:VDAFrequencyMid];
// low accuracy
[config startBackgroundLocationUpdateWithFrequency:VDAFrequencyLow];
```
{% endtab %}

{% endtabs %}

Once you have integrated the feature, you should test it to ensure it's working correctly. We recommend using the [Debug Mode]({% link docs/DebugMode.md %}) for this purpose. This mode allows you to interactively test your App events, including the geolocation collection, with messages displayed in the developer console.

## Set up Custom Events
Custom events are a powerful tool to gain insights into user behavior, and Data SDK makes it simple to set them up.

By utilizing the `tracker` method, you can set up events that carry unique names and contain additional data you wish to gather. The strength of this feature lies in its flexibility - there's no cap on the number of events you can set up, making it adaptable to your App's specific design and business goals.

Below, you will find examples of how to set up these custom events, along with representations of how the collected data may appear in a JSON string format on a mobile device. It's crucial to note that this data is encrypted for user privacy and cannot be directly accessed via the App developer console.

Let's consider an example where you're running an e-commerce App and you want to establish a conversion funnel. In this case, tracking user interactions with various product items becomes essential. By leveraging the tracker method, you can swiftly set up an `item_view` event that collects details such as the product's ID, size, color, and price.


{% tabs custom-event-ios %}
{% tab custom-event-ios Swift %}
```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("item_view", extraData: ["id": "payload", "name": "Coat", "price": 100, "color": "Blue", "size": "XL", "currency": "NTD"])
tracker.send(builder)
```
{% endtab %}

{% tab custom-event-ios Objective-C %}

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"item_view" extraData:@{@"id": @"payload", @"name": @"Coat", @"price": @(100), @"color": @"Blue", @"size": @"XL", @"currency": @"NTD"}];
[tracker send:builder];
```
{% endtab %}

{% tab custom-event-ios Collected Data in JSON %}
```json
{
    "event_name": "item_view",
    "id": "03356",
    "name": "Coat", 
    "price": 100, 
    "color": "Blue", 
    "size": "XL", 
    "currency": "NTD"
}
```
{% endtab %}

{% endtabs %}

Similarly, if you're operating an Online Travel Agency (OTA) App and want to optimize the user experience by understanding their browsing history, the tracker method can assist. It enables the configuration of a `page_view` event, tracing the user's navigation journey through your App.

{% tabs custom-event-ios2 %}

{% tab custom-event-ios2 Swift %}
```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("page_view", extraData: ["pervious": "URL of Last Page", "current": "URL of Current Page"])
tracker.send(builder)
```
{% endtab %}

{% tab custom-event-ios2 Objective-C %}

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"page_view" extraData:@{@"pervious": @"URL of Last Page", @"current": @"URL of Current Page"}];
[tracker send:builder];
```
{% endtab %}

{% tab custom-event-ios2 Collected Data in Json %}
```json
{
    "event_name": "page_view",
    "previous": "URL of Last Page", 
    "current": "URL of Current Page"
}
```
{% endtab %}

{% endtabs %}

## Sample Code
See also [Sample Code](https://github.com/vpon-sdk/Vpon-iOS-Analytics) for a complete integration reference.

## Download

|Data SDK 2.0.6|
|:-------:|
|[Download][1]|

[1]: https://m.vpon.com/data/sdk/ios/i-vda-v2.0.6-20230919-c4d7784-091866.tar.gz
