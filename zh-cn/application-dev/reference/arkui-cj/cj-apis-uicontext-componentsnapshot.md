# ComponentSnapshot

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

提供获取组件截图的能力，包括已加载组件的截图，适用于需要获取组件渲染结果用于展示或后续处理的场景。

> **说明：**
>
> 以下API需先使用[UIContext](./cj-apis-uicontext-uicontext.md#class-uicontext)中的[getComponentSnapshot()](./cj-apis-uicontext-uicontext.md#func-getcomponentsnapshot)方法获取ComponentSnapshot实例，再通过此实例调用对应方法。

## 导入模块

```cangjie
import kit.ArkUI.*
```

## class ComponentSnapshot

```cangjie
public class ComponentSnapshot {}
```

**功能：** 组件截图类，提供获取已加载组件截图的能力。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### func get(String, AsyncCallback<PixelMap>, ?SnapshotOptions)

```cangjie
public func get(id: String, callback: AsyncCallback<PixelMap>, options!: ?SnapshotOptions = Option.None): Unit
```

**功能：** 获取已加载的组件的截图，传入组件的[组件标识](./cj-universal-attribute-componentid.md)，找到对应组件进行截图，适用于生成组件预览图、保存或分享局部UI截图等场景。使用callback异步回调。

> **说明：**
>
> 截图会获取最近一帧的绘制内容。如果在组件触发更新的同时调用截图，更新的渲染内容不会被截取到，截图会返回上一帧的绘制内容。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|id|String|是|-|目标组件的[组件标识](./cj-universal-attribute-componentid.md)。<br>**说明：** 不支持未挂树组件，当传入的组件标识是离屏或缓存未挂树的节点时，系统不会对其进行截图。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap)>|是|-|回调函数。当截图返回结果成功，err为None，data为获取到的PixelMap；否则为错误对象。|
|options|?[SnapshotOptions](#class-snapshotoptions)|否|Option.None| **命名参数。** 截图相关的自定义参数。当需要自定义截图缩放比例、等待渲染完成策略等配置时传入；不传入时使用系统默认截图配置。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)、[截图错误码](./cj-errorcode-snapshot.md)和[接口调用异常错误码](./cj-errorcode-internal.md)。

  |错误码|说明|
  |:----|:----|
  |401|Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2.Incorrect parameters types. 3. Parameter verification failed.|
  |100001|Invalid ID.|
  |160003|Unsupported color space or dynamic range mode in snapshot options.|

**示例：**

<!-- run -->
```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import kit.ImageKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class SnapshotExample {
    @State
    var pixmap: ?PixelMap = None

    func build() {
        Column() {
            Row() {
                Image(this.pixmap)
                    .width(200)
                    .height(200)
                    .border(color: Color.Black, width: 2)
                    .margin(5)
                // $r('app.media.img')需要替换为开发者所需的图像资源文件
                Image($r("app.media.img"))
                    .autoResize(true)
                    .width(200)
                    .height(200)
                    .margin(5)
                    .id("root")
            }

            Button("click to generate UI snapshot")
                .onClick({
                    evt =>
                        // 建议使用this.getUIContext().getComponentSnapshot().get()
                        this.getUIContext().getComponentSnapshot().get("root", {
                            err: ?BusinessException, data: ?PixelMap =>
                                if (let Some(_) <- err) {
                                    println("error: ${err}")
                                    return
                                }
                                this.pixmap = data
                        }, options: SnapshotOptions(scale: 2.0, waitUntilRenderFinished: true))
                })
                .margin(10)
        }
        .width(100.percent)
        .height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }
}
```

## class SnapshotOptions

```cangjie
public class SnapshotOptions {
    public var scale: ?Float64
    public var waitUntilRenderFinished: ?Bool
    public var region: ?SnapshotRegionType
    public var colorMode: ?ColorModeOptions
    public var dynamicRangeMode: ?DynamicRangeModeOptions
    public init(
        scale!: ?Float64 = None,
        waitUntilRenderFinished!: ?Bool = None,
        region!: ?SnapshotRegionType = None,
        colorMode!: ?ColorModeOptions = None,
        dynamicRangeMode!: ?DynamicRangeModeOptions = None
    )
}
```

**功能：** 截图选项配置类，用于自定义截图的缩放比例、等待渲染完成策略、截图区域、色彩模式、动态范围模式等配置。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var scale

```cangjie
public var scale: ?Float64
```

**功能：** 截图时图形侧绘制pixelmap的缩放比例，比例过大时截图时间会变长，或者截图可能会失败。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

> **说明：**
>
> 请不要截取过大尺寸的图片，截图不建议超过屏幕尺寸的大小。当要截取的图片目标长宽超过底层限制时，截图会返回失败，不同设备的底层限制不同。

### var waitUntilRenderFinished

```cangjie
public var waitUntilRenderFinished: ?Bool
```

**功能：** 是否强制系统在截图前等待所有绘制指令执行完毕。true表示强制系统在截图前等待所有绘制指令执行完毕，false表示不强制系统在截图前等待所有绘制指令执行完毕。该选项可尽可能确保截图内容是最新的状态，应尽量开启。需要注意的是，开启后接口可能需要更长的时间返回，具体的时间依赖页面当前时刻需要重绘区域的大小。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var region

```cangjie
public var region: ?SnapshotRegionType
```

**功能：** 截图的矩形区域范围，默认为整个组件。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var colorMode

```cangjie
public var colorMode: ?ColorModeOptions
```

**功能：** 截图使用的色彩空间。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var dynamicRangeMode

```cangjie
public var dynamicRangeMode: ?DynamicRangeModeOptions
```

**功能：** 截图使用的动态范围模式。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### init(?Float64, ?Bool, ?SnapshotRegionType, ?ColorModeOptions, ?DynamicRangeModeOptions)

```cangjie
public init(
    scale!: ?Float64 = None,
    waitUntilRenderFinished!: ?Bool = None,
    region!: ?SnapshotRegionType = None,
    colorMode!: ?ColorModeOptions = None,
    dynamicRangeMode!: ?DynamicRangeModeOptions = None
)
```

**功能：** SnapshotOptions构造函数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|scale|?Float64|否|None| **命名参数。** 图形侧绘制PixelMap的缩放比例。取值范围：[0, +∞)，当值小于等于0时使用初始值1。|
|waitUntilRenderFinished|?Bool|否|None| **命名参数。** 是否强制系统在截图前等待所有绘制指令执行完毕。初始值：false。|
|region|?[SnapshotRegionType](#interface-snapshotregiontype)|否|None| **命名参数。** 矩形区域范围。默认为整个组件。|
|colorMode|?[ColorModeOptions](#class-colormodeoptions)|否|None| **命名参数。** 色彩空间。初始值：ColorModeOptions(colorSpace: ColorSpace.Srgb, isAuto: false)。|
|dynamicRangeMode|?[DynamicRangeModeOptions](#class-dynamicrangemodeoptions)|否|None| **命名参数。** 动态范围模式。初始值：DynamicRangeModeOptions(dynamicRangeMode: DynamicRangeMode.Standard, isAuto: false)。|

## class SnapshotRegion

```cangjie
public class SnapshotRegion {
    public var left: Float64
    public var right: Float64
    public var top: Float64
    public var bottom: Float64
    public init(left!: Float64, right!: Float64, top!: Float64, bottom!: Float64)
}
```

**功能：** 定义组件截图的矩形区域。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var left

```cangjie
public var left: Float64
```

**功能：** 矩形区域左上角的X坐标。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var right

```cangjie
public var right: Float64
```

**功能：** 矩形区域右下角的X坐标。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var top

```cangjie
public var top: Float64
```

**功能：** 矩形区域左上角的Y坐标。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var bottom

```cangjie
public var bottom: Float64
```

**功能：** 矩形区域右下角的Y坐标。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### init(Float64, Float64, Float64, Float64)

```cangjie
public init(left!: Float64, right!: Float64, top!: Float64, bottom!: Float64)
```

**功能：** SnapshotRegion构造函数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|left|Float64|是|-| **命名参数。** 左边界。单位：px。取值范围：[0, 组件宽度]。取值超出范围时，截图失败，返回错误码401。|
|right|Float64|是|-| **命名参数。** 右边界。单位：px。取值范围：[0, 组件宽度]。取值超出范围时，截图失败，返回错误码401。|
|top|Float64|是|-| **命名参数。** 上边界。单位：px。取值范围：[0, 组件高度]。取值超出范围时，截图失败，返回错误码401。|
|bottom|Float64|是|-| **命名参数。** 下边界。单位：px。取值范围：[0, 组件高度]。取值超出范围时，截图失败，返回错误码401。|

## class LocalizedSnapshotRegion

```cangjie
public class LocalizedSnapshotRegion {
    public var start: Float64
    public var end: Float64
    public var top: Float64
    public var bottom: Float64
    public init(start!: Float64, end!: Float64, top!: Float64, bottom!: Float64)
}
```

**功能：** 定义组件截图的矩形区域，start和end的值在布局方向为LTR时指定为left和right，在布局方向为RTL时指定为right和left。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var start

```cangjie
public var start: Float64
```

**功能：** LTR布局下为矩形区域左上角的X坐标；RTL布局下为矩形区域右上角的X坐标。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var end

```cangjie
public var end: Float64
```

**功能：** LTR布局下为矩形区域右下角的X坐标；RTL布局下为矩形区域左下角的X坐标。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var top

```cangjie
public var top: Float64
```

**功能：** LTR布局下为矩形区域左上角的Y坐标；RTL布局下为矩形区域右上角的Y坐标。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var bottom

```cangjie
public var bottom: Float64
```

**功能：** LTR布局下为矩形区域右下角的Y坐标；RTL布局下为矩形区域左下角的Y坐标。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### init(Float64, Float64, Float64, Float64)

```cangjie
public init(start!: Float64, end!: Float64, top!: Float64, bottom!: Float64)
```

**功能：** LocalizedSnapshotRegion构造函数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|start|Float64|是|-| **命名参数。** 起始边界。单位：px。取值范围：[0, 组件宽度]。取值超出范围时，截图失败，返回错误码401。|
|end|Float64|是|-| **命名参数。** 结束边界。单位：px。取值范围：[0, 组件宽度]。取值超出范围时，截图失败，返回错误码401。|
|top|Float64|是|-| **命名参数。** 上边界。单位：px。取值范围：[0, 组件高度]。取值超出范围时，截图失败，返回错误码401。|
|bottom|Float64|是|-| **命名参数。** 下边界。单位：px。取值范围：[0, 组件高度]。取值超出范围时，截图失败，返回错误码401。|

## interface SnapshotRegionType

```cangjie
public interface SnapshotRegionType {}
```

**功能：** 定义截图区域的类型。SnapshotRegionType是SnapshotRegion和LocalizedSnapshotRegion的联合类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### extend SnapshotRegion <: SnapshotRegionType

```cangjie
extend SnapshotRegion <: SnapshotRegionType {}
```

**功能：** 扩展SnapshotRegion为SnapshotRegionType子类。

### extend LocalizedSnapshotRegion <: SnapshotRegionType

```cangjie
extend LocalizedSnapshotRegion <: SnapshotRegionType {}
```

**功能：** 扩展LocalizedSnapshotRegion为SnapshotRegionType子类。

**示例：**

<!-- run -->
```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import kit.ImageKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class SnapshotExample {
    @State
    var pixmap: ?PixelMap = None

    func build() {
        Column() {
            Row() {
                Column() {
                    TextClock()
                    Button("Button ABCDE")
                        .type(ButtonType.Normal)
                    Row() {
                        Checkbox()
                        Text("√")
                        Text(" | ")
                        Checkbox()
                        Text("×")
                    }
                    .align(Alignment.Start)

                    TextInput()
                }
                .align(Alignment.Start)
                .id("component1")
                .width(600)
                .height(600)
                .borderRadius(6)
                .borderWidth(2)
                .borderColor(Color.Green)
            }

            Button("get capture")
                .onClick({
                    evt =>
                        this.getUIContext().getComponentSnapshot().get("component1", {
                            err: ?BusinessException, data: ?PixelMap =>
                                if (let Some(_) <- err) {
                                    println("get error message: ${err}")
                                    return
                                }
                                this.pixmap = data
                        }, options: SnapshotOptions(
                            scale: 2.0,
                            waitUntilRenderFinished: true,
                            region: LocalizedSnapshotRegion(start: 20, top: 20, end: 200, bottom: 240)
                        )
                        )
                })
                .margin(10)
            Image(this.pixmap)
                .border(color: Color.Black, width: 2)
                .width(600)
        }
        .width(100.percent)
        .align(Alignment.Center)
    }
}
```

## class ColorModeOptions

```cangjie
public class ColorModeOptions {
    public var colorSpace: ?ColorSpace
    public var isAuto: ?Bool
    public init(
        colorSpace!: ?ColorSpace = None,
        isAuto!: ?Bool = None
    )
}
```

**功能：** 定义截图时所使用的色彩空间。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var colorSpace

```cangjie
public var colorSpace: ?ColorSpace
```

**功能：** 截图使用的色彩空间。如果知道被截图组件使用的色彩空间，可以通过`colorSpace`字段指定，并将`isAuto`设置为false，以达到预期的截图效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var isAuto

```cangjie
public var isAuto: ?Bool
```

**功能：** 是否由系统自动决定所使用的色彩空间。true表示系统自动决定所使用的色彩空间；false表示使用通过`colorSpace`字段设置的色彩空间类型进行截图。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### init(?ColorSpace, ?Bool)

```cangjie
public init(
    colorSpace!: ?ColorSpace = None,
    isAuto!: ?Bool = None
)
```

**功能：** ColorModeOptions构造函数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|colorSpace|?[ColorSpace](../ArkGraphics2D/cj-apis-color_manager.md#enum-colorspace)|否|None| **命名参数。** 指定截图使用的色彩空间。<br>取值范围：[colorSpaceManager.ColorSpace](../ArkGraphics2D/cj-apis-color_manager.md#enum-colorspace)中DisplayP3、Srgb。<br>初始值：Srgb <br>如果值为Option.None或未设置，则使用初始值截图；其他异常值会导致截图失败，返回错误码160003。|
|isAuto|?Bool|否|None| **命名参数。** 是否由系统自动决定所使用的色彩空间。<br>true表示系统自动决定所使用的色彩空间；false表示使用通过`colorSpace`字段设置的色彩空间类型进行截图。取非法值时，按初始值false处理。<br>初始值：false<br>离屏截图仅支持设置为false，否则会返回错误码160004。<br>当`isAuto`设置为true时，建议将[SnapshotOptions](#class-snapshotoptions)中的`waitUntilRenderFinished`字段也设置为true，以便确保系统可以正常检测到所用的模式。<br>在不确定组件使用的色彩空间时，建议将`isAuto`设置为true，让系统根据实际情况自动决定使用的色彩空间。<br>当`isAuto`为true时，`colorSpace`字段设置的值会被忽略。此时，如果被截图组件同时包含不同色彩空间的子组件时，截图的色彩空间为优先级最高的色彩空间类型，优先级排序为DisplayP3 > Srgb。|

**示例：**

<!-- run -->
```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import kit.ArkGraphics2D.*
import kit.ImageKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class SnapshotColorModeExample {
    @State
    var pixmap: ?PixelMap = None

    func build() {
        Column() {
            Row() {
                Image(this.pixmap)
                    .width(200)
                    .height(200)
                    .border(color: Color.Black, width: 2)
                    .margin(5)
                // $r('app.media.img')需要替换为开发者所需的图像资源文件
                Image($r("app.media.img"))
                    .autoResize(true)
                    .width(200)
                    .height(200)
                    .margin(5)
                    .id("root")
            }

            Button("click to generate UI snapshot")
                .onClick({
                    evt =>
                        this.getUIContext().getComponentSnapshot().get("root", {
                            err: ?BusinessException, data: ?PixelMap =>
                                if (let Some(_) <- err) {
                                    println("error: ${err}")
                                    return
                                }
                                this.pixmap = data
                        }, options: SnapshotOptions(
                            scale: 2.0,
                            waitUntilRenderFinished: true,
                            // 设置色彩空间为：DisplayP3
                            colorMode: ColorModeOptions(colorSpace: ColorSpace.DisplayP3, isAuto: false)
                        )
                        )
                })
                .margin(10)
        }
        .width(100.percent)
        .height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }
}
```

## class DynamicRangeModeOptions

```cangjie
public class DynamicRangeModeOptions {
    public var dynamicRangeMode: ?DynamicRangeMode
    public var isAuto: ?Bool
    public init(
        dynamicRangeMode!: ?DynamicRangeMode = None,
        isAuto!: ?Bool = None
    )
}
```

**功能：** 定义截图使用的动态范围模式。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var dynamicRangeMode

```cangjie
public var dynamicRangeMode: ?DynamicRangeMode
```

**功能：** 截图使用的动态范围模式。

默认情况下，系统以[Standard](./cj-common-types.md#standard)模式进行截图。如果知道被截图组件使用的动态范围模式，可通过dynamicRangeMode字段指定具体的动态范围模式，并将isAuto设置为false，以达到预期的截图效果。

虽然动态范围模式有三种，但是[High](./cj-common-types.md#high)和[Constraint](./cj-common-types.md#constraint)的表现均为HDR（高动态范围）。[Standard](./cj-common-types.md#standard)模式对应表现为SDR（标准动态范围）。

在指定了合法的动态范围模式之后，截图实际采用的动态范围会受到被截图组件和设置值的双重影响，具体如下：
1. 当被截图组件的动态范围为SDR时，即使指定动态范围模式为[High](./cj-common-types.md#high)，截图实际采用的动态范围为SDR。
2. 当被截图组件的动态范围为HDR时，截图实际采用的动态范围为指定的动态范围模式。
3. 当配置色彩空间为Srgb或DisplayP3时，截图实际采用的动态范围为SDR。
4. 如果被截图组件同时包含SDR和HDR两种动态范围的子组件时，则当作HDR处理。
5. 如果3和4的条件同时被满足，则截图实际采用的动态范围为SDR。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### var isAuto

```cangjie
public var isAuto: ?Bool
```

**功能：** 是否由系统自动确定使用的动态范围模式。true表示由系统自动确定，false表示通过dynamicRangeMode手动设置。取非法值时，按初始值false处理。

离屏截图仅支持设置为false，否则会返回错误码160004。

当isAuto设置为true时，建议将SnapshotOptions中的waitUntilRenderFinished字段也设置为true，以便确保系统可以正常检测到所用的模式。

在不确定组件使用的动态范围模式时，建议将isAuto设置为true，让系统根据实际情况自动决定使用的动态范围模式。

当isAuto为true时，dynamicRangeMode字段设置的值会被忽略。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

### init(?DynamicRangeMode, ?Bool)

```cangjie
public init(
    dynamicRangeMode!: ?DynamicRangeMode = None,
    isAuto!: ?Bool = None
)
```

**功能：** DynamicRangeModeOptions构造函数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|dynamicRangeMode|?[DynamicRangeMode](./cj-common-types.md#enum-dynamicrangemode)|否|None| **命名参数。** 动态范围模式。初始值：DynamicRangeMode.Standard。如果值为Option.None或未设置，则使用初始值截图；其他异常值会导致截图失败，返回错误码160003。|
|isAuto|?Bool|否|None| **命名参数。** 是否自动确定动态范围模式。初始值：false。|

**示例：**

<!-- run -->
```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import kit.ImageKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class SnapshotDynamicRangeExample {
    @State
    var pixmap: ?PixelMap = None

    func build() {
        Column() {
            Row() {
                Image(this.pixmap)
                    .width(200)
                    .height(200)
                    .border(color: Color.Black, width: 2)
                    .margin(5)
                // $r('app.media.img')需要替换为开发者所需的图像资源文件
                Image($r("app.media.img"))
                    .autoResize(true)
                    .width(200)
                    .height(200)
                    .margin(5)
                    .id("root")
            }

            Button("click to generate UI snapshot")
                .onClick({
                    evt =>
                        this.getUIContext().getComponentSnapshot().get("root", {
                            err: ?BusinessException, data: ?PixelMap =>
                                if (let Some(_) <- err) {
                                    println("error: ${err}")
                                    return
                                }
                                this.pixmap = data
                        }, options: SnapshotOptions(
                            scale: 2.0,
                            waitUntilRenderFinished: true,
                            // 设置动态范围为自动模式
                            dynamicRangeMode: DynamicRangeModeOptions(dynamicRangeMode: DynamicRangeMode.Standard, isAuto: true)
                        )
                        )
                })
                .margin(10)
        }
        .width(100.percent)
        .height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }
}
```
