# 色彩管理开发指导

## 简介

色彩管理模块提供管理抽象化色域对象的能力，包括色域对象的创建与色域基础属性的获取等。通过该模块，开发者可以创建标准或自定义色域对象，并获取色域的各种属性信息。

## 场景介绍

主要场景有：

- 创建标准色域对象，如sRGB、Adobe RGB等。
- 创建自定义色域对象。
- 获取色域对象的属性信息，如色域类型、gamma值、白点值等。
- 在图形图像处理中使用不同的色域配置。

## 接口说明

完整的仓颉 API 说明以及实例代码请参见：[色彩管理接口](../../application-dev/reference/ArkGraphics2D/cj-apis-color_manager.md)。

具体接口说明如下表。

| 接口名 | 功能描述 |
| ------------------------------------------ | ----------------------------------------------------------- |
| create(colorSpaceName: ColorSpace) | 创建标准色域对象 |
| create(primaries: ColorSpacePrimaries, gamma: Float32) | 创建用户自定义色域对象 |
| ColorSpaceManager.getColorSpaceName() | 获取色域类型 |
| ColorSpaceManager.getGamma() | 获取色域gamma值 |
| ColorSpaceManager.getWhitePoint() | 获取色域白点值 |
| ColorSpaceManager.getPrimaries() | 获取色域三原色信息 |
| ColorSpacePrimaries | 色域三原色和白点信息类 |

## 开发示例

以下示例演示了如何使用色彩管理模块创建和操作色域对象。

### 创建标准色域对象

以下示例代码演示了如何创建标准色域对象并获取其属性。

<!-- compile -->

```cangjie
// index.cj
import kit.ArkGraphics2D.*
import ohos.base.*

func createStandardColorSpace(): Unit {
    // 创建sRGB色域对象
    let srgbColorSpace = create(ColorSpace.Srgb)
    AppLog.info("Created sRGB color space")
    
    // 获取色域类型
    let colorSpaceType = srgbColorSpace.getColorSpaceName()
    AppLog.info("Color space type: ${colorSpaceType.toString()}")
    
    // 获取gamma值
    let gammaValue = srgbColorSpace.getGamma()
    AppLog.info("Gamma value: ${gammaValue}")
    
    // 获取白点值
    let whitePoint = srgbColorSpace.getWhitePoint()
    AppLog.info("White point: [${whitePoint[0]}, ${whitePoint[1]}]")
    
    // 获取三原色信息
    let primaries = srgbColorSpace.getPrimaries()
    AppLog.info("Red point: [${primaries.redX}, ${primaries.redY}]")
    AppLog.info("Green point: [${primaries.greenX}, ${primaries.greenY}]")
    AppLog.info("Blue point: [${primaries.blueX}, ${primaries.blueY}]")
    AppLog.info("White point: [${primaries.whitePointX}, ${primaries.whitePointY}]")
}
```

### 创建自定义色域对象

以下示例代码演示了如何创建自定义色域对象。

<!-- compile -->

```cangjie
// index.cj
import kit.ArkGraphics2D.*
import ohos.base.*

func createCustomColorSpace(): Unit {
    // 定义三原色和白点坐标
    let primaries = ColorSpacePrimaries(
        redX=0.64, 
        redY=0.33,
        greenX=0.30, 
        greenY=0.60,
        blueX=0.15, 
        blueY=0.06,
        whitePointX=0.3127, 
        whitePointY=0.3290
    )
    
    // 创建自定义色域对象，gamma值设为2.2
    let customColorSpace = create(primaries, 2.2)
    AppLog.info("Created custom color space")
    
    // 获取色域类型（应为Custom）
    let colorSpaceType = customColorSpace.getColorSpaceName()
    AppLog.info("Color space type: ${colorSpaceType.toString()}")
    
    // 获取gamma值
    let gammaValue = customColorSpace.getGamma()
    AppLog.info("Gamma value: ${gammaValue}")
    
    // 获取白点值
    let whitePoint = customColorSpace.getWhitePoint()
    AppLog.info("White point: [${whitePoint[0]}, ${whitePoint[1]}]")
}
```

### 比较不同色域对象

以下示例代码演示了如何比较不同色域对象。

<!-- compile -->

