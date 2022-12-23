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
5. [Set up customized events](#set-up-customized-events) (Optional but recommended)
6. [Test in Debug Mode](#debug-mode)

After completing steps 1 to 4, the minimum requirements, you can observe [Auto Events](AutoEvents.md) in your App.

Furthermore, set up customized events according to your App design and user focus in step 5. The event setting is flexible and even skippable. Nevertheless, we encourage you to set up suitable customized events to obtain a comprehensive picture of your App users.

Finally, check the integration status in step 6, [Debug Mode](DebugMode.md). Debug Mode helps you test the SDK setting before submitting your App to the App marketplaces. You can turn Debug Mode on in the step of Data SDK initialization, check all go well, and then turn it off in the same place to publish your App.

## Check the Prerequisites
Supported version: iOS 10.0 or later

## Download Data SDK
Download Data SDK [HERE][1] and add the `.framework` file into your Project.

## Import Data SDK
Import `VponDataAnalytics` in your main function.

#### Swift

```swift
import VponDataAnalytics
```

#### Objective-C

```objc
#import <VponDataAnalytics/VponDataAnalytics.h>
```


## Initialize Data SDK
Initialize Data SDK in `AppDelegate.swift` or `AppDelegate.h`. in the application `didFinishLaunchingWithOptions` method to ensure [Auto Events](AutoEvents.md) functionality.

In addition, manage License Key, Opt-in, and Debug Mode switch in this step.


### License Key
You will receive a unique license key when your application is approved. See [Integration Process](IntegrationProcess.md) for more details.
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
#### Swift
```
config.setLicenseKey("testKey", withCustomID: "testCustomID", withOptIn: .CONSENT)
```
#### Objective-C
```
[config setLicenseKey:@"testKey" withCustomID:@"testCustomID" withOptIn:VDAOptInCONSENT];
```

### Debug Mode
Debug Mode allows you to interactively test your App events, including [Auto](AutoEvents.md) and [Customized](#set-up-customized-events), with messages displayed in the developer console.  

We suggest enabling Debug Mode and providing Debug Mode log to Vpon Contact before submitting your App in Marketplaces to guarantee the integration setting. See [Debug Mode](DebugMode.md) and [Integration Process](IntegrationProcess.md) for more details.

If all goes well, turn Debug Mode off and publish your App to the Marketplace.

Switch Debug Mode using the following codes
#### Swift
```
// Turn Debug Mode on/off
config.setDebugMode(true)
config.setDebugMode(false)
```
#### Objective-C
```
// Turn Debug Mode on/off
[config setDebugMode:YES];
[config setDebugMode:NO];
```

Combining all together, see a comprehensive example of Data SDK initialization.
#### Swift
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

#### Objective-C
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

## Set up customized events
If [Auto Events](AutoEvents.md) only partially fulfills your needs, Data SDK provides customized events to serve various App designs and meet your business focus.
 
By calling the `tracker` method, you can define your event name and any additional information you want to collect. It's flexible, and most importantly, no limit on the number of events.

For instance, an E-Commerce(EC) App wants to create a conversion funnel. Hence, recording users' views on which product item is essential. Using the `tracker` method, this EC App can quickly implement an `item_view` event that tracks a coat with id, size, color, price, etc...extra details.

Below are the sample codes and the final collected data.

#### Swift

```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("item_view", extraData: ["id": "payload", "name": "Coat", "price": 100, "color": "Blue", "size": "XL", "currency": "NTD"])
tracker.send(builder)
```

#### Objective-C

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"item_view" extraData:@{@"id": @"payload", @"name": @"Coat", @"price": @(100), @"color": @"Blue", @"size": @"XL", @"currency": @"NTD"}];
[tracker send:builder];
```

#### Collected data in JSON
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

Another example is that an Online Travel Agency(OTA) App wants to observe the browsing history to optimize its user experience. Using the `tracker` method, the OTA App can set up a `page_view` event that traces the user journey.  

Below are the sample codes and the collected data.

#### Swift

```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("page_view", extraData: ["pervious": "URL of Last Page", "current": "URL of Current Page"])
tracker.send(builder)
```

#### Objective-C

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"page_view" extraData:@{@"pervious": @"URL of Last Page", @"current": @"URL of Current Page"}];
[tracker send:builder];
```

#### Collected data in JSON
```
{
    "event_name": "page_view"
    "previous": "URL of Last Page", 
    "current": "URL of Current Page"
}
```

## Sample Code
See also [Sample Code](https://github.com/vpon-sdk/Vpon-iOS-Analytics)  for a complete integration reference.

## Download

|Data SDK 2.0.4|
|:-------:|
|[Download][1]|

[1]: https://m.vpon.com/data/sdk/ios/i-vda-v2.0.4-20221020-c15aa7d-252500.tar.gz
