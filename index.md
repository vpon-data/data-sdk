---
layout: default
title:          "Data SDK"
lead:           ""
description:    ""
keywords:       "datasdk"
permalink:      /
lang:           "en"
---

# Overview

Welcome to the developer's guide for Vpon Data Software Development Kit (**Data SDK**)! This comprehensive guide provides all the information developers need when embedding our SDK into iOS and Android mobile Apps. Here, you'll find detailed implementation guides, requirements, and sample codes to help you through the integration process.

## Data SDK Workflow

The general workflow of Data SDK includes three primary steps:

### 1. Event Triggering
Data SDK starts collecting data based on specific events. These events could be automatic, like launching the App, or customized to suit the specific needs of your App. In addition, the SDK can continuously collect geolocation data in the background. For more information about the different types of events and when to use them, please refer to our [Event]({%link docs/Event.md %}) page.

### 2. Data Collection
When an event is triggered, the SDK collects relevant device-based data, adhering to the same schema even for background geolocation collection. More details about data collection can be found in our [Data Collection](https://datasdk.vpon.com/introduction/data-collection) section.

### 3. Data Encryption and Transmission
After collection, the SDK encrypts the data to ensure its security and then sends it to the server for further analysis and application.

The whole process is designed to be efficient and secure, providing valuable data for you to better understand your users and improve the overall user experience.

![](/docs/images/Overview.png) 

## Next Steps

Ready to start integrating the Data SDK into your App? Head over to our 
[Integration Process]({% link docs/IntegrationProcess.md %}) page, which guides you step by step through the entire integration process. For any business-side queries, please visit our [official website][1] for further information.

Remember, a successful Data SDK integration can unlock valuable insights into your users' behavior, enhancing your App's performance, personalization, and overall user experience. Get started today!

[1]: https://datasdk.vpon.com/