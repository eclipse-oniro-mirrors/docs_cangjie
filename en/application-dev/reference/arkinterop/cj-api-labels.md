# ohos.labels (General Interface Labels)

Label descriptions. Labels include atomicservice (whether atomic service is supported), crossplatform (whether cross-platform is supported), deprecated (deprecated version), form (whether supported in forms), permission (required permissions), since (API level), stagemodelonly (whether only Stage model is supported), syscap (required system capabilities), etc.

## Import Module

```cangjie
import ohos.labels.*
```

## Usage Instructions

This package is used to add label annotations to APIs in the form of annotations and provide explanations for the annotation information. Not recommended for user use.

## interface PermissionValue

```cangjie
public interface PermissionValue {
    operator func &(rhs: PermissionValue): PermissionValue
    operator func |(rhs: PermissionValue): PermissionValue
}
```

**Function:** Used to handle "AND/OR" relationships between permissions.

**Since:** 22

### func &(PermissionValue)

```cangjie
operator func &(rhs: PermissionValue): PermissionValue
```

**Function:** Performs an "AND" operation with another permission set. Returns the permission set after the "AND" operation.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|Yes|-|Another permission set for the "AND" operation.|

**Return Value:**

|Type| Description    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| Operation result. |

### func |(PermissionValue)

```cangjie
operator func |(rhs: PermissionValue): PermissionValue
```

