# ohos.base（公共回调信息）

本模块定义了接口调用时出现的公共异常信息。

## 导入模块

```cangjie
import ohos.base.*
```

## let Main

```cangjie
public let Main: MainThreadContext = MainThreadContext.instance_
```

**功能：** Main 实际为 MainThreadContext 类型的对象，表示此上下文中的 thread 将会与主线程（UI线程）绑定。

**类型：** [MainThreadContext](#class-mainthreadcontext)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

## func launch(() -> Unit)

```cangjie
public func launch(task: () -> Unit): Unit
```

**功能：** 将任务提交到主线程进行执行。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|task|()->Unit|是|-|执行任务。|

## interface CollectionEx

```cangjie
public interface CollectionEx<T> {
    prop size: Int64
    operator func [](idx: Int64, value!: T): Unit
    operator func [](idx: Int64): T
}
```

**功能：** 数组类型。内部接口，框架使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### prop size

```cangjie
prop size: Int64
```

**功能：** 数组大小。

**类型：** Int64

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### func [](Int64, T)

```cangjie
operator func [](idx: Int64, value!: T): Unit
```

**功能：** 在指定索引处写入数组元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|idx|Int64|是|-|索引值。|
|value|T|是|-| **命名参数。** 写入值。|

### func \[](Int64)

```cangjie
operator func [](idx: Int64): T
```

**功能：** 通过索引获取数组元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|idx|Int64|是|-|索引值。|

**返回值：**

|类型|说明|
|:----|:----|
|T|数组元素。|

## interface Length

```cangjie
public interface Length {
    prop value: Float64
    prop unitType: LengthType
}
```

**功能：** Float64、Int64、AppResource 均实现了 Length 接口类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### prop unitType

```cangjie
prop unitType: LengthType
```

**功能：** UI框架使用。

**类型：** [LengthType](#enum-lengthtype)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### prop value

```cangjie
prop value: Float64
```

**功能：** UI框架使用。

**类型：** Float64

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

## interface LengthProp

```cangjie
public interface LengthProp {
    prop px: Length
    prop vp: Length
    prop fp: Length
    prop percent: Length
    prop lpx: Length
}
```

**功能：** 像素单位。UI框架使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### prop fp

```cangjie
prop fp: Length
```

**功能：** 字体像素，与vp类似适用屏幕密度变化，随系统字体大小设置变化。

**类型：** [Length](#interface-length)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### prop lpx

```cangjie
prop lpx: Length
```

**功能：**视窗逻辑像素单位，l.px单位为实际屏幕宽度与逻辑宽度（通过designWidth配置）的比值，designWidth默认值为720。当designWidth为720时，在实际宽度为1440物理像素的屏幕上，1l.px为2.px大小。

**类型：** [Length](#interface-length)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### prop percent

```cangjie
prop percent: Length
```

**功能：** 百分比类型，用于描述以percent像素单位为单位的长度。

**类型：** [Length](#interface-length)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### prop px

```cangjie
prop px: Length
```

**功能：** 屏幕物理像素单位。

**类型：** [Length](#interface-length)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### prop vp

```cangjie
prop vp: Length
```

**功能：** 屏幕密度相关像素，根据屏幕像素密度转换为屏幕物理像素，当数值不带单位时，默认单位vp。在实际宽度为1440物理像素的屏幕上，1vp约等于3px。<br/>**说明：** <br/> vp与px的比例与屏幕像素密度有关。

**类型：** [Length](#interface-length)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

## interface ResourceColor

```cangjie
public interface ResourceColor {
    func toUInt32(): UInt32
}
```

**功能：** Color、UInt32、Int64、AppResource 均实现了 ResourceColor 接口类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### func toUInt32()

```cangjie
func toUInt32(): UInt32
```

**功能：**转为Uint32颜色取值。

**返回值：**

|类型|说明|
|:----|:----|
|UInt32|Uint32颜色取值。|

## interface ResourceStr

```cangjie
public interface ResourceStr {}
```

**功能：** 字符串类型，用于描述字符串入参可以使用的类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

## class Color

```cangjie
public class Color <: ResourceColor {
    public static let Black: Color = Color(0xff000000)
    public static let Blue: Color = Color(0xff0000ff)
    public static let Gray: Color = Color(0xff808080)
    public static let Green: Color = Color(0xff008000)
    public static let Red: Color = Color(0xffff0000)
    public static let White: Color = Color(0xffffffff)
    public static let Transparent: Color = Color(0, 0, 0, alpha: 0.0)
    public init(red: UInt8, green: UInt8, blue: UInt8, alpha!: Float32 = 1.0)
    public init(value: UInt32)
}
```

**功能：** 颜色类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**父类型：**

- [ResourceColor](#interface-resourcecolor)

### static let Black

```cangjie
public static let Black: Color = Color(0xff000000)
```

**功能：** 黑色。

**类型：** [Color](#class-color)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### static let Blue

```cangjie
public static let Blue: Color = Color(0xff0000ff)
```

**功能：** 蓝色。

**类型：** [Color](#class-color)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### static let Gray

```cangjie
public static let Gray: Color = Color(0xff808080)
```

**功能：** 灰色。

**类型：** [Color](#class-color)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### static let Green

```cangjie
public static let Green: Color = Color(0xff008000)
```

**功能：** 绿色。

**类型：** [Color](#class-color)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### static let Red

```cangjie
public static let Red: Color = Color(0xffff0000)
```

**功能：** 红色。

**类型：** [Color](#class-color)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### static let Transparent

```cangjie
public static let Transparent: Color = Color(0, 0, 0, alpha: 0.0)
```

**功能：** 透明色。

**类型：** [Color](#class-color)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### static let White

```cangjie
public static let White: Color = Color(0xffffffff)
```

**功能：** 白色。

**类型：** [Color](#class-color)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### init(UInt8, UInt8, UInt8, Float32)

```cangjie
public init(red: UInt8, green: UInt8, blue: UInt8, alpha!: Float32 = 1.0)
```

**功能：**构造一个Color类型的对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|red|UInt8|是|-|RGB中红色通道取值。|
|green|UInt8|是|-|RGB中绿色通道取值。|
|blue|UInt8|是|-|RGB中蓝色通道取值。|
|alpha|Float32|否|1.0|***\*命名参数。\**** 透明通道取值，取值范围 [0.0, 1.0]。|

### init(UInt32)

```cangjie
public init(value: UInt32)
```

**功能：** 构造一个Color类型的对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|UInt32|是|-|Uint32颜色取值。alpha，R，G，B通道按顺序各占输入的8位，若只输入R,G,B三个通道，则alpha通道默认取0xff。|

### func toUInt32()

```cangjie
public func toUInt32(): UInt32
```

**功能：** 转为Uint32颜色取值。

**返回值：**

|类型|说明|
|:----|:----|
|UInt32|Uint32颜色取值。|

## class MainThreadContext

```cangjie
public class MainThreadContext {}
```

**功能：** 框架使用的线程上下文。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### func end()

```cangjie
public func end(): Unit
```

**功能：** UI框架使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### func hasEnded()

```cangjie
public func hasEnded(): Bool
```

**功能：** UI框架使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Bool|-|

## class ReuseParams

```cangjie
public class ReuseParams {
    public init(arr: Array<(String, Any)>)
}
```

**功能：** aboutToReuse生命周期函数的参数，开发者可以从中获取可复用组件的构造参数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### init(Array\<(String,Any)>)

```cangjie
public init(arr: Array<(String, Any)>)
```

**功能：** 创建一个ReuseParams对象，通常情况下开发者不会调用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|arr| Array\<(String, Any)> |是|-|存放组件构造参数元组的数组。|

### func get\<T>(String)

```cangjie
public func get<T>(key: String): ?T
```

**功能：** 通过key获取对应的构造参数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|key|String|是|-|构造参数的名称。|

**返回值：**

|类型|说明|
|:----|:----|
|?T|构造参数的值。|

## enum LengthType

```cangjie
public enum LengthType <: Length & Equatable<LengthType> {
    | px(Float64)
    | vp(Float64)
    | fp(Float64)
    | percent(Float64)
    | lpx(Float64)
    | ...
}
```

**功能：** 长度类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**父类型：**

- [Length](#interface-length)
- Equatable\<LengthType>

### fp(Float64)

```cangjie
fp(Float64)
```

**功能：** 字体像素单位。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### lpx(Float64)

```cangjie
lpx(Float64)
```

**功能：** 逻辑像素单位。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### percent(Float64)

```cangjie
percent(Float64)
```

**功能：** 百分比。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### px(Float64)

```cangjie
px(Float64)
```

**功能：** 基本像素单位。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### vp(Float64)

```cangjie
vp(Float64)
```

**功能：** 屏幕密度单位。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### prop unitType

```cangjie
public prop unitType: LengthType
```

**功能：** UI框架使用。

**类型：** [LengthType](#enum-lengthtype)

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### prop value

```cangjie
public prop value: Float64
```

**功能：** UI框架使用。

**类型：** Float64

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### static func parse(Int32)

```cangjie
public static func parse(value: Int32): LengthType
```

**功能：** 根据长度类型值，构造长度类型实例。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|Int32|是|-|长度类型的值。|

**返回值：**

|类型|说明|
|:----|:----|
|[LengthType](#enum-lengthtype)|长度类型实例。|

### func !=(LengthType)

```cangjie
public operator func !=(other: LengthType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[LengthType](#enum-lengthtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(LengthType)

```cangjie
public operator func ==(other: LengthType): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[LengthType](#enum-lengthtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func getValue()

```cangjie
public func getValue(): Int32
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Int32|枚举的值。|

## type Callback

```cangjie
public type Callback<T, V>=(T) -> V
```

**功能：** [Callback](#type-callback)是[(T) -> V](#type-callback)类型的别名。

## type VoidCallback

```cangjie
public type VoidCallback =() -> Unit
```

**功能：** [VoidCallback](#type-voidcallback)是[() -> Unit](#type-voidcallback)类型的别名。
