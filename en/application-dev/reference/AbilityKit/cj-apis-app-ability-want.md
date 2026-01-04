# ohos.app.ability.want

Want provides the capability for Ability startup and communication, containing information such as device ID, bundle name, Ability name, module name, flags, URI, action, entities, Want type, and parameters.

## Import Module

```cangjie
import kit.AbilityKit.*
```

## Permission List

ohos.permission.DISTRIBUTED_DATASYNC

ohos.permission.PREPARE_APP_TERMINATE

ohos.permission.PRIVACY_WINDOW

## Usage Instructions

API sample code usage instructions:

- If the sample code's first line contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the aforementioned sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class Want

```cangjie
public class Want {
    public var deviceId: String
    public var bundleName: String
    public var abilityName: String
    public var moduleName: String
    public var flags: UInt32
    public var uri: String
    public var action: String
    public var entities: Array<String>
    public var dataType: String
    public var parameters: HashMap<String, WantValueType>
    public init(
        deviceId!: String = "",
        bundleName!: String = "",
        abilityName!: String = "",
        moduleName!: String = "",
        flags!: UInt32 = 0,
        uri!: String = "",
        action!: String = "",
        entities!: Array<String> = [],
        dataType!: String = "",
        parameters!: HashMap<String, WantValueType> = HashMap<String, WantValueType>(),
        fds!: HashMap<String, Int32> = HashMap<String, Int32>()
    )
}
```

**Function:** Describes the Want information for application component startup requests.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### var abilityName

```cangjie
public var abilityName: String
```

**Function:** Ability name.

**Type:** String

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### var action

```cangjie
public var action: String
```

**Function:** Action.

**Type:** String

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### var bundleName

```cangjie
public var bundleName: String
```

**Function:** Bundle name.

**Type:** String

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### var deviceId

```cangjie
public var deviceId: String
```

**Function:** Device ID.

**Type:** String

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### var entities

```cangjie
public var entities: Array<String>
```

**Function:** Entities.

**Type:** Array\<String>

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### var flags

```cangjie
public var flags: UInt32
```

**Function:** Flags.

**Type:** UInt32

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### var moduleName

```cangjie
public var moduleName: String
```

**Function:** Module name.

**Type:** String

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### var parameters

```cangjie
public var parameters: HashMap<String, WantValueType>
```

**Function:** Parameters.

**Type:** HashMap\<String,[WantValueType](#enum-wantvaluetype)>

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### var uri

```cangjie
public var uri: String
```

**Function:** URI.

**Type:** String

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### var dataType

```cangjie
public var dataType: String
```

**Function:** data type.

**Type:** String

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### init(String, String, String, String, UInt32, String, String, Array\<String>, String, HashMap\<String,WantValueType>, HashMap\<String,Int32>)

```cangjie
public init(
    deviceId!: String = "",
    bundleName!: String = "",
    abilityName!: String = "",
    moduleName!: String = "",
    flags!: UInt32 = 0,
    uri!: String = "",
    action!: String = "",
    entities!: Array<String> = [],
    dataType!: String = "",
    parameters!: HashMap<String, WantValueType> = HashMap<String, WantValueType>(),
    fds!: HashMap<String, Int32> = HashMap<String, Int32>()
)
```

**Function:** Constructor, creates a Want instance.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| deviceId | String | No | "" | Device ID. |
| bundleName | String | No | "" | Bundle name. |
| abilityName | String | No | "" | Ability name. |
| moduleName | String | No | "" | Module name. |
| flags | UInt32 | No | 0 | Flags. |
| uri | String | No | "" | URI. |
| action | String | No | "" | Action. |
| entities | Array\<String> | No | [] | Entities. |
| dataType | String | No | "" | Want type. |
| parameters | HashMap\<String,[WantValueType](#enum-wantvaluetype)> | No | HashMap<String, WantValueType>() | Parameters. |
| fds | HashMap\<String,Int32> | No | HashMap<String, Int32>() | File descriptors. |

## enum WantValueType

```cangjie
public enum WantValueType {
    | Int64Value(Int64)
    | Float64Value(Float64)
    | StringValue(String)
    | BoolValue(Bool)
    | ArrayValue(Array<WantValueType>)
    | HashMapValue(HashMap<String, WantValueType>)
    | ...
}
```

**Function:** Want value type.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### ArrayValue(Array\<WantValueType>)

```cangjie
ArrayValue(Array<WantValueType>)
```

**Function:** Array value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### BoolValue(Bool)

```cangjie
BoolValue(Bool)
```

**Function:** Boolean value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### Float64Value(Float64)

```cangjie
Float64Value(Float64)
```

**Function:** 64-bit floating-point value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### HashMapValue(HashMap\<String, WantValueType>)

```cangjie
HashMapValue(HashMap<String, WantValueType>)
```

**Function:** Hash map value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### Int64Value(Int64)

```cangjie
Int64Value(Int64)
```

**Function:** 64-bit integer value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22

### StringValue(String)

```cangjie
StringValue(String)
```

**Function:** String value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 22