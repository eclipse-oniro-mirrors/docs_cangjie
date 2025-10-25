# Setting Calendar and Calendar Systems

## Usage Scenarios

Users in different regions use different calendar systems. Most regions follow the Gregorian calendar, while some users utilize other calendars such as the Lunar calendar, Islamic calendar, or Hebrew calendar. Additionally, time and date representations vary across time zones and daylight saving time adjustments. Therefore, users should configure calendars that align with local conventions. The internationalization module provides the [Calendar](../../../en/application-dev/reference/LocalizationKit/cj-apis-i18n.md#class-calendar) class, which enables setting calendar types, dates, year-month-day values, time zones, first day of the week, minimum days in the first week of the year, determining whether a specific day is a weekend, calculating day differences, and more. During application development, developers can select appropriate functions based on business requirements.

## Development Procedure

The following example demonstrates how to use the [Calendar](../../../en/application-dev/reference/LocalizationKit/cj-apis-i18n.md#class-calendar) class APIs by converting a Gregorian date to its corresponding Lunar calendar date.

1. Import the module.

    <!-- compile -->

    ```cangjie
    import kit.LocalizationKit.*
    ```

2. Gregorian calendar operations.

    <!-- compile -->

    ```cangjie
    let calendar: Calendar = getCalendar('zh-Hans', calendarType:  CalendarType.Chinese)
    // Set the calendar object's time
    calendar.setTime(10540800000.0)

    // Set the calendar object's datetime to 2022.05.13 08:00:00
    calendar.set(2022, 5, 13, hour: 8, minute: 0, second: 0)

    // Set the calendar object's time zone
    calendar.setTimeZone('Asia/Shanghai')

    // Get the calendar object's time zone
    let timezone: String = calendar.getTimeZone() // timezone = 'Asia/Shanghai'

    // Get the first day of the week
    let firstDayOfWeek: Int32 = calendar.getFirstDayOfWeek() // firstDayOfWeek = 1

    // Set the first day of the week
    calendar.setFirstDayOfWeek(1)

    // Get minimum days in the first week of the year
    let minimalDaysInFirstWeek: Int32 = calendar.getMinimalDaysInFirstWeek() // minimalDaysInFirstWeek = 1

    // Set minimum days in the first week of the year
    calendar.setMinimalDaysInFirstWeek(3)

    // Get the value associated with the specified field
    let year: Int32 = calendar.get('year') // year = 2022

    // Get the localized name of the calendar
    let calendarName: String = calendar.getDisplayName('zh-Hans') // calendarName = 'Gregorian Calendar'

    // Perform addition/subtraction operations on calendar fields
    calendar.set(2023, 10, 15)
    calendar.add('date', 2)
    let day: Int32 = calendar.get('date') // day = 17
   ```

3. Convert Gregorian date to Lunar calendar date.

   <!-- compile -->

    ```cangjie
    import std.time.DateTime as d

    let calendar: Calendar = getCalendar('zh-Hans', calendarType: CalendarType.Chinese)
    // Set Gregorian date to calendar object: 2023.07.25 08:00:00
    calendar.set(2023, 7,  25, hour:8, minute:0)
    // Get Lunar calendar year-month-day
    let year: Int32 = calendar.get('year') // year = 40, representing the 40th year in the sexagenary cycle (range 1-60)
    let month: Int32 = calendar.get('month') // month = 5, representing June
    let day: Int32 = calendar.get('date') // day = 8, representing the 8th day
    ```

Supported calendar types:

| Type | Chinese Name |
| -------- | -------- |
| buddhist | Buddhist Calendar |
| chinese | Lunar Calendar |
| coptic | Coptic Calendar |
| ethiopic | Ethiopian Calendar |
| hebrew | Hebrew Calendar |
| gregory | Gregorian Calendar |
| indian | Indian Calendar |
| islamic_civil | Islamic Hijri Calendar |
| islamic_tbla | Islamic Astronomical Calendar |
| islamic_umalqura | Islamic Umm al-Qura Calendar |
| japanese | Japanese Calendar |
| persian | Persian Calendar |