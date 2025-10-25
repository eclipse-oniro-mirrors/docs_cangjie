# Overview of Application Configuration Files (Stage Model)

Each application project's code directory must contain application configuration files, which provide basic information about the application to the compilation tools, operating system, and application market.

In application projects developed based on the Stage model, there is always an app.json5 configuration file and one or more module.json5 configuration files.

[app.json5 Configuration File](app-configuration-file.md) contains the following:

- Global configuration information of the application, including basic details such as the application's Bundle name, developer, version number, etc.

- Configuration information for specific device types.

[module.json5 Configuration File](module-configuration-file.md) contains the following:

- Basic configuration information of the Module, including fundamental details such as Module name, type, description, supported device types, etc.

- Application component information, including description details of UIAbility components and ExtensionAbility components.

- Permission information required during the application's runtime.