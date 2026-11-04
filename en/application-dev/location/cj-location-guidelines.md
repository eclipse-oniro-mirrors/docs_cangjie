# Development Guide for Obtaining Device Location Information

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Scenario Overview

Developers can call location-related interfaces to obtain the device's real-time location or recent historical location, as well as monitor changes in the device's location.

For applications with location-sensitive business logic, it is recommended to obtain the device's real-time location information. If real-time location information is not required and the goal is to minimize power consumption, developers may consider obtaining the most recent historical location instead.

## Interface Description

The following interfaces are used to obtain device location information. For detailed descriptions, refer to: [Location Kit](../reference/LocationKit/cj-apis-geo_location_manager.md).

This module's capabilities only support the WGS-84 coordinate system.

| Interface Name | Function Description |
| -------- | -------- |
| [on(CallbackType, LocationRequest, Callback1Argument\<Location>)](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-oncallbacktype-locationrequest-callback1argumentlocation) | Subscribe to location changes and initiate a location request. |
| [off(CallbackType, Callback1Argument\<Location>)](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-offcallbacktype-callback1argumentlocation) | Unsubscribe from location changes and remove the corresponding location request. |
| [getCurrentLocation()](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocation) | Get the current location. |
| [getCurrentLocation(CurrentLocationRequest)](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocationcurrentlocationrequest) | Get the current location. |
| [getCurrentLocation(SingleLocationRequest)](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocationsinglelocationrequest) | Get the current location. |
| [getLastLocation()](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getlastlocation) | Get the most recent location result. |
| [isLocationEnabled()](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-islocationenabled) | Check whether the location service is enabled. |

## Development Steps

1. To obtain device location information, location permissions are required. For methods and steps to request location permissions, refer to [Development Guide for Requesting Location Permissions](cj-location-permission-guidelines.md).

2. Import the `geoLocationManager` module. All APIs related to basic location capabilities are provided through this module.

    <!-- compile -->

    ```cangjie
    import kit.LocationKit.*
    ```

3. Before calling the location acquisition interfaces, check whether the location switch is turned on. Query the current status of the location switch, which returns a boolean value: `true` indicates the location switch is on, and `false` indicates it is off. Example code:

    <!-- run -->

    ```cangjie
    import kit.LocationKit.*
    import kit.ArkUI.*

    try {
        let locationEnabled = GeoLocationManager.isLocationEnabled()
    } catch (err: BusinessException) {
        Hilog.error(1, "info", "errCode: ${err.code}, message: ${err.message}")
    }
    ```

    If the location switch is not turned on, you can trigger a global settings dialog to guide users to enable the location switch. For details, refer to [Triggering the Global Settings Dialog](../reference/AbilityKit/cj-apis-ability_access_ctrl.md#func-requestglobalswitchcontext-switchtype-asynccallbackbool).

4. Obtain the current device location once. Commonly used for scenarios such as checking the current location, check-ins, and service recommendations.
    - Get the current location.<br/>

        First, instantiate the [SingleLocationRequest](../reference/LocationKit/cj-apis-geo_location_manager.md#class-singlelocationrequest) object to inform the system about the type of location service to provide to the application and the timeout duration for single location requests.<br/>

        - Set `LocatingPriority`:<br/>
            If high accuracy is required for location results, it is recommended to set the `LocatingPriority` parameter to `PRIORITY_ACCURACY`, which will return the most accurate results within a certain period.<br/>
            If faster location acquisition is prioritized, set the `LocatingPriority` parameter to `PRIORITY_LOCATING_SPEED`, which will return the first available location result.<br/>
            Both strategies utilize GNSS and network positioning technologies to ensure location results can be obtained in both indoor and outdoor scenarios, but they consume significant hardware resources and power.<br/>
        - Set `locatingTimeoutMs`:<br/>
            Due to factors such as device environment, device state, and system power management policies, the latency of location results may vary significantly. It is recommended to set the single location timeout to 10 seconds.<br/>

        Using the fast location strategy (`PRIORITY_LOCATING_SPEED`) as an example, the calling method is as follows:<br/>

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import kit.ArkUI.*

        let request: SingleLocationRequest = SingleLocationRequest(LocatingPriority.PRIORITY_LOCATING_SPEED, 10000)
        try {
            // Call getCurrentLocation to obtain the current device location
            let result = GeoLocationManager.getCurrentLocation(request)
            Hilog.info(1, "info", "current location: (${result.latitude}, ${result.longitude})")
        } catch (err: BusinessException) {
            Hilog.info(1, "info", "errCode: ${err.code}, message: ${err.message}")
        }
        ```

    The coordinates obtained through this module are all in the WGS-84 coordinate system. If coordinates in other coordinate systems are required, perform coordinate system conversion before use.
    <!--Del-->
    Third-party map SDKs can be used for coordinate system conversion. <!--DelEnd-->