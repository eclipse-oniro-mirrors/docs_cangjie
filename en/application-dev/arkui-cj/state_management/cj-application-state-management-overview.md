# Overview of Application-Owned State Management

The decorators introduced in the previous chapter can only share state variables within a page, i.e., on a single component tree. If developers need to achieve application-level state data sharing or share state across multiple pages, they must utilize the concept of application-level state management. Depending on different characteristics, the framework provides multiple capabilities for application state management:

- [LocalStorage](./cj-localstorage.md): Page-level UI state storage, typically used for state sharing within a [UIAbility](../../application-models/cj-uiability-overview.md) or between pages.

- [AppStorage](./cj-appstorage.md): A special singleton LocalStorage object created by the UI framework when the application starts, providing centralized storage for the application's UI state properties.

- [PersistentStorage](./cj-persiststorage.md): Persistent storage of UI state, usually used in conjunction with AppStorage. It selects data stored in AppStorage to write to disk, ensuring that these properties retain the same values when the application restarts as they had when the application was closed.

- [Environment](./cj-environment.md): Environmental parameters of the device on which the application is running. These parameters are synchronized to AppStorage and can be used in combination with AppStorage.