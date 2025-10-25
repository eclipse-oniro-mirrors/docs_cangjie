# System Time Development Guide (Cangjie)

## Scene Introduction

When an application needs to obtain system time, time zone information, or system runtime, the system_date_time module can be used. For example: obtaining the current timestamp, obtaining the system time zone, obtaining the device running time, etc.

For detailed API introduction, please refer to[SystemDateTime API](../../../en/application-dev/reference/BasicServicesKit/cj-apis-system_date_time.md)。

## Interface Description

| name | description |
| -------- | -------- |
| SystemDateTime.getTime(isNanoseconds: Bool): Int64 | Retrieve the time elapsed since the Unix era |
| SystemDateTime.getTimezone(): String | Get system time zone |
| SystemDateTime.getUptime(timeType: TimeType, isNanoseconds: Bool): Int64 | Retrieve the time elapsed since system startup |

## Development steps

The following introduces how to use the SystemDateTime class to obtain system time related information.

1. Import module.

    <!-- compile -->

    ```cangjie
    import kit.BasicServicesKit.*
    import ohos.base.*
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. Get the current timestamp.

    <!-- compile -->

    ```cangjie
    // index.cj
    
    func getCurrentTime(): Unit {
        try {
            // Get millisecond level timestamp
            let currentTimeMs = SystemDateTime.getTime()
            Hilog.info(0, "cangjie_ohos_test", "Current time (ms): ${currentTimeMs}")
            
            // Get nanosecond level timestamp
            let currentTimeNs = SystemDateTime.getTime(isNanoseconds: true)
            Hilog.info(0, "cangjie_ohos_test", "Current time (ns): ${currentTimeNs}")
        } catch (e: Exception) {
            Hilog.info(0, "cangjie_ohos_test", "Failed to get current time: ${e.toString()}")
        }
    }
    ```

3. Retrieve system time zone information.

    <!-- compile -->

    ```cangjie
    // index.cj
    
    func getSystemTimezone(): Unit {
        try {
            let timezone = SystemDateTime.getTimezone()
            Hilog.info(0, "cangjie_ohos_test", "System timezone: ${timezone}")
        } catch (e: Exception) {
            Hilog.info(0, "cangjie_ohos_test", "Failed to get timezone: ${e.toString()}")
        }
    }
    ```

4. Get the system running time.

    <!-- compile -->

    ```cangjie
    // index.cj
    
    func getSystemUptime(): Unit {
        try {
            // Obtain system runtime including deep sleep time
            let uptimeWithSleep = SystemDateTime.getUptime(TimeType.Startup)
            Hilog.info(0, "cangjie_ohos_test", "Uptime with sleep (ms): ${uptimeWithSleep}")
            
            // Obtain system runtime without deep sleep time
            let uptimeWithoutSleep = SystemDateTime.getUptime(TimeType.Active)
            Hilog.info(0, "cangjie_ohos_test", "Uptime without sleep (ms): ${uptimeWithoutSleep}")
            
            // Get nanosecond system runtime (excluding deep sleep)
            let uptimeNs = SystemDateTime.getUptime(TimeType.Active, isNanoseconds: true)
            Hilog.info(0, "cangjie_ohos_test", "Uptime without sleep (ns): ${uptimeNs}")
        } catch (e: Exception) {
            Hilog.info(0, "cangjie_ohos_test", "Failed to get uptime: ${e.toString()}")
        }
    }
    ```

5. Comprehensive usage example.

    <!-- compile -->

    ```cangjie
    // index.cj
    
    func getAllTimeInfo(): Unit {
        try {
            // Get the current timestamp
            let currentTime = SystemDateTime.getTime()
            Hilog.info(0, "cangjie_ohos_test", "Current timestamp: ${currentTime}")
            
            // Get time zone information
            let timezone = SystemDateTime.getTimezone()
            Hilog.info(0, "cangjie_ohos_test", "Current timezone: ${timezone}")
            
            // Get system running time
            let uptime = SystemDateTime.getUptime(TimeType.Active)
            Hilog.info(0, "cangjie_ohos_test", "System uptime: ${uptime} ms")
        } catch (e: Exception) {
            Hilog.info(0, "cangjie_ohos_test", "Failed to get time info: ${e.toString()}")
        }
    }
    ```

## Constraints and limitations

1. Obtaining system time, time zone, and runtime does not require special permissions.
2. The timestamp is calculated based on the Unix epoch (January 1, 1970 00:00:00 UTC).
3. TimeType.Startup includes deep sleep time, while TimeType.Active does not include deep sleep time.
4. The isNanoseconds parameter can be used to obtain nanosecond level accuracy in time, but the actual accuracy depends on the system implementation.