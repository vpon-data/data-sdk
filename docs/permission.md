---
layout: default
title:          "Permission"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /permission
lang:           "en"
---

**Permission**

Vpon Data SDK requires very limited permissions from App users. Based on the collected data type, all we need are geolocation and network permissions. 

![](docs/images/permission.png)

The details are shown as follows:

**Android**
* geolocation: 
    * ACCESS_COARSE_LOCATION or ACCESS_FINE_LOCATION
* network:
    * ACCESS_NETWORK_STATE
    * ACCESS_WIFI_STATE
    * CHANGE_WIFI_STATE
    * READ_PHONE_STATE

**iOS**

* geolocation:
  * Need Location Authority
  * Add LocationUsageDescription: 
    +NSLocationAlwaysAndWhenInUseUsageDescription
    +NSLocationUsageDescription
    +NSLocationWhenInUseUsageDescription
* network:
  * Add LocationUsageDescription: 
    +NSLocationAlwaysAndWhenInUseUsageDescription
    +NSLocationUsageDescription
    +NSLocationWhenInUseUsageDescription
  * Enable "Access WiFi Information" in ProjectSetting on iOS 12 and later versions"
