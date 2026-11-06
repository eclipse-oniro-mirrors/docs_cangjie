# Setting Calendar and Date Systems

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Usage Scenarios

Users in different regions utilize various calendar systems. Most regions follow the Gregorian calendar, while some users adopt alternative calendars such as the Lunar calendar, Islamic calendar, or Hebrew calendar. Additionally, time and date representations vary across time zones and daylight saving time adjustments. Therefore, users should configure calendars that align with local conventions. The internationalization module provides the [Calendar](../reference/LocalizationKit/cj-apis-i18n.md#class-calendar) class, which enables setting calendar types, dates, year-month-day values, time zones, first day of the week, minimum days in the first week of the year, determining whether a specific date falls on a weekend, calculating day differences, and more. During application development, developers can select appropriate functions based on business requirements.

## Development Steps

Using the example of converting Gregorian dates to Lunar calendar dates, this section demonstrates how to use the [Calendar](../reference/LocalizationKit/cj-apis-i18n.md#class-calendar) class interfaces.

1. Import the module.

    <!-- compile -->

    ```cangjie
    import kit.LocalizationKit.*
    ```

2. Gregorian calendar operations.

    <!-- compile -->

    ```cangjie
    let calendar: Calendar = getCalendar('zh-Hans', calendarType:  CalendarType.Chinese)
    // Set the time for the calendar object
    calendar.setTime(10540800000.0)

    // Set the calendar object's date to 2022.05.13 08:00:00
    calendar.set(2022, 5, 13, hour: 8, minute: 0, second: 0)

    // Set the time zone for the calendar object
    calendar.setTimeZone('Asia/Shanghai')

    // Get the time zone of the calendar object
    let timezone: String = calendar.getTimeZone() // timezone = 'Asia/Shanghai'

    // Get the first day of the week for the calendar object
    let firstDayOfWeek: Int32 = calendar.getFirstDayOfWeek() // firstDayOfWeek = 1

    // Set the first day of the week
    calendar.setFirstDayOfWeek(1)

    // Get the minimum days in the first week of the year
    let minimalDaysInFirstWeek: Int32 = calendar.getMinimalDaysInFirstWeek() // minimalDaysInFirstWeek = 1

    // Set the minimum days in the first week of the year
    calendar.setMinimalDaysInFirstWeek(3)

    // Get the value associated with the specified field in the calendar object
    let year: Int32 = calendar.get('year') // year = 2022

    // Get the localized name of the calendar object
    let calendarName: String = calendar.getDisplayName('zh-Hans') // calendarName = 'Gregorian Calendar'

    // Perform addition/subtraction operations on specified calendar fields
    calendar.set(2023, 10, 15)
    calendar.add('date', 2)
    let day: Int32 = calendar.get('date') // day = 17
   ```

3. Convert Gregorian dates to Lunar calendar dates.

   <!-- compile -->

    ```cangjie
    import std.time.DateTime as d

    let calendar: Calendar = getCalendar('zh-Hans', calendarType: CalendarType.Chinese)
    // Set Gregorian date information to the calendar object (2023.08.25 08:00:00)
    calendar.set(2023, 7,  25, hour:8, minute:0)
    // Get Lunar calendar year, month, and day
    let year: Int32 = calendar.get('year') // year = 40, representing the 40th year in the sexagenary cycle (range: 1-60)
    let month: Int32 = calendar.get('month') // month = 5, representing the 6th month
    let day: Int32 = calendar.get('date') // day = 8, representing the 8th day
    ```

Supported calendar types are as follows:

| Type | Chinese Name |
| -------- | -------- |
| buddhist | Buddhist Calendar |
| chinese | Lunar Calendar |
| coptic | Coptic Calendar |
| ethiopic | Ethiopian Calendar |
| hebrew | Hebrew Calendar |
| gregory | Gregorian Calendar |
| indian | Indian National Calendar |
| islamic_civil | Islamic Civil Calendar |
| islamic_tbla | Islamic Tabular Calendar |
| islamic_umalqura | Umm al-Qura Calendar |
| japanese | Japanese Calendar |
| persian | Persian Calendar |