# ohos.i18n (Internationalization-I18n)

This module provides system-related or enhanced internationalization capabilities, including locale management, phone number processing, calendars, etc. The interfaces here serve as supplements to those not defined in the ECMA 402 standard. The Intl module offers basic internationalization interfaces defined by ECMA 402, and when used together with this module, they provide comprehensive internationalization support.

## Importing the Module

```cangjie
import kit.LocalizationKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#Cangjie-example-code-instructions).

## func getCalendar(String, ?CalendarType)

```cangjie
public func getCalendar(locale: String, calendarType!: ?CalendarType = None): Calendar
```

**Function:** Obtains a calendar object corresponding to the specified locale and calendar type.  
**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| locale | String | Yes | - | A string representing locale information, composed of language, script, country, or region. |
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

let calendar = getCalendar("en-US", calendarType: CalendarType.Buddhist) // Obtains a Buddhist calendar object based on the en-US locale.
```

## class Calendar

```cangjie
public class Calendar {}
```

**Function:** A physical calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

### func add(String, Int32)

```cangjie
public func add(field: String, amount: Int32): Unit
```

**Function:** Performs addition or subtraction operations on the specified field of the calendar.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Specifies the calendar field to operate on. Currently supported field values include year, month, week_of_year, week_of_month, date, day_of_year, day_of_week, day_of_week_in_month, hour, hour_of_day, minute, second, millisecond. |
| amount | Int32 | Yes | - | The specific value for the addition or subtraction operation. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("zh-Hans")
calendar.set(2021,11,11) // Set time to 2021.12.11
calendar.add("year", 3)
let res = calendar.get("year") // res = 2024
```

### func get(String)

```cangjie
public func get(field: String): Int32
```

**Function:** Obtains the value associated with the specified field in the calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Obtains the corresponding value of the calendar object through the field. For currently supported field values, refer to the table below. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | The value associated with the field. For example, if the internal date year of the current Calendar object is 1990, get("year") returns 1990. |

**Example:**

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

**Function:** Obtains the name of the calendar object in the specified locale.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| locale | String | Yes | - | A string representing locale information, composed of language, script, country, or region. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | The name of the calendar in the locale specified by `locale`. For example, "Buddhist" displays as "Buddhist Calendar" in en-US. |

**Example:**

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

**Function:** Obtains the first day of the week for the calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | The first day of the week, where 1 represents Sunday and 7 represents Saturday. |

**Example:**

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

**Function:** Obtains the minimal number of days in the first week of the year.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | The minimal number of days in the first week of the year. This indicates the minimum number of days required to determine the first week of the year. For example, if this value is set to 4, the first week of the year must contain at least 4 days; otherwise, these days will be counted as part of the last week of the previous year. This setting ensures that week numbering conforms to regional customs. |

**Example:**

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

**Function:** Obtains the current calendar's UTC time in milliseconds.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Return Value:**

| Type | Description |
|:----|:----|
| Float64 | The current calendar's UTC time in milliseconds. |

**Example:**

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

**Function:** Obtains the time zone of the calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

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

let calendar = getCalendar("zh-Hans", calendarType: CalendarType.Chinese)
calendar.setTimeZone("Asia/Shanghai")
let timeZone = calendar.getTimeZone() // timeZone = "Asia/Shanghai"
```

### func set(Int32, Int32, Int32, ?Int32, ?Int32, ?Int32)

```cangjie
public func set(year: Int32, month: Int32, date: Int32, hour!: ?Int32 = None, minute!: ?Int32 = None, second!: ?Int32 = None): Unit
```

**Function:** Sets the year, month, day, hour, minute, and second of the calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| year | Int32 | Yes | - | The year to set. |
| month | Int32 | Yes | - | The month to set. Note: Months are counted from 0, where 0 represents January. |
| date | Int32 | Yes | - | The day to set. |
| hour | ?Int32 | No | None | **Named parameter.** The hour to set. -1 represents the system hour. |
| minute | ?Int32 | No | None | **Named parameter.** The minute to set. -1 represents the system minute. |
| second | ?Int32 | No | None | **Named parameter.** The second to set. -1 represents the system second. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("zh-Hans")
calendar.set(2021,11,11)  // Set time to 2021.12.11
```

### func setFirstDayOfWeek(Int32)

```cangjie
public func setFirstDayOfWeek(value: Int32): Unit
```

**Function:** Sets the first day of the week.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | The first day of the week to set, where 1 represents Sunday and 7 represents Saturday. |

**Example:**

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

**Function:** Sets the minimal number of days in the first week of the year.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | The minimal number of days in the first week of the year. This indicates the minimum number of days required to determine the first week of the year. For example, if this value is set to 4, the first week of the year must contain at least 4 days; otherwise, these days will be counted as part of the last week of the previous year. This setting ensures that week numbering conforms to regional customs. |

**Example:**

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

**Function:** Sets the internal date and time of the calendar object, where `time` is the number of milliseconds elapsed since 1970.1.1 00:00:00 GMT.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| time | Float64 | Yes | - | The number of milliseconds elapsed since 1970.1.1 00:00:00 GMT. |

**Example:**

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

**Function:** Sets the time zone of the calendar object.  

**System Capability:** SystemCapability.Global.I18n  

**Initial Version:** 21  

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| timeZone | String | Yes | - | A valid time zone ID, such as "Asia/Shanghai". |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.getCalendar

let calendar = getCalendar("en-US")
calendar.setTimeZone("Asia/Shanghai")
```## class System

```cangjie
public class System {}
```

**Function:** I18n system object.

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### static func getAppPreferredLanguage()

```cangjie
public static func getAppPreferredLanguage(): String
```

**Function:** Gets the preferred language of the application.

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

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

let appPreferredLanguage = System.getAppPreferredLanguage() // Get the application's preferred language
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

**Since:** 21

### Buddhist

```cangjie
Buddhist
```

**Function:** Buddhist calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### Chinese

```cangjie
Chinese
```

**Function:** Chinese calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### Coptic

```cangjie
Coptic
```

**Function:** Coptic calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### Ethiopic

```cangjie
Ethiopic
```

**Function:** Ethiopic calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### Hebrew

```cangjie
Hebrew
```

**Function:** Hebrew calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### Gregory

```cangjie
Gregory
```

**Function:** Gregorian calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### Indian

```cangjie
Indian
```

**Function:** Indian calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### IslamicCivil

```cangjie
IslamicCivil
```

**Function:** Islamic Civil calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### IslamicTbla

```cangjie
IslamicTbla
```

**Function:** Islamic Tabular calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### IslamicUmalqura

```cangjie
IslamicUmalqura
```

**Function:** Islamic Umm al-Qura calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### Japanese

```cangjie
Japanese
```

**Function:** Japanese calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21

### Persian

```cangjie
Persian
```

**Function:** Persian calendar type

**System Capability:** SystemCapability.Global.I18n

**Since:** 21