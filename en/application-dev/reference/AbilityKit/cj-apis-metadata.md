# ohos.metadata

This module describes metadata information.

## Importing the Module

```cangjie
import kit.AbilityKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the aforementioned sample project and configuration template, please refer to [Cangjie Sample Code Description](../cj-development-intro.md#Cangjie-Sample-Code-Description).

## class Metadata

```cangjie
public class Metadata {
    public var name: String
    public var value: String
    public var resource: String
}
```

**Function:** Metadata information. Obtained by calling the [getBundleInfoForSelf](./cj-apis-bundle_manager.md#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter passing the values of GET_BUNDLE_INFO_WITH_HAP_MODULE, GET_BUNDLE_INFO_WITH_ABILITY, and GET_BUNDLE_INFO_WITH_METADATA.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Initial Version:** 21

### var name

```cangjie
public var name: String
```

**Function:** Metadata name.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Initial Version:** 21

### var resource

```cangjie
public var resource: String
```

**Function:** Metadata resource.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Initial Version:** 21

### var value

```cangjie
public var value: String
```

**Function:** Metadata value.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Initial Version:** 21