```cangjie
// index.cj
import kit.ArkGraphics2D.*
import ohos.base.*

func compareColorSpaces(): Unit {
    // 创建不同的色域对象
    let srgbColorSpace = create(ColorSpace.Srgb)
    let adobeRgbColorSpace = create(ColorSpace.AdobeRgb1998)
    let bt709ColorSpace = create(ColorSpace.Bt709)
    
    // 获取色域类型
    let srgbType = srgbColorSpace.getColorSpaceName()
    let adobeRgbType = adobeRgbColorSpace.getColorSpaceName()
    let bt709Type = bt709ColorSpace.getColorSpaceName()
    
    AppLog.info("sRGB type: ${srgbType.toString()}")
    AppLog.info("Adobe RGB type: ${adobeRgbType.toString()}")
    AppLog.info("BT.709 type: ${bt709Type.toString()}")
    
    // 比较色域类型
    if (srgbType == ColorSpace.Srgb) {
        AppLog.info("Confirmed sRGB color space")
    }
    
    if (srgbType != adobeRgbType) {
        AppLog.info("sRGB and Adobe RGB are different color spaces")
    }
    
    // 比较gamma值
    let srgbGamma = srgbColorSpace.getGamma()
    let adobeRgbGamma = adobeRgbColorSpace.getGamma()
    let bt709Gamma = bt709ColorSpace.getGamma()
    
    AppLog.info("sRGB gamma: ${srgbGamma}")
    AppLog.info("Adobe RGB gamma: ${adobeRgbGamma}")
    AppLog.info("BT.709 gamma: ${bt709Gamma}")
}
```

### 实际应用场景示例

以下示例代码演示了色彩管理在实际应用场景中的使用。

<!-- compile -->

```cangjie
// index.cj
import kit.ArkGraphics2D.*
import ohos.base.*

class ColorSpaceManagerExample {
    var currentColorSpace: ?ColorSpaceManager = None
    
    // 设置当前工作色域
    public func setColorSpace(spaceType: ColorSpace): Unit {
        try {
            this.currentColorSpace = create(spaceType)
            AppLog.info("Set color space to: ${spaceType.toString()}")
        } catch (e: BusinessException) {
            AppLog.error("Failed to create color space. Error code: ${e.code}, message: ${e.message}")
        }
    }
    
    // 获取当前色域信息
    public func getCurrentColorSpaceInfo(): Unit {
        if (this.currentColorSpace.isNone()) {
            AppLog.warn("No color space set")
            return
        }
        
        try {
            let colorSpaceType = this.currentColorSpace?.getColorSpaceName()
            let gamma = this.currentColorSpace?.getGamma()
            let whitePoint = this.currentColorSpace?.getWhitePoint()
            
            AppLog.info("Current color space: ${colorSpaceType.getOrThrow().toString()}")
            AppLog.info("Gamma: ${gamma.getOrThrow()}")
            AppLog.info("White point: [${whitePoint.getOrThrow()[0]}, ${whitePoint.getOrThrow()[1]}]")
        } catch (e: BusinessException) {
            AppLog.error("Failed to get color space info. Error code: ${e.code}, message: ${e.message}")
        }
    }
    
    // 转换色域（示例）
    public func convertColorSpace(source: ColorSpace, target: ColorSpace): Unit {
        AppLog.info("Converting from ${source.toString()} to ${target.toString()}")
        // 实际的色彩转换逻辑会更复杂，这里仅作演示
        this.setColorSpace(target)
    }
}

// 使用示例
let colorManager = ColorSpaceManagerExample()

// 设置为sRGB色域
colorManager.setColorSpace(ColorSpace.Srgb)
colorManager.getCurrentColorSpaceInfo()

// 转换为Adobe RGB色域
colorManager.convertColorSpace(ColorSpace.Srgb, ColorSpace.AdobeRgb1998)
colorManager.getCurrentColorSpaceInfo()
```

## 相关信息

- 支持的标准色域类型：
  - Srgb：sRGB色域，系统默认色域类型
  - AdobeRgb1998：Adobe RGB(1998)色域
  - Bt709：BT.709色域
  - DisplayP3：Display P3色域
  - Bt2020Hlg、Bt2020Pq：BT.2020色域的不同转换函数
  - 更多色域类型请参考[ColorSpace枚举](../../application-dev/reference/ArkGraphics2D/cj-apis-color_manager.md#enum-colorspace)