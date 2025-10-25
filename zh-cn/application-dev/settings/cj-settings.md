# 设置开发指导（仓颉）

## 场景介绍

当应用需要访问或修改系统设置项时，可以使用settings模块。例如：获取或设置屏幕亮度、获取日期时间格式、获取字体缩放比例等系统设置信息。

详细的API介绍请参见[Settings API](../../../zh-cn/application-dev/reference/BasicServicesKit/cj-apis-settings.md)。

## 接口说明

| 名称 | 描述 |
| -------- | -------- |
| getValue\<T>(context: UIAbilityContext, name: T, defValue: String): String where T <: ToString | 获取指定设置项的值 |
| getValue\<T, P>(context: UIAbilityContext, name: T, defValue: String, domainName: P): String where T <: ToString, P <: ToString | 获取指定域中指定设置项的值 |

## 开发步骤

以下以获取屏幕亮度设置为例，介绍如何使用settings模块。

1. 导入模块。

    <!-- compile -->

    ```cangjie
    import kit.BasicServicesKit.*
    import kit.AbilityKit.*
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. 创建全局Context管理类。

    <!-- compile -->

    ```cangjie
    // 在Global类中定义context变量
    public class Global {
        public static var _abilityContext: Option<UIAbilityContext> = None
        public static prop abilityContext: UIAbilityContext {
            get() {
                match (this._abilityContext) {
                    case Some(context) => context
                    case None => throw Exception("Global.abilityContext is not set")
                }
            }
        }
    }
    ```

3. 在UIAbility中设置Context。

    <!-- compile -->

    ```cangjie
    // 在UIAbility的onWindowStageCreate方法中设置context
    class MainAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
            Global._abilityContext = Some(this.context)
            // ... 其他代码 ...
        }
    }
    ```

4. 获取设置项的值。

    <!-- compile -->

    ```cangjie
    func getScreenBrightness(): Unit {
        try {
            let context = Global.abilityContext
            // 获取屏幕亮度设置项的值
            let brightness = getValue(context, Display.ScreenBrightnessStatus, "128")
            Hilog.info(0, "cangjie_ohos_test", "Screen brightness setting: ${brightness}")
        } catch (e: Exception) {
            Hilog.info(0, "cangjie_ohos_test", "Failed to get screen brightness setting: ${e.toString()}")
        }
    }
    ```

5. 获取指定域中的设置项值。

    <!-- compile -->

    ```cangjie
    func getScreenBrightnessWithDomain(): Unit {
        try {
            let context = Global.abilityContext
            // 获取设备共享域中的屏幕亮度设置项的值
            let brightness = getValue(context, Display.ScreenBrightnessStatus, "100", DomainName.DeviceShared)
            Hilog.info(0, "cangjie_ohos_test", "Device shared screen brightness: ${brightness}")
        } catch (e: Exception) {
            Hilog.info(0, "cangjie_ohos_test", "Failed to get device shared screen brightness: ${e.toString()}")
        }
    }
    ```

6. 获取其他常用设置项的值。

    <!-- compile -->

    ```cangjie
    func getCommonSettings(): Unit {
        try {
            let context = Global.abilityContext
            
            // 获取日期格式
            let dateFormat = getValue(context, Date.DateFormat, "MM/dd/yyyy")
            Hilog.info(0, "cangjie_ohos_test", "Date format setting: ${dateFormat}")
            
            // 获取时间格式
            let timeFormat = getValue(context, Date.TimeFormat, "24")
            Hilog.info(0, "cangjie_ohos_test", "Time format setting: ${timeFormat}")
            
            // 获取字体缩放比例
            let fontScale = getValue(context, Display.FontScale, "1.0")
            Hilog.info(0, "cangjie_ohos_test", "Font scale setting: ${fontScale}")
            
            // 获取屏幕超时时间
            let screenOffTimeout = getValue(context, Display.ScreenOffTimeout, "30000")
            Hilog.info(0, "cangjie_ohos_test", "Screen off timeout setting: ${screenOffTimeout} ms")
        } catch (e: Exception) {
            Hilog.info(0, "cangjie_ohos_test", "Failed to get settings: ${e.toString()}")
        }
    }
    ```

## 约束与限制

1. 使用settings模块需要获取相应的权限，请确保在应用配置文件中声明了相关权限。
2. 部分设置项可能需要系统级权限才能修改，普通应用只能读取。
3. 不同设备可能支持的设置项存在差异，建议在使用前先确认设备是否支持相应的设置项。
4. 获取Context对象时需要确保Ability已经正确初始化，否则可能抛出异常。