# ohos.i18n (Internationalization-I18n)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides system-related or enhanced internationalization capabilities, including locale management, phone number processing, calendars, etc. The interfaces here supplement those not defined in the ECMA 402 standard. The Intl module offers basic internationalization interfaces as defined by ECMA 402 standard, which when used together with this module provide comprehensive internationalization support.

## Importing the Module

```cangjie
import kit.LocalizationKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code begins with a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the aforementioned sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## func getCalendar(String, ?CalendarType)

```cangjie
public func getCalendar(locale: String, calendarType!: ?CalendarType = None): Calendar
```

**Function:** Obtains a calendar object corresponding to the specified locale and calendar type.  
**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| locale | String | Yes | - | A string representing locale information, composed of language, script, country or region. |
| calendarType | ?CalendarType | No | None | The calendar type. |

**Return Value:**

| Type | Description |
|:----|:----|
| Calendar | Returns the calendar object corresponding to the specified locale and calendar type. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.i18n.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("en-US", calendarType: CalendarType.Buddhist) // Obtains a Buddhist calendar object based on en-US locale
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class Calendar

```cangjie
public class Calendar {}
```

**Function:** A physical calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

### func add(String, Int32)

```cangjie
public func add(field: String, amount: Int32): Unit
```

**Function:** Performs addition or subtraction operations on the specified field of the calendar.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Specifies the calendar field for the operation. Currently supported field values include year, month, week_of_year, week_of_month, date, day_of_year, day_of_week, day_of_week_in_month, hour, hour_of_day, minute, second, millisecond. |
| amount | Int32 | Yes | - | The specific value for the addition or subtraction operation. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("zh-Hans")
    calendar.set(2021,11,11) // set time to 2021.12.11
    calendar.add("year", 3)
    let res = calendar.get("year") // res = 2024
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func get(String)

```cangjie
public func get(field: String): Int32
```

**Function:** Gets the value associated with the specified field in the calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Retrieves the corresponding value from the calendar object via the field. For currently supported field values, refer to the table below. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | The value associated with the field. For example, if the internal date year of the current Calendar object is 1990, get("year") returns 1990. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("en-US")
    calendar.set(2024, 1, 1, hour: 12, minute: 30, second: 30)
    let year = calendar.get("year") // 2024
    let month = calendar.get("month") // 1
    let date = calendar.get("date") // 1
    let hour = calendar.get("hour_of_day") // 12
    let minute = calendar.get("minute") // 30
    let second = calendar.get("second") // 30
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getDisplayName(String)

```cangjie
public func getDisplayName(locale: String): String
```

**Function:** Gets the name of the calendar object in the specified locale.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| locale | String | Yes | - | A string representing locale information, composed of language, script, country or region. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | The name of the calendar in the locale indicated. For example, "Buddhist Calendar" is displayed for "buddhist" in en-US. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.i18n.CalendarType
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("en-US", calendarType: CalendarType.Buddhist)
    let res = calendar.getDisplayName("zh") // res = "佛历"
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getFirstDayOfWeek()

```cangjie
public func getFirstDayOfWeek(): Int32
```

**Function:** Gets the first day of the week for the calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Gets the first day of the week, where 1 represents Sunday and 7 represents Saturday. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("en-US")
    let res = calendar.getFirstDayOfWeek() // res = 1
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getMinimalDaysInFirstWeek()

```cangjie
public func getMinimalDaysInFirstWeek(): Int32
```

**Function:** Gets the minimal number of days in the first week of the year.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | The minimal number of days in the first week of the year. This indicates the minimum number of days required to determine the first week of the year. For example, if this value is set to 4, then the first week of the year must contain at least 4 days; otherwise, these days will be counted as part of the last week of the previous year. This setting helps ensure week numbering conforms to regional customs. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("zh-Hans")
    let res = calendar.getMinimalDaysInFirstWeek() // res = 1
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getTimeInMillis()

```cangjie
public func getTimeInMillis(): Float64
```

**Function:** Gets the current calendar's UTC time in milliseconds.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Return Value:**

| Type | Description |
|:----|:----|
| Float64 | The current calendar's UTC time in milliseconds. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("en-US")
    calendar.setTime(5000.0)
    let millis = calendar.getTimeInMillis() // millis = 5000
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getTimeZone()

```cangjie
public func getTimeZone(): String
```

**Function:** Gets the time zone of the calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Return Value:**

| Type | Description |
|:----|:----|
| String | A valid time zone ID, such as "Asia/Shanghai". |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.i18n.CalendarType
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("zh-Hans", calendarType: CalendarType.Chinese)
    calendar.setTimeZone("Asia/Shanghai")
    let timeZone = calendar.getTimeZone() // timeZone = "Asia/Shanghai"
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func set(Int32, Int32, Int32, ?Int32, ?Int32, ?Int32)

```cangjie
public func set(year: Int32, month: Int32, date: Int32, hour!: ?Int32 = None, minute!: ?Int32 = None, second!: ?Int32 = None): Unit
```

**Function:** Sets the year, month, day, hour, minute, and second of the calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| year | Int32 | Yes | - | The year to set. |
| month | Int32 | Yes | - | The month to set. Note: Months start from 0, where 0 represents January. |
| date | Int32 | Yes | - | The day to set. |
| hour | ?Int32 | No | None | **Named parameter.** The hour to set. -1 represents the system hour. |
| minute | ?Int32 | No | None | **Named parameter.** The minute to set. -1 represents the system minute. |
| second | ?Int32 | No | None | **Named parameter.** The second to set. -1 represents the system second. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("zh-Hans")
    calendar.set(2021,11,11)  // set time to 2021.12.11
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setFirstDayOfWeek(Int32)

```cangjie
public func setFirstDayOfWeek(value: Int32): Unit
```

**Function:** Sets the first day of the week.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Sets the first day of the week, where 1 represents Sunday and 7 represents Saturday. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("zh-Hans")
    calendar.setFirstDayOfWeek(3)
    let firstDayOfWeek = calendar.getFirstDayOfWeek() // firstDayOfWeek = 3
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setMinimalDaysInFirstWeek(Int32)

```cangjie
public func setMinimalDaysInFirstWeek(value: Int32): Unit
```

**Function:** Sets the minimal number of days in the first week of the year.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | The minimal number of days in the first week of the year. This indicates the minimum number of days required to determine the first week of the year. For example, if this value is set to 4, then the first week of the year must contain at least 4 days; otherwise, these days will be counted as part of the last week of the previous year. This setting helps ensure week numbering conforms to regional customs. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("zh-Hans")
    calendar.setMinimalDaysInFirstWeek(3)
    let minimalDaysInFirstWeek = calendar.getMinimalDaysInFirstWeek() // minimalDaysInFirstWeek = 3
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setTime(Float64)

```cangjie
public func setTime(time: Float64): Unit
```

**Function:** Sets the internal date and time of the calendar object, where time is the number of milliseconds elapsed since 1970.1.1 00:00:00 GMT.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| time | Float64 | Yes | - | The number of milliseconds elapsed since 1970.1.1 00:00:00 GMT. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("en-US")
    calendar.setTime(10540800000.0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setTimeZone(String)

```cangjie
public func setTimeZone(timeZone: String): Unit
```

**Function:** Sets the time zone of the calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Since:** 22  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| timeZone | String | Yes | - | A valid time zone ID, such as "Asia/Shanghai". |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let calendar = getCalendar("en-US")
    calendar.setTimeZone("Asia/Shanghai")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class System

```cangjie
public class System {}
```

**Function:** I18n system object.

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### static func getAppPreferredLanguage()

```cangjie
public static func getAppPreferredLanguage(): String
```

**Function:** Gets the preferred language of the application.

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|The preferred language of the application.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.i18n.*
import kit.LocalizationKit.getCalendar
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let appPreferredLanguage = System.getAppPreferredLanguage() // Get application preferred language
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func getSystemLanguage()

```cangjie
public static func getSystemLanguage(): String
```

**Function:** Obtains the current system language. To listen for system language changes, listen for the common event `Support.COMMON_EVENT_LOCALE_CHANGED`. For details, see [System Language and Region](../../internationalization/cj-i18n-system-language-region.md#how-to-develop).

**System Capability:** SystemCapability.Global.I18n

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representing the language ID. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.i18n.*
import kit.PerformanceAnalysisKit.Hilog

let systemLanguage = System.getSystemLanguage() // If the system language is simplified Chinese, systemLanguage = 'zh-Hans'
Hilog.info(0, "test", "systemLanguage=${systemLanguage}")
```

