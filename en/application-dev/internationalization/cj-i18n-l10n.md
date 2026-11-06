# Overview of Internationalization and Localization

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Function Introduction

Users from different regions have diverse languages and cultural backgrounds, with some speaking multiple languages. Therefore, when releasing application versions for various regions, it is essential to fully recognize differences in language, region, and culture. Through the processes of internationalization and localization, an application's interface can be displayed in a way that aligns with local user habits, thereby expanding its potential market.

**Internationalization (I18n)** is a set of system capabilities that support the configuration of regional characteristics, time zones, daylight saving time, and more, meeting the design requirements for multilingual and multicultural applications. Regional characteristics include settings for date and time formats, numbers and units of measurement, phone numbers, calendars, languages, etc. Time zone and daylight saving time capabilities involve obtaining time zones and handling daylight saving time transitions. Internationalization is typically implemented during the application design and development phases, where the user's language is not predetermined, and universal design principles are adopted.

To ensure applications can operate in different markets, internationalization provides development guidelines, including:
- Avoid making assumptions about users' cultures and habits. For example, do not assume all regions use commas as digit group separators and hardcode them in the code.
- UI elements (e.g., images, strings) should be separated from the code logic as application resources. When creating versions for other regions, only the corresponding resources need translation, avoiding code modifications. This improves efficiency and eliminates the need for redesign or redevelopment.

**Localization (L10n)** occurs during the application customization phase, where developers tailor the application to meet the linguistic and cultural needs of users in specific regions. This involves translating and customizing the application for target languages, including:
- **Configuring multilingual resources**: Providing content tailored to different countries, regions, and languages so the interface displays content aligned with local usage habits.
- **Resource translation**: A fundamental step in localization, where resources are translated to create multilingual versions. This includes translating UI elements and code, following the principle of separating UI elements from code logic to simplify the process. After translation, UI elements (e.g., images, audio/video) are loaded into the corresponding language-specific resource files. During interface loading, resources are displayed based on the application's language list.
- **Sensitivity and taboo checks**: Developers must review interface content to ensure it does not display politically, religiously, or culturally sensitive material that could cause public backlash.
- **Testing**: Developers use system localization testing capabilities to check for untranslated strings, translation accuracy, interface layout, and whether the display conforms to local user habits.