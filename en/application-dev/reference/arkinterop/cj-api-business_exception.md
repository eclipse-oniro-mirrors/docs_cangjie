# ohos.business_exception (General Exception Information)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module defines common exception information that occurs during interface calls.

## Import Module

```cangjie
import ohos.business_exception.*
```

> **Note:**
>
> Kit import methods are not supported and are expected to be supported in the next version.

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
