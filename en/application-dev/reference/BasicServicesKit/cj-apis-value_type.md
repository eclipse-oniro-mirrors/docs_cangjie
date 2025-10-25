# ohos.value_type

This module contains additional information for common events.

## Importing the Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above example projects and configuration templates, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## enum ValueType

```cangjie
public enum ValueType {
    | Int32Value(Int32)
    | Float64Value(Float64)
    | StringValue(String)
    | BoolValue(Bool)
    | Fd(Int32)
    | ArrayString(Array<String>)
    | ArrayInt32(Array<Int32>)
    | ArrayInt64(Array<Int64>)
    | ArrayBool(Array<Bool>)
    | ArrayFloat64(Array<Float64>)
    | ArrayFd(Array<Int32>)
    | ...
}
```

**Description:** Contains value types for additional information of common events.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### ArrayBool(Array\<Bool>)

```cangjie
ArrayBool(Array<Bool>)
```

**Description:** Represents Bool array type data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### ArrayFd(Array\<Int32>)

```cangjie
ArrayFd(Array<Int32>)
```

**Description:** Represents file descriptor array data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### ArrayFloat64(Array\<Float64>)

```cangjie
ArrayFloat64(Array<Float64>)
```

**Description:** Represents Float64 array type data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### ArrayInt32(Array\<Int32>)

```cangjie
ArrayInt32(Array<Int32>)
```

**Description:** Represents Int32 array type data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### ArrayInt64(Array\<Int64>)

```cangjie
ArrayInt64(Array<Int64>)
```

**Description:** Represents Int64 array type data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### ArrayString(Array\<String>)

```cangjie
ArrayString(Array<String>)
```

**Description:** Represents String array type data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### BoolValue(Bool)

```cangjie
BoolValue(Bool)
```

**Description:** Represents Bool type data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### Fd(Int32)

```cangjie
Fd(Int32)
```

**Description:** Represents file descriptor data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### Float64Value(Float64)

```cangjie
Float64Value(Float64)
```

**Description:** Represents Float64 type data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### Int32Value(Int32)

```cangjie
Int32Value(Int32)
```

**Description:** Represents Int32 type data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### StringValue(String)

```cangjie
StringValue(String)
```

**Description:** Represents String type data.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21