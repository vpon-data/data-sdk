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

Please be noted that Vpon supports both Objective-C and Swift languages.


## Import Data SDK

Please import VponDataAnalytics in the files expected to be integrated with Data SDK.

### Objective-C

```objc
#import <VponDataAnalytics/VponDataAnalytics.h>
```

### Swift

```swift
import VponDataAnalytics
```

## Data SDK Initialization

Please follow the instructions to initialize Data SDK in the AppDelegae.h

### Objective-C

```objc
#import <VponDataAnalytics/VponDataAnalytics.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    VDAConfiguration *config = [VDAConfiguration sharedInstance];
    [config setLicenseKey:@"testKey" withCustomID:@"customID" withOptIn:VDAOptInDefault];
    [config setDebugMode:NO];
    [config initialize];
}
```

### Swift

```swift
import VponDataAnalytics

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions:      
    [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        let config = VDAConfiguration.sharedInstance
        config.setLicenseKey("testkey", withCustomID: "customID", withOptIn: .default)
        config.setDebugMode(false)
        config.initialize()
}
```


## Send Data
Data SDK provides methods to send data in different scenarios:

### tracker.send()
tracker.send() can be used when a specific event is triggered. By using the tracker.send(), you can define a custom event that collects specific data. Please refer to the sample code below:


### Objective-C

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"item_view" extraData:@{@"id": @"payload", @"name": @"Coat", @"price": @(10), @"color": @"Blue", @"size": @"XL", @"tags": @"OrangeBear,fiber", @"currency": @"NTD"}];
[tracker send:builder];

```


### Swift

```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("item_view", extraData: ["id": "payload", "name": "Coat", "price": 10, "color": "Blue", "size": "XL", "tags": "OrangeBear,fiber", "currency": "NTD"])
tracker.send(builder)
```

Another example is that you want to collect the URL accessed by a user. Using tracker.send(), you can define another event to collect the data of previous URL and current URL accessed by a user.


### Objective-C

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"page_view" extraData:@{@"pervious": @"URL of Last Page", @"current": @"URL of Current Page"}];
[tracker send:builder];

```

### Swift

```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("page_view", extraData: ["pervious": "URL of Last Page", "current": "URL of Current Page"])
tracker.send(builder)
```


## Debug Mode
When you initilize Data SDK, you can enable debug mode with setDebugMode:Yes / setDebugMode(true). 


### Objective-C

```objc
#import <VponDataAnalytics/VponDataAnalytics.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    VDAConfiguration *config = [VDAConfiguration sharedInstance];
    ...
    [config setDebugMode:Yes];
    ...
}
```


### Swift

```swift
import VponDataAnalytics

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions:      
    [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        ...
        config.setDebugMode(true)
        ...
}
```

> **Note**：Set vpdataAnalytics.setDebugMode(false) before the App is launched.

## Sample Code
Please refer to [Sample Code](https://github.com/vpon-sdk/Vpon-iOS-Analytics) for a complete integration sample.

## Download

|Data SDK 2.0.0|
|:-------:|
|[Download][1]|

[1]: assets/download/i-vda-20201225-9fd4af0-v2.0.0.tar.gz


