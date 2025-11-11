# ohos.business_exception (General Exception Information)

This module defines common exception information that occurs during interface calls.

## class BusinessException

```cangjie
public class BusinessException <: Exception {
    public let code: Int32
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

### func getData<T>()

```cangjie
public func getData<T>(): ?T
```

**Description:** Additional supplementary exception information.

**Type:** T

**Access:** Read-only

**Since:** 22

### func toString()

```cangjie
public open func toString(): String
```

**Description:** Gets the error message string.

**System Capability:** SystemCapability.Base

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:-----------|
| String | Error message. |

### func getClassName()

```cangjie
protected override func getClassName(): String
```

**Description:** Gets the exception type name.

**System Capability:** SystemCapability.Base

**Since:** 22

**Return Value:**

| Type     | Description |
|:--------|:-----------|
| String | Type name. |

## type AsyncCallback

```cangjie
public type AsyncCallback<T>=(Option<AsyncError>, Option<T>) -> Unit
```

**Description:** Defines the asynchronous callback type.

**System Capability:** SystemCapability.Base

**Since:** 22