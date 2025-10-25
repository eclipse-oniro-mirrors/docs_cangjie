# ohos.i18n（国际化-I18n）

本模块提供系统相关的或者增强的国际化能力，包括区域管理、电话号码处理、日历等，相关接口为ECMA 402标准中未定义的补充接口。Intl模块提供了ECMA 402标准定义的基础国际化接口，与本模块共同使用可提供完整地国际化支持能力。

## 导入模块

```cangjie
import kit.LocalizationKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func getCalendar(String, ?CalendarType)

```cangjie
public func getCalendar(locale: String, calendarType!: ?CalendarType = None): Calendar
```

**功能：** 获取指定区域和日历类型对应的日历对象。
**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|locale|String|是|-|表示区域信息的字符串，由语言、脚本、国家或地区组成。|
|calendarType|?CalendarType|否|None|日历类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Calendar|返回与指定区域和日历类型对应的日历对象。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.i18n.*

let calendar = getCalendar("en-US", calendarType: CalendarType.Buddhist)// 获得一个基于 en-US 区域设置的佛教日历对象
```

## class Calendar

```cangjie
public class Calendar {}
```

**功能：** 实体日历对象。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### func add(String, Int32)

```cangjie
public func add(field: String, amount: Int32): Unit
```

**功能：** 在日历的给定字段进行加减操作。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|field|String|是|-|指定进行操作的日历字段，目前支持的field值有year, month, week_of_year, week_of_month, date, day_of_year, day_of_week, day_of_week_in_month, hour, hour_of_day, minute, second, millisecond。|
|amount|Int32|是|-|进行加减操作的具体数值。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("zh-Hans")
calendar.set(2021,11,11) // set time to 2021.12.11
calendar.add("year", 3)
let res = calendar.get("year") // res = 2024
```

### func get(String)

```cangjie
public func get(field: String): Int32
```

**功能：** 获取日历对象中与field相关联的值。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|field|String|是|-|通过field来获取日历对象相应的值。目前支持的field值请参考下表。|

**返回值：**

|类型|说明|
|:----|:----|
|Int32|与field相关联的值，如当前Calendar对象的内部日期的年份为1990，get(“year”)返回1990。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("en-US")
calendar.set(2024, 1, 1, hour: 12, minute: 30, second: 30)
let year = calendar.get("year") // 2024
let month = calendar.get("month") // 1
let date = calendar.get("date") // 1
let hour = calendar.get("hour_of_day") // 12
let minute = calendar.get("minute") // 30
let second = calendar.get("second") // 30
```

### func getDisplayName(String)

```cangjie
public func getDisplayName(locale: String): String
```

**功能：** 获取日历对象在该区域的名字。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|locale|String|是|-|表示区域信息的字符串，由语言、脚本、国家或地区组成。|

**返回值：**

|类型|说明|
|:----|:----|
|String|日历在locale所指示区域的名字。如buddhist在en-US上显示的名称为“Buddhist Calendar”。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.i18n.CalendarType

let calendar = getCalendar("en-US", calendarType: CalendarType.Buddhist)
let res = calendar.getDisplayName("zh") // res = "佛历"
```

### func getFirstDayOfWeek()

```cangjie
public func getFirstDayOfWeek(): Int32
```

**功能：** 获取日历对象的一周起始日。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Int32|获取一周的起始日，1代表周日，7代表周六。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("en-US")
let res = calendar.getFirstDayOfWeek() // res = 1
```

### func getMinimalDaysInFirstWeek()

```cangjie
public func getMinimalDaysInFirstWeek(): Int32
```

**功能：** 获取一年中第一周的最小天数。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Int32|一年中第一周的最小天数。这表示为了确定一年中的第一周至少需要包含的天数。例如，如果这个值设置为4，那么一年的第一周必须至少包含4天，否则这些天将被算作上一年的最后一周。这一设定帮助确保周数的计算符合不同地区的习惯。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("zh-Hans")
let res = calendar.getMinimalDaysInFirstWeek() // res = 1
```

### func getTimeInMillis()

```cangjie
public func getTimeInMillis(): Float64
```

**功能：** 获取当前日历的UTC毫秒数。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Float64|当前日历的UTC毫秒数。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("en-US")
calendar.setTime(5000.0)
let millis = calendar.getTimeInMillis() // millis = 5000
```

### func getTimeZone()

```cangjie
public func getTimeZone(): String
```

**功能：** 获取日历对象的时区。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|合法的时区ID，如“Asia/Shanghai”。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.i18n.CalendarType

