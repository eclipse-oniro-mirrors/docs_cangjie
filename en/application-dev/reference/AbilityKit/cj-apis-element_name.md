# ohos.element_name

This module describes the ElementName information.

## Import Module

```cangjie
import kit.AbilityKit.*
```

## class ElementName

```cangjie
public class ElementName {
    public var deviceId: String
    public var bundleName: String
    public var abilityName: String
    public var moduleName: String
    public init(bundleName: String, abilityName: String, deviceId!: String = "", moduleName!: String = "")
}
```

**Description:** ElementName information.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var abilityName

```cangjie
public var abilityName: String
```

**Description:** Ability name.

**Type:** String

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var bundleName

```cangjie
public var bundleName: String
```

**Description:** Application Bundle name.

**Type:** String

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var deviceId

```cangjie
public var deviceId: String
```

**Description:** Device ID.

**Type:** String

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var moduleName

```cangjie
public var moduleName: String
```

**Description:** Module name of the HAP to which the Ability belongs.

**Type:** String

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### init(String, String, String, String)

```cangjie
public init(bundleName: String, abilityName: String, deviceId!: String = "", moduleName!: String = "")
```

**Description:** Constructs an ElementName by specifying the device ID, application Bundle name, Ability name, and module name.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| bundleName | String | Yes | - | Application Bundle name. |
| abilityName | String | Yes | - | Ability name. |
| deviceId | String | No | "" | Device ID. |
| moduleName | String | No | "" | Module name of the HAP to which the Ability belongs. |