---
layout: default
title:          "SDK-Android"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /android
lang:           "en"
---

# Prerequisites
---
Data SDK support version:

* Android：`Android 5.0 or later`


### Prepare for Data SDK import
You can [download Data SDK here][1] and import the file into your Android Studio project.

Open build.gradle in App-level, modify dependencies as below:

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

### Permission
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


# Start To Implement Data SDK
---
Please follow the steps to integrate Data SDK.

### Import Data SDK

```java
import com.vpon.sdk.VpdataAnalytics;
```

### Declare VpdataAnalytics and Indicate License Key and Custom ID

```java
public class MainActivity extends Activity {

    // TODO set your licenseKey & customerId
    private String licenseKey = "mock_license_key";
    private String customerId = "mock_custom_id";

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

        vpdataAnalytics.initialize(this, licenseKey, customerId);

        // Construct a Tracker for sending event
        tracker = new VpdataAnalytics.Tracker();
    }
}

```




### Send Data
Data SDK provides methods to send data in different scenarios:

#### tracker.sendEvent()
tracker.sendEvent() can be used when a specific event is triggered. 
By using the tracker.sendEvent(), you can define a custom event that collects specific data. For example, you can define a onClick() event when a user clicks a item. Please refer to the sample code below:

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

Another example is that you want to collect the URL accessed by a user. Using tracker.sendEvent(), you can define another onClick() event to collect the data of previous URL and current URL accessed by a user.

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


# Debug Mode
---
When you initilize Data SDK, you can enable debug mode with vpdataAnalytics.setDebugMode(true).


```java

VpdataAnalytics vpdataAnalytics = VpdataAnalytics.INSTANCE;

vpdataAnalytics.setDebugMode(true);
// Set true to enable Debug Mode, remember to disable this setting before app release!
// Must be set before vpdataAnalytics.initialize()

vpdataAnalytics.initialize(this, licenseKey, customerId);
```
> **Note**：Set vpdataAnalytics.setDebugMode(false) before the App is launched.

# Sample Code
Please refer to our [Sample Code](https://github.com/vpon-sdk/Vpon-Android-Analytics) for a complete integration sample.

# Download
---

|Data SDK 2.0.0|
|:-------:|
|[Download][1]|


[1]: assets/download/vpon-data-sdk-v200-release.aar
