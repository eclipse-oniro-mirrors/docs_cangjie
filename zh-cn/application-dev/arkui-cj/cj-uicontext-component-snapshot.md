# 使用组件截图（ComponentSnapshot）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

<!--Kit: ArkUI-->
<!--Subsystem: ArkUI-->

## 能力介绍

组件截图是将应用内一个组件节点树的渲染结果生成位图（[PixelMap](../reference/ImageKit/cj-apis-image.md#class-pixelmap)）的能力。当前支持对已挂树显示的组件进行截图。

> **说明：**
>
> - 组件截图依赖UI上下文，需先通过[UIContext](../reference/arkui-cj/cj-apis-uicontext-uicontext.md#class-uicontext)中的[getComponentSnapshot()](../reference/arkui-cj/cj-apis-uicontext-uicontext.md#func-getcomponentsnapshot)方法获取[ComponentSnapshot](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-componentsnapshot)实例，再通过该实例调用对应方法。
>
> - 仓颉当前仅支持通过[get](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#func-getstringasynccallbackpixelmap-snapshotoptions)方法对已加载组件进行截图，不支持离线组件截图（createFromBuilder/createFromComponent）、同步截图（getSync）以及基于UniqueId的截图。

### 对挂树组件截图

对已明确挂树的组件进行截图，可通过[get](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#func-getstringasynccallbackpixelmap-snapshotoptions)方法实现，传入组件标识（需提前通过[.id](../reference/arkui-cj/cj-universal-attribute-componentid.md)通用属性配置）以指定组件根节点。系统在通过指定的ID查找待截图组件时，仅遍历已挂树的组件，不对cache或离屏组件进行查找。系统以首个查找到的结果为准，故应用需**确保组件标识ID的唯一性**。

截图仅能获取最近一帧的绘制内容。若在组件触发更新的同时调用截图，更新的渲染内容不会被截取，截图将返回前一帧的绘制内容。

> **说明：**
>
> 尽量避免在使用截图时触发待截图组件的刷新，防止对截图内容的干扰。

## 典型使用场景

### 基础截图

通过组件的[.id](../reference/arkui-cj/cj-universal-attribute-componentid.md)属性配置组件标识，调用[get](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#func-getstringasynccallbackpixelmap-snapshotoptions)方法获取截图，并通过[SnapshotOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotoptions)自定义缩放比例、等待渲染完成策略等配置。

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

### 指定截图区域

通过[SnapshotOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotoptions)中的`region`字段指定截图的矩形区域范围，可使用[SnapshotRegion](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotregion)或[LocalizedSnapshotRegion](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-localizedsnapshotregion)两种类型。

- **SnapshotRegion**：指定固定坐标的矩形区域，适用于不区分布局方向的场景。
- **LocalizedSnapshotRegion**：根据布局方向（LTR/RTL）确定坐标，若布局方向为RTL，会把指定的截图区域做左右翻转处理以适应RTL布局方向。

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import kit.ImageKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class SnapshotRegionExample {
    @State
    var pixmap: ?PixelMap = None

    func build() {
        Column() {
            Column() {
                TextClock()
                Button("Button ABCDE").type(ButtonType.Normal)
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
                        ))
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

### 指定截图色彩空间

通过[SnapshotOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotoptions)中的`colorMode`字段指定截图使用的色彩空间，使用[ColorModeOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-colormodeoptions)配置色彩空间类型及是否自动确定色彩空间。

- **colorSpace**：指定截图使用的色彩空间，支持 [ColorSpace.Srgb](../reference/ArkGraphics2D/cj-apis-color_manager.md#enum-colorspace) 和 [ColorSpace.DisplayP3](../reference/ArkGraphics2D/cj-apis-color_manager.md#enum-colorspace)。
- **isAuto**：是否由系统自动决定所使用的色彩空间。设为true时，`colorSpace`字段设置的值会被忽略。

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
                        ))
                })
                .margin(10)
        }
        .width(100.percent)
        .height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }
}
```

### 指定截图动态范围模式

通过[SnapshotOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotoptions)中的`dynamicRangeMode`字段指定截图使用的动态范围模式，使用[DynamicRangeModeOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-dynamicrangemodeoptions)配置动态范围模式及是否自动确定动态范围模式。

- **dynamicRangeMode**：指定截图使用的动态范围模式，支持 [DynamicRangeMode.Standard](./cj-common-types.md#standard)、[DynamicRangeMode.High](./cj-common-types.md#high)、[DynamicRangeMode.Constraint](./cj-common-types.md#constraint)。其中[High](./cj-common-types.md#high)和[Constraint](./cj-common-types.md#constraint)的表现均为HDR（高动态范围），[Standard](./cj-common-types.md#standard)模式对应表现为SDR（标准动态范围）。
- **isAuto**：是否由系统自动决定所使用的动态范围模式。设为true时，`dynamicRangeMode`字段设置的值会被忽略。

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
                        ))
                })
                .margin(10)
        }
        .width(100.percent)
        .height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }
}
```

## 组件截图最佳实践

### 合理控制截图时机

在实现截图功能时，需注意组件的渲染过程非一次性完成。系统在构建与显示组件时，将经过测量、布局、提交指令等多个复杂步骤，最终在一次硬件刷新时呈现于屏幕上。因此，在特定情况下，若在组件刷新后立即调用截图，可能无法获取预期内容或出现截图失败报错。

为了确保截图结果准确，建议在组件完全渲染后再执行截图操作。

**明确等待绘制完成**

影响截图预期的主要因素是截图时机与系统服务执行绘制指令的时间差。在发起截图调用时，应用侧之前提交的所有绘制指令可能尚未被图形服务真正执行。为此，可以通过指定[SnapshotOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotoptions)参数中的`waitUntilRenderFinished`为true，来确保系统在执行截图请求时等待所有之前的绘制指令均执行完毕，从而截取到更完整的内容。

> **说明：**
>
> 建议始终开启`waitUntilRenderFinished`参数。

**了解资源加载对截图的影响**

影响截图预期的另一个常见原因，是图片资源的加载。图片组件支持在线资源链接，也可指定本地资源，且绝大多数图片资源为PNG、JPEG等压缩格式。这些资源需要系统解码为可提交绘制的位图格式，此过程默认在异步IO线程上进行，因此可能由于该过程耗时的不确定性而导致截图不符合预期。

应用可通过以下几种方式进行优化：
1. 自行提前解析图片为PixelMap格式，将PixelMap配置给图片组件；建议优先以此方法进行优化。
2. 配置所使用的图片组件的syncLoad属性为true来强制同步加载，这样组件被构建时，即可确保资源可以直接被提交。

### 及时保存和释放位图对象

为了及时释放资源，当截图接口返回的PixelMap对象不再使用时，应将其赋值为空（None）。

### 合理控制采样精度

请不要截取过大尺寸的图片，截图不建议超过屏幕尺寸大小。当要截取的图片目标长宽超过底层限制时，截图会返回失败。可以通过控制[SnapshotOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotoptions)中的`scale`参数，减小采样精度，这可以在很大程度上节省内存，并大幅度提高截图的效率。
