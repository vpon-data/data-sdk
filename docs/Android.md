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

Welcome to the integration guide of Data SDK. You can leverage Data SDK in just several steps:
1. [Check the Prerequisites](#check-the-prerequisites)
2. [Download Data SDK](#download-data-sdk)
3. [Set up App Configurations](#set-up-app-configurations)
4. [Import Data SDK](#import-data-sdk)
5. [Initialize Data SDK](#initialize-data-sdk)
5. [Set Up Background Geolocation Collection](#set-up-background-geolocation-collection) (Optional)
5. [Set up Customized Events](#set-up-customized-events) (Optional)
6. [Test in Debug Mode](#debug-mode)

After completing steps 1 to 5, the minimum requirements, you can observe [Auto Events]({% link docs/AutoEvents.md %}) in your App.

Furthermore, set up [Customized Events](#set-up-customized-events) according to your App design and user focus in step 6. The event setting is flexible and even skippable. Nevertheless, we encourage you to set up suitable customized events to obtain a comprehensive picture of your App users.

Finally, check the integration status in step 7, [Debug Mode]({% link docs/DebugMode.md %}). Debug Mode helps you test the SDK setting before submitting your App to the App marketplaces. You can turn Debug Mode on in the step of Data SDK initialization, check all go well, and then turn it off in the same place to publish your App.

## Check the Prerequisites
Support version: Android 5.0 or later

## Download Data SDK 
Download Data SDK [HERE][1] and add the file to your Android Studio project.

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

### Add Permissions
In your `AndroidManifest.xml`, add the required permissions as below.
See [Permission]({% link docs/Permission.md %}) for more details.

```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
```

## Import Data SDK
Import `VpondataAnalytics` in your main Application or main Activity files. For example, MainApplication, MainActivity, or other core functions of your App.

```
import com.vpon.sdk.VpdataAnalytics;
```

## Initialize Data SDK
Initialize Data SDK in your main Application `onCreate()` method and main Activity `onCreate()` method separately to ensure [Auto Events]({% link docs/AutoEvents.md %}) functionality.
In addition, manage [License Key](#license-key), [Opt-in](#opt-in), and [Debug Mode](#debug-mode) switch in this step.

### License Key
You will receive a unique license key when your application is approved. See [Integration Process]({% link docs/IntegrationProcess.md %}) for more details.

If you are still waiting to receive it or get into trouble with it, please email Vpon Contact for further assistance.

### Opt-In
Data SDK is committed to protecting App user privacy. Therefore, Data SDK only collects data with user consent, which means Data SDK only gathers data under the condition that a user agrees to App terms of use or privacy policy.

To help you manage App user consent efficiently, Data SDK provides three Opt-In options: DEFAULT, CONSENT, and NOCONSENT.
- `DEFAULT`: the user has neither granted nor declined permission
- `CONSENT`: the user gives consent
- `NOCONSENT`: the user refuses to provide consent

We recommend determining the status of user consent in the initialization step. After that, update the Opt-In option automatically and forward it to Data SDK simultaneously, depending on the latest permission status.
Warning messages will display on the developer console if Opt-In is set either as `NOCONSENT` or `DEFAULT`.

Below is a setup example of License Key and Opt-in

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
Debug Mode allows you to interactively test your App events, including [Auto]({% link docs/AutoEvents.md %})  and [Customized](#set-up-customized-events), with messages displayed in the developer console.

We suggest enabling Debug Mode and providing Debug Mode log to Vpon Contact before submitting your App in Marketplaces to guarantee the integration correctness. See [Debug Mode]({% link docs/DebugMode.md %}) and [Integration Process]({% link docs/IntegrationProcess.md %}) for more details.

If all goes well, turn Debug Mode off and publish your App to the Marketplace.

Switch Debug Mode using the following codes

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

Combining all together, see a comprehensive example of Data SDK initialization.
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
        val vpdataAnalytics = VpdataAnalytic
	
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

## Set Up Background Geolocation Collection
Background Geolocation Collection is a powerful feature that allows your app to continuously gather geolocation data from users, even when your app is running in the background. By leveraging this feature, you can provide more personalized experiences and services to your users. However, it's crucial to strictly adhere to Google's guidelines and respect user privacy when implementing this feature​.

Before using this function, ensure that your project settings and permissions are properly set up. You can refer to the [Permission]({% link docs/Permission.md %}) section for more details on this.

To integrate the Background Geolocation Collection feature into your Android app, follow these steps:

1. Initialization: Make sure the Data SDK is properly initialized in your app before you start using the background geolocation collection feature.

2. Start/Stop Interface: Data SDK provides an interface that allows app developers to easily call and control the geolocation tracking. When calling the `startBackgroundLocationUpdate` method to begin collecting geolocation data, remember to set up the frequency for data collection as needed. Use the `stopBackgroundLocationUpdate` method to stop the data collection when it's no longer required.

3. Accuracy Level Configuration: The SDK allows you to set the level of accuracy for geolocation data collection. There are three options available: `high`, `mid`, and `low` accuracy respectively. Note that the accuracy level and the frequency of updates may affect the app's battery usage, so choose your settings carefully.

Here is a sample code snippet to use these methods:

{% tabs setup-background %}
{% tab setup-background java %}
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

{% tab setup-background kotlin%}
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

Once you have integrated the feature, you should test it to ensure it's working correctly. We recommend using the [Debug Mode]({% link docs/DebugMode.md %}) for this purpose. This mode allows you to interactively test your app events, including the geolocation collection, with messages displayed in the developer console.


## Set up Customized Events
If [Auto Events]({% link docs/AutoEvents.md %})  only partially fulfills your needs, Data SDK provides customized events to serve various App designs and meet your business focus.

By calling the tracker method, you can define your event name and any additional information you want to collect. It's flexible, and most importantly, no limit on the number of events.

For instance, an E-Commerce App wants to create a conversion funnel. Hence, recording users' views on which product item is essential. Using the tracker method, this EC App can quickly implement an `item_view` event that tracks a coat with id, size, color, price, etc...extra details.
Below are the sample codes and the final collected data.

{% tabs customized-event-android %}

{% tab customized-event-android Java %}
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

{% tab customized-event-android Kotlin %}

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
        } catch (JSONException e) {
            e.printStackTrace();
        }
        tracker?.sendEvent("item_view", payloadJsonObj);
    }
```
{% endtab %}

{% tab customized-event-android Collected Data in JSON %}
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

Another example is that an Online Travel Agency(OTA) App wants to observe the browsing history to optimize its user experience. Using the tracker method, the OTA App can set up a `page_view` event that traces the user journey.  

Below are the sample codes and the collected data.

{% tabs customized-event-android2 %}

{% tab customized-event-android2 Java %}
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

{% tab customized-event-android2 Kotlin %}
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

{% tab customized-event-android2 Collected Data in JSON %}
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

|Data SDK 2.0.4|
|:-------:|
|[Download][1]|

[1]: https://m.vpon.com/data/sdk/android/a-vda-obf-v2.0.4-20221020-57f65c7-148627.aar
