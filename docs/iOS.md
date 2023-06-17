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

Welcome to the integration guide of Data SDK. You can leverage Data SDK in just several steps:
1. [Check the Prerequisites](#check-the-prerequisites)
2. [Download Data SDK](#download-data-sdk)
3. [Import Data SDK](#import-data-sdk)
4. [Initialize Data SDK](#initialize-data-sdk)
5. [Set Up Background Geolocation Collection](#set-up-background-geolocation-collection) (Optional)
5. [Set up Customized Events](#set-up-customized-events) (Optional)
6. [Test in Debug Mode](#debug-mode)

After completing steps 1 to 4, the minimum requirements, you can observe [Auto Events]({% link docs/AutoEvents.md %}) in your App.

Furthermore, set up customized events according to your App design and user focus in step 5. The event setting is flexible and even skippable. Nevertheless, we encourage you to set up suitable customized events to obtain a comprehensive picture of your App users.

Finally, check the integration status in step 6, [Debug Mode]({% link docs/DebugMode.md %}). Debug Mode helps you test the SDK setting before submitting your App to the App marketplaces. You can turn Debug Mode on in the step of Data SDK initialization, check all go well, and then turn it off in the same place to publish your App.

## Check the Prerequisites
Supported version: iOS 10.0 or later

## Download Data SDK
Download Data SDK [HERE][1] and add the `.framework` file into your Project.

## Import Data SDK
Import `VponDataAnalytics` in your main function.

{% tabs import-ios %}

{% tab import-ios Swift %}
```swift
import VponDataAnalytics
```
{% endtab %}

{% tab import-ios Objective-C%}
```objc
#import <VponDataAnalytics/VponDataAnalytics.h>
```
{% endtab %}

{% endtabs %}

## Initialize Data SDK
Initialize Data SDK in `AppDelegate.swift` or `AppDelegate.h`. in the application `didFinishLaunchingWithOptions` method to ensure [Auto Events]({% link docs/AutoEvents.md %})  functionality.

In addition, manage [License Key](#license-key), [Opt-in](#opt-in), and [Debug Mode](#debug-mode) switch in this step.


### License Key
You will receive a unique license key when your application is approved. See [Integration Process]({% link docs/IntegrationProcess.md %}) for more details.
If you are still waiting to receive it or get into trouble with it, please email Vpon Contact for further assistance.

### Opt-in
Data SDK is committed to protecting App user privacy. Therefore, Data SDK only collects data with user consent, which means Data SDK only gathers data under the condition that a user agrees to App terms of use or privacy policy.

To help you manage App user consent efficiently, Data SDK provides three Opt-In options: `DEFAULT`, `CONSENT`, and `NOCONSENT`.
- `DEFAULT`: the user has neither granted nor declined permission
- `CONSENT`: the user gives consent
- `NOCONSENT`: the user refuses to provide consent.

We recommend determining the status of user consent in the application `didFinishLaunchingWithOptions` method. After that, update the Opt-In option automatically and forward it to Data SDK simultaneously, depending on the latest permission status.

Warning messages will display on the developer console if Opt-In is set either as `NOCONSENT` or `DEFAULT`.

Below is a setup example of License Key and Opt-in:
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
Debug Mode allows you to interactively test your App events, including [Auto]({% link docs/AutoEvents.md %}) and [Customized](#set-up-customized-events), with messages displayed in the developer console.  

We suggest enabling Debug Mode and providing Debug Mode log to Vpon Contact before submitting your App in Marketplaces to guarantee the integration setting. See [Debug Mode]({% link docs/DebugMode.md %}) and [Integration Process]({% link docs/IntegrationProcess.md %}) for more details.

If all goes well, turn Debug Mode off and publish your App to the Marketplace.

Switch Debug Mode using the following codes

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

Combining all together, see a comprehensive example of Data SDK initialization.
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

## Set Up Background Geolocation Collection
Background Geolocation Collection is a powerful feature that allows your app to continuously gather geolocation data from users, even when your app is running in the background. By leveraging this feature, you can provide more personalized experiences and services to your users. However, it's crucial to strictly adhere to Apple's guidelines and respect user privacy when implementing this feature​

Before using this function, ensure that your project settings and permissions are properly set up. You can refer to the [Permission]({% link docs/IntegrPermission.md %}) section for more details on this.

To integrate the Background Geolocation Collection feature into your iOS app, follow these steps:

1. Initialization: Make sure the Data SDK is properly initialized in your app before you start using the geolocation collection feature.

2. Start/Stop Interface: Data SDK provides an interface that allows app developers to easily call and control the geolocation tracking. Use the startLocationCollection method to begin collecting geolocation data, and the stopLocationCollection method to stop the data collection.

3. Accuracy Level Configuration: The SDK allows you to set the level of accuracy for geolocation data collection by using the setLocationCollectionAccuracy method. There are three options available: high, mid, and low accuracy respectively.

Here is a sample code snippet to use these methods:

{% tabs setup-background %}
{% tab setup-background Swift %}
```swift
// to start or stop geolocation collection with mid accuracy
let config = VDAConfiguration.sharedInstance
// Start geolocation collection
config.startBackgroundLocationUpdate(frequency: .mid)

// Stop geolocation collection
config.stopBackgroundLocationUpdate()

// to setup different accuracy levels
config.startBackgroundLocationUpdate(frequency: .high)
config.startBackgroundLocationUpdate(frequency: .mid)
config.startBackgroundLocationUpdate(frequency: .low)

```
{% endtab %}

{% tab setup-background Objective-C%}
```objc
// to start and stop geolocation collection with mid accuracy
VDAConfiguration *config = [VDAConfiguration sharedInstance];
// to start geolocation collection
[config 
startBackgroundLocationUpdateWithFrequency:VDAFrequencyMid];
// to stop geolocation collection
[config stopBackgroundLocationUpdate];
// to setup different accuracy levels
[config startBackgroundLocationUpdateWithFrequency:VDAFrequencyHigh];
[config startBackgroundLocationUpdateWithFrequency:VDAFrequencyMid];
[config startBackgroundLocationUpdateWithFrequency:VDAFrequencyLow];
```
{% endtab %}

{% endtabs %}

Once you have integrated the feature, you should test it to ensure it's working correctly. We recommend using the [Debug Mode]({% link docs/DebugMode.md %}) for this purpose. This mode allows you to interactively test your app events, including the geolocation collection, with messages displayed in the developer console.

## Set up Customized Events
If [Auto Events]({% link docs/AutoEvents.md %}) only partially fulfills your needs, Data SDK provides customized events to serve various App designs and meet your business focus.
 
By calling the `tracker` method, you can define your event name and any additional information you want to collect. It's flexible, and most importantly, no limit on the number of events.

For instance, an E-Commerce(EC) App wants to create a conversion funnel. Hence, recording users' views on which product item is essential. Using the `tracker` method, this EC App can quickly implement an `item_view` event that tracks a coat with id, size, color, price, etc...extra details.

Below are the sample codes and the final collected data.

{% tabs customized-event-ios %}
{% tab customized-event-ios Swift %}
```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("item_view", extraData: ["id": "payload", "name": "Coat", "price": 100, "color": "Blue", "size": "XL", "currency": "NTD"])
tracker.send(builder)
```
{% endtab %}
{% tab customized-event-ios Objective-C %}

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"item_view" extraData:@{@"id": @"payload", @"name": @"Coat", @"price": @(100), @"color": @"Blue", @"size": @"XL", @"currency": @"NTD"}];
[tracker send:builder];
```
{% endtab %}
{% tab customized-event-ios Collected Data in JSON-C %}
```
{
    "event_name": "item_view"
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


Another example is that an Online Travel Agency(OTA) App wants to observe the browsing history to optimize its user experience. Using the `tracker` method, the OTA App can set up a `page_view` event that traces the user journey.  

Below are the sample codes and the collected data.

{% tabs customized-event-ios2 %}
{% tab customized-event-ios2 Swift %}
```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("page_view", extraData: ["pervious": "URL of Last Page", "current": "URL of Current Page"])
tracker.send(builder)
```
{% endtab %}
{% tab customized-event-ios2 Objective-C %}

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"page_view" extraData:@{@"pervious": @"URL of Last Page", @"current": @"URL of Current Page"}];
[tracker send:builder];
```
{% endtab %}
{% tab customized-event-ios2 Collected Data in Json %}
```
{
    "event_name": "page_view"
    "previous": "URL of Last Page", 
    "current": "URL of Current Page"
}
```
{% endtab %}
{% endtabs %}

## Sample Code
See also [Sample Code](https://github.com/vpon-sdk/Vpon-iOS-Analytics)  for a complete integration reference.

## Download

|Data SDK 2.0.5|
|:-------:|
|[Download][1]|
[1]: https://m.vpon.com/data/sdk/ios/i-vda-v2.0.5-20230519-00657ea-465785.tar.gz
