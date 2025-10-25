# Common Actions and Entities (Not Recommended)

## Actions

Represent common operations that the caller intends to perform (e.g., view, share, application details). When actions are declared in the [skills field](../cj-start/basic-knowledge/module-configuration-file.md#skills标签) of the callee application's configuration file, it indicates that the application supports the declared operations. Common actions are listed below.

**Common Actions:**

- ACTION_HOME: An action to launch the application's entry component, which must be used in conjunction with ENTITY_HOME. The system desktop application icon serves as an explicit entry component, and clicking it triggers the action to launch the entry component. Multiple entry components can be configured.
- ACTION_CHOOSE: Select local resource data, such as contacts, photo albums, etc. The system typically has corresponding Picker applications for different types of data, such as contacts and galleries.
- ACTION_VIEW_DATA: View data. When a URL URI is used, it indicates displaying the content corresponding to that URL. For specific operation procedures, refer to [Launching File Processing Applications via startAbility](./cj-file-processing-apps-startup.md).
- ACTION_VIEW_MULTIPLE_DATA: An operation to send multiple data records.

## Entities

Represent category information of the target application component (e.g., browser, video player). When entities are declared in the [skills field](../cj-start/basic-knowledge/module-configuration-file.md#skills标签) of the callee application's configuration file, it indicates the categories supported by the application. Common entities are listed below.

**Common Entities:**

- ENTITY_DEFAULT: A default category with no practical significance.
- ENTITY_HOME: A category for the home screen with a clickable icon entry.
- ENTITY_BROWSABLE: Indicates the browser category.