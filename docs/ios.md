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
Please follow the instructions to send data.

NOTE: extraData is optional. If you want to collect data when a specific event is triggered, please call send() and use extraData to collect that data.


### Objective-C

```objc
VDATracker *tracker = [[VDATracker alloc] init];
VDABuilder *builder = [VDABuilder createEventWithEventName:@"login" extraData:@{@"key": @"value"}];
[tracker send:builder];
```


### Swift

```swift
let tracker = VDATracker()
let builder = VDABuilder.createEventWithEventName("login", extraData: ["key": "value"])
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
