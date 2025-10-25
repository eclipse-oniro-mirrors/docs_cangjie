# Application Package Terminology

## E

### ExtensionAbility

A component type name in the Stage model, referring to the ExtensionAbility component. It provides extension capabilities for specific scenarios (such as cards, input methods) to meet diverse usage requirements.

## H

### HAP

Harmony Ability Package. A HAP file contains all contents of an application, consisting of code, resources, third-party libraries, and application configuration files. Its file extension is .hap.

### HAR

Harmony Archive, a static shared package for compile-time reuse. It may contain code, C++ libraries, resources, and configuration files. With the file extension .har, it enables code and resource sharing.

### HSP

Harmony Shared Package, a dynamic shared package for runtime reuse. It may contain code, C++ libraries, resources, and configuration files. With the file extension .hsp, it facilitates code and resource sharing.

## M

### Module

A part of an application where each module has its own module.json5 configuration file. In project engineering, Entry, Feature, HSP, and HAR each represent a module of the application.

## S

### Stage Model

An application model introduced from API version 9, providing two major types of application components: UIAbility and ExtensionAbility. Named the Stage model because it also offers classes like AbilityStage and WindowStage as "stages" for application components and Window interfaces.

## U

### UIAbility

A component type name in the Stage model, referring to the UIAbility component. It contains UI elements and provides UI display capabilities, primarily used for user interaction.