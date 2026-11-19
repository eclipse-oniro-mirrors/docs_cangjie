# Development Guide for Obtaining Device Location Information

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Scenario Overview

Developers can call location-related interfaces to obtain the device's real-time location or recent historical location, as well as monitor changes in the device's location.

For applications with location-sensitive business logic, it is recommended to obtain the device's real-time location information. If real-time location information is not required and the goal is to minimize power consumption, developers may consider obtaining the most recent historical location instead.

In addition, you can subscribe to events such as location changes, location errors, location switch status changes, and country code changes, and use capabilities such as extended command sending to build a richer location experience.

## Interface Description

The following interfaces are used to obtain device location information. For detailed descriptions, refer to: [Location Kit](../reference/LocationKit/cj-apis-geo_location_manager.md).

This module's capabilities only support the WGS-84 coordinate system.

| Interface Name | Function Description |
| -------- | -------- |
| [getCurrentLocation()](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocation) | Get the current location. |
| [getCurrentLocation(CurrentLocationRequest)](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocationcurrentlocationrequest) | Get the current location. |
| [getCurrentLocation(SingleLocationRequest)](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocationsinglelocationrequest) | Get the current location. |
| [isLocationEnabled()](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-islocationenabled) | Check whether the location service is enabled. |
| [getLastLocation()](../reference/LocationKit/cj-apis-geo_location_manager.md#func-getlastlocation) | Obtain the last location. |
| [onLocationChange(LocationRequest, Callback1Argument\<Location>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onlocationchangelocationrequest-callback1argumentlocation) | Subscribe to location changes and initiate a location request. |
| [onLocationChange(ContinuousLocationRequest, Callback1Argument\<Location>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onlocationchangecontinuouslocationrequest-callback1argumentlocation) | Subscribe to location changes and initiate a continuous location request. |
| [offLocationChange(?Callback1Argument\<Location>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offlocationchangecallback1argumentlocation) | Unsubscribe from location changes and remove the corresponding location request. |
| [onLocationError(Callback1Argument\<LocationError>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onlocationerrorcallback1argumentlocationerror) | Subscribe to error information during continuous positioning. |
| [offLocationError(?Callback1Argument\<LocationError>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offlocationerrorcallback1argumentlocationerror) | Unsubscribe from error information during continuous positioning. |
| [onLocationEnabledChange(Callback1Argument\<Bool>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onlocationenabledchangecallback1argumentbool) | Subscribe to location service status changes. |
| [offLocationEnabledChange(?Callback1Argument\<Bool>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offlocationenabledchangecallback1argumentbool) | Unsubscribe from location service status changes. |
| [onSatelliteStatusChange(Callback1Argument\<SatelliteStatusInfo>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onsatellitestatuschangecallback1argumentsatellitestatusinfo) | Subscribe to satellite status changes. |
| [offSatelliteStatusChange(?Callback1Argument\<SatelliteStatusInfo>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offsatellitestatuschangecallback1argumentsatellitestatusinfo) | Unsubscribe from satellite status changes. |
| [onNmeaMessage(Callback1Argument\<String>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onnmeamessagecallback1argumentstring) | Subscribe to NMEA message events. |
| [offNmeaMessage(?Callback1Argument\<String>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offnmeamessagecallback1argumentstring) | Unsubscribe from NMEA message events. |
| [onCountryCodeChange(Callback1Argument\<CountryCode>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-oncountrycodechangecallback1argumentcountrycode) | Subscribe to country code change events. |
| [offCountryCodeChange(?Callback1Argument\<CountryCode>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offcountrycodechangecallback1argumentcountrycode) | Unsubscribe from country code change events. |
| [sendCommand(LocationCommand, AsyncCallback\<Unit>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-sendcommandlocationcommand-asynccallbackunit) | Send an extended command to the components of the location subsystem. |
| [getCountryCode(AsyncCallback\<CountryCode>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-getcountrycodeasynccallbackcountrycode) | Query the current country code. |

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
    import kit.CangjieKit.BusinessException
    import kit.PerformanceAnalysisKit.Hilog

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
        import kit.CangjieKit.BusinessException
        import kit.PerformanceAnalysisKit.Hilog

        let request: SingleLocationRequest = SingleLocationRequest(LocatingPriority.PriorityLocatingSpeed, 10000)
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

5. Continuous positioning. This is commonly used in scenarios such as navigation, motion tracks, and travel.
    - Obtain the last location.<br/>

        If the real-time device location is not required, you can call the getLastLocation API to obtain the most recent location result cached by the system, reducing power consumption. If the system does not have a cached location, an error code is returned.

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import kit.CangjieKit.*
        import kit.PerformanceAnalysisKit.Hilog

        try {
            let location = getLastLocation()
            Hilog.info(0, "test", "last location: (${location.latitude}, ${location.longitude})")
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        }
        ```

    - Subscribe to location changes and initiate a location request.<br/>

        First, instantiate a [LocationRequest](../reference/LocationKit/cj-apis-geo_location_manager.md#class-locationrequest) object to inform the system about the type of location service to provide to the application and the frequency of location reporting.<br/>

        - Set priority/scenario:<br/>
            When scenario is set to Unset, the priority parameter takes effect; otherwise, it does not. If both scenario and priority are set to Unset, the location request cannot be initiated.<br/>
            It is recommended that priority be set based on the requirements for location results. Select Accuracy if high accuracy is required, FirstFix if fast location acquisition is required, and LowPower if power saving is expected.<br/>
        - Set timeInterval:<br/>
            Represents the time interval for reporting location information, in seconds. If there is no special requirement on the location reporting time interval, this field can be left unset.<br/>

        The following is an example using fast location acquisition priority (FirstFix):

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import kit.CangjieKit.*
        import kit.PerformanceAnalysisKit.Hilog

        class LocationCallback <: Callback1Argument<Location> {
            public func invoke(err: ?BusinessException, arg: Location): Unit {
                Hilog.info(0, "test", "latitude=${arg.latitude}, longitude=${arg.longitude}")
            }
        }

        try {
            let request = LocationRequest(priority: LocationRequestPriority.FirstFix,
                scenario: LocationRequestScenario.Unset, timeInterval: 1)
            // Call onLocationChange to subscribe to location changes and receive the reported location through the callback
            onLocationChange(request, LocationCallback())
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        }
        ```

    - Initiate positioning using a continuous location request.<br/>

        Alternatively, you can instantiate a [ContinuousLocationRequest](../reference/LocationKit/cj-apis-geo_location_manager.md#class-continuouslocationrequest) object to describe the continuous positioning requirement through a user activity scenario or a power consumption scenario.<br/>

        - Set locationScenario:<br/>
            It is recommended that this parameter be set based on the application scenario. For example, a map application can use the Navigation parameter during navigation to continuously obtain locations in both indoor and outdoor scenarios for navigation. For valid values, see [ScenarioValueType](../reference/LocationKit/cj-apis-geo_location_manager.md#enum-scenariovaluetype).<br/>
        - Set interval:<br/>
            Represents the time interval for reporting location information, in seconds. The default value is 1. If there is no special requirement on the location reporting time interval, you can set it to 1.<br/>

        The following is an example using the map navigation scenario:

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import kit.CangjieKit.*
        import kit.PerformanceAnalysisKit.Hilog

        class LocationCallback <: Callback1Argument<Location> {
            public func invoke(err: ?BusinessException, arg: Location): Unit {
                Hilog.info(0, "test", "latitude=${arg.latitude}, longitude=${arg.longitude}")
            }
        }

        try {
            let request = ContinuousLocationRequest(1,
                ScenarioValueType.UserActivityScenarioValue(UserActivityScenario.Navigation))
            onLocationChange(request, LocationCallback())
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        }
        ```

    - Subscribe to error information during continuous positioning.<br/>

        During continuous positioning, positioning may fail due to reasons such as permission verification failure, location switch off, or network unavailability. You can call the onLocationError API to subscribe to error information and handle it based on the value of [LocationError](../reference/LocationKit/cj-apis-geo_location_manager.md#enum-locationerror).

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import kit.CangjieKit.*
        import kit.PerformanceAnalysisKit.Hilog

        class ErrorCallback <: Callback1Argument<LocationError> {
            public func invoke(err: ?BusinessException, arg: LocationError): Unit {
                Hilog.info(0, "test", "location error: ${arg.toString()}")
            }
        }

        try {
            onLocationError(ErrorCallback())
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        }
        ```

    Failure to stop positioning actively may result in high power consumption and fast battery drain. It is recommended that you stop positioning in time when location information is no longer needed.

    <!-- run -->

    ```cangjie
    import kit.LocationKit.*
    import kit.CangjieKit.*
    import kit.PerformanceAnalysisKit.Hilog

    // The callback instance must be the same as the callback instance passed in to onLocationChange; otherwise, the unsubscription fails. If no callback is passed in, all subscriptions of this type are canceled.
    try {
        offLocationChange()
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
    }
    ```

6. Monitor location service status changes. When the location switch is turned on or off, the system notifies the application through a callback. The callback returns true if the location switch is turned on, and returns false if the location switch is turned off.

    <!-- run -->

    ```cangjie
    import kit.LocationKit.*
    import kit.CangjieKit.*
    import kit.PerformanceAnalysisKit.Hilog

    class SwitchCallback <: Callback1Argument<Bool> {
        public func invoke(err: ?BusinessException, arg: Bool): Unit {
            Hilog.info(0, "test", "location enabled: ${arg}")
        }
    }

    try {
        onLocationEnabledChange(SwitchCallback())
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
    }
    ```

    If monitoring is no longer needed, you can unsubscribe. The callback instance passed in must be the same as the callback instance passed in to onLocationEnabledChange. If no callback is passed in, all subscriptions of this type are canceled.

    <!-- run -->

    ```cangjie
    import kit.LocationKit.*
    import kit.CangjieKit.*
    import kit.PerformanceAnalysisKit.Hilog

    try {
        offLocationEnabledChange()
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
    }
    ```

7. Query and subscribe to the country code. This is commonly used in scenarios that provide differentiated services based on the country code.
    - Call the getCountryCode API to query the current country code. For the country code sources, see [CountryCodeType](../reference/LocationKit/cj-apis-geo_location_manager.md#enum-countrycodetype).

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import kit.CangjieKit.*
        import kit.PerformanceAnalysisKit.Hilog

        try {
            let callback: AsyncCallback<CountryCode> = {
                err: Option<BusinessException>, data: Option<CountryCode> =>
                if (let Some(e) <- err) {
                    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
                } else if (let Some(countryCode) <- data) {
                    Hilog.info(0, "test", "country: ${countryCode.country}")
                }
            }
            getCountryCode(callback)
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        }
        ```

    - Call the onCountryCodeChange API to subscribe to country code change events. When subscription is no longer needed, call the offCountryCodeChange API to unsubscribe. The callback instance passed in must be the same as the callback instance passed in to onCountryCodeChange. If no callback is passed in, all subscriptions of this type are canceled.

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import kit.CangjieKit.*
        import kit.PerformanceAnalysisKit.Hilog

        class CountryCodeCallback <: Callback1Argument<CountryCode> {
            public func invoke(err: ?BusinessException, arg: CountryCode): Unit {
                Hilog.info(0, "test", "country: ${arg.country}, type: ${arg.countryCodeType.toString()}")
            }
        }

        try {
            onCountryCodeChange(CountryCodeCallback())
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        }
        ```

8. Send an extended command. This is commonly used in scenarios where extended commands need to be delivered to the components of the location subsystem. If the command is sent successfully, err of the callback is None; otherwise, err contains the error information.

    <!-- run -->

    ```cangjie
    import kit.LocationKit.*
    import kit.CangjieKit.*
    import kit.PerformanceAnalysisKit.Hilog

    try {
        let command = LocationCommand(LocationRequestScenario.Navigation, "command_1")
        let callback: AsyncCallback<Unit> = {
            err: Option<BusinessException>, data: Option<Unit> =>
            if (let Some(e) <- err) {
                Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
            } else {
                Hilog.info(0, "test", "sendCommand success")
            }
        }
        sendCommand(command, callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
    }
    ```

9. Subscribe to satellite status and NMEA messages. This is commonly used in scenarios such as checking satellite signal quality and troubleshooting positioning issues.
    - Call onSatelliteStatusChange to subscribe to satellite status changes. The callback parameter [SatelliteStatusInfo](../reference/LocationKit/cj-apis-geo_location_manager.md#class-satellitestatusinfo) contains the number of satellites, satellite IDs, carrier-to-noise densities, altitudes, azimuths, carrier frequencies, constellation types, and other information. When the subscription is no longer needed, call offSatelliteStatusChange to unsubscribe. The callback passed in must be the same as the callback passed in to onSatelliteStatusChange. If no callback is passed in, all subscriptions of this type are canceled.

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import kit.CangjieKit.*
        import kit.PerformanceAnalysisKit.Hilog

        class SatelliteCallback <: Callback1Argument<SatelliteStatusInfo> {
            public func invoke(err: ?BusinessException, arg: SatelliteStatusInfo): Unit {
                Hilog.info(0, "test", "satellites: ${arg.satellitesNumber}, ids: ${arg.satelliteIds.size}")
            }
        }

        try {
            onSatelliteStatusChange(SatelliteCallback())
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        }
        ```

    - Call onNmeaMessage to subscribe to NMEA message events. This API is used to obtain raw NMEA sentences output by the GNSS chip. Both the ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION permissions are required. When the subscription is no longer needed, call offNmeaMessage to unsubscribe. The callback passed in must be the same as the callback passed in to onNmeaMessage. If no callback is passed in, all subscriptions of this type are canceled.

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import kit.CangjieKit.*
        import kit.PerformanceAnalysisKit.Hilog

        class NmeaCallback <: Callback1Argument<String> {
            public func invoke(err: ?BusinessException, arg: String): Unit {
                Hilog.info(0, "test", "nmea: ${arg}")
            }
        }

        try {
            onNmeaMessage(NmeaCallback())
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        }
        ```