**Function:** Performs an "OR" operation with another permission set. Returns the permission set after the "OR" operation.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default| Description                     |
|:---|:---|:---|:---|:-----------------------|
|rhs|[PermissionValue](#interface-permissionvalue)|Yes|-| Another permission set for the "OR" operation. |

**Return Value:**

|Type| Description    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| Operation result. |

## class APILevel

```cangjie
public class APILevel {
    public let level: UInt8
    public let atomicservice: Bool
    public let crossplatform: Bool
    public let deprecated: UInt8
    public let form: Bool
    public let permission:?PermissionValue
    public let stagemodelonly: Bool
    public let syscap: String
    public const init(level_val: UInt8, atomicservice!: Bool = false, crossplatform!: Bool = false,
        deprecated!: UInt8 = 0, form!: Bool = false, permission!: ?PermissionValue= None,
        stagemodelonly!: Bool = true, syscap!: String = "")
}
```

**Function:** Definition of labels. Labels are used to annotate APIs. Labels include atomicservice (whether atomic service is supported), crossplatform (whether cross-platform is supported), deprecated (deprecated version), form (whether supported in forms), permission (required permissions), since (API level), stagemodelonly (whether only Stage model is supported), syscap (required system capabilities), etc.

**Since:** 22

### let atomicservice

```cangjie
public let atomicservice: Bool
```

**Function:** Whether the current API supports atomic service.

**Type:** Bool

**Read/Write:** Read-only

**Since:** 22

### let crossplatform

```cangjie
public let crossplatform: Bool
```

**Function:** Whether cross-platform is supported.

**Type:** Bool

**Read/Write:** Read-only

**Since:** 22

### let deprecated

```cangjie
public let deprecated: UInt8
```

**Function:** The deprecated version of the current API, default value is 0, indicating not deprecated.

**Type:** UInt8

**Read/Write:** Read-only

**Since:** 22

### let form

```cangjie
public let form: Bool
```

**Function:** Whether the current API is supported in forms.

**Type:** Bool

**Read/Write:** Read-only

**Since:** 22

### let level

```cangjie
public let level: UInt8
```

**Function:** API starting level.

**Type:** UInt8

**Read/Write:** Read-only

**Since:** 22

### let permission

```cangjie
public let permission:?PermissionValue
```

**Function:** Permissions required to use the current API.

**Type:** ?[PermissionValue](#interface-permissionvalue)

**Read/Write:** Read-only

**Since:** 22

### let stagemodelonly

```cangjie
public let stagemodelonly: Bool
```

**Function:** Whether the current API only supports the Stage model.

**Type:** Bool

**Read/Write:** Read-only

**Since:** 22

### let syscap

```cangjie
public let syscap: String
```

**Function:** System capabilities required by the current API.

**Type:** String

**Read/Write:** Read-only

**Since:** 22

### init(UInt8, Bool, Bool, UInt8, Bool, ?PermissionValue, Bool, String)

```cangjie
public const init(level_val: UInt8, atomicservice!: Bool = false, crossplatform!: Bool = false, deprecated!: UInt8 = 0, form!: Bool = false, permission!: ?PermissionValue= None,
    stagemodelonly!: Bool = true, syscap!: String = "")
```
**Function:** APILevel constructor.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default| Description                 |
|:---|:---|:---|:---|:-------------------|
|level_val|UInt8|Yes|-| API level.         |
|atomicservice|Bool|No|false| Named parameter - whether atomic service is supported.     |
|crossplatform|Bool|No|false| Named parameter - whether cross-platform is supported.      |
|deprecated|UInt8|No|0| Named parameter - deprecated version.         |
|form|Bool|No|false| Named parameter - whether forms are supported.    |
|permission|?[PermissionValue](#interface-permissionvalue)|No|None| Named parameter - required permissions.      |
|stagemodelonly|Bool|No|true| Named parameter - whether only Stage model is supported. |
|syscap|String|No|""| Named parameter - required system capabilities.      |

## class PermissionAnd

```cangjie
public class PermissionAnd <: PermissionValue {
    public let lhs: PermissionValue
    public let rhs: PermissionValue
    public const init(lhs: PermissionValue, rhs: PermissionValue)
}
```

**Function:** Represents the "AND" operation of multiple permissions.

**Since:** 22

**Parent Type:**

- [PermissionValue](#interface-permissionvalue)

### let lhs

```cangjie
public let lhs: PermissionValue
```

**Function:** Left operand of the operator.

**Type:** PermissionValue

**Read/Write:** Read-only

**Since:** 22

### let rhs

```cangjie
public let rhs: PermissionValue
```

**Function:** Right operand of the operator.

**Type:** PermissionValue

**Read/Write:** Read-only

**Since:** 22

### init(PermissionValue, PermissionValue)

```cangjie
public const init(lhs: PermissionValue, rhs: PermissionValue)
```

**Function:** Constructs a PermissionAnd permission set, representing the "AND" operation of two permission sets.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default| Description                   |
|:---|:---|:---|:---|:---------------------|
|lhs|[PermissionValue](#interface-permissionvalue)|Yes|-| One permission set for constructing the "AND" permission set.  |
|rhs|[PermissionValue](#interface-permissionvalue)|Yes|-| Another permission set for constructing the "AND" permission set. |

### func &(PermissionValue)

```cangjie
public const override operator func &(rhs: PermissionValue): PermissionValue
```

**Function:** Performs an "AND" operation with another permission set. Returns the permission set after the "AND" operation.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|Yes|-|Another permission set for the "AND" operation.|

**Return Value:**

|Type| Description    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| Operation result. |

### func |(PermissionValue)

```cangjie
public const override operator func |(rhs: PermissionValue): PermissionValue
```

**Function:** Performs an "OR" operation with another permission set. Returns the permission set after the "OR" operation.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|Yes|-|Another permission set for the "OR" operation.|

**Return Value:**

|Type| Description    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| Operation result. |

## class PermissionOr

```cangjie
public class PermissionOr <: PermissionValue {
    public let lhs: PermissionValue
    public let rhs: PermissionValue
    public const init(lhs: PermissionValue, rhs: PermissionValue)
}
```

**Function:** Represents the logical "OR" operation of multiple permissions.

**Since:** 22

**Parent Type:**

- [PermissionValue](#interface-permissionvalue)

### let lhs

```cangjie
public let lhs: PermissionValue
```

**Function:** Left operand of the operator.

**Type:** PermissionValue

**Read/Write:** Read-only

**Since:** 22

### let rhs

```cangjie
public let rhs: PermissionValue
```

**Function:** Right operand of the operator.

**Type:** PermissionValue

**Read/Write:** Read-only

**Since:** 22

### init(PermissionValue, PermissionValue)

```cangjie
public const init(lhs: PermissionValue, rhs: PermissionValue)
```

**Function:** Constructs a PermissionOr permission set, representing the logical "OR" operation of two permission sets.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default| Description   |
|:---|:---|:---|:---|:-----|
|lhs|[PermissionValue](#interface-permissionvalue)|Yes|-| Parameter 1. |
|rhs|[PermissionValue](#interface-permissionvalue)|Yes|-| Parameter 2. |

### func &(PermissionValue)

```cangjie
public const override operator func &(rhs: PermissionValue): PermissionValue
```

**Function:** Performs a logical "AND" operation with another permission set. Returns the result permission set after the "AND" operation.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|Yes|-|Another permission set for the "AND" operation.|

**Return Value:**

|Type|Description|
|:----|:----|
|[PermissionValue](#interface-permissionvalue)|Permission set after performing the logical "AND" operation with another permission set.|

### func |(PermissionValue)

```cangjie
public const override operator func |(rhs: PermissionValue): PermissionValue
```

**Function:** Performs a logical "OR" operation with another permission set. Returns the result permission set after the "OR" operation.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default| Description                |
|:---|:---|:---|:---|:------------------|
|rhs|[PermissionValue](#interface-permissionvalue)|Yes|-| Another permission set for the "OR" operation. |

**Return Value:**

|Type| Description    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| Operation result. |## extend String

```cangjie
extend String <: PermissionValue {}
```

**Functionality:** The following is an implementation that extends the PermissionValue interface, using strings to represent individual permissions.

**Since:** 22

**Parent Type:**

- [PermissionValue](#interface-permissionvalue)

### func &(PermissionValue)

```cangjie
public const operator func &(rhs: PermissionValue): PermissionValue
```

**Functionality:** Performs a logical "AND" operation with another permission set. Returns the resulting permission set after the "AND" operation.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|Yes|-|Another permission set for the "AND" operation.|

**Return Value:**

|Type|Description|
|:----|:----|
|[PermissionValue](#interface-permissionvalue)|The permission set resulting from the logical "AND" operation with another permission set.|

### func |(PermissionValue)

```cangjie
public const operator func |(rhs: PermissionValue): PermissionValue
```

**Functionality:** Performs a logical "OR" operation with another permission set and returns the resulting permission set after the operation.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|Yes|-|Another permission set for the "OR" operation.|

**Return Value:**

|Type| Description    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| The operation result. |