# Introduction to Location Kit

## Scenario Overview

Mobile terminal devices have become deeply integrated into various aspects of people's daily lives, such as checking local weather, news stories, ride-hailing, travel navigation, and fitness tracking. These commonplace activities all rely on locating the user's terminal device.

When users engage in these diverse scenarios, the system's location capabilities can provide real-time and accurate position data. For developers, designing services with location-based experiences can make applications more tailored to each user's needs.

When implementing device location-based features—such as driving navigation or recording exercise routes—applications can call this module's APIs to obtain location information.

## Basic Concepts

The location subsystem utilizes multiple positioning technologies to provide services, including GNSS positioning, cell tower positioning, and WLAN/Bluetooth positioning (the latter two are collectively referred to as "network positioning technologies"). These technologies enable accurate device location determination, whether indoors or outdoors.

In addition to basic positioning services, Location Kit offers functionalities and interfaces such as geofencing, geocoding, reverse geocoding, and country code support.

- **Coordinates**  
  The system uses the World Geodetic System 1984 (WGS84) as a reference, employing longitude and latitude data to describe a location on Earth.

- **GNSS Positioning**  
  Based on global navigation satellite systems, including GPS, GLONASS, BeiDou, and Galileo, this method determines a device's precise location through algorithms provided by navigation satellites and device chips. The specific positioning systems used depend on the hardware capabilities of the user's device.

- **Cell Tower Positioning**  
  Estimates the device's current location based on the positions of its connected and neighboring cell towers. This method offers relatively lower accuracy and requires the device to have access to a cellular network.

- **WLAN and Bluetooth Positioning**  
  Estimates the device's current location by detecting surrounding WLAN and Bluetooth devices. The accuracy of this method depends on the distribution of fixed WLAN and Bluetooth devices nearby. Higher density yields better accuracy compared to cell tower positioning, but it also requires network access.

## Constraints and Limitations

As a fundamental service provided by the system, location capabilities require applications to actively initiate requests during relevant business scenarios and terminate them when the scenarios conclude. During this process, the system reports real-time positioning results to the application.

Using the device's location capabilities requires user confirmation and manual activation of the location switch. If the location switch is off, the system will not provide positioning services to any application.

Device location information is sensitive user data. Even if the location switch is enabled, applications must request location access permission from users. The system only provides positioning services after user approval.

Location Kit offers varying capabilities across different devices, with some functionalities dependent on hardware support. For example, devices with GPS or BeiDou positioning chips can utilize GNSS positioning, while devices without such chips but equipped with WLAN or cellular networks can access WLAN or cell tower positioning capabilities.