---
layout: default
title:          "opt-out-ios"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:       /opt-out-ios
lang:           "en"
---

# iOS IDFA opt-out setting instructions
---

From iOS 10 to iOS 13, iOS devices offer two functions related to privacy protection. The first is to Limit Ad Tracking (LAT), while the second is to Reset Advertising Identifier (IDFA).

Please follow the below steps to access **Limit Ad Tracking** and  **Reset Advertising Identifier :** 
Go to Setting→Privacy→Advertising: **Limit Ad Tracking** and **Reset Advertising Identifier** are shown

**Limit Ad Tracking (LAT)**  
If you turn off **Limit Ad Tracking**, you agree that Apps track your IDFA and/or provide personalized Ads to you. On the other hand, if you turn on **Limit Ad Tracking**, you disagree that Apps track your IDFA and/or provide personalized Ads to you.

**Reset Advertising Identifier**  
Click **Reset Advertising Identifier** to reset your IDFA. 

<img src="/docs/images/LAT_1.png" alt="drawing" width="200" height="350"/> <img src="/docs/images/LAT_2.png" alt="drawing" width="200" height="350"/>


**LAT → ATT**  
Starting from iOS 14, instead of Limit Ad Tracking (LAT), Apple provides App Tracking Transparency (ATT) framework to manage App’s permission to track your IDFA. 

When you first launch an App that implemented ATT framework, a pop-out window will ask your permission for tracking your activity across Apps and webs. If you click “Ask App Not to Track,” the App can't track your IDFA and/or provide personalized Ads to you. On the other hand, if you click “Allow,” the App can track your IDFA and/or provide personalized Ads to you.

In the Setting→Privacy→Advertising page, you can also manage App tracking permissions in **Allow Apps to Request to Track**. If you turn off **Allow Apps to Request to Track**, all Apps are not allowed to track your device, and no more ATT pop-out window will be displayed once you chose to turn off . On the other hand, if you turn on **Allow Apps to Request to Track**, you can decide to give tracking permission to different Apps.

**Reset Advertising Identifier**  
Turn off **Allow Apps to Request to Track**, and turn it on will reset IDFA.

<img src="/docs/images/ATT_1.png" alt="drawing" width="200" height="350"/> <img src="/docs/images/ATT_2.png" alt="drawing" width="200" height="350"/>

 
