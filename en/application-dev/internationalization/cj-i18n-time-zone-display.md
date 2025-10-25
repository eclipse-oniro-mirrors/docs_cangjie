# Localized Time Zone Names

## Use Cases

In multilingual environments, users from different regions may refer to time zones differently. For example, in Chinese contexts, the Central Time Zone is called "中部时区," while in English contexts, it is referred to as "Central Time Zone." To ensure that time zone displays align with local language conventions, time zone names need to be localized.

## Development Steps

For detailed usage and instructions of the API, refer to the [getDisplayName](../../../en/application-dev/reference/LocalizationKit/cj-apis-i18n.md#func-getdisplaynamestring) API documentation.

1. Import the module.

   <!-- compile -->

   ```cangjie
   // index.cj
   import kit.LocalizationKit.*
   ```

2. Localize the time zone name, using America/Sao_Paulo as an example.

   <!-- compile -->

   ```cangjie
    // index.cj
    let timezone: TimeZone = getTimeZone(zoneID: 'America/Sao_Paulo')
    let timeZoneName: String = timezone.getDisplayName(locale:'zh-Hans', isDST: true) // timeZoneName = 'Brasília Standard Time'
   ```