let calendar = getCalendar("zh-Hans", calendarType: CalendarType.Chinese)
calendar.setTimeZone("Asia/Shanghai")
let timeZone = calendar.getTimeZone() // timeZone = "Asia/Shanghai"
```

### func set(Int32, Int32, Int32, ?Int32, ?Int32, ?Int32)

```cangjie
public func set(year: Int32, month: Int32, date: Int32, hour!: ?Int32 = None, minute!: ?Int32 = None, second!: ?Int32 = None): Unit
```

**功能：** 设置日历对象的年、月、日、时、分、秒。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|year|Int32|是|-|设置的年。|
|month|Int32|是|-|设置的月。说明：月份从0开始计数，如0表示一月。|
|date|Int32|是|-|设置的日。|
|hour|?Int32|否|None|**命名参数。** 设置的小时。-1代表系统小时。|
|minute|?Int32|否|None|**命名参数。** 设置的分钟。-1代表系统分钟。|
|second|?Int32|否|None|**命名参数。** 设置的秒。-1代表系统秒。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("zh-Hans")
calendar.set(2021,11,11)  // set time to 2021.12.11
```

### func setFirstDayOfWeek(Int32)

```cangjie
public func setFirstDayOfWeek(value: Int32): Unit
```

**功能：** 设置每一周的起始日。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|Int32|是|-|设置一周的起始日，1代表周日，7代表周六。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("zh-Hans")
calendar.setFirstDayOfWeek(3)
let firstDayOfWeek = calendar.getFirstDayOfWeek() // firstDayOfWeek = 3
```

### func setMinimalDaysInFirstWeek(Int32)

```cangjie
public func setMinimalDaysInFirstWeek(value: Int32): Unit
```

**功能：** 设置一年中第一周的最小天数。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|Int32|是|-|一年中第一周的最小天数。这表示为了确定一年中的第一周至少需要包含的天数。例如，如果这个值为4，那么一年的第一周必须至少包含4天，否则这些天将被算作上一年的最后一周。这一设定帮助确保周数的计算符合不同地区的习惯。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("zh-Hans")
calendar.setMinimalDaysInFirstWeek(3)
let minimalDaysInFirstWeek = calendar.getMinimalDaysInFirstWeek() // minimalDaysInFirstWeek = 3
```

### func setTime(Float64)

```cangjie
public func setTime(time: Float64): Unit
```

**功能：** 设置日历对象内部的时间日期，time为从1970.1.1 00:00:00 GMT逝去的毫秒数。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|time|Float64|是|-|time为从1970.1.1 00:00:00 GMT逝去的毫秒数。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("en-US")
calendar.setTime(10540800000.0)
```

### func setTimeZone(String)

```cangjie
public func setTimeZone(timeZone: String): Unit
```

**功能：** 设置日历对象的时区。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|timeZone|String|是|-|合法的时区ID，如“Asia/Shanghai”。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("en-US")
calendar.setTimeZone("Asia/Shanghai")
```

## class System

```cangjie
public class System {}
```

**功能：** I18n系统对象。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### static func getAppPreferredLanguage()

```cangjie
public static func getAppPreferredLanguage(): String
```

**功能：** 获取应用的偏好语言。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|应用的偏好语言。|

**示例：**

<!-- compile -->

```cangjie
// index.cj
import ohos.i18n.*
import kit.LocalizationKit.getCalendar

let appPreferredLanguage = System.getAppPreferredLanguage() // 获取应用偏好语言
```

## enum CalendarType

```cangjie
public enum CalendarType {
    | Buddhist
    | Chinese
    | Coptic
    | Ethiopic
    | Hebrew
    | Gregory
    | Indian
    | IslamicCivil
    | IslamicTbla
    | IslamicUmalqura
    | Japanese
    | Persian
    | ...
}
```

**功能：** 日历类型枚举，用于指定不同的日历系统。

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### Buddhist

```cangjie
Buddhist
```

**功能：** buddhist日历类型

**系统能力：**  SystemCapability.Global.I18n

**起始版本：** 22

### Chinese

```cangjie
Chinese
```

**功能：**  coptic日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### Coptic

```cangjie
Coptic
```

**功能：**  coptic日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### Ethiopic

```cangjie
Ethiopic
```

**功能：**  ethiopic日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### Hebrew

```cangjie
Hebrew
```

**功能：**  hebrew日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### Gregory

```cangjie
Gregory
```

**功能：**  gregory日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### Indian

```cangjie
Indian
```

**功能：**  indian日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### IslamicCivil

```cangjie
IslamicCivil
```

**功能：**  IslamicCivil日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### IslamicTbla

```cangjie
IslamicTbla
```

**功能：**  IslamicTbla日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### IslamicUmalqura

```cangjie
IslamicUmalqura
```

**功能：**  IslamicUmalqura日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### Japanese

```cangjie
Japanese
```

**功能：**  Japanese日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22

### Persian

```cangjie
Persian
```

**功能：**  Persian日历类型

**系统能力：** SystemCapability.Global.I18n

**起始版本：** 22
