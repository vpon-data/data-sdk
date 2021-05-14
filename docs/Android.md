---
layout: default
title:          "SDK-Android"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /android
lang:           "en"
---

# Android SDK
---

## Prerequisites
Data SDK support version:

* Android：`Android 5.0 or later`


### Prepare for Data SDK import
You can [download Data SDK here][1] and import the file into your Android Studio project.

Open `build.gradle` in App-level, modify dependencies as below:

```xml
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar', '*.aar'])
    ...
    implementation 'com.google.android.gms:play-services-ads-identifier:17.0.0'

    //coroutines
    implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core:1.3.9'
    implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.3.9'
}
```

## Permission
Please add the Permissions below in your `AndroidManifest.xml`

(Required) Please add below premissions for basic data collection:

```xml
<!-- Required permissions -->
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
```

(Optional) Please add below permissions for advanced data collection and data analysis:

```xml
<!-- Optional permissions -->
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
```

## Import Data SDK
Please import VpondataAnalytics as below

```java
import com.vpon.sdk.VpdataAnalytics;
```

## Initialize Data SDK

Declare VpdataAnalytics and setup License Key & Opt-In in this step. 

#### License Key
You should receive a unique license key when your application is approved. If you do not receive it, please email it to Vpon Contact.


#### Opt-In
To manage user consent in your App, Data SDK provides three Opt-In options: DEFAULT, CONSENT, and NOCONSENT. DEFAULT indicates the user has neither granted nor declined consent, CONSENT indicates the user gives his/her consent, and NOCONSENT indicates the user refuses to give his/her consent. Please refer to the sample code below:

```
// Opt-In options: 
// VpdataAnalytics.OptIn.DEFAULT 
// VpdataAnalytics.OptIn.CONSENT
// VpdataAnalytics.OptIn.NOCONSENT

// Opt-In is setup as VpdataAnalytics.OptIn.DEFAULT by default  

// If a user gives his/her consent, configure Opt-In as CONSENT 
vpdataAnalytics.initialize(this, licenseKey, customerId, VpdataAnalytics.OptIn.CONSENT)

//If a user refuse to give his/her consent, configure Opt-In as NOCONSENT
vpdataAnalytics.initialize(this, licenseKey, customerId, VpdataAnalytics.OptIn.NOCONSENT)

```

If a user gives his/her consent, you should configure Opt-In as CONSENT. If a user refuses to give his/her consent, you should configure Opt-In as NOCONSENT and should NOT send data to Vpon. Data SDK will display warning messages on the developer console if Opt-In is set either as  NOCONSENT or DEFAULT.

It is recommended that you determine the status of a user's consent at every app launch. After that, update the Opt-In value and forward it to Data SDK simultaneously according to the user's latest consent status. 

If a user changes his/her consent status, for example, from provides the consent to declines the consent, your App must automatically update the Opt-In value from CONSENT to NOCONSENT and then forward the status to Data SDK.

Below is an example to initialize Data SDK with users' explicit authorization:


```java
public class MainActivity extends Activity {

    // TODO set your licenseKey & customerId
    private String licenseKey = "mock_license_key";
    private String customerId = "";

    private VpdataAnalytics vpdataAnalytics;

    private VpdataAnalytics.Tracker tracker = null;

    private final int PERMISSION_REQUEST_CODE = 2001;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Request optional permission
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            requestPermissions(new String[]{ACCESS_FINE_LOCATION, ACCESS_COARSE_LOCATION, READ_PHONE_STATE}, PERMISSION_REQUEST_CODE);
        }

        vpdataAnalytics = VpdataAnalytics.INSTANCE;

        // Set true to enable debug mode, set false before app release
        // Set up before vpdataAnalytics.initialize
        vpdataAnalytics.setDebugMode(false);
	
	
        // Set up license_key and opt-in
	// If a user gives his/her consent, configure Opt-In as CONSENT 
        vpdataAnalytics.initialize(this, licenseKey, customerId, VpdataAnalytics.OptIn.CONSENT);
        
        // Construct a Tracker for sending event
        tracker = new VpdataAnalytics.Tracker();
    }
}

```

## Send Data
Data SDK provides tracker.sendEvent() method to send data in different scenarios.

By using the tracker.sendEvent(), you can define a custom event that collects specific data. For example, you can define an onClick() event when a user clicks an item. Please refer to the sample code below:


```java
public void onClick(View v) {
	JSONObject payloadJsonObj = new JSONObject();
	try {
		payloadJsonObj.put("id", "payloadJsonObj");
		payloadJsonObj.put("name", "Coat");
		payloadJsonObj.put("price", 100);
		payloadJsonObj.put("color", "Blue");
		payloadJsonObj.put("size", "XL");
		payloadJsonObj.put("tags", "OrangeBear,fiber");
		payloadJsonObj.put("currency", "NTD");
		} catch (JSONException e) {
		e.printStackTrace();
	        }
	tracker.sendEvent("item_view", payloadJsonObj);
        }
}
```
Another example is that you want to collect the URL accessed by a user. Using tracker.sendEvent(), you can define another onClick() event to collect the data of the previous URL and current URL accessed by a user.

```java
public void onClick(View v) {
	JSONObject payloadJsonObj = new JSONObject();
	try {
		payloadJsonObj.put("pervious", "URL of Last Page");
		payloadJsonObj.put("current", "URL of Current Page");
	} catch (JSONException e) {
		e.printStackTrace();
	}
	tracker.sendEvent("page_view", payloadJsonObj);
}
```


## Debug Mode
When you initialize Data SDK, you can enable debug mode with vpdataAnalytics.setDebugMode(true) to check SDK integration status.

```java

VpdataAnalytics vpdataAnalytics = VpdataAnalytics.INSTANCE;

vpdataAnalytics.setDebugMode(true);
// Set true to enable Debug Mode, remember to disable this setting before app release!
// Must be set before vpdataAnalytics.initialize()

vpdataAnalytics.initialize(this, licenseKey, customerId, VpdataAnalytics.OptIn.DEFAULT);
```
> **Note**：Set vpdataAnalytics.setDebugMode(false) before the App is launched.

## Sample Code
Please refer to our [Sample Code](https://github.com/vpon-sdk/Vpon-Android-Analytics) for a complete integration.

## Download

|Data SDK 2.0.2|
|:-------:|
|[Download][1]|

[1]: https://m.vpon.com/data/sdk/android/vpon-analytics-sdk-obf202-32401202-2104231437-c31526e.aar 
