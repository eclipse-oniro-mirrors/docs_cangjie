# 系统时间开发指导（仓颉）

## 场景介绍

当应用需要获取系统时间、时区信息或系统运行时间时，可以使用system_date_time模块。例如：获取当前时间戳、获取系统时区、获取设备运行时间等。

详细的API介绍请参见[SystemDateTime API](../../../zh-cn/application-dev/reference/BasicServicesKit/cj-apis-system_date_time.md)。

## 接口说明

| 名称 | 描述 |
| -------- | -------- |
| SystemDateTime.getTime(isNanoseconds: Bool): Int64 | 获取自Unix纪元以来经过的时间 |
| SystemDateTime.getTimezone(): String | 获取系统时区 |
| SystemDateTime.getUptime(timeType: TimeType, isNanoseconds: Bool): Int64 | 获取自系统启动以来经过的时间 |

## 开发步骤

以下介绍如何使用SystemDateTime类获取系统时间相关信息。

1. 导入模块。

    <!-- compile -->

    ```cangjie
    import kit.BasicServicesKit.*
    import ohos.base.*
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. 获取当前时间戳。

    <!-- compile -->

    ```cangjie
    // index.cj
    
    func getCurrentTime(): Unit {
        try {
            // 获取毫秒级时间戳
            let currentTimeMs = SystemDateTime.getTime()
            Hilog.info(0, "cangjie_ohos_test", "Current time (ms): ${currentTimeMs}")
            
            // 获取纳秒级时间戳
            let currentTimeNs = SystemDateTime.getTime(isNanoseconds: true)
            Hilog.info(0, "cangjie_ohos_test", "Current time (ns): ${currentTimeNs}")
        } catch (e: Exception) {
            Hilog.info(0, "cangjie_ohos_test", "Failed to get current time: ${e.toString()}")
        }
    }
    ```

3. 获取系统时区信息。

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

4. 获取系统运行时间。

    <!-- compile -->

    ```cangjie
    // index.cj
    
    func getSystemUptime(): Unit {
        try {
            // 获取包含深度睡眠时间的系统运行时间
            let uptimeWithSleep = SystemDateTime.getUptime(TimeType.Startup)
            Hilog.info(0, "cangjie_ohos_test", "Uptime with sleep (ms): ${uptimeWithSleep}")
            
            // 获取不包含深度睡眠时间的系统运行时间
            let uptimeWithoutSleep = SystemDateTime.getUptime(TimeType.Active)
            Hilog.info(0, "cangjie_ohos_test", "Uptime without sleep (ms): ${uptimeWithoutSleep}")
            
            // 获取纳秒级系统运行时间（不包含深度睡眠）
            let uptimeNs = SystemDateTime.getUptime(TimeType.Active, isNanoseconds: true)
            Hilog.info(0, "cangjie_ohos_test", "Uptime without sleep (ns): ${uptimeNs}")
        } catch (e: Exception) {
            Hilog.info(0, "cangjie_ohos_test", "Failed to get uptime: ${e.toString()}")
        }
    }
    ```

5. 综合使用示例。

    <!-- compile -->

    ```cangjie
    // index.cj
    
    func getAllTimeInfo(): Unit {
        try {
            // 获取当前时间戳
            let currentTime = SystemDateTime.getTime()
            Hilog.info(0, "cangjie_ohos_test", "Current timestamp: ${currentTime}")
            
            // 获取时区信息
            let timezone = SystemDateTime.getTimezone()
            Hilog.info(0, "cangjie_ohos_test", "Current timezone: ${timezone}")
            
            // 获取系统运行时间
            let uptime = SystemDateTime.getUptime(TimeType.Active)
            Hilog.info(0, "cangjie_ohos_test", "System uptime: ${uptime} ms")
        } catch (e: Exception) {
            Hilog.info(0, "cangjie_ohos_test", "Failed to get time info: ${e.toString()}")
        }
    }
    ```

## 约束与限制

1. 获取系统时间、时区和运行时间不需要特殊权限。
2. 时间戳基于Unix纪元（1970年1月1日00:00:00 UTC）计算。
3. TimeType.Startup包含深度睡眠时间，TimeType.Active不包含深度睡眠时间。
4. isNanoseconds参数可用于获取纳秒级精度的时间，但实际精度取决于系统实现。