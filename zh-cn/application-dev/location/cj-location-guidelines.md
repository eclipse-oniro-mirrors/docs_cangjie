# 获取设备的位置信息开发指导

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

## 场景概述

开发者可以调用位置相关接口，获取设备实时位置或最近的历史位置，以及监听设备的位置变化。

对于位置敏感的应用业务，建议获取设备实时位置信息。如果不需要设备实时位置信息，并且希望尽可能地节省耗电，开发者可以考虑获取最近的历史位置。

此外，还可以订阅位置变化、定位错误、位置开关状态、国家码变化等事件，并使用扩展命令发送等能力，构建更加丰富的位置体验。

## 接口说明

获取设备的位置信息所使用的接口如下，详细说明参见：[Location Kit](../reference/LocationKit/cj-apis-geo_location_manager.md)。

本模块能力仅支持WGS-84坐标系。

| 接口名 | 功能描述 |
| -------- | -------- |
| [getCurrentLocation()](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocation) | 获取当前位置。|
| [getCurrentLocation(CurrentLocationRequest)](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocationcurrentlocationrequest) | 获取当前位置。|
| [getCurrentLocation(SingleLocationRequest)](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-getcurrentlocationsinglelocationrequest) | 获取当前位置。|
| [isLocationEnabled()](../reference/LocationKit/cj-apis-geo_location_manager.md#static-func-islocationenabled) | 判断位置服务是否已经开启。 |
| [getLastLocation()](../reference/LocationKit/cj-apis-geo_location_manager.md#func-getlastlocation) | 获取上一次位置。 |
| [onLocationChange(LocationRequest, Callback1Argument\<Location>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onlocationchangelocationrequest-callback1argumentlocation) | 开启位置变化订阅，并发起定位请求。 |
| [onLocationChange(ContinuousLocationRequest, Callback1Argument\<Location>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onlocationchangecontinuouslocationrequest-callback1argumentlocation) | 开启位置变化订阅，并发起持续定位请求。 |
| [offLocationChange(?Callback1Argument\<Location>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offlocationchangecallback1argumentlocation) | 关闭位置变化订阅，并删除对应的定位请求。 |
| [onLocationError(Callback1Argument\<LocationError>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onlocationerrorcallback1argumentlocationerror) | 订阅持续定位过程中的错误信息。 |
| [offLocationError(?Callback1Argument\<LocationError>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offlocationerrorcallback1argumentlocationerror) | 取消订阅持续定位过程中的错误信息。 |
| [onLocationEnabledChange(Callback1Argument\<Bool>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onlocationenabledchangecallback1argumentbool) | 订阅位置服务状态变化。 |
| [offLocationEnabledChange(?Callback1Argument\<Bool>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offlocationenabledchangecallback1argumentbool) | 取消订阅位置服务状态变化。 |
| [onSatelliteStatusChange(Callback1Argument\<SatelliteStatusInfo>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onsatellitestatuschangecallback1argumentsatellitestatusinfo) | 订阅卫星状态变化事件。 |
| [offSatelliteStatusChange(?Callback1Argument\<SatelliteStatusInfo>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offsatellitestatuschangecallback1argumentsatellitestatusinfo) | 取消订阅卫星状态变化事件。 |
| [onNmeaMessage(Callback1Argument\<String>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-onnmeamessagecallback1argumentstring) | 订阅NMEA消息事件。 |
| [offNmeaMessage(?Callback1Argument\<String>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offnmeamessagecallback1argumentstring) | 取消订阅NMEA消息事件。 |
| [onCountryCodeChange(Callback1Argument\<CountryCode>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-oncountrycodechangecallback1argumentcountrycode) | 订阅国家码信息变化事件。 |
| [offCountryCodeChange(?Callback1Argument\<CountryCode>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-offcountrycodechangecallback1argumentcountrycode) | 取消订阅国家码信息变化事件。 |
| [sendCommand(LocationCommand, AsyncCallback\<Unit>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-sendcommandlocationcommand-asynccallbackunit) | 给位置服务子系统的各个部件发送扩展命令。 |
| [getCountryCode(AsyncCallback\<CountryCode>)](../reference/LocationKit/cj-apis-geo_location_manager.md#func-getcountrycodeasynccallbackcountrycode) | 查询当前的国家码。 |

## 开发步骤

1. 获取设备的位置信息，需要有位置权限，位置权限申请的方法和步骤见[申请位置权限开发指导](cj-location-permission-guidelines.md)。

2. 导入geoLocationManager模块，所有与基础定位能力相关的功能API，都是通过该模块提供的。

    <!-- compile -->

    ```cangjie
    import kit.LocationKit.*
    ```

3. 调用获取位置接口之前需要先判断位置开关是否打开。查询当前位置开关状态，返回结果为布尔值，true代表位置开关开启，false代表位置开关关闭，示例代码如下：

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

4. 单次获取当前设备位置。多用于查看当前位置、签到打卡、服务推荐等场景。
    - 获取当前位置。<br/>

        首先要实例化[SingleLocationRequest](../reference/LocationKit/cj-apis-geo_location_manager.md#class-singlelocationrequest)对象，用于告知系统该向应用提供何种类型的位置服务，以及单次定位超时时间。<br/>

        - 设置LocatingPriority：<br/>
            如果对位置的返回精度要求较高，建议LocatingPriority参数优先选择PRIORITY_ACCURACY，会将一段时间内精度较好的结果返回给应用。<br/>
            如果对定位速度要求较高，建议LocatingPriority参数选择PRIORITY_LOCATING_SPEED，会将最先拿到的定位结果返回给应用。<br/>
            两种定位策略均会同时使用GNSS定位和网络定位技术，以便在室内和户外场景下均可以获取到位置结果，对设备的硬件资源消耗较大，功耗也较大。<br/>
        - 设置locatingTimeoutMs：<br/>
            因为设备环境、设备所处状态、系统功耗管控策略等的影响，定位返回的时延会有较大波动，建议把单次定位超时时间设置为10秒。<br/>

        以快速定位策略(PRIORITY_LOCATING_SPEED)为例，调用方式如下：<br/>

        <!-- run -->

        ```cangjie
        import kit.LocationKit.*
        import kit.CangjieKit.BusinessException
        import kit.PerformanceAnalysisKit.Hilog

        let request: SingleLocationRequest = SingleLocationRequest(LocatingPriority.PriorityLocatingSpeed, 10000)
        try {
            // 调用getCurrentLocation获取当前设备位置
            let result = GeoLocationManager.getCurrentLocation(request)
            Hilog.info(1, "info", "current location: (${result.latitude}, ${result.longitude})")
        } catch (err: BusinessException) {
            Hilog.info(1, "info", "errCode: ${err.code}, message: ${err.message}")
        }
        ```

    通过本模块获取到的坐标均为WGS-84坐标系坐标点，如需使用其他坐标系类型的坐标点，请进行坐标系转换后再使用。
    可使用三方地图提供的SDK能力进行坐标系转换。

5. 持续定位。多用于导航、运动轨迹、出行等场景。
    - 获取上一次位置。<br/>

        如果不需要设备实时位置，可以调用getLastLocation接口获取系统缓存的最近一次定位结果，减少设备功耗。如果系统当前没有缓存位置，会返回错误码。

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

    - 开启位置变化订阅，并发起定位请求。<br/>

        首先要实例化[LocationRequest](../reference/LocationKit/cj-apis-geo_location_manager.md#class-locationrequest)对象，用于告知系统该向应用提供何种类型的位置服务，以及位置结果上报的频率。<br/>

        - 设置priority/scenario：<br/>
            当scenario取值为Unset时，priority参数生效，否则priority参数不生效；当scenario和priority均取值为Unset时，无法发起定位请求。<br/>
            priority建议根据对定位结果的要求进行设置，如对定位结果精度要求较高选择Accuracy，对定位速度要求较高选择FirstFix，希望节省功耗选择LowPower。<br/>
        - 设置timeInterval：<br/>
            表示上报位置信息的时间间隔，单位为秒。如果对位置上报时间间隔无特殊要求，可以不填写该字段。<br/>

        以快速获取位置优先（FirstFix）为例，调用方式如下：

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
            // 调用onLocationChange开启位置变化订阅，并通过回调接收上报的位置
            onLocationChange(request, LocationCallback())
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        }
        ```

    - 使用持续定位请求发起定位。<br/>

        也可以实例化[ContinuousLocationRequest](../reference/LocationKit/cj-apis-geo_location_manager.md#class-continuouslocationrequest)对象，通过用户活动场景或功耗场景描述持续定位需求。<br/>

        - 设置locationScenario：<br/>
            建议优先根据应用的使用场景进行设置，例如地图在导航时使用Navigation参数，可以持续在室内和室外场景获取位置用于导航。取值范围参见[ScenarioValueType](../reference/LocationKit/cj-apis-geo_location_manager.md#enum-scenariovaluetype)。<br/>
        - 设置interval：<br/>
            表示上报位置信息的时间间隔，单位是秒，默认值为1。如果对位置上报时间间隔无特殊要求，可以设置为1。<br/>

        以地图导航场景为例，调用方式如下：

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

    - 订阅持续定位过程中的错误信息。<br/>

        持续定位过程中可能因为权限校验失败、位置开关关闭、网络不可用等原因导致定位失败，可以调用onLocationError接口订阅错误信息，并根据[LocationError](../reference/LocationKit/cj-apis-geo_location_manager.md#enum-locationerror)的取值进行相应处理。

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

    如果不主动结束定位可能导致设备功耗高，耗电快；建议在不需要获取定位信息时及时结束定位。

    <!-- run -->

    ```cangjie
    import kit.LocationKit.*
    import kit.CangjieKit.*
    import kit.PerformanceAnalysisKit.Hilog

    // 该回调实例需要与onLocationChange接口传入的回调实例保持一致，否则取消订阅失败；不传入callback时取消当前类型的所有订阅。
    try {
        offLocationChange()
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
    }
    ```

6. 监听位置服务开关状态。位置开关开启或关闭时，系统会回调通知应用，回调返回true表示位置信息开关已经开启，返回false表示位置信息开关已经关闭。

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

    如果不再需要监听，可以取消订阅，传入的回调实例需要与onLocationEnabledChange接口传入的回调实例保持一致；不传入callback时取消当前类型的所有订阅。

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

7. 查询与订阅国家码。多用于根据国家码提供差异化服务的场景。
    - 调用getCountryCode接口查询当前的国家码，国家码来源参见[CountryCodeType](../reference/LocationKit/cj-apis-geo_location_manager.md#enum-countrycodetype)。

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

    - 调用onCountryCodeChange接口订阅国家码信息变化事件；不再需要时调用offCountryCodeChange接口取消订阅，传入的回调实例需要与onCountryCodeChange接口传入的回调实例保持一致；不传入callback时取消当前类型的所有订阅。

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

8. 发送扩展命令。多用于向位置服务子系统的各个部件下发扩展指令的场景，命令发送成功时callback的err为None，否则err包含错误信息。

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

9. 订阅卫星状态与NMEA消息。多用于查看卫星信号质量、调试定位问题等场景。
    - 调用onSatelliteStatusChange接口订阅卫星状态变化事件，回调参数[SatelliteStatusInfo](../reference/LocationKit/cj-apis-geo_location_manager.md#class-satellitestatusinfo)包含卫星数量、卫星ID、载波噪声密度、高度角、方位角、载波频率、星座类型等信息；不再需要时调用offSatelliteStatusChange接口取消订阅，传入的回调实例需要与onSatelliteStatusChange接口传入的回调实例保持一致；不传入callback时取消当前类型的所有订阅。

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

    - 调用onNmeaMessage接口订阅NMEA消息事件，用于获取GNSS芯片输出的原始NMEA语句，该接口需要同时申请ohos.permission.LOCATION和ohos.permission.APPROXIMATELY_LOCATION权限；不再需要时调用offNmeaMessage接口取消订阅，传入的回调实例需要与onNmeaMessage接口传入的回调实例保持一致；不传入callback时取消当前类型的所有订阅。

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

<!--Del-->
## 示例代码

[获取当前位置的经纬度](https://gitcode.com/openharmony/applications_app_samples_cangjie/tree/master/code/BasicFeature/DeviceManagement/CurrentLocation)
<!--DelEnd-->
