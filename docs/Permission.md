---
layout: default
title:          "Permission"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /permission
lang:           "en"
---

# Permission
---

Vpon Data SDK requires very limited permissions from App users. 

The basic requirements are Network and Wi-Fi permissions to enable data collection in devices.  

Geolocation permission is optional according to your App type.

![](docs/images/permission.png)

The permission setup details are shown as follows:

**Android**
* network:
    * ACCESS_NETWORK_STATE
    * ACCESS_WIFI_STATE
    * CHANGE_WIFI_STATE
    * READ_PHONE_STATE
* geolocation: 
    * ACCESS_COARSE_LOCATION or ACCESS_FINE_LOCATION

**iOS**
* network:
  * Add LocationUsageDescription: 
    * +NSLocationAlwaysAndWhenInUseUsageDescription
    * +NSLocationUsageDescription
    * +NSLocationWhenInUseUsageDescription
  * Enable "Access WiFi Information" in ProjectSetting on iOS 12 and later versions"
* geolocation:
  * Need Location Authority
  * Add LocationUsageDescription: 
    * +NSLocationAlwaysAndWhenInUseUsageDescription
    * +NSLocationUsageDescription
    * +NSLocationWhenInUseUsageDescription
