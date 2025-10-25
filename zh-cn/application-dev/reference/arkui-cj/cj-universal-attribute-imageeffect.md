# 图像效果

设置组件的模糊、阴影、球面效果以及设置图片的图像效果。

## 导入模块

```cangjie
import kit.ArkUI.*
```

## func blur(?Float64)

```cangjie
public func blur(value: ?Float64): T
```

**功能：** 为当前组件添加内容模糊效果。输入参数为模糊半径，半径越大内容越模糊，为0时不模糊。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?Float64|是|-|模糊半径。初始值:  0.0|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## func colorBlend(?ResourceColor)

```cangjie
public func colorBlend(value: ?ResourceColor): T
```

**功能：** 为组件添加颜色混合效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?[ResourceColor](./cj-common-types.md#interface-resourcecolor)|是|-|颜色混合值。初始值:  Color.Transparent|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## func backdropBlur(?Float64)

```cangjie
public func backdropBlur(value: ?Float64): T
```

**功能：** 为组件添加背景模糊效果，可以自定义模糊半径。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?Float64|是|-|模糊半径。初始值:  0.0|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## func shadow(?Float64, ?ResourceColor, ?Float64, ?Float64)

```cangjie
public func shadow(radius!: ?Float64, color!: ?ResourceColor = None, offsetX!: ?Float64 = None, offsetY!: ?Float64 = None): T
```

**功能：** 为组件添加阴影效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|radius|?Float64|是|-|**命名参数。** 阴影模糊半径。初始值:  0.0|
|color|?[ResourceColor](./cj-common-types.md#interface-resourcecolor)|否|None|**命名参数。** 阴影颜色。初始值:  Color(0x666666)|
|offsetX|?Float64|否|None|**命名参数。** 阴影X轴偏移量。初始值:  0.0|
|offsetY|?Float64|否|None|**命名参数。** 阴影Y轴偏移量。初始值:  0.0|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## func grayscale(?Float64)

```cangjie
public func grayscale(value: ?Float64): T
```

**功能：** 为组件添加灰度效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?Float64|是|-|灰度值。值定义为灰度转换的比例，入参1.0则完全转为灰度图像，入参0.0则图像无变化，入参在0.0和1.0之间时，效果呈线性变化。取值范围：[0.0, 1.0]。初始值:  0.0|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## func brightness(?Float64)

```cangjie
public func brightness(value: ?Float64): T
```

**功能：** 为组件添加亮度效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?Float64|是|-|亮度值。初始值:  1.0|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## func saturate(?Float64)

```cangjie
public func saturate(value: ?Float64): T
```

**功能：** 为组件添加饱和度效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?Float64|是|-|饱和度值。初始值:  1.0|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## func contrast(?Float64)

```cangjie
public func contrast(value: ?Float64): T
```

**功能：** 为组件添加对比度效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?Float64|是|-|对比度值。值为1时，显示原图，大于1时，值越大对比度越高，图像越清晰醒目，小于1时，值越小对比度越低。推荐取值范围：[0, 10)。初始值:  1.0|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## func invert(?Float64)

```cangjie
public func invert(value: ?Float64): T
```

**功能：** 为组件添加反色效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?Float64|是|-|反色值，取值范围[0.0, 1.0]。值为1时表示完全反色，值小于等于0时图像无变化。初始值:  0.0|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## func invert(?Float64, ?Float64, ?Float64, ?Float64)

```cangjie
public func invert(low!: ?Float64, high!: ?Float64, threshold!: ?Float64, thresholdRange!: ?Float64): T
```

**功能：** 为组件添加指定范围和阈值的反色效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|low|?Float64|是|-|**命名参数。** 低阈值。初始值:  0.0|
|high|?Float64|是|-|**命名参数。** 高阈值。初始值:  0.0|
|threshold|?Float64|是|-|**命名参数。** 阈值。初始值:  0.0|
|thresholdRange|?Float64|是|-|**命名参数。** 阈值范围。初始值:  0.0|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## func sepia(?Float64)

```cangjie
public func sepia(value: ?Float64): T
```

**功能：** 为组件添加深褐色效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?Float64|是|-|深褐色值。将图像转换为深褐色，降低色彩度，产生温暖复古的图像风格。入参为褐色滤镜强度，值为1则完全是深褐色的，值小于等于0则图像无变化，值大于1会进一步放大色彩偏移比例，图像整体会变得更亮且色彩更加偏黄/偏红，但不属于标准sepia效果。<br> 取值范围：[0.0, +∞)，推荐取值范围：(0.0, 1.0]。初始值:  0.0|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|

## func hueRotate(?Float32)

```cangjie
public func hueRotate(value: ?Float32): T
```

**功能：** 为组件添加色相旋转效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?Float32|是|-|色相旋转角度值。<br>初始值：0.0。|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|


## 示例代码

### 示例1（设置图片不同属性效果）

设置图片的效果，包括阴影，灰度，高光，饱和度，对比度，图像反转，叠色，色相旋转等。

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.UIKit.*
import ohos.state_macro_manage.*
import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    @State
    var cnt: Int64 = 0
    func build() {
        Scroll() {
            Column(10) {
                Text("font blur")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                    .width(90.percent)
                Flex(FlexParams(alignItems: ItemAlign.Center)) {
                    Text("original text")
                        .margin(10)
                    Text("blur text")
                        .blur(5)
                        .margin(10)
                    Text("blur text")
                        .blur(10)
                        .margin(10)
                    Text("blur text")
                        .blur(15)
                        .margin(10)
                }
                    .width(90.percent)
                    .height(40)
                    .backgroundColor(0xF9CF93)

                // 对背景进行模糊
                Text("backdropBlur")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                    .width(90.percent)
                Text("")
                    .width(90.percent)
                    .height(40)
                    .fontSize(16)
                    .backdropBlur(3)
                    .backgroundImage(src: @r(app.media.icon))
                    .backgroundImageSize(width: 300, height: 160)

                Text("shadow")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                    .width(90.percent)
                Image(@r(app.media.icon))
                    .shadow(radius: 10)
                    .height(40)

                // 灰度效果0~1，越接近1，灰度越明显
                Text("grayscale")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                Image(@r(app.media.icon))
                    .grayscale(0.3)
                    .height(40)
                Image(@r(app.media.icon))
                    .grayscale(0.8)
                    .height(40)

                // 高光效果，1为正常图片，<1变暗，>1亮度增大
                Text("brightness")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                Image(@r(app.media.icon))
                    .brightness(1.8)
                    .height(40)
                Image(@r(app.media.icon))
                    .brightness(0)
                    .height(40)

                // 饱和度，原图为1
                Text("saturate")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                    .width(90.percent)
                Image(@r(app.media.icon))
                    .saturate(2.0)
                    .height(40)
                Image(@r(app.media.icon))
                    .saturate(0.7)
                    .height(40)

                // 对比度，1为原图，>1值越大越清晰，<1值越小越模糊
                Text("contrast")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                    .width(90.percent)
                Image(@r(app.media.icon))
                    .contrast(2.0)
                    .height(40)
                Image(@r(app.media.icon))
                    .contrast(0.8)
                    .height(40)

                // 图像反转比例
                Text("invert")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                    .width(90.percent)
                Image(@r(app.media.icon))
                    .invert(0.2)
                    .height(40)
                Image(@r(app.media.icon))
                    .invert(0.8)
                    .height(40)

                // 叠色添加
                Text("colorBlend")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                    .width(90.percent)
                Image(@r(app.media.icon))
                    .colorBlend(Color.GREEN)
                    .height(40)
                Image(@r(app.media.icon))
                    .colorBlend(Color.BLUE)
                    .height(40)

                // 深褐色
                Text("sepia")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                    .width(90.percent)
                Image(@r(app.media.icon))
                    .sepia(0.8)
                    .height(40)

                // 色相旋转
                Text("hueRotate")
                    .fontSize(15)
                    .fontColor(0xCCCCCC)
                    .width(90.percent)
                Image(@r(app.media.icon))
                    .hueRotate(90)
                    .height(40)
            }
        }
    }
}
```

![uni_image_effect](figures/uni_image_effect.png)

### 示例2（设置图片不同变化效果）

该示例主要演示通过invert来实现前景智能取反色，通过pixelStretchEffect设置组件的图像边缘像素扩展效果，通过blendMode将当前组件内容与下方画布内容混合，通过lightUpEffect设置组件的图像渐亮效果，通过sphericalEffect设置组件的图像球面效果，通过renderGroup来设置组件是否先整体离屏渲染绘制后，再与父控件融合绘制，通过systemBarEffect来实现系统导航条智能反色，通过useShadowBatching搭配shadow实现同层阴影不重叠效果，通过freeze设置当前控件和子控件是否整体离屏渲染绘制后重复绘制缓存，通过linearGradientBlur设置组件的内容线性渐变模糊效果。

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.UIKit.*
import ohos.state_macro_manage.*
import ohos.resource_manager.{AppResource, __GenerateResource__}

@Entry
@Component
class EntryView {
    public func build() {
        Scroll() {
            Column() {
                Text("invert").margin(5)
                Stack() {
                    Column()
                    Stack() {
                        Image(@r(app.media.background))
                        Column() {
                            Column()
                                .width(100.percent)
                                .height(30.vp)
                                .invert(
                                    low: 0.0,
                                    high: 1.0,
                                    threshold: 0.5,
                                    thresholdRange: 0.2
                                )
                            Column()
                                .width(100.percent)
                                .height(30.vp)
                                .invert(
                                    low: 0.2,
                                    high: 0.5,
                                    threshold: 0.3,
                                    thresholdRange: 0.2
                                )
                        }
                    }
                    .width(100.vp)
                    .height(100.vp)
                }

                Text("pixelStretchEffect").margin(5)
                Column() {
                    Text('This is the text content with letterSpacing 0.')
                        .letterSpacing(0)
                        .fontSize(12)
                        .borderWidth(1.vp)
                        .padding(10.vp)
                        .width(50.percent)
                        .pixelStretchEffect(top: 5.vp, left: 20.vp, bottom: 10.vp)
                        .id("test_pixelStretchEffect")
                }
                .width(200.vp)
                .height(110.vp)
                Column() {
                    Text('This is the text content with letterSpacing 0.')
                        .letterSpacing(0)
                        .fontSize(12)
                        .borderWidth(1.vp)
                        .padding(10.vp)
                        .width(50.percent)
                }
                .width(200.vp)
                .height(110.vp)

                Text("blendMode")
                Column() {
                    Column() {
                        Text("Blue")
                            .width(40)
                            .height(40)
                            .backgroundColor(Color.BLUE)
                        Text("red")
                            .width(40)
                            .height(40)
                            .backgroundColor(Color.RED)
                            .position(x: 20, y: 20)
                    }
                        .height(80)
                        .width(100)
                        .blendMode(BlendMode.OVERLAY, BlendApplyType.OFFSCREEN)
                        .id("test_blendMode")
                }
                    .height(90)
                    .width(200)
                    .backgroundImage(repeat: ImageRepeat.X, src: @r(app.media.background))

                Text("lightUpEffect")
                Text('This is the text content with letterSpacing 0.')
                    .borderWidth(1)
                    .padding(10)
                    .width(100)
                    .lightUpEffect(0.6)
                    .id("test_lightUpEffect")

                Text("sphericalEffect")
                TextInput(placeholder: "请输入变化范围百分比（[0%,100%]）")
                    .width(200)
                    .height(35)
                    .caretColor(Color.RED)
                    .placeholderColor(Color.BLUE)
                    .placeholderFont(size: 20.vp)
                    .sphericalEffect(0.5)
                    .id("test_sphericalEffect")

                Text("renderGroup")
                Column() {
                    Row() {
                        Row() {
                            Row()
                                .backgroundColor(Color.BLACK)
                                .width(100.vp)
                                .height(100.vp)
                                .opacity(1)
                        }
                        .backgroundColor(Color.WHITE)
                        .width(150.vp)
                        .height(150.vp)
                        .justifyContent(FlexAlign.Center)
                        .opacity(0.6)
                        .renderGroup(true)
                    }
                    .backgroundColor(Color.BLACK)
                    .width(200)
                    .height(200)
                    .justifyContent(FlexAlign.Center)
                    .opacity(1)
                    .margin(20.vp)

                    Row() {
                        Row() {
                            Row()
                                .backgroundColor(Color.BLACK)
                                .width(100.vp)
                                .height(100.vp)
                                .opacity(1)
                        }
                        .backgroundColor(Color.WHITE)
                        .width(150.vp)
                        .height(150.vp)
                        .justifyContent(FlexAlign.Center)
                        .opacity(0.6)
                        .renderGroup(false)
                        .id("test_renderGroup")
                    }
                    .backgroundColor(Color.BLACK)
                    .width(200)
                    .height(200)
                    .justifyContent(FlexAlign.Center)
                    .opacity(1)
                    .margin(20.vp)
                }
                .width(380.vp)
                .height(500.vp)

                Text("systemBarEffect")
                Stack() {
                    Image("")
                        .width(100)
                        .height(100)
                        .backgroundColor(Color.BLUE)
                    Column()
                        .width(80)
                        .height(10)
                        .systemBarEffect()
                        .borderRadius(5)
                        .margin(bottom: 20)
                        .id("test_systemBarEffect")
                }

                Text("useShadowBatching")
                Column() {
                    Column() {
                    }
                    .width(200)
                    .height(30)
                    .margin(top: 5)
                    .backgroundColor(0xFFE4C4)
                    .shadow(radius: 120, color: Color.GREEN, offsetX: 0, offsetY: 0)

                    Column() {
                    }
                    .width(200)
                    .height(30)
                    .margin(top: 5)
                    .backgroundColor(0xFFE4C4)
                    .shadow(radius: 120, color: Color.RED, offsetX: 0, offsetY: 0)
                    .backgroundColor(Color.WHITE)
                }
                .borderWidth(1)
                .width(300)
                .height(100)
                .useShadowBatching(true)
                .id("test_useShadowBatching")

                Text("freeze")
                Column() {
                    Text("freeze: true")
                        .width(100)
                        .height(40)
                        .backgroundColor(Color.BLUE)
                }
                .opacity(0.5)
                .freeze(true)
                .id("test_freeze")
                Column() {
                    Text("freeze: false")
                        .width(100)
                        .height(40)
                        .backgroundColor(Color.BLUE)
                }
                .opacity(0.5)
                .freeze(false)

                Text("linearGradientBlur")
                Image(@r(app.media.startIcon))
                    .linearGradientBlur(
                        60.0,
                        LinearGradientBlurOptions(fractionStops: [(0.0, 0.0), (0.0, 0.33), (1.0, 0.66), (1.0, 1.0)],
                        direction: GradientDirection.Bottom)
                    )
                    .width(200)
                    .height(200)
                    .id("test_linearGradientBlur")
            }
            .width(380)
            .borderWidth(1)
            .backgroundColor(Color.GRAY)
        }
    }
}
```

![uni_image_effect](figures/uni_image_effect_1.png)

![uni_image_effect](figures/uni_image_effect_2.png)

![uni_image_effect](figures/uni_image_effect_3.png)

