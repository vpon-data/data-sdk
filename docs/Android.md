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

Welcome to your comprehensive guide to integrating the Data SDK!

With our streamlined process, you can equip your App with powerful features, such as Auto, Custom Events and Background Geolocation Collection, in a few straightforward steps:

1. [Check the Prerequisites](#check-the-prerequisites)
2. [Download Data SDK](#download-data-sdk)
3. [Set up App Configurations](#set-up-app-configurations)
4. [Import Data SDK](#import-data-sdk)
5. [Initialize Data SDK](#initialize-data-sdk)
5. [Set up Background Geolocation Collection](#set-up-background-geolocation-collection) (Optional)
5. [Set up Custom Events](#set-up-custom-events) (Optional)
6. [Test in Debug Mode](#debug-mode)

Upon completing steps 1 to 5, you'll have fulfilled the minimum requirements and enabled [Auto Events]({% link docs/Event.md %}#1-auto-events) tracking in your App.

Step 6 involves the optional setup of [Background Geolocation Collection]({% link docs/BackgroundGeolocation.md %}). This powerful feature allows continuous gathering of geolocation data from users, even when your App runs in the background, to provide more personalized experiences and services.

Step 7 allows you to set up [Custom Events]({% link docs/Event.md %}#2-custom-events)according to your App's design and user needs. While optional, we highly recommend creating suitable custom events to obtain a comprehensive view of your App users.

Lastly, in step 8, use the [Debug Mode]({% link docs/DebugMode.md %} ) to verify your integration status. Debug Mode facilitates testing of all SDK configurations, including Background Geolocation Collection, Auto & Custom events, before launching your App on various platforms. We recommend enabling Debug Mode to ensure everything is functioning as expected, and then disabling it before your App's publication.

This guide is designed to make the integration process intuitive and efficient, letting you focus on building and enhancing your App.

## Check the Prerequisites
Ensure that your App supports Android version `5.0 or later` before proceeding with the Data SDK integration.

## Download Data SDK 
Start by downloading the Data SDK [HERE][1]. Once downloaded, include the `aar` file in your  Android Studio project.

## Set up App Configurations
### Build dependencies 
In your module (app-level) Gradle file (usually `<project>/<app-module>/build.gradle` ), modify dependencies as below.

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

If you choose to activate background geolocation data collection, also add Google Play Service Location dependency
```xml
dependencies {
    ...
    //for background gelocation collection
    implementation 'com.google.android.gms:play-services-location:21.0.1'
}
```    


### Adjust Permissions
To ensure the maximum functionality of the Data SDK, it's essential to modify your `AndroidManifest.xml` file to include specific permissions. Here's the suggested way to do it:

#### Required Permissions
These permissions are necessary for the SDK to operate effectively. Make sure to include these in your `AndroidManifest.xml`:
```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
```

#### Recommended Additional Permissions
We recommend adding these additional permissions to your `AndroidManifest.xml` file to enable data collection for network information and geolocation:
```xml
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
```
While these permissions are technically optional, adding them is strongly advised to take full advantage of the SDK's features.

#### Background Geolocation Permission
If you choose to activate background geolocation data collection, add this optional permission:
```xml
<uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION"/>
```

For more details about these permissions, refer to the [Permission]({% link docs/Permission.md %}).


## Import Data SDK
Import `VpondataAnalytics` in your main Application or main Activity files. For example, MainApplication, MainActivity, or other core functions of your App. You can do this using either `Java` or `Kotlin`.

{% tabs import-android %}

{% tab import-android Java %}

```java
import com.vpon.sdk.VpdataAnalytics;
```
{% endtab %}

{% tab import-android Kotlin %}
```kotlin
import com.vpon.sdk.VpdataAnalytics
```
{% endtab %}

{% endtabs %}


## Initialize Data SDK
Initialize Data SDK in your main Application `onCreate()` method and main Activity `onCreate()` method separately. This ensures the Auto Events feature operates correctly.

You'll also manage the [License Key](#license-key), [Opt-in](#opt-in), and [Debug Mode](#debug-mode) in this step.


### License Key
Upon approval of your application, you'll receive a unique license key. If you encounter any issues or haven't received your key, please refer to the [Integration Process]({% link docs/IntegrationProcess.md %}) for further details or email Vpon’s support team for additional support.

### Opt-In
Data SDK respects user privacy by only collecting data with the user's explicit consent, meaning data is gathered only when a user agrees to your App's terms of use or privacy policy.

To help you manage this consent effectively, Data SDK offers three Opt-In options: `DEFAULT`, `CONSENT`, and `NOCONSENT`.
- `DEFAULT`: neither granted nor declined
- `CONSENT`: granted
- `NOCONSENT`: declined

We recommend determining the status of user consent in the initialization step, then updating the Opt-In option and forwarding it to Data SDK depending on the latest permission status. If Opt-In is set to either `NOCONSENT` or `DEFAULT`, warning messages will display on the developer console.

Here's a setup example of License Key and Opt-in:
{% tabs lic-android %}

{% tab lic-android Java %}
```java
vpdataAnalytics.initialize(this, licenseKey, customerId, VpdataAnalytics.OptIn.CONSENT);
```
{% endtab %}

{% tab lic-android Kotlin %}
```kotlin
vpdataAnalytics!!.initialize(this, licenseKey, customerId, VpdataAnalytics.OptIn.CONSENT)
```
{% endtab %}

{% endtabs %}

### Debug Mode
Debug Mode allows you to interactively test your App events, including Auto, Custom, and Background Geolocation Collection.

We recommend enabling Debug Mode and providing the Debug Mode log to Vpon Vpon’s support team before submitting your App to various marketplaces, ensuring correct integration settings. If everything is working as expected, disable Debug Mode before publishing your App.

For more detailed information, you can refer to the sections on [Debug Mode]({% link docs/DebugMode.md %}) and [Integration Process]({% link docs/IntegrationProcess.md %}).

Here's how to toggle Debug Mode:
{% tabs debug-android %}

{% tab debug-android Java %}
```
// Turn Debug Mode on
vpdataAnalytics.setDebugMode(true);

// Turn Debug Mode off
vpdataAnalytics.setDebugMode(false);
```
{% endtab %}

{% tab debug-android Kotlin %}
```
// Turn Debug Mode on
vpdataAnalytics!!.setDebugMode(true)

// Turn Debug Mode off
vpdataAnalytics!!.setDebugMode(false)
```
{% endtab %}

{% endtabs %}

Here's a complete example that demonstrates how to initialize the Data SDK:
#### In your main Application

{% tabs all-application-android %}

{% tab all-application-android Java %}
```java
// Opt-In options: 
// VpdataAnalytics.OptIn.DEFAULT 
// VpdataAnalytics.OptIn.CONSENT
// VpdataAnalytics.OptIn.NOCONSENT

// Debug Mode options: true/false

public class MainApplication extends Application {
    // Set your license_key & customer_id
    private String licenseKey = "testKey";
    private String customerId = "";

    // Configure Opt-In as VpdataAnalytics.OptIn.CONSENT when a user gives consent
    // Turn Debug Mode on
    @Override
    public void onCreate() {
        super.onCreate();
        VpdataAnalytics vpdataAnalytics = VpdataAnalytics.INSTANCE;

        // Set up before vpdataAnalytics.initialize
        vpdataAnalytics.setDebugMode(true);

        // Set up license_key and opt-in
    	// If a user gives their consent, configure Opt-In as CONSENT
        vpdataAnalytics.initialize(this, licenseKey, customerId, VpdataAnalytics.OptIn.CONSENT);  
    }
}
```
{% endtab %}

{% tab all-application-android Kotlin %}
```kotlin
// Opt-In options: 
// VpdataAnalytics.OptIn.DEFAULT 
// VpdataAnalytics.OptIn.CONSENT
// VpdataAnalytics.OptIn.NOCONSENT

// Debug Mode options: true/false

class MainApplication : Application() {
    // set up your license_key & customer_id
    private val licenseKey = "testKey"
    private val customerId = ""
    
    // Configure Opt-In as VpdataAnalytics.OptIn.CONSENT when a user gives consent
    // Turn Debug Mode on
    override fun onCreate() {
        super.onCreate()
        val vpdataAnalytics = VpdataAnalytics
	
        // Set up before vpdataAnalytics.initialize
        vpdataAnalytics!!.setDebugMode(true)
	
        // Set up license_key and opt-in
        vpdataAnalytics!!.initialize(this, licenseKey, customerId, VpdataAnalytics.OptIn.CONSENT)
    }
}
```
{% endtab %}

{% endtabs %}

#### In your main Activity

{% tabs all-activity-android %}

{% tab all-activity-android Java %}
```java
public class MainActivity extends Activity {
    private VpdataAnalytics.Tracker tracker = null;
    private final int PERMISSION_REQUEST_CODE = 2001;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Request permissions
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            requestPermissions(new String[]{ACCESS_FINE_LOCATION, ACCESS_COARSE_LOCATION,READ_PHONE_STATE}, PERMISSION_REQUEST_CODE);
        }
	
        // Construct a Tracker for sending event
        tracker = new VpdataAnalytics.Tracker();
    }
}
```
{% endtab %}

{% tab all-activity-android Kotlin %}
```kotlin
class MainActivity : Activity() {
    private var tracker: VpdataAnalytics.Tracker? = null
    private val PERMISSION_REQUEST_CODE = 2001
    
    override fun onCreate(savedInstanceState: Bundle) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
	
        // Request optional permission
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            requestPermissions(arrayOf(ACCESS_FINE_LOCATION, ACCESS_COARSE_LOCATION, READ_PHONE_STATE), PERMISSION_REQUEST_CODE)
        }

        // Construct a Tracker for sending event
        tracker = VpdataAnalytics.Tracker()
    }
}
```
{% endtab %}

{% endtabs %}

## Set up Background Geolocation Collection
Background Geolocation Collection is a powerful feature that allows continuous geolocation data collection, even when your App is running in the background. However, it's essential to respect user privacy and adhere to Google's guidelines when implementing this feature.

Before using this function, ensure that your project settings and permissions are properly set up. You can refer to the [Background Geolocation Collection]({% link docs/BackgroundGeolocation.md %}) and [Permission]({% link docs/Permission.md %}) sections for more details on this.

To integrate the Background Geolocation Collection feature into your Android App, follow these steps:

1. Initialization: Make sure the Data SDK is properly initialized in your App before you start using the background geolocation collection feature.

2. Start/Stop Interface: Data SDK provides an interface that allows App developers to easily call and control the geolocation tracking. When calling the `startBackgroundLocationUpdate` method to begin collecting geolocation data, remember to set up the frequency for data collection as needed. Use the `stopBackgroundLocationUpdate` method to stop the data collection when it's no longer required.

3. Accuracy Level Configuration: The SDK allows you to set the level of accuracy for geolocation data collection. There are three options available: `high`, `mid`, and `low` accuracy respectively. Note that the accuracy level and the frequency of updates may affect the App's battery usage, so choose your settings carefully.

Here is a sample code snippet to use these methods:

{% tabs setup-background-Android %}

{% tab setup-background-Android java %}
```java
// to start geolocation collection with mid accuracy
VpdataAnalytics.INSTANCE.startBackgroundLocationUpdate(VpdataAnalytics.Frequency.MID);

// to stop geolocation collection
VpdataAnalytics.INSTANCE.stopBackgroundLocationUpdate();

// three accuracy options: high/mid/low
// high accuracy 
VpdataAnalytics.INSTANCE.startBackgroundLocationUpdate(VpdataAnalytics.Frequency.HIGH);
// mid accuracy
VpdataAnalytics.INSTANCE.startBackgroundLocationUpdate(VpdataAnalytics.Frequency.MID);
// low accuracy
VpdataAnalytics.INSTANCE.startBackgroundLocationUpdate(VpdataAnalytics.Frequency.LOW);
```
{% endtab %}

{% tab setup-background-Android kotlin%}
```kotlin
// to start geolocation collection with mid accuracy
VpdataAnalytics.startBackgroundLocationUpdate(VpdataAnalytics.Frequency.MID)

// to stop geolocation collection
VpdataAnalytics.stopBackgroundLocationUpdate()

// three accuracy options: high/mid/low
// high accuracy 
VpdataAnalytics.startBackgroundLocationUpdate(VpdataAnalytics.Frequency.HIGH)    
// mid accuracy
VpdataAnalytics.startBackgroundLocationUpdate(VpdataAnalytics.Frequency.MID)
// low accuracy
VpdataAnalytics.startBackgroundLocationUpdate(VpdataAnalytics.Frequency.LOW)
```
{% endtab %}

{% endtabs %}

Once you have integrated the feature, you should test it to ensure it's working correctly. We recommend using the [Debug Mode]({% link docs/DebugMode.md %}) for this purpose. This mode allows you to interactively test your App events, including the geolocation collection, with messages displayed in the developer console.


## Set up Custom Events
Custom events are a powerful tool to gain insights into user behavior, and Data SDK makes it simple to set them up.

By utilizing the `tracker` method, you can set up events that carry unique names and contain additional data you wish to gather. The strength of this feature lies in its flexibility - there's no cap on the number of events you can set up, making it adaptable to your App's specific design and business goals.

Below, you will find examples of how to set up these custom events, along with representations of how the collected data may appear in a JSON string format on a mobile device. It's crucial to note that this data is encrypted for user privacy and cannot be directly accessed via the App developer console.

Let's consider an example where you're running an e-commerce App and you want to establish a conversion funnel. In this case, tracking user interactions with various product items becomes essential. By leveraging the tracker method, you can swiftly set up an `item_view` event that collects details such as the product's ID, size, color, and price.


{% tabs custom-event-android %}

{% tab custom-event-android Java %}
```java
public void onClick(View v) {
	JSONObject payloadJsonObj = new JSONObject();
	try {
		payloadJsonObj.put("id", "payloadJsonObj");
		payloadJsonObj.put("name", "Coat");
		payloadJsonObj.put("price", 100);
		payloadJsonObj.put("color", "Blue");
		payloadJsonObj.put("size", "XL");
		payloadJsonObj.put("currency", "NTD");
		} catch (JSONException e) {
		e.printStackTrace();
	    }
	tracker.sendEvent("item_view", payloadJsonObj);
}
```
{% endtab %}

{% tab custom-event-android Kotlin %}

```kotlin
val sendClickListener = View.OnClickListener {
        val payloadJsonObj = JSONObject();
        try {
            payloadJsonObj.put("id", "payloadJsonObj");
            payloadJsonObj.put("name", "Coat");
            payloadJsonObj.put("price", 100);
            payloadJsonObj.put("color", "Blue");
            payloadJsonObj.put("size", "XL");
            payloadJsonObj.put("currency", "NTD");
        } catch (e: JSONException) {
            e.printStackTrace();
        }
        tracker?.sendEvent("item_view", payloadJsonObj);
    }
```
{% endtab %}

{% tab custom-event-android Collected Data in JSON %}
```json
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

Similarly, if you're operating an Online Travel Agency (OTA) App and want to optimize the user experience by understanding their browsing history, the tracker method can assist. It enables the configuration of a `page_view` event, tracing the user's navigation journey through your App.

{% tabs custom-event-android2 %}

{% tab custom-event-android2 Java %}
```java
public void onClick(View v) {
	JSONObject payloadJsonObj = new JSONObject();
	try {
		payloadJsonObj.put("previous", "URL of Last Page");
		payloadJsonObj.put("current", "URL of Current Page");
	} catch (JSONException e) {
		e.printStackTrace();
	}
	tracker.sendEvent("page_view", payloadJsonObj);
}
```
{% endtab %}

{% tab custom-event-android2 Kotlin %}
```kotlin
val sendClickListener = View.OnClickListener {
        val payloadJsonObj = JSONObject()
        try {
            payloadJsonObj.put("pervious", "URL of Last Page")
            payloadJsonObj.put("current", "URL of Current Page")
        } catch (e: JSONException) {
            e.printStackTrace()
        }
        tracker?.sendEvent("page_view", payloadJsonObj)    
    }
```
{% endtab %}

{% tab custom-event-android2 Collected Data in JSON %}
```json
{
    "event_name": "page_view"
    "previous": "URL of Last Page", 
    "current": "URL of Current Page"
}
```
{% endtab %}

{% endtabs %}

## Sample Code
See also [Sample Code](https://github.com/vpon-sdk/Vpon-Android-Analytics) for a complete integration reference.

## Download

|Data SDK 2.0.5|
|:-------:|
|[Download][1]|

[1]: https://m.vpon.com/data/sdk/android/a-vda-obf-v2.0.5-20230630-30a0423-670651.aar