# ohos.business_exception (General Exception Information)

This module defines common exception information that occurs during interface calls.

## class BusinessException

```cangjie
public open class BusinessException <: Exception {
    public let code: Int32
    public init(code: Int32, msg: String)
}
```

**Description:** Business exception class, inherits from the Exception class.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parent Type:**

- Exception

### let code

```cangjie
public let code: Int32
```

**Description:** Error code.

**Type:** Int32

**Access:** Read-only

**Since:** 22

### init(Int32, String)

```cangjie
public init(code: Int32, msg: String)
```

**Description:** Creates an instance of the BusinessException class.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Description |
|:---|:---|:---|:------|
| code | Int32 | Yes | Error code. |
| msg | String | Yes | Error message. |

### func toString()

```cangjie
public open func toString(): String
```

**Description:** Gets the error message string.

**System Capability:** SystemCapability.Base

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:------|
| String | Error message. |

## class BusinessError

```cangjie
public class BusinessError<T> <: BusinessException  {
    public var data: T
    public init (data: T, code: Int32, msg: String)
}
```

**Description:** Business error class, inherits from BusinessException.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parent Type:**

- BusinessException

### let data

```cangjie
public var data: T
```

**Description:** Defines additional error information.

**Type:** T

**Access:** Read-write

**Since:** 22

### init(T, Int32, String)

```cangjie
public init(data: T, code: Int32, msg: String)
```

**Description:** Creates an instance of the BusinessError class.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Description |
|:---|:---|:---|:------|
| data | T | Yes | Additional information |
| code | Int32 | Yes | Error code. |
| msg | String | Yes | Error message. |

### getClassName()

```cangjie
protected override func getClassName(): String
```

**Description:** Gets the exception type name.

**System Capability:** SystemCapability.Base

**Since:** 22

**Return Value:**

| Type | Description |
|:-------|:------|
| String | Type name. |

## type AsyncCallback

```cangjie
public type AsyncCallback<T>=(Option<AsyncError>, Option<T>) -> Unit
```

**Description:** Defines the asynchronous callback type.

**System Capability:** SystemCapability.Base

**Since:** 22