# 资源管理

## 使用场景

资源管理（Resource Manager）提供了根据当前设备配置（如语言、区域、屏幕方向、设备类型、屏幕密度等）获取应用资源的能力。开发者可以使用资源管理模块来实现应用的多语言支持、图片资源适配、主题切换等功能。

## 开发步骤

接口具体说明请参见[ResourceManager](../../../zh-cn/application-dev/reference/LocalizationKit/cj-apis-resource_manager.md#class-resourcemanager)的API文档。

1. 导入模块。

```cangjie
import kit.LocalizationKit.*
```

2. 获取资源管理对象。

在使用资源管理功能之前，需要先获取ResourceManager实例：

```cangjie
// index.cj

import kit.LocalizationKit.*
import kit.AbilityKit.*

let stageContext = getStageContext(MainAbility.abilityContext.getOrThrow())
let resMgr = ResourceManager.getResourceManager(stageContext)
```

3. 获取字符串资源。

通过资源ID或资源名称获取字符串资源，支持格式化参数：

```cangjie
// 通过资源ID获取字符串
let resource = @r(app.string.test)
let str = resMgr.getString(Int32(resource.id))

// 通过资源名称获取字符串
let strByName = resMgr.getStringByName("test")

// 获取并格式化字符串
let formattedStr = resMgr.getString(Int32(resource.id), 
    FormatArgs.STRING("format string"), 
    FormatArgs.INT(10), 
    FormatArgs.FLOAT(98.78))
```

4. 获取字符串数组资源。

获取字符串数组资源，用于列表、下拉框等场景：

```cangjie
// 通过资源ID获取字符串数组
let strArrayResource = @r(app.strarray.test)
let strArray = resMgr.getStringArrayValue(Int32(strArrayResource.id))

// 通过资源名称获取字符串数组
let strArrayByName = resMgr.getStringArrayByName("test")
```

5. 获取数字资源。

获取integer或float类型的数字资源：

```cangjie
// 通过资源ID获取数字资源
let numberResource = @r(app.integer.test)
let number = resMgr.getNumber(Int32(numberResource.id))
match (number) {
    case INT(v) => AppLog.info(v.toString())
    case FLOAT(v) => AppLog.info(v.toString())
    case _ => throw IllegalArgumentException("The type is not supported.")
}

// 通过资源名称获取数字资源
let numberByName = resMgr.getNumberByName("test")
```

6. 获取布尔资源。

获取布尔类型的资源：

```cangjie
// 通过资源ID获取布尔资源
let boolResource = @r(app.boolean.test)
let boolValue = resMgr.getBoolean(Int32(boolResource.id))

// 通过资源名称获取布尔资源
let boolByName = resMgr.getBooleanByName("test")
```

7. 获取颜色资源。

获取颜色资源的值：

```cangjie
// 通过资源ID获取颜色资源
let colorResource = @r(app.color.test)
let colorValue = resMgr.getColor(Int32(colorResource.id))

// 通过资源名称获取颜色资源
let colorByName = resMgr.getColorByName("test")
```

8. 获取图片资源。

获取DrawableDescriptor对象用于图片显示：

```cangjie
// 通过资源ID获取图片资源
let mediaResource = @r(app.media.test)
let drawableDescriptor = resMgr.getDrawableDescriptor(Int32(mediaResource.id))

// 通过资源名称获取图片资源
let drawableDescriptorByName = resMgr.getDrawableDescriptorByName("test")
```

9. 获取单复数字符串资源。

根据数量获取对应的单复数字符串资源（英文环境下区分单复数）：

```cangjie
// 通过资源ID获取单复数字符串
let pluralResource = @r(app.plural.test)
let pluralStr = resMgr.getPluralStringValue(Int32(pluralResource.id), 1)

// 通过资源名称获取单复数字符串
let pluralStrByName = resMgr.getPluralStringByName("test", 1)
```

10. 获取Raw文件资源。

读取resources/rawfile目录下的文件内容：

```cangjie
// 获取raw文件内容
let rawFileContent = resMgr.getRawFileContent("test.txt")

// 获取raw文件描述符
let rawFd = resMgr.getRawFd("test.txt")
AppLog.info("${rawFd.fd} ${rawFd.offset} ${rawFd.length}")

// 获取raw文件列表
let rawFileList = resMgr.getRawFileList("")
```

11. 获取设备配置信息。

获取当前设备的配置和能力信息：

```cangjie
// 获取设备配置信息
let configuration = resMgr.getConfiguration()
AppLog.info(configuration.locale)
AppLog.info(configuration.direction.getValue().toString())

// 获取设备能力信息
let deviceCapability = resMgr.getDeviceCapability()
AppLog.info(deviceCapability.screenDensity.getValue().toString())
AppLog.info(deviceCapability.deviceType.getValue().toString())
```

12. 获取应用支持的语言列表。

```cangjie
// 获取应用语言列表
let locales = resMgr.getLocales()

// 获取包括系统资源在内的语言列表
let allLocales = resMgr.getLocales(includeSystem: true)
```
