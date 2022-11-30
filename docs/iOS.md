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
---

## Prerequisites

Data SDK support version:

* iOS：`iOS 10.0 or later`


### Prepare for Data SDK import
You can [download Data SDK here][1] and add the .framework file into your Project. 

Please be noted that Vpon supports both Objective-C and Swift languages. If your App is developed using Objective-C, please refer to [iOS developer's guideline](https://developer.apple.com/documentation/swift/imported_c_and_objective-c_apis/importing_swift_into_objective-c) or 
[Sample Code](https://github.com/vpon-sdk/Vpon-iOS-Analytics) for a complete integration setting.



## Import Data SDK

Please import VponDataAnalytics as below.

#### Objective-C

```objc
#import <VponDataAnalytics/VponDataAnalytics.h>
```

#### Swift

```swift
import VponDataAnalytics
```

## Initialize Data SDK

Please initialize Data SDK in the `AppDelegae.h` or `AppDelegae.swift` as below

### License Key
You should receive a unique license key when your application is approved. If you do not receive it, please email it to Vpon Contact.


### Opt-in
To manage user consent in your App, Data SDK provides three Opt-In options: DEFAULT, CONSENT, and NOCONSENT. DEFAULT indicates the user has neither granted nor declined consent, CONSENT indicates the user gives his/her consent, and NOCONSENT indicates the user refuses to give his/her consent. Please refer to the sample code below:

#### Objective-C
```objc
// Opt-In options: 
// VDAOptInDEFAULT 
// VDAOptInCONSENT
// VDAOptInNOCONSENT

// The default value of Opt-In is VDAOptInDEFAULT

// If a user gives his/her consent, configure Opt-In as VDAOptInCONSENT 
[config setLicenseKey:@"testKey" withCustomID:@"" withOptIn:VDAOptInCONSENT];

//If a user refuses to give his/her consent, configure Opt-In as VDAOptInNOCONSENT
[config setLicenseKey:@"testKey" withCustomID:@"" withOptIn:VDAOptInNOCONSENT];

```
#### Swift
```swift
// Opt-In options: 
// .DEFAULT 
// .CONSENT
// .NOCONSENT

// The default value of Opt-In is .DEFAULT

// If a user gives his/her consent, configure Opt-In as .CONSENT 
config.setLicenseKey("testkey", withCustomID: "customID", withOptIn: .CONSENT);

//If a user refuses to give his/her consent, configure Opt-In as .NOCONSENT
config.setLicenseKey("testkey", withCustomID: "customID", withOptIn: .NOCONSENT);

```

If a user gives his/her consent, you should configure Opt-In as CONSENT. If a user refuses to give his/her consent, you should configure Opt-In as NOCONSENT and should NOT send data to Vpon. Data SDK will display warning messages on the developer console if Opt-In is set either as NOCONSENT or DEFAULT.

It is recommended that you determine the status of a user's consent at every app launch. After that, update the Opt-In value and forward it to Data SDK simultaneously according to the user's latest consent status. 

If a user changes his/her consent status, for example, from provides the consent to declines the consent, your App must automatically update the Opt-In value from CONSENT to NOCONSENT and then forward the status to Data SDK.

Below is an example to initialize Data SDK with users' explicit authorization:



#### Objective-C
```objc
#import <VponDataAnalytics/VponDataAnalytics.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    VDAConfiguration *config = [VDAConfiguration sharedInstance];
    [config setLicenseKey:@"testKey" withCustomID:@"customID" withOptIn:VDAOptInCONSENT];
    [config setDebugMode:NO];
    [config initialize];
}
```

#### Swift
```swift
import VponDataAnalytics

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions:      
    [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        let config = VDAConfiguration.sharedInstance
        config.setLicenseKey("testkey", withCustomID: "customID", withOptIn: .CONSENT)
        config.setDebugMode(false)
        config.initialize()
}
```

## Send Data
Data SDK provides tracker.send() method to send data in different scenarios.

By using the tracker.send(), you can define a custom event that collects specific data. Please refer to the sample code below:


#### Objective-C

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"item_view" extraData:@{@"id": @"payload", @"name": @"Coat", @"price": @(10), @"color": @"Blue", @"size": @"XL", @"tags": @"OrangeBear,fiber", @"currency": @"NTD"}];
[tracker send:builder];

```


#### Swift

```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("item_view", extraData: ["id": "payload", "name": "Coat", "price": 10, "color": "Blue", "size": "XL", "tags": "OrangeBear,fiber", "currency": "NTD"])
tracker.send(builder)
```

Another example is that you want to collect the URL accessed by a user. Using tracker.send(), you can define another event to collect the data of the previous URL and current URL accessed by a user.


#### Objective-C

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"page_view" extraData:@{@"pervious": @"URL of Last Page", @"current": @"URL of Current Page"}];
[tracker send:builder];

```

#### Swift

```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("page_view", extraData: ["pervious": "URL of Last Page", "current": "URL of Current Page"])
tracker.send(builder)
```


## Debug Mode
When you initialize Data SDK, you can enable debug mode with setDebugMode:Yes / setDebugMode(true). 

#### Objective-C

```objc
#import <VponDataAnalytics/VponDataAnalytics.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    VDAConfiguration *config = [VDAConfiguration sharedInstance];
    ...
    [config setDebugMode:Yes];
    ...
}
```


#### Swift

```swift
import VponDataAnalytics

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions:      
    [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        ...
        config.setDebugMode(true)
        ...
}
```

> **Note**：Set `setDebugMode:Yes` \ `setDebugMode(false)` before the App is launched.

## Sample Code
Please refer to [Sample Code](https://github.com/vpon-sdk/Vpon-iOS-Analytics) for a complete integration sample.

## Download

|Data SDK 2.0.3|
|:-------:|
|[Download][1]|

[1]: https://m.vpon.com/data/sdk/ios/i-vda-v2.0.3-20220107-de7a407-546430.tar.gz
