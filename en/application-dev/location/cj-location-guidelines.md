# Development Guide for Obtaining Device Location Information

## Scenario Overview

Developers can call location-related interfaces to obtain the device's real-time location or recent historical location, as well as monitor changes in the device's location.

For applications with location-sensitive business logic, it is recommended to obtain real-time device location information. If real-time location information is not required and minimizing power consumption is a priority, developers may consider retrieving the most recent historical location.

## Interface Description

The following interfaces are used to obtain device location information. For detailed descriptions, refer to: [Location Kit](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md).

This module's capabilities only support the WGS-84 coordinate system.

| Interface Name | Function Description |
| -------- | -------- |
| [on(CallbackType, LocationRequest, Callback1Argument\<Location>)](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md#static-func-oncallbacktype-locationrequest-callback1argumentlocation) | Subscribes to location changes and initiates a location request. |
| [off(CallbackType, Callback1Argument\<Location>)](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md#static-func-offcallbacktype-callback1argumentlocation) | Unsubscribes from location changes and removes the corresponding location request. |
| [getCurrentLocation()](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocation) | Retrieves the current location. |
| [getCurrentLocation(CurrentLocationRequest)](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocationcurrentlocationrequest) | Retrieves the current location. |
| [getCurrentLocation(SingleLocationRequest)](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocationsinglelocationrequest) | Retrieves the current location. |
| [getLastLocation()](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getlastlocation) | Retrieves the most recent location result. |
| [isLocationEnabled()](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md#static-func-islocationenabled) | Checks whether the location service is enabled. |

## Development Steps

1. Obtaining device location information requires location permissions. For methods and steps to apply for location permissions, refer to the [Development Guide for Applying for Location Permissions](cj-location-permission-guidelines.md).

2. Import the `geoLocationManager` module. All APIs related to basic location capabilities are provided through this module.

    <!-- compile -->

    ```cangjie
    import kit.LocationKit.*
    ```

3. Before calling location retrieval interfaces, check whether the location service is enabled. The current status of the location service is returned as a boolean value: `true` indicates the service is enabled, and `false` indicates it is disabled. Example code:

    <!-- run -->

    ```cangjie
    import kit.LocationKit.*
    import ohos.base.*

    try {
        let locationEnabled = GeoLocationManager.isLocationEnabled()
    } catch (err: BusinessException) {
        AppLog.error("errCode: ${err.code}, message: ${err.message}")
    }
    ```

    If the location service is not enabled, you can prompt the user to enable it by launching a global settings dialog. For details, refer to [Launching the Global Settings Dialog](../../../en/application-dev/reference/AbilityKit/cj-apis-ability_access_ctrl.md#func-requestglobalswitchcontext-switchtype-asynccallbackbool).

4. Single-time retrieval of the current device location. Commonly used for scenarios such as checking the current location, check-ins, or service recommendations.
    - Method 1: Retrieve the most recent cached location.<br/>
        If no cached location is available, an error code will be returned.<br/>
        This method is recommended to minimize system power consumption.<br/>
        If location freshness is critical, compare the timestamp of the cached location with the current time. If the freshness is insufficient, use Method 2.<br/>

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import ohos.base.*

        try {
            let location = GeoLocationManager.getLastLocation()
        } catch (err: BusinessException) {
            AppLog.error("errCode: ${err.code}, message: ${err.message}")
        }
        ```

    - Method 2: Retrieve the current location.<br/>

        First, instantiate a [SingleLocationRequest](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md#class-singlelocationrequest) object to specify the type of location service and the timeout for single-time location retrieval.<br/>

        - Set `LocatingPriority`:<br/>
            For high-accuracy requirements, set `LocatingPriority` to `PRIORITY_ACCURACY` to return the most accurate result within a period.<br/>
            For faster location retrieval, set `LocatingPriority` to `PRIORITY_LOCATING_SPEED` to return the first available result.<br/>
            Both strategies use GNSS and network positioning to ensure results in indoor and outdoor scenarios, but they consume more hardware resources and power.<br/>
        - Set `locatingTimeoutMs`:<br/>
            Due to environmental factors, device state, and system power management, location retrieval delays may vary. A timeout of 10 seconds is recommended.<br/>

        Example for fast location retrieval (`PRIORITY_LOCATING_SPEED`):<br/>

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import ohos.base.*

        let request: SingleLocationRequest = SingleLocationRequest(LocatingPriority.PRIORITY_LOCATING_SPEED, 10000)
        try {
            // Call getCurrentLocation to retrieve the current device location
            let result = GeoLocationManager.getCurrentLocation(request)
            AppLog.info("current location: (${result.latitude}, ${result.longitude})")
        } catch (err: BusinessException) {
            AppLog.error("errCode: ${err.code}, message: ${err.message}")
        }
        ```

    Coordinates obtained through this module are in the WGS-84 coordinate system. For other coordinate systems, perform a coordinate conversion before use.
    <!--Del-->
    Third-party map SDKs can be used for coordinate conversion.<!--DelEnd-->

5. Continuous location tracking. Commonly used for navigation, activity tracking, or travel scenarios.</br>
    First, instantiate a [ContinuousLocationRequest](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md#class-continuouslocationrequest) object to specify the type of location service and the frequency of location updates.<br/>
    - Set `locationScenario`:<br/>
        The `locationScenario` parameter should align with the application's use case. For enum values, refer to [UserActivityScenario](../../../en/application-dev/reference/LocationKit/cj-apis-geo_location_manager.md#enum-useractivityscenario). For example, use `NAVIGATION` for map navigation to ensure continuous location updates indoors and outdoors.</br>
    - Set `interval`:<br/>
        Specifies the time interval (in seconds) for location updates. The default is 1 second. If no specific interval is required, this field can be omitted.

    Example for map navigation:

    <!-- run -->

    ```cangjie
    import kit.LocationKit.*
    import ohos.base.*

    class LocationCallback <: Callback1Argument<Location> {
        init() {}
        public open func invoke(info: Location): Unit {
            AppLog.info("location change.")
        }
    }

    let request: ContinuousLocationRequest = ContinuousLocationRequest(1, UserActivityScenario.NAVIGATION)
    let locationCallback = LocationCallback()
    try {
        GeoLocationManager.on(CallbackType.LocationChange, request, locationCallback)
    } catch (err: BusinessException) {
        AppLog.error("errCode: ${err.code}, message: ${err.message}")
    }
    ```

    Failing to stop continuous tracking may lead to high power consumption. It is recommended to stop tracking when location updates are no longer needed.

    <!-- compile -->

    ```cangjie
    // The callback function must match the one passed to the `on` interface.
    GeoLocationManager.off(CallbackType.LocationChange, locationCallback)
    ```