### static func getSystemRegion()

```cangjie
public static func getSystemRegion(): String
```

**Function:** Obtains the current system country/region. To listen for system region changes, listen for the common event `Support.COMMON_EVENT_LOCALE_CHANGED`. For details, see [System Language and Region](../../internationalization/cj-i18n-system-language-region.md#how-to-develop).

**System Capability:** SystemCapability.Global.I18n

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representing the country/region ID. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.i18n.*
import kit.PerformanceAnalysisKit.Hilog

let systemRegion = System.getSystemRegion() // If the system region is China, systemRegion = 'CN'
Hilog.info(0, "test", "systemRegion=${systemRegion}")
```

## func isRTL(String)

```cangjie
public func isRTL(locale: String): Bool
```

**Function:** Checks whether a language is an RTL language. For an RTL language, the UI needs to be displayed in [mirrored mode](../../internationalization/cj-i18n-ui-design.md#interface-mirroring).

**System Capability:** SystemCapability.Global.I18n

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| locale | String | Yes | - | String representing the locale ID, which consists of the language, script, and country/region, for example, ar-EG. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | **true** indicates that the language is an RTL language, and **false** indicates the opposite. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.i18n.*
import kit.PerformanceAnalysisKit.Hilog

let isZhRTL = isRTL("zh-CN") // Chinese is not an RTL language, false is returned
let isArRTL = isRTL("ar-EG") // Arabic is an RTL language, true is returned
Hilog.info(0, "test", "isZhRTL=${isZhRTL}, isArRTL=${isArRTL}")
```

## class Transliterator

```cangjie
public class Transliterator {}
```

**Function:** Provides text transliteration capabilities, including creating transliterator objects and transliterating text.

**System Capability:** SystemCapability.Global.I18n

**Since:** 26.1.0

### static func getInstance(String)

```cangjie
public static func getInstance(id: String): Transliterator
```

**Function:** Creates a transliterator object with the specified conversion ID.

**System Capability:** SystemCapability.Global.I18n

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | Conversion ID supported by transliteration, for example, Any-Latn. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Transliterator](#class-transliterator) | Transliterator object. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.i18n.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let transliterator = Transliterator.getInstance("Any-Latn")
    Hilog.info(0, "test", "getInstance success")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func transform(String)

```cangjie
public func transform(text: String): String
```

**Function:** Converts the input text from the source format to the target format.

**System Capability:** SystemCapability.Global.I18n

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| text | String | Yes | - | Input text. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Text after conversion. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.i18n.*
import kit.PerformanceAnalysisKit.Hilog

let transliterator = Transliterator.getInstance("Any-Latn")
let transliterateLatn = transliterator.transform("中国") // transliterateLatn = 'zhōng guó'
Hilog.info(0, "test", "transliterateLatn=${transliterateLatn}")

let asciiTransliterator = Transliterator.getInstance("Any-Latn;Latin-Ascii")
let transliterateAscii = asciiTransliterator.transform("中国") // transliterateAscii = 'zhong guo'
Hilog.info(0, "test", "transliterateAscii=${transliterateAscii}")
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

**Function:** Calendar type enumeration, used to specify different calendar systems.

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### Buddhist

```cangjie
Buddhist
```

**Function:** Buddhist calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### Chinese

```cangjie
Chinese
```

**Function:** Chinese calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### Coptic

```cangjie
Coptic
```

**Function:** Coptic calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### Ethiopic

```cangjie
Ethiopic
```

**Function:** Ethiopic calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### Hebrew

```cangjie
Hebrew
```

**Function:** Hebrew calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### Gregory

```cangjie
Gregory
```

**Function:** Gregorian calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### Indian

```cangjie
Indian
```

**Function:** Indian calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### IslamicCivil

```cangjie
IslamicCivil
```

**Function:** Islamic Civil calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### IslamicTbla

```cangjie
IslamicTbla
```

**Function:** Islamic Tabular calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### IslamicUmalqura

```cangjie
IslamicUmalqura
```

**Function:** Islamic Umm al-Qura calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### Japanese

```cangjie
Japanese
```

**Function:** Japanese calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22

### Persian

```cangjie
Persian
```

**Function:** Persian calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 22