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

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the aforementioned sample project and configuration template, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

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
    public var wantType: String
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
        wantType!: String = "",
        parameters!: HashMap<String, WantValueType> = HashMap<String, WantValueType>(),
        fds!: HashMap<String, Int32> = HashMap<String, Int32>()
    )
}
```

**Function:** Describes the Want information for application component startup requests.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var abilityName

```cangjie
public var abilityName: String
```

**Function:** Ability name.

**Type:** String

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var action

```cangjie
public var action: String
```

**Function:** Action.

**Type:** String

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var bundleName

```cangjie
public var bundleName: String
```

**Function:** Bundle name.

**Type:** String

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var deviceId

```cangjie
public var deviceId: String
```

**Function:** Device ID.

**Type:** String

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var entities

```cangjie
public var entities: Array<String>
```

**Function:** Entities.

**Type:** Array\<String>

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var flags

```cangjie
public var flags: UInt32
```

**Function:** Flags.

**Type:** UInt32

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var moduleName

```cangjie
public var moduleName: String
```

**Function:** Module name.

**Type:** String

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var parameters

```cangjie
public var parameters: HashMap<String, WantValueType>
```

**Function:** Parameters.

**Type:** HashMap\<String,[WantValueType](#enum-wantvaluetype)>

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var uri

```cangjie
public var uri: String
```

**Function:** URI.

**Type:** String

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var wantType

```cangjie
public var wantType: String
```

**Function:** Want type.

**Type:** String

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

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
    wantType!: String = "",
    parameters!: HashMap<String, WantValueType> = HashMap<String, WantValueType>(),
    fds!: HashMap<String, Int32> = HashMap<String, Int32>()
)
```

**Function:** Constructor to create a Want instance.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

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
| wantType | String | No | "" | Want type. |
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

**Function:** Want value types.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### ArrayValue(Array\<WantValueType>)

```cangjie
ArrayValue(Array<WantValueType>)
```

**Function:** Array value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### BoolValue(Bool)

```cangjie
BoolValue(Bool)
```

**Function:** Boolean value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### Float64Value(Float64)

```cangjie
Float64Value(Float64)
```

**Function:** 64-bit floating-point value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### HashMapValue(HashMap\<String, WantValueType>)

```cangjie
HashMapValue(HashMap<String, WantValueType>)
```

**Function:** Hash map value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### Int64Value(Int64)

```cangjie
Int64Value(Int64)
```

**Function:** 64-bit integer value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### StringValue(String)

```cangjie
StringValue(String)
```

**Function:** String value.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21