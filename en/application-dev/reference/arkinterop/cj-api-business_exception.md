# ohos.business_exception (General Exception Information)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module defines common exception information that occurs during interface calls.

## Import Module

```cangjie
import kit.CangjieKit.*
```

The interface capabilities of this module (ohos.business_exception) are encapsulated in CangjieKit and can be used after being imported through `import kit.CangjieKit.*`. For more details about importing Kits, see [Interface Usage Notes](../cj-development-intro.md#interface-usage-notes).

## class BusinessException

```cangjie
public class BusinessException <: Exception {
    public let code: Int32
}
```

**Description:** Business exception class, inherits from the Exception class.

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

### func getData\<T>()

```cangjie
public func getData<T>(): ?T
```

**Description:** Gets the custom data information carried in the exception.

**Since:** 22

**Return Value:**

| Type | Description    |
|:----|:------|
| ?T | Additional supplementary exception information.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the error message string.

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:-----------|
| String | Error message. |

## type AsyncCallback\<T>

```cangjie
public type AsyncCallback<T> = (Option<BusinessException>, Option<T>) -> Unit
```

**Description:** Defines the asynchronous callback type.
