# ohos.ark_interop (ArkTS Interoperability Library)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The development languages for ArkTS applications include ArkTS, TypeScript, and JavaScript. The ArkTS interoperation library provides interoperability capabilities between the Cangjie language and ArkTS language.

## Import Module

```cangjie
import ohos.ark_interop.*
```

> **Note:**
>
> Kit import methods are not supported and are expected to be supported in the next version.

## interface JSInteropByte

```cangjie
sealed interface JSInteropByte {}
```

**Description:** This interface is used to implement generic constraints for Arrays that can be used in declarative interoperation macros. It is used in declarative interoperation macro framework scenarios and developers do not need to use this API.

The following types extend this interface:

- Byte

**Since:** 22

## interface JSInteropType\<T>

```cangjie
public interface JSInteropType<T> {
    static func fromJSValue(context: JSContext, input: JSValue): T
    func toJSValue(context: JSContext): JSValue
    static func toArktsType(): String
}
```

**Description:** This interface provides extension methods for types that support declarative interoperation macros. This interface is for internal use by the declarative interoperation macro framework only, and developers do not need to call it directly.

The following types extend this interface:

- User-defined classes annotated with @Interop[ArkTS]

- User-defined interfaces annotated with @Interop[ArkTS]

**Since:** 22

**Example:**

<!--compile-->
```cangjie
@Interop[ArkTS]
public class MyCustomClass {
    public let name: String   // String implements JSInteropType<String>, so it can be used here.
    public let age: Int64     // Int64 implements JSInteropType<Int64>, so it can be used here.

    public init(name: String, age: Int64) {
        this.name = name
        this.age = age
    }
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
static func fromJSValue(context: JSContext, input: JSValue): T
```

**Description:** Converts JSValue type data to the corresponding Cangjie type.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | Cangjie type. |

### static func toArktsType()

```cangjie
static func toArktsType(): String
```

**Description:** Gets the ArkTS type name corresponding to the Cangjie type.

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
func toJSValue(context: JSContext): JSValue
```

**Description:** Converts Cangjie type data to JSValue.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

## interface JSKeyable

```cangjie
sealed interface JSKeyable <: ToString & ToJSValue {
}
```

**Description:** Interface that can be used as a key for JSObject. This interface implements extension methods for the String type. It is used in declarative interoperation macro framework scenarios and developers do not need to use this API.

**Since:** 22

**Parent Types:**

- ToString
- ToJSValue

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func keyableUsage(context: JSContext): Unit {
    // Create an array that can be used as JSObject keys
    let keys: Array<JSKeyable> = [
        "1",                 // String
        context.string("a"), // JSString
        context.symbol()     // JSSymbol
    ]
    let object = context.object()
    let value = context.boolean(true).toJSValue()
    for (key in keys) {
        object[key] = value
    }
    let isBool = object[keys[0]].isBoolean()
    Hilog.info(0, "test", "isBool: ${isBool}")
}
```

## interface ToJSValue

```cangjie
public interface ToJSValue {
    func toJSValue(context: JSContext): JSValue
}
```

**Description:** Interface that can be used to implement ToJSValue.

**Since:** 22

### func toJSValue(JSContext)

```cangjie
func toJSValue(context: JSContext): JSValue
```

**Description:** Converts Cangjie type data to JSValue.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

## extend Int8 <: JSInteropType\<Int8>

**Description:** This interface can be used to implement extension methods for the built-in type Int8.

**Since:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func int8Translate(context: JSContext): Unit {
    let source: Int8 = 123
    let value = source.toJSValue(context)
    let result = Int8.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): Int8
```

**Description:** Converts JSValue type data to the corresponding Int8 type.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int8 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 34300002   | Outside error occurred. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |
| 34300005   | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Description:** Gets the ArkTS type name corresponding to the Cangjie Int8 type.

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Description:** Converts Cangjie Int8 type data to JSValue.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

## extend Int16 <: JSInteropType\<Int16>

**Description:** This interface can be used to implement extension methods for the built-in type Int16.

**Since:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func int16Translate(context: JSContext): Unit {
    let source: Int16 = 123
    let value = source.toJSValue(context)
    let result = Int16.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): Int16
```

**Description:** Converts JSValue type data to the corresponding Int16 type.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int16 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |
| 34300005   | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Description:** Gets the ArkTS type name corresponding to the Cangjie Int16 type.

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Description:** Converts Cangjie Int16 type data to JSValue.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

## extend Int32 <: JSInteropType\<Int32>

**Description:** This interface can be used to implement extension methods for the built-in type Int32.

**Since:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func int32Translate(context: JSContext): Unit {
    let source: Int32 = 123
    let value = source.toJSValue(context)
    let result = Int32.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): Int32
```

**Description:** Converts JSValue type data to the corresponding Int32 type.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |
| 34300005   | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Description:** Gets the ArkTS type name corresponding to the Cangjie Int32 type.

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Description:** Converts Cangjie Int32 type data to JSValue.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

## extend Int64 <: JSInteropType\<Int64>

**Functionality:** This interface can be used to implement extension methods for the built-in type Int64.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func int64Translate(context: JSContext): Unit {
    let source: Int64 = 123
    let value = source.toJSValue(context)
    let result = Int64.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): Int64
```

**Functionality:** Converts JSValue type data to corresponding Int64 type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |
| 5 | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Functionality:** Gets the ArkTS type name corresponding to the Cangjie Int64 type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Functionality:** Converts Cangjie Int64 type data to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

## extend UInt8 <: JSInteropType\<UInt8>

**Functionality:** This interface can be used to implement extension methods for the built-in type UInt8.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func uint8Translate(context: JSContext): Unit {
    let source: UInt8 = 123
    let value = source.toJSValue(context)
    let result = UInt8.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): UInt8
```

**Functionality:** Converts JSValue type data to corresponding UInt8 type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| UInt8 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |
| 5 | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Functionality:** Gets the ArkTS type name corresponding to the Cangjie UInt8 type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Functionality:** Converts Cangjie UInt8 type data to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

## extend UInt16 <: JSInteropType\<UInt16>

**Functionality:** This interface can be used to implement extension methods for the built-in type UInt16.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func uint16Translate(context: JSContext): Unit {
    let source: UInt16 = 123
    let value = source.toJSValue(context)
    let result = UInt16.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): UInt16
```

**Functionality:** Converts JSValue type data to corresponding UInt16 type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| UInt16 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |
| 5 | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Functionality:** Gets the ArkTS type name corresponding to the Cangjie UInt16 type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Functionality:** Converts Cangjie UInt16 type data to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:---|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

## extend UInt32 <: JSInteropType\<UInt32>

**Functionality:** This interface can be used to implement extension methods for the built-in type UInt32.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func uint32Translate(context: JSContext): Unit {
    let source: UInt32 = 123
    let value = source.toJSValue(context)
    let result = UInt32.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): UInt32
```

**Functionality:** Converts JSValue type data to corresponding UInt32 type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |
| 5 | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Functionality:** Gets the ArkTS type name corresponding to the Cangjie UInt32 type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Functionality:** Converts Cangjie UInt32 type data to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:---|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

## extend UInt64 <: JSInteropType\<UInt64>

**Functionality:** This interface can be used to implement extension methods for the built-in type UInt64.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func uint64Translate(context: JSContext): Unit {
    let source: UInt64 = 123
    let value = source.toJSValue(context)
    let result = UInt64.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): UInt64
```

**Functionality:** Converts JSValue type data to corresponding UInt64 type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| UInt64 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |
| 5 | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Functionality:** Gets the ArkTS type name corresponding to the Cangjie UInt64 type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Functionality:** Converts Cangjie UInt64 type data to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

## extend Float16 <: JSInteropType\<Float16>

**Function:** This interface can be used to implement extension methods for the built-in type Float16.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func float16Translate(context: JSContext): Unit {
    let source: Float16 = 123.0
    let value = source.toJSValue(context)
    let result = Float16.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): Float16
```

**Function:** Converts JSValue type data to the corresponding Float16 type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| Float16 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |
| 5 | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Function:** Gets the ArkTS type name corresponding to the Cangjie Float16 type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Function:** Converts Cangjie Float16 type data to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

## extend Float32 <: JSInteropType\<Float32>

**Function:** This interface can be used to implement extension methods for the built-in type Float32.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func float32Translate(context: JSContext): Unit {
    let source: Float32 = 123.0
    let value = source.toJSValue(context)
    let result = Float32.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): Float32
```

**Function:** Converts JSValue type data to the corresponding Float32 type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| Float32 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |
| 5 | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Function:** Gets the ArkTS type name corresponding to the Cangjie Float32 type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Function:** Converts Cangjie Float32 type data to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

## extend Float64 <: JSInteropType\<Float64>

**Function:** This interface can be used to implement extension methods for the built-in type Float64.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func float64Translate(context: JSContext): Unit {
    let source: Float64 = 123.0
    let value = source.toJSValue(context)
    let result = Float64.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): Float64
```

**Function:** Converts JSValue type data to the corresponding Float64 type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| Float64 | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |
| 5 | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Function:** Gets the ArkTS type name corresponding to the Cangjie Float64 type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Function:** Converts Cangjie Float64 type data to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

## extend Bool <: JSInteropType\<Bool>

**Function:** This interface can be used to implement extension methods for the built-in type Bool.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func boolTranslate(context: JSContext): Unit {
    let source: Bool = true
    let value = source.toJSValue(context)
    let result = Bool.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): Bool
```

**Function:** Converts JSValue type data to the corresponding Bool type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Cangjie type. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Function:** Gets the ArkTS type name corresponding to the Cangjie Bool type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |
| 5 | The ArkTS data types do not match. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Function:** Converts Cangjie Bool type data to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

## extend String <: JSInteropType\<String>

**Function:** This interface can be used to implement extension methods for the built-in type String.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func stringTranslate(context: JSContext): Unit {
    let source: String = "123.0"
    let value = source.toJSValue(context)
    let result = String.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): String
```

**Function:** Converts JSValue type data to the corresponding String type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Cangjie type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |
| 5 | The ArkTS data types do not match. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Function:** Gets the ArkTS type name corresponding to the Cangjie String type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

## extend String <: JSKeyable

**Functionality:** This interface can be used to implement extension methods for the built-in String type.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func stringTranslate(context: JSContext): Unit {
    let source: String = "123.0"
    let value = source.toJSValue(context)
    let result = String.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Functionality:** Converts Cangjie String type data to JSValue.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](#class-jscontext)|Yes|-|ArkTS interoperability context.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.              |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

## extend Unit <: JSInteropType\<Unit>

**Functionality:** This interface can be used to implement extension methods for the built-in Unit type.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
func unitTranslate(context: JSContext): Unit {
    let source: Unit = ()
    let value = source.toJSValue(context)
    let result = Unit.fromJSValue(context, value)
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, _: JSValue): Unit
```

**Functionality:** Converts JSValue type data to corresponding Bool type.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|_|[JSContext](#class-jscontext)|Yes|-|ArkTS interoperability context.|
|_|[JSValue](#class-jsvalue)|Yes|-|ArkTS unified type.|

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Functionality:** Gets the ArkTS type name corresponding to the Cangjie Unit type.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|Converted ArkTS type name.|

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Functionality:** Converts Cangjie Unit type data to JSValue.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](#class-jscontext)|Yes|-|ArkTS interoperability context.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

## extend\<T> Option\<T> <: JSInteropType<Option\<T>> where T <: JSInteropType\<T>

**Functionality:** This interface can be used to implement extension methods for the Option\<T> type.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func optionTranslate(context: JSContext): Unit {
    let sources: Array<?String> = ["abc", None, "123"]
    for (v in sources) {
        let value = v.toJSValue(context)
        let result = Option<String>.fromJSValue(context, value)
        Hilog.info(0, "test", "result: ${result}")
    }
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(context: JSContext, input: JSValue): Option<T>
```

**Functionality:** Converts JSValue type data to corresponding Option\<T> type.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](#class-jscontext)|Yes|-|ArkTS interoperability context.|
|input|[JSValue](#class-jsvalue)|Yes|-|ArkTS unified type.|

**Return Value:**

|Type|Description|
|:----|:----|
|Option\<T>|Cangjie Option type.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Functionality:** Gets the ArkTS type name corresponding to the Cangjie Option\<T> type.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|Converted ArkTS type name.|

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Functionality:** Converts Cangjie Option\<T> type data to JSValue.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](#class-jscontext)|Yes|-|ArkTS interoperability context.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

## extend\<T> Array\<T> <: JSInteropType<Array\<T>> where T <: JSInteropByte

**Functionality:** This interface can be used to implement extension methods for the Array\<T> type.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func arrayTranslate(context: JSContext): Unit {
    let sources: Array<Byte> = [1, 4, 5]
    let value = sources.toJSValue(context)
    let result = Array<Byte>.fromJSValue(context, value)
    Hilog.info(0, "test", "result: ${result}")
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): Array<T>
```

**Functionality:** Converts JSValue type data to corresponding Array\<T> type.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|_|[JSContext](#class-jscontext)|Yes|-|ArkTS interoperability context.|
|input|[JSValue](#class-jsvalue)|Yes|-|ArkTS unified type.|

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<T>|Cangjie Option type.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |
| 34300005   | The ArkTS data types do not match.|

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Functionality:** Gets the ArkTS type name corresponding to the Cangjie Array\<T> type.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|Converted ArkTS type name.|

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Functionality:** Converts Cangjie Array\<T> type data to JSValue.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](#class-jscontext)|Yes|-|ArkTS interoperability context.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

## class JSArray

```cangjie
public class JSArray <: JSHeapObject {}
```

**Functionality:** A safe reference to an ArkTS array. Supports getting length and reading/writing elements.

**Initial Version:** 22

**Parent Type:**

- [JSHeapObject](#class-jsheapobject)

### prop size

```cangjie
public prop size: Int64
```

**Functionality:** Gets the number of elements.

**Initial Version:** 22

**Type:** Int64

**Read/Write Capability:** Read-only

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------| :--- |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

### operator func \[](Int64)

```cangjie
public operator func [](index: Int64): JSValue
```

**Functionality:** Writes an element to the ArkTS array.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|index|Int64|Yes|-|Input index, safe range: [0, input count).|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                  |
|:------|:--------------------------------------|
| 34300001   | The accessing index is out of range.  |
| 34300003   | Accessing reference is beyond reach.  |
| 34300004   | Thread mismatch.                      |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsArr = callInfo[0].asArray()
    let firstElement = jsArr[0]
    return firstElement
}
```

### operator func \[](Int64, JSValue)

```cangjie
public operator func [](index: Int64, value!: JSValue): Unit
```

**Functionality:** Writes an element to the ArkTS array.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|index|Int64|Yes|-|Write index.|
|value|[JSValue](#class-jsvalue)|Yes|-| **Named parameter.** Value to write.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                  |
|:------|:--------------------------------------|
| 34300001   | The accessing index is out of range.  |
| 34300003   | Accessing reference is beyond reach.  |
| 34300004   | Thread mismatch.                      |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsArr = callInfo[0].asArray()
    let setValue = context.number(1.0).toJSValue()
    jsArr[0] = setValue
    return setValue
}
```

### operator func \[](Int64, JSHeapObject)

```cangjie
public operator func [](index: Int64, value!: JSHeapObject): Unit
```

**Functionality:** Writes an element to the ArkTS array.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|index|Int64|Yes|-|Write index.|
|value|[JSHeapObject](#class-jsheapobject)|Yes|-| **Named parameter.** Value to write.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                  |
|:------|:--------------------------------------|
| 34300001   | The accessing index is out of range.  |
| 34300003   | Accessing reference is beyond reach.  |
| 34300004   | Thread mismatch.                      |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsArr = callInfo[0].asArray()
    let setValue = context.string("abc")
    jsArr[0] = setValue
    return setValue.toJSValue()
}
```

## class JSArrayBuffer

```cangjie
public class JSArrayBuffer <: JSHeapObject {}
```

**Function:** The JSArrayBuffer object is used to represent a generic raw binary data buffer. By creating a JSArrayBuffer object, you can obtain its byte length and convert it to a Cangjie array.

**Initial Version:** 22

**Parent Type:**

- [JSHeapObject](#class-jsheapobject)

### prop byteLength

```cangjie
public prop byteLength: Int32
```

**Function:** The byte length of the ArrayBuffer.

**Initial Version:** 22

**Type:** Int32

**Read/Write Capability:** Read-only

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                  |
|:-------------|:---------------------------------------------|
| 34300003          | Accessing reference is beyond reach.          |
| 34300004          | Thread mismatch.                              |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getBufferLength(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let length = arrayBuffer.byteLength
    Hilog.info(0, "test", "ArrayBuffer length: ${length}")
    return context.number(Float64(length)).toJSValue()
}
```

### func readBytes()

```cangjie
public func readBytes(): Array<Byte>
```

**Function:** Reads binary data and converts it to a Cangjie array.

**Initial Version:** 22

**Return Value:**

| Type          | Description       |
|:-------------|:-----------------|
| Array\<Byte> | Cangjie array.    |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                  |
|:-------------|:---------------------------------------------|
| 34300003          | Accessing reference is beyond reach.          |
| 34300004          | Thread mismatch.                              |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func readBufferBytes(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let bytes = arrayBuffer.readBytes()
    Hilog.info(0, "test","Read ${bytes.size} bytes from ArrayBuffer")
    return context.number(Float64(bytes.size)).toJSValue()
}
```

### func toArrayBufferJSValue()

```cangjie
public func toArrayBufferJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's ArrayBuffer.

**Initial Version:** 22

**Return Value:**

| Type          | Description               |
|:-------------|:-------------------------|
| [JSValue](#class-jsvalue) | ArkTS unified type.       |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                     |
|:-------------|:--------------------------------|
| 34300002          | Outside error occurred.          |
| 34300003          | Accessing reference is beyond reach. |
| 34300004          | Thread mismatch.                 |

**Example:**

<!--compile-->
```cangjie
func getArrayBufferJSValue(context: JSContext): JSValue {
    let data: Array<Byte> = [1, 2, 3, 4]
    let arrayBuffer = context.arrayBuffer(data)
    let jsValue = arrayBuffer.toArrayBufferJSValue()
    return jsValue
}
```

### func toFloat32Array()

```cangjie
public func toFloat32Array(): Array<Float32>
```

**Function:** Converts to a Cangjie array Array\<Float32>.

**Initial Version:** 22

**Return Value:**

| Type          | Description       |
|:-------------|:-----------------|
| Array\<Float32> | Cangjie array.    |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                     |
|:-------------|:--------------------------------|
| 34300002          | Outside error occurred.          |
| 34300003          | Accessing reference is beyond reach. |
| 34300004          | Thread mismatch.                 |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createFloat32Array(context: JSContext): Unit {
    let data: Array<Float32> = [1.0, 2.0, 3.0, 4.0]
    let arrayBuffer = context.arrayBuffer(data)
    let received = arrayBuffer.toFloat32Array()
    Hilog.info(0, "test", "Converted to Float32Array ${received}")
}
```

### func toFloat32ArrayJSValue()

```cangjie
public func toFloat32ArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's Float32Array.

**Initial Version:** 22

**Return Value:**

| Type          | Description               |
|:-------------|:-------------------------|
| [JSValue](#class-jsvalue) | ArkTS unified type.       |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                     |
|:-------------|:--------------------------------|
| 34300002          | Outside error occurred.          |
| 34300003          | Accessing reference is beyond reach. |
| 34300004          | Thread mismatch.                 |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToFloat32Array(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let float32Array = arrayBuffer.toFloat32Array()
    Hilog.info(0, "test","Converted to Float32Array with ${float32Array.size} elements")
    return context.number(Float64(float32Array.size)).toJSValue()
}
```

### func toFloat64Array()

```cangjie
public func toFloat64Array(): Array<Float64>
```

**Function:** Converts to a Cangjie array Array\<Float64>.

**Initial Version:** 22

**Return Value:**

| Type          | Description       |
|:-------------|:-----------------|
| Array\<Float64> | Cangjie array.    |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                     |
|:-------------|:--------------------------------|
| 34300002          | Outside error occurred.          |
| 34300003          | Accessing reference is beyond reach. |
| 34300004          | Thread mismatch.                 |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToFloat64Array(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let float64Array = arrayBuffer.toFloat64Array()
    Hilog.info(0, "test","Converted to Float64Array with ${float64Array.size} elements")
    return context.number(Float64(float64Array.size)).toJSValue()
}
```

### func toFloat64ArrayJSValue()

```cangjie
public func toFloat64ArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's Float64Array.

**Initial Version:** 22

**Return Value:**

| Type          | Description               |
|:-------------|:-------------------------|
| [JSValue](#class-jsvalue) | ArkTS unified type.       |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                     |
|:-------------|:--------------------------------|
| 34300002          | Outside error occurred.          |
| 34300003          | Accessing reference is beyond reach. |
| 34300004          | Thread mismatch.                 |

**Example:**

<!--compile-->
```cangjie
func getFloat64ArrayJSValue(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let float64ArrayJSValue = arrayBuffer.toFloat64ArrayJSValue()
    return float64ArrayJSValue
}
```

### func toInt16Array()

```cangjie
public func toInt16Array(): Array<Int16>
```

**Function:** Converts to a Cangjie array Array\<Int16>.

**Initial Version:** 22

**Return Value:**

| Type          | Description       |
|:-------------|:-----------------|
| Array\<Int16> | Cangjie array.    |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                     |
|:-------------|:--------------------------------|
| 34300002          | Outside error occurred.          |
| 34300003          | Accessing reference is beyond reach. |
| 34300004          | Thread mismatch.                 |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToInt16Array(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let int16Array = arrayBuffer.toInt16Array()
    Hilog.info(0, "test","Converted to Int16Array with ${int16Array.size} elements")
    return context.number(Float64(int16Array.size)).toJSValue()
}
```

### func toInt16ArrayJSValue()

```cangjie
public func toInt16ArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's Int16Array.

**Initial Version:** 22

**Return Value:**

| Type          | Description               |
|:-------------|:-------------------------|
| [JSValue](#class-jsvalue) | ArkTS unified type.       |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                     |
|:-------------|:--------------------------------|
| 34300002          | Outside error occurred.          |
| 34300003          | Accessing reference is beyond reach. |
| 34300004          | Thread mismatch.                 |

**Example:**

<!--compile-->
```cangjie
func getInt16ArrayJSValue(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let int16ArrayJSValue = arrayBuffer.toInt16ArrayJSValue()
    return int16ArrayJSValue
}
```

### func toInt32Array()

```cangjie
public func toInt32Array(): Array<Int32>
```

**Function:** Converts to a Cangjie array Array\<Int32>.

**Initial Version:** 22

**Return Value:**

| Type          | Description       |
|:-------------|:-----------------|
| Array\<Int32> | Cangjie array.    |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                     |
|:-------------|:--------------------------------|
| 34300002          | Outside error occurred.          |
| 34300003          | Accessing reference is beyond reach. |
| 34300004          | Thread mismatch.                 |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToInt32Array(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let int32Array = arrayBuffer.toInt32Array()
    Hilog.info(0, "test", "Converted to Int32Array with ${int32Array.size} elements")
    return context.number(Float64(int32Array.size)).toJSValue()
}
```

### func toInt32ArrayJSValue()

```cangjie
public func toInt32ArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's Int32Array.

**Initial Version:** 22

**Return Value:**

| Type          | Description               |
|:-------------|:-------------------------|
| [JSValue](#class-jsvalue) | ArkTS unified type.       |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                     |
|:-------------|:--------------------------------|
| 34300002          | Outside error occurred.          |
| 34300003          | Accessing reference is beyond reach. |
| 34300004          | Thread mismatch.                 |

**Example:**

<!--compile-->
```cangjie
func getInt32ArrayJSValue(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let int32ArrayJSValue = arrayBuffer.toInt32ArrayJSValue()
    return int32ArrayJSValue
}
```

### func toInt64Array()

```cangjie
public func toInt64Array(): Array<Int64>
```

**Function:** Converts to a Cangjie array Array\<Int64>.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<Int64>|Cangjie array.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                                  |
|:------|:-----------------------------------------|
| 34300002   | Outside error occurred.　             |
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToInt64Array(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let int64Array = arrayBuffer.toInt64Array()
    Hilog.info(0, "test", "Converted to Int64Array with ${int64Array.size} elements")
    return context.number(Float64(int64Array.size)).toJSValue()
}
```

### func toInt64ArrayJSValue()

```cangjie
public func toInt64ArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's BigInt64Array.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------| :--- |
| 34300002   | Outside error occurred. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func getInt64ArrayJSValue(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let int64ArrayJSValue = arrayBuffer.toInt64ArrayJSValue()
    return int64ArrayJSValue
}
```

### func toInt8Array()

```cangjie
public func toInt8Array(): Array<Int8>
```

**Function:** Converts to a Cangjie array Array\<Int8>.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<Int8>|Cangjie array.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                                  |
|:------|:-----------------------------------------|
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToInt8Array(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let int8Array = arrayBuffer.toInt8Array()
    Hilog.info(0, "test", "Converted to Int8Array with ${int8Array.size} elements")
    return context.number(Float64(int8Array.size)).toJSValue()
}
```

### func toInt8ArrayJSValue()

```cangjie
public func toInt8ArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's Int8Array.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------| :--- |
| 34300002   | Outside error occurred. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func getInt8ArrayJSValue(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let int8ArrayJSValue = arrayBuffer.toInt8ArrayJSValue()
    return int8ArrayJSValue
}
```

### func toUInt16Array()

```cangjie
public func toUInt16Array(): Array<UInt16>
```

**Function:** Converts to a Cangjie array Array\<UInt16>.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<UInt16>|Cangjie array.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.　             |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToUInt16Array(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let uint16Array = arrayBuffer.toUInt16Array()
    Hilog.info(0, "test","Converted to UInt16Array with ${uint16Array.size} elements")
    return context.number(Float64(uint16Array.size)).toJSValue()
}
```

### func toUInt16ArrayJSValue()

```cangjie
public func toUInt16ArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's Uint16Array.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------| :--- |
| 34300002   | Outside error occurred. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func getUInt16ArrayJSValue(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let uint16ArrayJSValue = arrayBuffer.toUInt16ArrayJSValue()
    return uint16ArrayJSValue
}
```

### func toUInt32Array()

```cangjie
public func toUInt32Array(): Array<UInt32>
```

**Function:** Converts to a Cangjie array Array\<UInt32>.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<UInt32>|Cangjie array.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                                  |
|:------|:-----------------------------------------|
| 34300002   | Outside error occurred.　             |
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToUInt32Array(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let uint32Array = arrayBuffer.toUInt32Array()
    Hilog.info(0, "test", "Converted to UInt32Array with ${uint32Array.size} elements")
    return context.number(Float64(uint32Array.size)).toJSValue()
}
```

### func toUInt32ArrayJSValue()

```cangjie
public func toUInt32ArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's Uint32Array.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------| :--- |
| 34300002   | Outside error occurred. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func getUInt32ArrayJSValue(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let uint32ArrayJSValue = arrayBuffer.toUInt32ArrayJSValue()
    return uint32ArrayJSValue
}
```

### func toUInt64Array()

```cangjie
public func toUInt64Array(): Array<UInt64>
```

**Function:** Converts to a Cangjie array Array\<UInt64>.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<UInt64>|Cangjie array.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                                  |
|:------|:-----------------------------------------|
| 34300002   | Outside error occurred.　             |
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToUInt64Array(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let uint64Array = arrayBuffer.toUInt64Array()
    Hilog.info(0, "test", "Converted to UInt64Array with ${uint64Array.size} elements")
    return context.number(Float64(uint64Array.size)).toJSValue()
}
```

### func toUInt64ArrayJSValue()

```cangjie
public func toUInt64ArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's BigUint64Array.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------| :--- |
| 34300002   | Outside error occurred. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func getUInt64ArrayJSValue(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let uint64ArrayJSValue = arrayBuffer.toUInt64ArrayJSValue()
    return uint64ArrayJSValue
}
```

### func toUInt8Array()

```cangjie
public func toUInt8Array(): Array<UInt8>
```

**Function:** Converts to a Cangjie array Array\<UInt8>.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<UInt8>|Cangjie array.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                                  |
|:------|:-----------------------------------------|
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToUInt8Array(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let uint8Array = arrayBuffer.toUInt8Array()
    Hilog.info(0, "test", "Converted to UInt8Array with ${uint8Array.size} elements")
    return context.number(Float64(uint8Array.size)).toJSValue()
}
```

### func toUInt8ArrayJSValue()

```cangjie
public func toUInt8ArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's Uint8Array.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------| :--- |
| 34300002   | Outside error occurred. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func getUInt8ArrayJSValue(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let uint8ArrayJSValue = arrayBuffer.toUInt8ArrayJSValue()
    return uint8ArrayJSValue
}
```

### func toUInt8ClampedArrayJSValue()

```cangjie
public func toUInt8ClampedArrayJSValue(): JSValue
```

**Function:** Returns the JSValue of ArkTS's Uint8ClampedArray.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------| :--- |
| 34300002   | Outside error occurred. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func getUInt8ClampedArrayJSValue(context: JSContext, callInfo: JSCallInfo): JSValue {
    let arrayBuffer = callInfo[0].asArrayBuffer()
    let uint8ClampedArrayJSValue = arrayBuffer.toUInt8ClampedArrayJSValue()
    return uint8ClampedArrayJSValue
}
```

## class JSArrayEx\<T> where T <: JSInteropType\<T>

```cangjie
public class JSArrayEx<T> <: JSInteropType<JSArrayEx<T>> where T <: JSInteropType<T> {
    public init(arr: Array<T>)
}
```

**Function:** Used in declarative interop macros, corresponding to ArkTS's Array\<T> type.

**Initial Version:** 22

**Parent Type:**

- [JSInteropType\<JSArrayEx\<T>>](#interface-jsinteroptypet)

### prop size

```cangjie
public prop size: Int64
```

**Function:** Gets the number of elements.

**Initial Version:** 22

**Type:** Int64

**Read-Write Capability:** Read-only

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------| :--- |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch. |

### init(Array\<T>)

```cangjie
public init(arr: Array<T>)
```

**Function:** Constructs a corresponding JSArrayEx\<T> instance given an Array\<T>.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| arr | Array\<T> | Yes | - | Created based on this Array instance. |

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(context: JSContext, input: JSValue): JSArrayEx<T>
```

**Function:** Converts from JSValue to JSArrayEx. Used in declarative interop macro framework scenarios; developers do not need to use this API.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interop context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSArrayEx](#class-jsarrayext-where-t--jsinteroptypet)\<T> | Declarative interop macro type JSArrayEx. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------|:-----------------------------------------|
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |
| 34300005   | The ArkTS data types do not match.       |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Function:** Gets the ArkTS type name corresponding to the Cangjie type. Used in declarative interop macro framework scenarios; developers do not need to use this API.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func clone()

```cangjie
public func clone(): JSArrayEx<T>
```

**Function:** Clones JSArrayEx, performing a deep copy of the JSArrayEx data.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [JSArrayEx](#class-jsarrayext-where-t--jsinteroptypet)\<T> | New JSArrayEx obtained from cloning. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------|:-----------------------------------------|
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func cloneArrayEx(context: JSContext): JSValue {
    let originalArray: Array<Int64> = [1, 2, 3, 4, 5]
    let jsArrayEx = JSArrayEx<Int64>(originalArray)
    let clonedArrayEx = jsArrayEx.clone()

    Hilog.info(0, "test", "Original size: ${jsArrayEx.size}")
    Hilog.info(0, "test", "Cloned size: ${clonedArrayEx.size}")

    return clonedArrayEx.toJSValue(context)
}
```

### func concat(JSArrayEx\<T>)

```cangjie
public func concat(other: JSArrayEx<T>): JSArrayEx<T>
```

**Function:** This function creates a new JSArrayEx by concatenating the current JSArrayEx with the JSArrayEx pointed to by `other`.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [JSArrayEx](#class-jsarrayext-where-t--jsinteroptypet)\<T> | Yes | - | JSArrayEx to concatenate at the end. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSArrayEx](#class-jsarrayext-where-t--jsinteroptypet)\<T> | New JSArrayEx obtained from concatenation. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------|:-----------------------------------------|
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func concatArrayEx(context: JSContext): JSValue {
    let array1: Array<Int64> = [1, 2, 3]
    let array2: Array<Int64> = [4, 5, 6]

    let jsArrayEx1 = JSArrayEx<Int64>(array1)
    let jsArrayEx2 = JSArrayEx<Int64>(array2)

    let concatenated = jsArrayEx1.concat(jsArrayEx2)
    Hilog.info(0, "test", "Concatenated array size: ${concatenated.size}")

    return concatenated.toJSValue(context)
}
```

### func get(Int64)

```cangjie
public func get(index: Int64): Option<T>
```

**Function:** Gets the element at the specified `index` in the array.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | Index of the value to retrieve. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<T> | Value at the specified `index` in the current array. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------|:-----------------------------------------|
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getElementFromArrayEx(context: JSContext, callInfo: JSCallInfo): JSValue {
    let array: Array<String> = ["apple", "banana", "cherry"]
    let jsArrayEx = JSArrayEx<String>(array)

    let element = jsArrayEx.get(1)  // Get element at index 1
    if (element != None) {
        Hilog.info(0, "test", "Element at index 1: ${element}")
    }

    return jsArrayEx.toJSValue(context)
}
```

### func isEmpty()

```cangjie
public func isEmpty(): Bool
```

**Function:** Checks if the array is empty.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the array is empty; otherwise, returns `false`. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------|:-----------------------------------------|
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func checkArrayExEmpty(context: JSContext): JSValue {
    let emptyArray: Array<Int64> = []
    let nonEmptyArray: Array<Int64> = [1, 2, 3]

    let emptyJSArrayEx = JSArrayEx<Int64>(emptyArray)
    let nonEmptyJSArrayEx = JSArrayEx<Int64>(nonEmptyArray)

    Hilog.info(0, "test", "Is empty array empty: ${emptyJSArrayEx.isEmpty()}")
    Hilog.info(0, "test", "Is non-empty array empty: ${nonEmptyJSArrayEx.isEmpty()}")

    return context.boolean(emptyJSArrayEx.isEmpty()).toJSValue()
}
```

### func set(Int64, T)

```cangjie
public func set(index: Int64, element: T): Unit
```

**Function:** Modifies the value at the specified `index` in the array.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | Index of the value to modify, range: [0..this.size]. |
| element | T | Yes | - | Target value to set. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------|:-----------------------------------------|
| 34300001   | The accessing index is out of range.     |
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func setElementInArrayEx(context: JSContext): JSValue {
    let array: Array<Int64> = [1, 2, 3, 4, 5]
    let jsArrayEx = JSArrayEx<Int64>(array)

    // Modify element at index 2 to 10
    jsArrayEx.set(2, 10)
    Hilog.info(0, "test", "Modified element at index 2 to 10")

    return jsArrayEx.toJSValue(context)
}
```

### func toArray()

```cangjie
public func toArray(): Array<T>
```

**Function:** Converts to Array.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<T> | Converted Cangjie array. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------|:-----------------------------------------|
| 34300003   | Accessing reference is beyond reach.     |
| 34300004   | Thread mismatch.                         |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertArrayExToArray(context: JSContext): JSValue {
    let array: Array<String> = ["hello", "world", "cangjie"]
    let jsArrayEx = JSArrayEx<String>(array)

    let convertedArray = jsArrayEx.toArray()
    Hilog.info(0, "test", "Converted array size: ${convertedArray.size}")

    return jsArrayEx.toJSValue(context)
}
```

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Function:** Converts to JSValue. Used in declarative interop macro framework scenarios; developers do not need to use this API.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interop context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.              |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### operator func \[](Int64)

```cangjie
public operator func [](index: Int64): T
```

**Function:** Gets the value at the specified `index` in the array.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | Index of the value to retrieve. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | Value at the specified `index` in the current array. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------|:--------------------------------------|
| 34300001   | The accessing index is out of range.  |
| 34300003   | Accessing reference is beyond reach.  |
| 34300004   | Thread mismatch.                      |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getIndexOperator(context: JSContext): JSValue {
    let array: Array<Int64> = [10, 20, 30, 40]
    let jsArrayEx = JSArrayEx<Int64>(array)

    let value = jsArrayEx[2]  // Get element at index 2
    Hilog.info(0, "test", "Value at index 2: ${value}")

    return context.number(Float64(value)).toJSValue()
}
```

### operator func \[](Int64, T)

```cangjie
public operator func [](index: Int64, value!: T): Unit
```

**Function:** Modifies the value at the specified `index` in the array.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | Index of the value to modify, range: [0..this.size]. |
| value | T | Yes | - | **Named parameter.** Target value to set. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message |
|:------|:--------------------------------------|
| 34300001   | The accessing index is out of range.  |
| 34300003   | Accessing reference is beyond reach.  |
| 34300004   | Thread mismatch.                      |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func setIndexOperator(context: JSContext): JSValue {
    let array: Array<Int64> = [1, 2, 3, 4]
    let jsArrayEx = JSArrayEx<Int64>(array)

    // Set element at index 1 to 100
    jsArrayEx[1] = 100
    Hilog.info(0, "test", "Set value at index 1 to 100")

    return jsArrayEx.toJSValue(context)
}
```

## class JSBigInt

```cangjie
public class JSBigInt <: JSHeapObject {}
```

**Initial Version:** 22

**Description:** The JSBigInt object is used to represent a secure reference to the JS bigint type. By creating a JS bigint object, it can be converted to a Cangjie Int64 or Cangjie BigInt.

**Parent Type:**

- [JSHeapObject](#class-jsheapobject)

### func toBigInt()

```cangjie
public func toBigInt(): BigInt
```

**Description:** Converts to a Cangjie BigInt.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|BigInt|Cangjie BigInt.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                |
|:------|:--------------------------------------|
| 34300003   | Accessing reference is beyond reach.  |
| 34300004   | Thread mismatch.                      |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToBigInt(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsBigInt = callInfo[0].asBigInt()
    let bigIntValue = jsBigInt.toBigInt()

    Hilog.info(0, "test", "Converted BigInt value: ${bigIntValue}")

    return context.string(bigIntValue.toString()).toJSValue()
}
```

## class JSBoolean

```cangjie
public class JSBoolean {}
```

**Function:** ArkTS boolean type.

**Initial Version:** 22

### func toBool()

```cangjie
public func toBool(): Bool
```

**Function:** Converts to Cangjie Bool.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:-----|:------------|
| Bool | Cangjie boolean value. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                           |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsBool = context.boolean(true)
    let value = jsBool.toBool()
    Hilog.info(0, "test", "value is ${value}")
    return jsBool.toJSValue()
}
```

### func toJSValue()

```cangjie
public func toJSValue(): JSValue
```

**Function:** Converts to JSValue.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                           |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

## class JSCallInfo

```cangjie
public class JSCallInfo {}
```

**Function:** Contains information about an ArkTS function call. Allows accessing this pointer, parameter count, and retrieving parameters by index.

Each ArkTS function call stores parameter lists and related information on the ArkTS stack. JSCallInfo is a pointer to this information.

Lifecycle: The JSCallInfo becomes invalid when the ArkTS function call ends.

**Initial Version:** 22

### prop count

```cangjie
public prop count: Int64
```

**Function:** Number of input parameters.

**Initial Version:** 22

**Type:** Int64

**Access:** Read-only

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                           |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

### prop thisArg

```cangjie
public prop thisArg: JSValue
```

**Function:** this pointer.

**Initial Version:** 22

**Type:** [JSValue](#class-jsvalue)

**Access:** Read-only

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                           |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

### operator func \[](Int64)

```cangjie
public operator func [](index: Int64): JSValue
```

**Function:** Retrieves the corresponding parameter by index.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:----------|:-----|:---------|:--------|:------------|
| index | Int64 | Yes | - | Parameter index, safe range: [0, parameter count). |

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSValue](#class-jsvalue) | Parameter value. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:--------------------------------------|
| 34300001          | The accessing index is out of range.  |
| 34300003          | Accessing reference is beyond reach.  |
| 34300004          | Thread mismatch.                      |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    if (callInfo.count > 0) {
        let firstArg = callInfo[0]
        return firstArg
    }
    return context.undefined().toJSValue()
}
```

## class JSClass

```cangjie
public class JSClass <: JSHeapObject {}
```

**Description:** A secure reference to an ArkTS class (constructor). Methods and accessors can be added to this class, and instances of this class can be created.

**Initial Version:** 22

**Parent Type:**

- [JSHeapObject](#class-jsheapobject)

### prop prototype

```cangjie
public prop prototype: JSObject
```

**Description:** The prototype object of the class.

**Initial Version:** 22

**Type:** [JSObject](#class-jsobject)

**Read-Write Capability:** Read-only

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                           |
|:------|:-------------------------------|
| 34300002   | Outside error occurred.　             |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func accessClassPrototype(context: JSContext): JSValue {
    let ctor: JSLambda = { _, callInfo =>
        return callInfo.thisArg
    }
    let clazz = context.clazz(ctor)

    let prototype = clazz.prototype
    Hilog.info(0, "test", "Class prototype accessed")

    return prototype.toJSValue()
}
```

### func addAccessor(JSKeyable, ?JSFunction, ?JSFunction)

```cangjie
public func addAccessor(key: JSKeyable, getter!: ?JSFunction = None, setter!: ?JSFunction = None): Unit
```

**Description:** Defines a pair of getter and setter for the current ArkTS class.

**Initial Version:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|key|[JSKeyable](#interface-jskeyable)|Yes|-|Property key.|
|getter|?[JSFunction](#class-jsfunction)|No|None| **Named parameter.** Getter implementation.|
|setter|?[JSFunction](#class-jsfunction)|No|None| **Named parameter.** Setter implementation.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                 |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let ctor: JSLambda = { _, callInfo =>
        return callInfo.thisArg
    }
    let clazz = context.clazz(ctor)
    let getClassKind: JSLambda = { context, _ =>
        context.string("aaa").toJSValue()
    }
    clazz.addAccessor("classKind", getter: context.function(getClassKind))
    let obj = clazz.new()
    let classKind = obj.getProperty("classKind").toString()
    Hilog.info(0, "test", "class kind is ${classKind}")
    return obj
}
```

### func addAccessor(JSKeyable, ?JSLambda, ?JSLambda)

```cangjie
public func addAccessor(key: JSKeyable, getter!: ?JSLambda = None, setter!: ?JSLambda = None): Unit
```

**Description:** Defines a pair of getter and setter for the current ArkTS class.

**Initial Version:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|key|[JSKeyable](#interface-jskeyable)|Yes|-|Property key.|
|getter|?[JSLambda](#type-jslambda)|No|None| **Named parameter.** Getter implementation.|
|setter|?[JSLambda](#type-jslambda)|No|None| **Named parameter.** Setter implementation.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                 |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let ctor: JSLambda = { _, callInfo =>
        return callInfo.thisArg
    }
    let clazz = context.clazz(ctor)
    let getClassKind: JSLambda = { context, _ =>
        context.string("aaa").toJSValue()
    }
    clazz.addAccessor("classKind", getter: getClassKind)
    let obj = clazz.new()
    let classKind = obj.getProperty("classKind").toString()
    Hilog.info(0, "test", "class kind is ${classKind}")
    return obj
}
```

### func addMethod(JSKeyable, JSFunction)

```cangjie
public func addMethod(key: JSKeyable, method: JSFunction): Unit
```

**Description:** Defines a method for the current ArkTS class.

**Initial Version:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|key|[JSKeyable](#interface-jskeyable)|Yes|-|Property key.|
|method|[JSFunction](#class-jsfunction)|Yes|-|Method implementation.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                 |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let ctor: JSLambda = { _, callInfo =>
        return callInfo.thisArg
    }
    let clazz = context.clazz(ctor)
    let getClassKind: JSLambda = { context, _ =>
        context.string("aaa").toJSValue()
    }
    clazz.addMethod("getClassKind", context.function(getClassKind))
    let obj = clazz.new()
    let classKind = obj.getProperty("classKind").toString()
    Hilog.info(0, "test", "class kind is ${classKind}")
    return obj
}
```

### func addMethod(JSKeyable, JSLambda)

```cangjie
public func addMethod(key: JSKeyable, method: JSLambda): Unit
```

**Description:** Defines a method for the current ArkTS class.

**Initial Version:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|key|[JSKeyable](#interface-jskeyable)|Yes|-|Property key.|
|method|[JSLambda](#type-jslambda)|Yes|-|Method implementation.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                 |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let ctor: JSLambda = { _, callInfo =>
        return callInfo.thisArg
    }
    let clazz = context.clazz(ctor)
    let getClassKind: JSLambda = { context, _ =>
        context.string("aaa").toJSValue()
    }
    clazz.addMethod("getClassKind", getClassKind)
    let obj = clazz.new()
    let classKind = obj.getProperty("classKind").toString()
    Hilog.info(0, "test", "class kind is ${classKind}")
    return obj
}
```

### func addProperty(JSKeyable, JSValue)

```cangjie
public func addProperty(key: JSKeyable, value: JSValue): Unit
```

**Description:** Adds a data member to the target ArkTS class, typically used to define immutable properties.

**Initial Version:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|key|[JSKeyable](#interface-jskeyable)|Yes|-|Property key.|
|value|[JSValue](#class-jsvalue)|Yes|-|Property value.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                 |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let ctor: JSLambda = { _, callInfo =>
        return callInfo.thisArg
    }
    let clazz = context.clazz(ctor)
    clazz.addProperty("classKind", context.string("CustomClass").toJSValue())
    let obj = clazz.new()
    let classKind = obj.getProperty("classKind").toString()
    Hilog.info(0, "test", "class kind is ${classKind}")
    return obj
}
```

### func new()

```cangjie
public func new(): JSValue
```

**Description:** Instantiates a new object using the ArkTS class.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|The newly instantiated object.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                 |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let ctor: JSLambda = { _, callInfo =>
        return callInfo.thisArg
    }
    let clazz = context.clazz(ctor)
    let obj = clazz.new()
    return obj
}
```

### func new(JSValue)

```cangjie
public func new(arg: JSValue): JSValue
```

**Description:** Instantiates a new object using the ArkTS class.

**Initial Version:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|arg|[JSValue](#class-jsvalue)|Yes|-|Constructor argument.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|The newly instantiated object.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                 |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let ctor: JSLambda = { context, callInfo =>
        let firstArg = callInfo[0]
        let thisArg = callInfo.thisArg
        thisArg.setProperty("id", firstArg)
        return thisArg
    }
    let clazz = context.clazz(ctor)
    let id = context.number(1.0)
    let obj = clazz.new(id.toJSValue())
    return obj
}
```

### func new(Array\<JSValue>)

```cangjie
public func new(args: Array<JSValue>): JSValue
```

**Description:** Instantiates a new object using the ArkTS class.

**Initial Version:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|args|Array\<[JSValue](#class-jsvalue)>|Yes|-|Constructor argument list.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|The newly instantiated object.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message                                 |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let ctor: JSLambda = { context, callInfo =>
        let id = callInfo[0]
        let name = callInfo[1]
        let thisArg = callInfo.thisArg
        thisArg.setProperty("id", id)
        thisArg.setProperty("name", name)
        return thisArg
    }
    let clazz = context.clazz(ctor)
    let id = context.number(1.0)
    let name = context.string("aaa")
    let obj = clazz.new([id.toJSValue(), name.toJSValue()])
    return obj
}
```

## class JSContext

```cangjie
public class JSContext {}
```

**Description:** A single-threaded execution context for ArkTS interoperability.

There is a one-to-one correspondence between JSContext and the ArkTS runtime. Its primary purpose is to create JSValue and safe references, and manage the lifecycle of Cangjie objects referenced on the ArkTS side.

A JSContext holds a weak reference to an ArkTS runtime. This JSContext does not affect the lifecycle of the ArkTS runtime. When the ArkTS runtime becomes invalid, using this JSContext will throw a Cangjie exception.

**Since:** 22

### prop env

```cangjie
public prop env: JSEnv
```

**Description:** ArkTS interoperability context.

**Since:** 22

**Type:** JSEnv

**Access:** Read-only

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:--------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func accessContextEnv(context: JSContext): JSValue {
    let env = context.env
    Hilog.info(0, "test", "Context env accessed")

    return context.undefined().toJSValue()
}
```

### prop global

```cangjie
public prop global: JSObject
```

**Description:** The JavaScript global environment variable `globalThis`.

**Since:** 22

**Type:** [JSObject](#class-jsobject)

**Access:** Read-only

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:--------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func accessGlobalObject(context: JSContext): JSValue {
    let globalObj = context.global
    let globalKeys = globalObj.keys()

    Hilog.info(0, "test", "Global object has ${globalKeys.size} keys")

    return globalObj.toJSValue()
}
```

### func newScope\<T>(()->T)

```cangjie
public func newScope<T>(callback: ()->T): T
```

**Description:** Create an ArkTS handle scope。

**Since:** 24

**Parameters:**

| Parameter | Type | Required | Default | Description    |
|:---------|:---|:---------|:---|:---------------|
| callback | ()->T | Yes      |-| User callback。 |

**Return Value:**

| Type | Description                  |
|:---|:-----------------------------|
| T  | The result of user callback。 |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    spawn (UIThread) {
        context.newScope {
            let callback = context.function { c, _ =>
                Hilog.info(0, "test", "newScope called")
            }
            callback.call()
        }
    }
    return context.undefined().toJSValue()
}
```

### func array(Array\<JSValue>)

```cangjie
public func array(arr: Array<JSValue>): JSArray
```

**Description:** Creates an ArkTS array.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| arr      | Array\<[JSValue](#class-jsvalue)> | Yes | - | Reference to an ArkTS array. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSArray](#class-jsarray) | ArkTS array |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:--------------|:---------------------------------------|
| 34300002          | Outside error occurred.                |
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.array([])
    return result.toJSValue()
}
```

### func arrayBuffer(Int32)

```cangjie
public func arrayBuffer(length: Int32): JSArrayBuffer
```

**Description:** Creates an ArkTS ArrayBuffer from a memory block.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| length   | Int32 | Yes | - | Size of the memory block. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to an ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:--------------|:---------------------------------------|
| 34300001          | The arrayBuffer length is invalid.     |
| 34300002          | Outside error occurred.                |
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.arrayBuffer(Int32(10))
    return result.toJSValue()
}
```

### func arrayBuffer(Array\<Byte>)

```cangjie
public func arrayBuffer(data: Array<Byte>): JSArrayBuffer
```

**Description:** Creates an ArkTS ArrayBuffer from a memory block.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| data     | Array\<Byte> | Yes | - | Cangjie array. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to an ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:--------------|:---------------------------------------|
| 34300002          | Outside error occurred.                |
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let array : Array<Byte> = [1, 2, 3, 4, 5]
    let result = context.arrayBuffer(array)
    return result.toJSValue()
}
```

### func arrayBuffer(Array\<Int8>)

```cangjie
public func arrayBuffer(data: Array<Int8>): JSArrayBuffer
```

**Description:** Creates an ArkTS ArrayBuffer from a memory block.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| data     | Array\<Int8> | Yes | - | Cangjie array. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to an ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:--------------|:---------------------------------------|
| 34300002          | Outside error occurred.                |
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createArrayBufferFromInt8(context: JSContext): JSValue {
    let int8Array: Array<Int8> = [1, 2, 3]
    let arrayBuffer = context.arrayBuffer(int8Array)

    Hilog.info(0, "test", "Created ArrayBuffer from Int8 array")

    return arrayBuffer.toJSValue()
}
```

### func arrayBuffer(Array\<Int16>)

```cangjie
public func arrayBuffer(data: Array<Int16>): JSArrayBuffer
```

**Description:** Creates an ArkTS ArrayBuffer from a memory block.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| data     | Array\<Int16> | Yes | - | Cangjie array. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to an ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:--------------|:---------------------------------------|
| 34300002          | Outside error occurred.                |
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createArrayBufferFromInt16(context: JSContext): JSValue {
    let int16Array: Array<Int16> = [1, 2, 3]
    let arrayBuffer = context.arrayBuffer(int16Array)

    Hilog.info(0, "test", "Created ArrayBuffer from Int16 array")

    return arrayBuffer.toJSValue()
}
```

### func arrayBuffer(Array\<UInt16>)

```cangjie
public func arrayBuffer(data: Array<UInt16>): JSArrayBuffer
```

**Description:** Creates an ArkTS ArrayBuffer from a memory block.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| data     | Array\<UInt16> | Yes | - | Cangjie array. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to an ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:--------------|:---------------------------------------|
| 34300002          | Outside error occurred.                |
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createArrayBufferFromUInt16(context: JSContext): JSValue {
    let uint16Array: Array<UInt16> = [1, 2, 3]
    let arrayBuffer = context.arrayBuffer(uint16Array)

    Hilog.info(0, "test", "Created ArrayBuffer from UInt16 array")

    return arrayBuffer.toJSValue()
}
```

### func arrayBuffer(Array\<UInt32>)

```cangjie
public func arrayBuffer(data: Array<UInt32>): JSArrayBuffer
```

**Description:** Creates an ArkTS ArrayBuffer from a memory block.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| data     | Array\<UInt32> | Yes | - | Cangjie array. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to an ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:--------------|:---------------------------------------|
| 34300002          | Outside error occurred.                |
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createArrayBufferFromUInt32(context: JSContext): JSValue {
    let uint32Array: Array<UInt32> = [1, 2, 3]
    let arrayBuffer = context.arrayBuffer(uint32Array)

    Hilog.info(0, "test", "Created ArrayBuffer from UInt32 array")

    return arrayBuffer.toJSValue()
}
```

### func arrayBuffer(Array\<Int32>)

```cangjie
public func arrayBuffer(data: Array<Int32>): JSArrayBuffer
```

**Description:** Creates an ArkTS ArrayBuffer from a memory block.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| data     | Array\<Int32> | Yes | - | Cangjie array. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to an ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below.

| Error Code ID | Error Message                           |
|:--------------|:---------------------------------------|
| 34300002          | Outside error occurred.                |
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createArrayBufferFromInt32(context: JSContext): JSValue {
    let int32Array: Array<Int32> = [1, 2, 3]
    let arrayBuffer = context.arrayBuffer(int32Array)

    Hilog.info(0, "test", "Created ArrayBuffer from Int32 array")

    return arrayBuffer.toJSValue()
}
```

### func arrayBuffer(Array\<Float32>)

```cangjie
public func arrayBuffer(data: Array<Float32>): JSArrayBuffer
```

**Function:** Creates an ArkTS ArrayBuffer from a memory block.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| data | Array\<Float32> | Yes | - | Cangjie array. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to the ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createArrayBufferFromFloat32(context: JSContext): JSValue {
    let float32Array: Array<Float32> = [1.0, 2.0, 3.0]
    let arrayBuffer = context.arrayBuffer(float32Array)

    Hilog.info(0, "test", "Created ArrayBuffer from Float32 array")

    return arrayBuffer.toJSValue()
}
```

### func arrayBuffer(Array\<Int64>)

```cangjie
public func arrayBuffer(data: Array<Int64>): JSArrayBuffer
```

**Function:** Creates an ArkTS ArrayBuffer from a memory block.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| data | Array\<Int64> | Yes | - | Cangjie array. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to the ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createArrayBufferFromInt64(context: JSContext): JSValue {
    let int64Array: Array<Int64> = [1, 2, 3]
    let arrayBuffer = context.arrayBuffer(int64Array)

    Hilog.info(0, "test", "Created ArrayBuffer from Int64 array")

    return arrayBuffer.toJSValue()
}
```

### func arrayBuffer(Array\<UInt64>)

```cangjie
public func arrayBuffer(data: Array<UInt64>): JSArrayBuffer
```

**Function:** Creates an ArkTS ArrayBuffer from a memory block.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| data | Array\<UInt64> | Yes | - | Cangjie array. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to the ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createArrayBufferFromUInt64(context: JSContext): JSValue {
    let uint64Array: Array<UInt64> = [1u64, 2u64, 3u64]
    let arrayBuffer = context.arrayBuffer(uint64Array)

    Hilog.info(0, "test", "Created ArrayBuffer from UInt64 array")

    return arrayBuffer.toJSValue()
}
```

### func arrayBuffer(Array\<Float64>)

```cangjie
public func arrayBuffer(data: Array<Float64>): JSArrayBuffer
```

**Function:** Creates an ArkTS ArrayBuffer from a memory block.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| data | Array\<Float64> | Yes | - | Cangjie array. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to the ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createArrayBufferFromFloat64(context: JSContext): JSValue {
    let float64Array: Array<Float64> = [1.0, 2.0, 3.0]
    let arrayBuffer = context.arrayBuffer(float64Array)

    Hilog.info(0, "test", "Created ArrayBuffer from Float64 array")

    return arrayBuffer.toJSValue()
}
```

### func arrayBuffer(CPointer\<Byte>, Int32, JSBufferFinalizer)

```cangjie
public unsafe func arrayBuffer(rawData: CPointer<Byte>, length: Int32, finalizer: JSBufferFinalizer): JSArrayBuffer
```

**Function:** Creates an ArkTS ArrayBuffer from a memory block.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| rawData | CPointer\<Byte> | Yes | - | Memory block address. |
| length | Int32 | Yes | - | Memory block size. |
| finalizer | [JSBufferFinalizer](#type-jsbufferfinalizer) | Yes | - | Memory block cleanup function. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSArrayBuffer](#class-jsarraybuffer) | Reference to the ArkTS ArrayBuffer object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let rawPtr = unsafe {
        LibC.malloc<Byte>(count: 10)
    }
    let result = unsafe { context.arrayBuffer(rawPtr, 10) { rawPtr =>
        LibC.free(rawPtr)
    }}
    return result.toJSValue()
}
```

### func bigint(Int64)

```cangjie
public func bigint(value: Int64): JSBigInt
```

**Function:** Creates an ArkTS bigint with the same value as the Cangjie BigInt.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int64 | Yes | - | Cangjie BigInt. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSBigInt](#class-jsbigint) | Reference to the ArkTS bigint object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.bigint(100)
    return result.toJSValue()
}
```

### func bigint(BigInt)

```cangjie
public func bigint(value: BigInt): JSBigInt
```

**Function:** Creates an ArkTS bigint with the same value as the Cangjie BigInt.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | BigInt | Yes | - | Cangjie BigInt. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSBigInt](#class-jsbigint) | Reference to the ArkTS bigint object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import std.math.numeric.BigInt

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.bigint(BigInt(100))
    return result.toJSValue()
}
```

### func boolean(Bool)

```cangjie
public func boolean(value: Bool): JSBoolean
```

**Function:** Creates an ArkTS boolean.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Cangjie boolean value. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSBoolean](#class-jsboolean) | ArkTS boolean value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.boolean(true)
    return result.toJSValue()
}
```

### func clazz(JSLambda, ?JSClass)

```cangjie
public func clazz(ctor: JSLambda, superClass!: ?JSClass = None): JSClass
```

**Function:** Creates an ArkTS class.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| ctor | [JSLambda](#type-jslambda) | Yes | - | Cangjie function serving as the class constructor. |
| superClass | ?[JSClass](#class-jsclass) | No | None | **Named parameter.** Parent class of the ArkTS class. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSClass](#class-jsclass) | Reference to the ArkTS class. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func clsCtor(context: JSContext, callInfo: JSCallInfo): JSValue {
    callInfo.thisArg
}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.clazz(clsCtor)
    return result.toJSValue()
}
```

### func external(SharedObject)

```cangjie
public func external(data: SharedObject): JSExternal
```

**Function:** Creates an ArkTS reference to a Cangjie object.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| data | [SharedObject](#class-sharedobject) | Yes | - | Original Cangjie object. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSExternal](#class-jsexternal) | ArkTS reference to the Cangjie object. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
class Data <: SharedObject {}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let data = Data()
    let result = context.external(data)
    return result.toJSValue()
}
```

### func function(JSLambda)

```cangjie
public func function(lambda: JSLambda): JSFunction
```

**Function:** Creates an ArkTS function.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| lambda | [JSLambda](#type-jslambda) | Yes | - | Cangjie function. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSFunction](#class-jsfunction) | Reference to the ArkTS function. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func jsCallback(context: JSContext, callInfo: JSCallInfo): JSValue {
    return context.undefined().toJSValue()
}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.function(jsCallback)
    return result.toJSValue()
}
```

### func getNapiEnv()

```cangjie
public func getNapiEnv(): napi_env
```

**Function:** Retrieves a pointer to the global environment.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [napi_env](#type-napi_env) | Pointer to the global environment. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getNapiEnvironment(context: JSContext): JSValue {
    let napiEnv = context.getNapiEnv()
    Hilog.info(0, "test", "Got napi environment")

    return context.undefined().toJSValue()
}
```

### func isInBindThread()

```cangjie
public func isInBindThread(): Bool
```

**Function:** Multithreading utility: Checks whether the current thread can execute interoperation interfaces.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the current thread can call interoperation interfaces. |

**Example:**

<!--compile-->
```cangjie
func createObject(context: JSContext): JSObject {
    if (!context.isInBindThread()) {
        throw Exception("not able to call arkts on current thread")
    }
    return context.object()
}
```

### func null()

```cangjie
public func null(): JSNull
```

**Function:** Creates an ArkTS `null`.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [JSNull](#class-jsnull) | Returns ArkTS `null`. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.null()
    return result.toJSValue()
}
```

### func number(Float64)

```cangjie
public func number(value: Float64): JSNumber
```

**Function:** Creates an ArkTS number.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Cangjie Int32 number. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSNumber](#class-jsnumber) | ArkTS number. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.number(1.0)
    return result.toJSValue()
}
```

### func number(Int32)

```cangjie
public func number(value: Int32): JSNumber
```

**Function:** Creates an ArkTS number.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Cangjie Int32 number. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSNumber](#class-jsnumber) | ArkTS number. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.number(Int32(10))
    return result.toJSValue()
}
```

### func object()

```cangjie
public func object(): JSObject
```

**Function:** Creates an empty ArkTS object reference.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [JSObject](#class-jsobject) | ArkTS object reference. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.object()
    return result.toJSValue()
}
```

### func postJSTask(() -> Unit)

```cangjie
public func postJSTask(callback: ()->Unit): Unit
```

**Function:** Multithreading utility: Creates a task to be executed on the ArkTS thread.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | ()->Unit | Yes | - | Task to be executed on the ArkTS thread. |

**Example:**

<!--compile-->
```cangjie
func createObject(context: JSContext, callback: (JSObject)->Unit): Unit {
    if (context.isInBindThread()) {
        callback(context.object())
    } else {
        context.postJSTask {
            callback(context.object())
        }
    }
}
```

### func promiseCapability()

```cangjie
public func promiseCapability(): JSPromiseCapability
```

**Function:** Creates an ArkTS Promise.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [JSPromiseCapability](#class-jspromisecapability) | Native reference to the ArkTS Promise. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.promiseCapability()
    return result.toJSValue()
}
```

### func requireArkModule(String)

```cangjie
public func requireArkModule(path: String): JSValue
```

**Function:** Import an ArkTS module, including system modules, files in HAP modules, files in HAR modules, files in HSP modules and Native modules, see [Importing ArkTS Modules in Cangjie Code](../../learn-cj/FFI/cangjie-arkts/cangjie-load-arkts.md).

**Initial Version:** 23

**Parameters:**

| Parameter | Type   | Required | Default | Description           |
| :-------- | :----- | :------- | :------ | :-------------------- |
| path      | String | Yes      | -       | The module specifier. |

**Return Value:**

| Type                      | Description           |
| :------------------------ | :-------------------- |
| [JSValue](#class-jsvalue) | The module's JSValue. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                                     |
| :------------ | :---------------------------------------------------------------- |
| 34300002      | Module initialize fail.                                           |
| 34300004      | Thread mismatch.                                                  |
| 34300006      | Target module not exist.                                          |
| 34300007      | Can not requireArkModule during initializing cangjie module.      |
| 34300008      | Current application have not support requireArkModule of the url. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog
import ohos.business_exception.BusinessException

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    try {
        let hilog = context.requireArkModule("@ohos.hilog").asObject()
        hilog.callMethod("info", [
            context.number(0).toJSValue(),
            context.string("test").toJSValue(),
            context.string("call hilog success").toJSValue()
        ])
    } catch (e: BusinessException) {
        Hilog.info(0, "test", e.message)
    }
    return context.undefined().toJSValue()
}
```

### func requireSystemNativeModule(String, ?String)

```cangjie
public func requireSystemNativeModule(moduleName: String, prefix!: ?String = None): JSValue
```

**Function:** Loads a system-built ArkTS NAPI module.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| moduleName | String | Yes | - | Registered name of the ArkTS NAPI module. |
| prefix | ?String | No | None | **Named parameter.** Archive directory of the ArkTS NAPI module. Can be omitted if under `/system/lib64/module`; otherwise, specify the subdirectory name. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | Module return value, typically an object. Returns `undefined` if loading fails. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext): Unit {
    let hilog = context.requireSystemNativeModule("hilog")
    let pushService = context.requireSystemNativeModule("core.push.pushService", prefix: "hms")
}
```

### func string(String)

```cangjie
public func string(value: String): JSString
```

**Function:** Creates an ArkTS string.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | Cangjie string. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSString](#class-jsstring) | ArkTS string reference. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.string("abc")
    return result.toJSValue()
}
```

### func string(Utf16String)

```cangjie
public func string(value: Utf16String): JSString
```

**Function:** Creates a JSString from a Utf16String.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Utf16String](#class-utf16string) | Yes | - | Source Utf16String object. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSString](#class-jsstring) | JSString created from the source object. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let utf16string = Utf16String("abc")
    let result = context.string(utf16string)
    return result.toJSValue()
}
```

### func symbol(String)

```cangjie
public func symbol(description!: String = ""): JSSymbol
```

**Function:** Creates an ArkTS symbol object.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| description | String | No | "" | **Named parameter.** Description of the symbol. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSSymbol](#class-jssymbol) | ArkTS symbol object reference. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.symbol()
    let symbol1 = context.symbol(description: "Symbol1")
    return result.toJSValue()
}
```

### func undefined()

```cangjie
public func undefined(): JSUndefined
```

**Function:** Creates an ArkTS `undefined`.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [JSUndefined](#class-jsundefined) | Returns ArkTS `undefined`. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let result = context.undefined()
    return result.toJSValue()
}
```

## class JSExternal

```cangjie
public class JSExternal <: JSHeapObject {}
```

**Function:** A Cangjie object reference that can be passed to the ArkTS side. Allows accessing the bound Cangjie object.

JSExternal aims to pass a strong reference of a Cangjie object to the ArkTS runtime. Combined with other user-defined interoperability interfaces, it enables access to this Cangjie object.

**Initial Version:** 22

**Parent Type:**

- [JSHeapObject](#class-jsheapobject)

### func cast\<T>() where T <: SharedObject

```cangjie
public func cast<T>(): Option<T> where T <: SharedObject
```

**Function:** Gets the bound SharedObject and converts it to type T.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Option\<T>|The bound Cangjie object.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.              |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
class Data <: SharedObject {
    func doSth() {}
}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let external = callInfo[0].asExternal()

    if (let Some(data) <- external.cast<Data>()) {
         data.doSth()
     }

    context.undefined().toJSValue()
}
```

### func getData()

```cangjie
public func getData(): SharedObject
```

**Function:** Gets the bound SharedObject.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[SharedObject](#class-sharedobject)|The bound Cangjie object.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.              |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
class Data <: SharedObject {
    func doSth() {}
}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let external = callInfo[0].asExternal()

    let sharedObject = external.getData()
    if (let Some(data) <- (sharedObject as Data)) {
         data.doSth()
     }

    context.undefined().toJSValue()
}
```

## class JSFunction

```cangjie
public class JSFunction <: JSHeapObject {}
```

**Function:** A safe reference to an ArkTS function.

**Initial Version:** 22

**Parent Type:**

- [JSHeapObject](#class-jsheapobject)

### func call(JSValue)

```cangjie
public func call(thisArg!: JSValue = context.undefined().toJSValue()): JSValue
```

**Function:** Performs an ArkTS function call (multiple parameters).

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|thisArg|[JSValue](#class-jsvalue)|No|context.undefined().toJSValue()| **Named parameter.** this pointer.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|Function call return value.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.              |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let callback = callInfo[0].asFunction()
    return callback.call()
}
```

### func call(JSValue, JSValue)

```cangjie
public func call(arg: JSValue, thisArg!: JSValue = context.undefined().toJSValue()): JSValue
```

**Function:** Performs an ArkTS function call (multiple parameters).

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|arg|[JSValue](#class-jsvalue)|Yes|-|ArkTS function input parameter.|
|thisArg|[JSValue](#class-jsvalue)|No|context.undefined().toJSValue()| **Named parameter.** ArkTS function this pointer.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|Function call return value.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.              |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let callback = callInfo[0].asFunction()
    let arg0 = context.number(1.0).toJSValue()
    return callback.call(arg0)
}
```

### func call(Array\<JSValue>, JSValue)

```cangjie
public func call(args: Array<JSValue>, thisArg!: JSValue = context.undefined().toJSValue()): JSValue
```

**Function:** Performs an ArkTS function call (multiple parameters).

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|args|Array\<[JSValue](#class-jsvalue)>|Yes|-|Parameter list.|
|thisArg|[JSValue](#class-jsvalue)|No|context.undefined().toJSValue()| **Named parameter.** this pointer.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|Function call return value.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.              |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let callback = callInfo[0].asFunction()
    let arg0 = context.number(1.0).toJSValue()
    let arg1 = context.boolean(false).toJSValue()
    return callback.call([arg0, arg1])
}
```

## class JSHashMapEx<K, V> where K <: JSKeyable & Hashable & Equatable\<K> & JSInteropType\<K>, V <: JSInteropType\<V>

```cangjie
public class JSHashMapEx<K, V> <: JSInteropType<JSHashMapEx<K, V>> where K <: JSKeyable & Hashable & Equatable<K> & JSInteropType<K>, V <: JSInteropType<V> {
    public init(map: HashMap<K, V>)
    public init()
}
```

**Function:** Used in declarative interoperability macros, corresponding to ArkTS Map type.

**Initial Version:** 22

**Parent Type:**

- [JSInteropType\<JSHashMapEx\<K,V>>](#interface-jsinteroptypet)

### prop size

```cangjie
public prop size: Int64
```

**Function:** Returns the number of key-value pairs.

**Initial Version:** 22

**Type:** Int64

**Access:** Read-only

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### init(HashMap\<K,V>)

```cangjie
public init(map: HashMap<K, V>)
```

**Function:** Constructs an empty JSHashMapEx\<K, V> instance.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|map|HashMap\<K, V>|Yes|-|Creates from this HashMap instance.|

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog
import std.collection.HashMap

func createHashMapExFromHashMap(context: JSContext): JSValue {
    let hashMap = HashMap<String, Int64>()
    hashMap["key1"] = 1
    hashMap["key2"] = 2

    let jsHashMapEx = JSHashMapEx<String, Int64>(hashMap)
    Hilog.info(0, "test", "Created JSHashMapEx from HashMap with ${jsHashMapEx.size} elements")

    return jsHashMapEx.toJSValue(context)
}
```

### init()

```cangjie
public init()
```

**Function:** Constructs an empty JSHashMapEx\<K, V> instance.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createEmptyHashMapEx(context: JSContext): JSValue {
    let jsHashMapEx = JSHashMapEx<String, Int64>()
    Hilog.info(0, "test", "Created empty JSHashMapEx")

    return jsHashMapEx.toJSValue(context)
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(context: JSContext, input: JSValue): JSHashMapEx<K, V>
```

**Function:** Converts from JSValue to JSHashMapEx. For declarative interoperability macro framework scenarios. Developers don't need to use this API.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](#class-jscontext)|Yes|-|ArkTS interoperability context.|
|input|[JSValue](#class-jsvalue)|Yes|-|ArkTS unified type.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSHashMapEx](#class-jshashmapexk-v-where-k--jskeyable--hashable--equatablek--jsinteroptypek-v--jsinteroptypev)\<K, V>|Declarative interoperability macro type JSHashMapEx.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertJSValueToStringHashMapEx(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Create a JSHashMapEx<String, String>
    let source = JSHashMapEx<String, String>()
    // Add key-value pairs
    source["key1"] = "value1"
    // Convert to JSValue
    let jsValue = source.toJSValue(context)

    // Convert from JSValue to JSHashMapEx<String, String>
    let received = JSHashMapEx<String, String>.fromJSValue(context, jsValue)

    // Get all keys
    let keys = received.keys()

    // Iterate all key-value pairs
    for (key in keys) {
        let value = source[key]
        Hilog.info(0, "test", "Key: ${key}, Value: ${value}")
    }

    return jsValue
}
```

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Function:** Gets the corresponding ArkTS type name for the Cangjie type. Used in declarative interoperability macro framework scenarios; developers do not need to use this API.

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|Converted ArkTS type name.|

### func clear()

```cangjie
public func clear(): Unit
```

**Function:** Removes all elements from this HashMapEx.

**Since:** 22

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func clone()

```cangjie
public func clone(): JSHashMapEx<K, V>
```

**Function:** Clones the JSHashMapEx, performing a deep copy of the JSHashMapEx data.

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSHashMapEx](#class-jshashmapexk-v-where-k--jskeyable--hashable--equatablek--jsinteroptypek-v--jsinteroptypev)\<K, V>|New JSHashMapEx obtained from cloning.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func containsAll(Collection\<K>)

```cangjie
public func containsAll(keys: Collection<K>): Bool
```

**Function:** Determines whether mappings for all keys in the specified collection are contained.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|keys|Collection\<K>|Yes|-|Keys to be checked.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if all are contained; otherwise, returns false.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func delete(K)

```cangjie
public func delete(key: K): Bool
```

**Function:** Removes the mapping for the specified key from this JSHashMapEx (if present).

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|key|K|Yes|-|Key to be deleted.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the key existed and was successfully deleted; otherwise, returns false.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func deleteAll(Collection\<K>)

```cangjie
public func deleteAll(keys: Collection<K>): Unit
```

**Function:** Removes mappings for all keys in the specified collection from this JSHashMapEx (if present).

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|keys|Collection\<K>|Yes|-|Collection of keys to be deleted.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func deleteIf((K,V) -> Bool)

```cangjie
public func deleteIf(predicate: (K, V) -> Bool): Unit
```

**Function:** Takes a lambda expression and deletes key-value pairs that satisfy the condition.

This function traverses the entire JSHashMapEx, deleting all key-value pairs where predicate(K, V) == true.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|predicate|(K, V)->Bool|Yes|-|Lambda expression for evaluation.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func get(K)

```cangjie
public func get(key: K): Option<V>
```

**Function:** Returns the value to which the specified key is mapped, or Option\<V>.None if no mapping exists.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|key|K|Yes|-|Input key.|

**Return Value:**

|Type|Description|
|:----|:----|
|Option\<V>|Value corresponding to the key, wrapped in Option.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func has(K)

```cangjie
public func has(key: K): Bool
```

**Function:** Determines whether a mapping exists for the specified key.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|key|K|Yes|-|Key to be checked.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the mapping exists; otherwise, returns false.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func isEmpty()

```cangjie
public func isEmpty(): Bool
```

**Function:** Determines whether the JSHashMapEx is empty. Returns true if empty; otherwise, returns false.

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Whether the JSHashMapEx is empty.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func checkHashMapExEmpty(context: JSContext): JSValue {
    let emptyMap = JSHashMapEx<String, Int64>()
    let nonEmptyMap = JSHashMapEx<String, Int64>()
    nonEmptyMap.set("key", 1)

    Hilog.info(0, "test", "Is empty map empty: ${emptyMap.isEmpty()}")
    Hilog.info(0, "test", "Is non-empty map empty: ${nonEmptyMap.isEmpty()}")

    return context.boolean(emptyMap.isEmpty()).toJSValue()
}
```

### func keys()

```cangjie
public func keys(): EquatableCollection<K>
```

**Function:** Returns all keys in the JSHashMapEx, storing them in a Keys container.

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|EquatableCollection\<K>|Container holding all returned keys.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getHashMapExKeys(context: JSContext): JSValue {
    let jsHashMapEx = JSHashMapEx<String, Int64>()
    jsHashMapEx.set("key1", 1)
    jsHashMapEx.set("key2", 2)
    jsHashMapEx.set("key3", 3)

    let keys = jsHashMapEx.keys()
    Hilog.info(0, "test", "HashMapEx has ${keys.size} keys")

    return context.number(Float64(keys.size)).toJSValue()
}
```

### func set(K, V)

```cangjie
public func set(key: K, value: V): Unit
```

**Function:** Inserts a key-value pair into the JSHashMapEx.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|key|K|Yes|-|Key to be inserted.|
|value|V|Yes|-|Value to be assigned.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func setHashMapExValue(context: JSContext): JSValue {
    let jsHashMapEx = JSHashMapEx<String, Int64>()
    jsHashMapEx.set("myKey", 42)

    Hilog.info(0, "test", "Set value in HashMapEx")

    return jsHashMapEx.toJSValue(context)
}
```

### func setAll(Collection\<(K,V)>)

```cangjie
public func setAll(elements: Collection<(K, V)>): Unit
```

**Function:** Inserts a new collection of key-value pairs into the JSHashMapEx in the order of the elements' iterator.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|elements|Collection\<(K, V)>|Yes|-|Collection of key-value pairs to be added to the JSHashMapEx.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func setAllHashMapExValues(context: JSContext): JSValue {
    let jsHashMapEx = JSHashMapEx<String, Int64>()
    let elements: Array<(String, Int64)> = [("key1", 1), ("key2", 2), ("key3", 3)]

    jsHashMapEx.setAll(elements)
    Hilog.info(0, "test", "Set all values in HashMapEx")

    return jsHashMapEx.toJSValue(context)
}
```

### func setIfAbsent(K, V)

```cangjie
public func setIfAbsent(key: K, value: V): Bool
```

**Function:** Inserts the key-value pair (key, value) into the JSHashMapEx if the key does not already exist.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|key|K|Yes|-|Key to be inserted.|
|value|V|Yes|-|Value to be assigned.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns false if the key existed before assignment; otherwise, returns true.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func toHashMap()

```cangjie
public func toHashMap(): HashMap<K, V>
```

**Function:** Converts to HashMap.

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|HashMap\<K, V>|Converted HashMap.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(c: JSContext): JSValue
```

**Function:** Converts to JSValue. Used in declarative interoperability macro framework scenarios; developers do not need to use this API.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|c|[JSContext](#class-jscontext)|Yes|-|ArkTS interoperability context.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func values()

```cangjie
public func values(): Collection<V>
```

**Function:** Returns all values in the JSHashMapEx, storing them in a Values container.

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Collection\<V>|Container holding all returned values.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### operator func \[](K)

```cangjie
public operator func [](key: K): V
```

**Function:** Operator overload for the set method. If the key exists, the new value overwrites the old one; if the key does not exist, the key-value pair is added.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|key|K|Yes|-|Key to be inserted.|

**Return Value:**

|Type|Description|
|:----|:----|
|V|Value corresponding to the key.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.              |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getIndexOperatorHashMapEx(context: JSContext): JSValue {
    let jsHashMapEx = JSHashMapEx<String, Int64>()
    jsHashMapEx.set("myKey", 100)

    let value = jsHashMapEx["myKey"]
    Hilog.info(0, "test", "Value for 'myKey': ${value}")

    return context.number(Float64(value)).toJSValue()
}
```

### operator func \[](K, V)

```cangjie
public operator func [](key: K, value!: V): Unit
```

**Function:** Operator overload for the set method. If the key exists, the new value overwrites the old one; if the key does not exist, the key-value pair is added.

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|key|K|Yes|-|Key to be inserted.|
|value|V|Yes|-| **Named parameter.** Value to be assigned.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func setIndexOperatorHashMapEx(context: JSContext): JSValue {
    let jsHashMapEx = JSHashMapEx<String, Int64>()
    jsHashMapEx["newKey"] = 200

    Hilog.info(0, "test", "Set value using index operator")

    return jsHashMapEx.toJSValue(context)
}
```

## class JSHeapObject

```cangjie
abstract sealed class JSHeapObject {}
```

**Function:** A strong reference to an ArkTS runtime object (but it will not exceed the lifecycle of the ArkTS runtime nor prevent its destruction). Can be converted to JSValue.

It serves as the base class for all safe references. Users cannot create instances of this class directly, only its subclasses (hidden constructor). Its purpose is to allow the referenced ArkTS runtime object to outlive the Cangjie object itself.

**Initial Version:** 22

### func toJSValue()

```cangjie
public func toJSValue(): JSValue
```

**Function:** Converts to JSValue.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let external = context.number(123)
    let jsValue = external.toJSValue()
    return jsValue
}
```

## class JSModule

```cangjie
public class JSModule {}
```

**Function:** A static class providing symbol export registration interfaces.

The goal of JSModule is to provide symbol export capability (exporting to ArkTS). It works in conjunction with custom static initialization functions to register export targets into a global table when the dynamic library is loaded, which are then executed by the ArkTS engine for export.

**Initial Version:** 22

### static func registerClass(String, ClassRegister)

```cangjie
public static func registerClass(name: String, register: ClassRegister): Unit
```

**Function:** Registers an ArkTS class (constructor) to be exported to ArkTS.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Export name. |
| register | [ClassRegister](#type-classregister) | Yes | - | A function that returns an ArkTS class. |

**Example:**

<!--compile-->
```cangjie
class Main {
    static init() {
        JSModule.registerClass("SomeClass") { context =>
            let ctor: JSLambda = { context, callInfo =>
                return callInfo.thisArg
            }
            context.clazz(ctor)
        }
    }
}
```

### static func registerFunc(String, FuncRegister)

```cangjie
public static func registerFunc(name: String, register: FuncRegister): Unit
```

**Function:** Registers a function to be exported to ArkTS.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Export function name. |
| register | [FuncRegister](#type-funcregister) | Yes | - | A function that returns a JSFunction. |

**Example:**

<!--compile-->
```cangjie
class Main {
    static init() {
        JSModule.registerFunc("doSth") { context, callInfo =>
            return context.undefined().toJSValue()
        }
    }
}
```

### static func registerFunc(String, JSLambda)

```cangjie
public static func registerFunc(name: String, lambda: JSLambda): Unit
```

**Function:** Registers a function to be exported to ArkTS.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Export function name. |
| lambda | [JSLambda](#type-jslambda) | Yes | - | The function to be exported. |

**Example:**

<!--compile-->
```cangjie
class Main {
    static init() {
        JSModule.registerFunc("doSth") { context, callInfo =>
            return context.undefined().toJSValue()
        }
    }
}
```

### static func registerModule(ModuleRegister)

```cangjie
public static func registerModule(register: ModuleRegister): Unit
```

**Function:** Registers interfaces to be exported to ArkTS.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| register | [ModuleRegister](#type-moduleregister) | Yes | - | A function that can return an ArkTS class (constructor). |

**Example:**

<!--compile-->
```cangjie
class Main {
    static init() {
        JSModule.registerModule { context, exports =>
            exports["doSth"] = context.function { context, callInfo =>
                context.undefined().toJSValue()
            }.toJSValue()
        }
    }
}
```

## class JSNull

```cangjie
public class JSNull {}
```

**Function:** ArkTS null type.

**Initial Version:** 22

### func toJSValue()

```cangjie
public func toJSValue(): JSValue
```

**Function:** Converts to ArkTS unified type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:--------------------------------------|
| 34300003          | Accessing reference is beyond reach.  |
| 34300004          | Thread mismatch.                      |

## class JSNumber

```cangjie
public class JSNumber {}
```

**Function:** ArkTS number type.

**Initial Version:** 22

### func toFloat64()

```cangjie
public func toFloat64(): Float64
```

**Function:** Converts to Float64.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:-----|:------------|
| Float64 | Cangjie floating-point number. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:--------------------------------------|
| 34300003          | Accessing reference is beyond reach.  |
| 34300004          | Thread mismatch.                      |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsNum = context.number(1.0)
    let value = jsNum.toFloat64()
    Hilog.info(0, "test", "value is ${value}")
    return jsNum.toJSValue()
}
```

### func toJSValue()

```cangjie
public func toJSValue(): JSValue
```

**Function:** Converts to JSValue.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:--------------------------------------|
| 34300003          | Accessing reference is beyond reach.  |
| 34300004          | Thread mismatch.                      |

## class JSObject

```cangjie
public class JSObject <: JSObjectBase {}
```

**Function:** A safe reference to an ArkTS object.

**Initial Version:** 22

**Parent Type:**

- [JSObjectBase](#class-jsobjectbase)

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func setObjectProperties(context: JSContext): JSValue {
    let jsObject = context.object()

    // Set properties of different types
    jsObject.setProperty("name", context.string("John").toJSValue())
    jsObject.setProperty("age", context.number(30).toJSValue())
    jsObject.setProperty("isActive", context.boolean(true).toJSValue())

    // Set nested object
    let address = context.object()
    address.setProperty("city", context.string("Beijing").toJSValue())
    address.setProperty("country", context.string("China").toJSValue())
    jsObject.setProperty("address", address.toJSValue())

    Hilog.info(0, "test", "Set object properties")

    return jsObject.toJSValue()
}
```

## class JSObjectBase

```cangjie
abstract sealed class JSObjectBase <: JSHeapObject {}
```

**Function:** The base class for safe references to ArkTS objects. Allows manipulation of ArkTS objects.

**Initial Version:** 22

**Parent Type:**

- [JSHeapObject](#class-jsheapobject)

### func attachCJObject(JSExternal)

```cangjie
public func attachCJObject(target: JSExternal): Unit
```

**Function:** Binds a Cangjie object reference in ArkTS to the current object.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| target | [JSExternal](#class-jsexternal) | Yes | - | ArkTS reference to the Cangjie object. |

**Example:**

<!--compile-->
```cangjie
class Data <: SharedObject {}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = context.object()
    let data = Data()
    let ext = context.external(data)
    obj.attachCJObject(ext)
    return obj.toJSValue()
}
```

### func callMethod(JSKeyable, Array\<JSValue>)

```cangjie
public func callMethod(key: JSKeyable, args: Array<JSValue>): JSValue
```

**Function:** Invokes a method under the current object.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [JSKeyable](#interface-jskeyable) | Yes | - | Target method name. |
| args | Array\<[JSValue](#class-jsvalue)> | Yes | - | List of arguments for the invocation. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | Method invocation return value. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let json = context.global["JSON"].asObject()
    json.callMethod("parse", [context.string("{a: 1, b: 2}").toJSValue()])
}
```

### func defineOwnAccessor(JSKeyable, ?JSFunction, ?JSFunction, Bool, Bool)

```cangjie
public func defineOwnAccessor(key: JSKeyable, getter!:? JSFunction = None, setter!: ?JSFunction = None,
    isEnumerable!: Bool = false,
    isConfigurable!: Bool = false
): Bool
```

**Function:** Defines accessors for the current object.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [JSKeyable](#interface-jskeyable) | Yes | - | Target key. |
| getter | ?[JSFunction](#class-jsfunction) | No | None | **Named parameter.** Getter implementation. |
| setter | ?[JSFunction](#class-jsfunction) | No | None | **Named parameter.** Setter implementation. |
| isEnumerable | Bool | No | false | **Named parameter.** Whether enumerable. |
| isConfigurable | Bool | No | false | **Named parameter.** Whether redefinable. |

**Return Value:**

| Type | Description |
|:-----|:------|
| Bool | Whether successful. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = context.object()
    let getter = context.function { context, callInfo =>
        context.number(1.0).toJSValue()
    }
    obj.defineOwnAccessor("a", getter: getter, isConfigurable: false)
    return obj.toJSValue()
}
```

### func defineOwnAccessor(JSKeyable, ?JSLambda, ?JSLambda, Bool, Bool)

```cangjie
public func defineOwnAccessor(key: JSKeyable, getter!:? JSLambda = None, setter!: ?JSLambda = None,
    isEnumerable!: Bool = false,
    isConfigurable!: Bool = false
): Bool
```

**Function:** Defines accessors for the current object.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [JSKeyable](#interface-jskeyable) | Yes | - | Target key. |
| getter | ?[JSLambda](#type-jslambda) | No | None | **Named parameter.** Getter implementation. |
| setter | ?[JSLambda](#type-jslambda) | No | None | **Named parameter.** Setter implementation. |
| isEnumerable | Bool | No | false | **Named parameter.** Whether enumerable. |
| isConfigurable | Bool | No | false | **Named parameter.** Whether redefinable. |

**Return Value:**

| Type | Description |
|:-----|:------|
| Bool | Whether successful. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = context.object()
    let getter: JSLambda = { context, callInfo =>
        context.number(1.0).toJSValue()
    }
    obj.defineOwnAccessor("a", getter: getter, isConfigurable: false)
    return obj.toJSValue()
}
```

### func defineOwnProperty(JSKeyable, JSValue, Bool, Bool, Bool)

```cangjie
public func defineOwnProperty(key: JSKeyable, setValue: JSValue,
    isWritable!: Bool = true,
    isEnumerable!: Bool = true,
    isConfigurable!: Bool = true
): Bool
```

**Function:** Defines a property on the current object.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [JSKeyable](#interface-jskeyable) | Yes | - | Target key. |
| setValue | [JSValue](#class-jsvalue) | Yes | - | Target value. |
| isWritable | Bool | No | true | **Named parameter.** Whether writable. |
| isEnumerable | Bool | No | true | **Named parameter.** Whether enumerable. |
| isConfigurable | Bool | No | true | **Named parameter.** Whether redefinable. |

**Return Value:**

| Type | Description |
|:-----|:------|
| Bool | Whether successful. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = context.object()
    obj.defineOwnProperty("a", context.number(1.0).toJSValue(), isWritable: true, isConfigurable: false)
    return obj.toJSValue()
}
```

### func getAttachInfo()

```cangjie
public func getAttachInfo(): ?JSExternal
```

**Function:** Retrieves the bound Cangjie object from the current object.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| ?[JSExternal](#class-jsexternal) | ArkTS reference to the Cangjie object or None. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
class Data <: SharedObject {
    func doSth() {}
}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = callInfo[0].asObject()
    let sharedObJ = obj.getAttachInfo().getOrThrow()
    let data = (sharedObJ as Data).getOrThrow()
    data.doSth()
    context.undefined().toJSValue()
}
```

### func getProperty(JSKeyable)

```cangjie
public func getProperty(key: JSKeyable): JSValue
```

**Function:** Retrieves the target property value from the current object.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [JSKeyable](#interface-jskeyable) | Yes | - | Target key. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | Retrieved value. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = callInfo[0].asObject()
    let result = obj.getProperty("a")
    return result
}
```

### func hasProperty(JSKeyable)

```cangjie
public func hasProperty(key: JSKeyable): Bool
```

**Function:** Determines whether the current object has the target property.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [JSKeyable](#interface-jskeyable) | Yes | - | Target key. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the current object has the target property. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = callInfo[0].asObject()
    let hasA = obj.hasProperty("a")
    Hilog.info(0, "test", "obj has property of a: ${hasA}")
    obj.toJSValue()
}
```

### func instanceOf(JSClass)

```cangjie
public func instanceOf(clazz: JSClass): Bool
```

**Function:** Determines whether the current object is an instance of the target ArkTS class.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| clazz | [JSClass](#class-jsclass) | Yes | - | Target ArkTS class. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the object is an instance of the target ArkTS class. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let ctor: JSLambda = { context, callInfo =>
        callInfo.thisArg
    }
    let classA = context.clazz(ctor)
    let obj = classA.new().asObject()
    let isClassA = obj.instanceOf(classA)
    Hilog.info(0, "test", "obj is classA: ${isClassA}")
    return obj.toJSValue()
}
```

### func keys()

```cangjie
public func keys(): Array<String>
```

**Function:** Enumerates all enumerable property names of the current object.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | List of keys. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let keys = context.global.keys()
    Hilog.info(0, "test", "global keys: ${keys}")
    context.undefined().toJSValue()
}
```

### func setProperty(JSKeyable, JSValue)

```cangjie
public func setProperty(key: JSKeyable, setValue: JSValue): Unit
```

**Function:** Assigns a value to a property of the current object.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [JSKeyable](#interface-jskeyable) | Yes | - | Target key. |
| setValue | [JSValue](#class-jsvalue) | Yes | - | Target value. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = context.object()
    obj.setProperty("a", context.number(1.0).toJSValue())
    return obj.toJSValue()
}
```

### operator func \[](JSKeyable)

```cangjie
public operator func [](key: JSKeyable): JSValue
```

**Function:** Assigns a value to a property of the current object.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [JSKeyable](#interface-jskeyable) | Yes | - | Target key. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | Retrieved value. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = callInfo[0].asObject()
    let result = obj["a"]
    return result
}
```

### operator func \[](JSKeyable, JSValue)

```cangjie
public operator func [](key: JSKeyable, value!: JSValue): Unit
```

**Function:** Assigns a value to a property of the current object.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [JSKeyable](#interface-jskeyable) | Yes | - | Target key. |
| value | [JSValue](#class-jsvalue) | Yes | - | **Named parameter.** Target value. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 2 | Outside error occurred. |
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = context.object()
    obj["a"] = context.number(1.0).toJSValue()
    return obj.toJSValue()
}
```

## class JSPromise

```cangjie
public class JSPromise <: JSHeapObject {}
```

**Function:** A callback mechanism encapsulation object.

JSPromise aims to provide a consistent encapsulation for callback patterns, greatly enhancing usability when combined with async/await syntax sugar.

The lifecycle of JSPromise exceeds that of the referenced ArkTS object.

**Initial Version:** 22

**Parent Type:**

- [JSHeapObject](#class-jsheapobject)

### func catchError(JSFunction)

```cangjie
public func catchError(callback: JSFunction): Unit
```

**Function:** Registers an exception handling callback.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [JSFunction](#class-jsfunction) | Yes | - | Exception handling callback. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let promise = callInfo[0].asPromise()
    let onError: JSLambda = {context, callInfo =>
        context.undefined().toJSValue()
    }
    promise.catchError(context.function(onError))
    context.undefined().toJSValue()
}
```

### func then(JSFunction, ?JSFunction)

```cangjie
public func then(onFulfilled: JSFunction, onRejected!: ?JSFunction = None): Unit
```

**Function:** Registers a result handling callback.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| onFulfilled | [JSFunction](#class-jsfunction) | Yes | - | Result handling callback. |
| onRejected | ?[JSFunction](#class-jsfunction) | No | None | **Named parameter.** Exception handling callback. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let promise = callInfo[0].asPromise()
    let onFulfilled: JSLambda = {context, callInfo =>
        context.undefined().toJSValue()
    }
    promise.then(context.function(onFulfilled))
    context.undefined().toJSValue()
}
```

## class JSPromiseCapability

```cangjie
public class JSPromiseCapability {
}
```

**Function:** JSPromiseCapability corresponds to a Promise object, allowing resolution and rejection of that Promise.

Lifecycle: JSPromiseCapability is a weak reference. The lifecycle of the corresponding ArkTS object ends upon first resolution or rejection. Subsequent usage after termination will throw a Cangjie exception.

**Initial Version:** 22

### func reject(JSValue)

```cangjie
public func reject(value: JSValue): Unit
```

**Function:** Submits an exception to the Promise.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [JSValue](#class-jsvalue) | Yes | - | Exception data, typically an Error object or string. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let promise = context.promiseCapability()
    // toJSValue must be called before reject, as the object becomes inaccessible after rejection
    let result = promise.toJSValue()
    promise.reject(context.string("a exception occured").toJSValue())
    return result
}
```

### func resolve(JSValue)

```cangjie
public func resolve(value: JSValue): Unit
```

**Function:** Notifies the Promise of normal completion and submits a return value.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [JSValue](#class-jsvalue) | Yes | - | Processing result. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func addNumberAsync(context: JSContext, callInfo: JSCallInfo): JSValue {
    let a = callInfo[0].toNumber()
    let b = callInfo[1].toNumber()
    let promise = context.promiseCapability()
    // toJSValue must be called before resolve, as the object becomes inaccessible after resolution
    let result = promise.toJSValue()
    promise.resolve(context.number(a + b).toJSValue())
    return result
}
```

### func toJSValue()

```cangjie
public func toJSValue(): JSValue
```

**Function:** Converts to the ArkTS unified type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func addNumberAsync(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Convert ArkTS input parameters to Cangjie types
    let a = callInfo[0].toNumber()
    let b = callInfo[1].toNumber()
    // Create PromiseCapability
    let promise = context.promiseCapability()
    spawn {
        // Use a new thread for computationally intensive tasks
        let result = a + b
        // Return to the ArkTS thread
        context.postJSTask {
            // Submit result to ArkTS
            promise.resolve(context.number(result).toJSValue())
        }
    }
    // Return Promise
    promise.toJSValue()
}
```

## class JSRuntime

```cangjie
public class JSRuntime {
    public init()
}
```

**Function:** ArkTS runtime created by Cangjie.

**Initial Version:** 22

> **Note:**
>
> In Cangjie applications, JSRuntime() can only be used on the main thread to create an ArkTS runtime.

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getJSRuntimeInstance(): Unit {
    // Create JSRuntime instance
    let runtime = JSRuntime()
    // Get JSContext instance
    let context = runtime.mainContext

    Hilog.info(0, "test", "Got JSRuntime instance")

    let jsValue = context.string("JSRuntime instance obtained").toJSValue()
}
```

### prop mainContext

```cangjie
public prop mainContext: JSContext
```

**Function:** Interoperation context.

**Initial Version:** 22

**Type:** [JSContext](#class-jscontext)

**Access:** Read-only

### init()

```cangjie
public init()
```

**Function:** Constructor.

**Initial Version:** 22

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.　             |

### func getNapiEnv()

```cangjie
public func getNapiEnv(): CPointer<Unit>
```

**Function:** Retrieves the environment pointer.

**Return Value:**

| Type | Description |
|:---------|:------------|
| CPointer\<Unit> | napi interface env. |

**Initial Version:** 22

## class JSString

```cangjie
public class JSString <: JSHeapObject & ToString & JSKeyable {}
```

**Function:** A safe reference to an ArkTS string. Can be converted to String.

**Initial Version:** 22

**Parent Types:**

- [JSHeapObject](#class-jsheapobject)
- ToString
- [JSKeyable](#interface-jskeyable)

### func toJSValue(JSContext)

```cangjie
public func toJSValue(_: JSContext): JSValue
```

**Function:** Converts to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts to a Cangjie string.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Cangjie string. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsStr = context.string("abc")
    let value = jsStr.toString()
    Hilog.info(0, "test", "value is ${value}")
    return jsStr.toJSValue()
}
```

### func toUtf16String()

```cangjie
public func toUtf16String(): Utf16String
```

**Function:** Converts from JSString to Utf16String.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Utf16String](#class-utf16string) | Converted Utf16String object. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### extend JSString <: JSInteropType\<JSString>

**Function:** Implements extension methods for the class type JSString.

**Initial Version:** 22

**Parent Types:**

- [JSInteropType\<JSString>](#interface-jsinteroptypet)

#### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, input: JSValue): JSString
```

**Function:** Converts JSValue type to the corresponding JSString type.

**Initial Version:** 22

**Parameters:**

| Parameter | Type                          | Required | Default | Description                   |
| :-------- | :---------------------------- | :------- | :------ | :---------------------------- |
| _         | [JSContext](#class-jscontext) | Yes      | -       | ArkTS interoperation context. |
| input     | [JSValue](#class-jsvalue)     | Yes      | -       | ArkTS unified type.           |

**Return Value:**

| Type                        | Description             |
| :-------------------------- | :---------------------- |
| [JSString](#class-jsstring) | JSString type converted by JSValue type. |

**Exceptions:**

- BusinessException: Error codes as follows，see [Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                        |
| :------------ | :----------------------------------- |
| 34300002      | Outside error occurred.              |
| 34300003      | Accessing reference is beyond reach. |
| 34300004      | Thread mismatch.                     |
| 34300005      | The ArkTS data types do not match.   |

#### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Function:** Gets the ArkTS type name corresponding to the JSString type.

**Initial Version:** 22

**Return Value:**

| Type   | Description                |
| :----- | :------------------------- |
| String | Corresponding ArkTS type name, i.e., "string" |

## class JSStringEx

```cangjie
public class JSStringEx <: JSInteropType<JSStringEx> & Equatable<JSStringEx> & ToString {
    public init(str: String)
}
```

**Function:** Extends the functionality and performance of [JSString](#class-jsstring), usable in declarative interoperation macros.

**Initial Version:** 22

**Parent Types:**

- [JSInteropType\<JSStringEx>](#interface-jsinteroptypet)
- Equatable\<JSStringEx>
- ToString

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createJSStringEx(context: JSContext): JSValue {
    // Create a JSStringEx object
    let sourceString: String = "Hello, World!"
    let jsStringEx = JSStringEx(sourceString)

    Hilog.info(0, "test", "Created JSStringEx with content: ${jsStringEx.toString()}")

    return jsStringEx.toJSValue(context)
}
```

### init(String)

```cangjie
public init(str: String)
```

**Function:** Constructs a corresponding JSStringEx instance from a given String.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| str | String | Yes | - | Initial string. |

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(context: JSContext, input: JSValue): JSStringEx
```

**Function:** Converts from JSValue to JSStringEx. Used in declarative interoperation macro framework scenarios; developers do not need to use this API.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |
| input | [JSValue](#class-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSStringEx](#class-jsstringex) | Declarative interoperation macro type JSStringEx. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Function:** Retrieves the ArkTS type name corresponding to the Cangjie type. Used in declarative interoperation macro framework scenarios; developers do not need to use this API.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted ArkTS type name. |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Function:** Converts to JSValue. Used in declarative interoperation macro framework scenarios; developers do not need to use this API.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperation context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts to String.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted string. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### operator func !=(JSStringEx)

```cangjie
public operator func !=(str: JSStringEx): Bool
```

**Function:** Determines if two JSStringEx instances are not equal.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| str | [JSStringEx](#class-jsstringex) | Yes | - | String to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if not equal, false if equal. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

### operator func ==(JSStringEx)

```cangjie
public operator func ==(str: JSStringEx): Bool
```

**Function:** Determines if two JSStringEx instances are equal.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| str | [JSStringEx](#class-jsstringex) | Yes | - | String to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if equal, false if not equal. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

## class JSSymbol

```cangjie
public class JSSymbol <: JSHeapObject & JSKeyable {}
```

**Function:** A secure reference to a JavaScript symbol.

**Initial Version:** 22

**Parent Types:**

- [JSHeapObject](#class-jsheapobject)
- [JSKeyable](#interface-jskeyable)

**Example:**

<!--compile-->
```cangjie
func createSymbol(context: JSContext): JSValue {
    // Create a JSSymbol object
    let symbol = context.symbol(description: "mySymbol")
    // Create a JSObject
    let object = context.object()
    // Use symbol as key to store a hidden property
    object[symbol] = context.string("123").toJSValue()
    // Create a publicly visible function that accesses the object property via symbol
    object["name"] = context.function { context, callInfo =>
        return object[symbol]
    }.toJSValue()
    return object.toJSValue()
}
```

### prop description

```cangjie
public prop description: String
```

**Function:** Description of the symbol.

**Initial Version:** 22

**Type:** String

**Access:** Read-only

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                           |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

### func toJSValue(JSContext)

```cangjie
public func toJSValue(_: JSContext): JSValue
```

**Function:** Converts to JSValue. Used in declarative interoperability macro framework scenarios. Developers should not use this API directly.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:----------|:-----|:---------|:--------|:------------|
| _ | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                           |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts to String.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:-----|:------------|
| String | Converted string. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                           |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |

## class JSUndefined

```cangjie
public class JSUndefined {}
```

**Function:** ArkTS null.

**Initial Version:** 22

### func toJSValue()

```cangjie
public func toJSValue(): JSValue
```

**Function:** Converts to JSValue.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|ArkTS unified type.|

**Exceptions:**

- BusinessException: Error codes are listed below.

| Error Code ID | Error Message                               |
|:------|:--------------------------------------|
| 34300003   | Accessing reference is beyond reach.  |
| 34300004   | Thread mismatch.                      |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let undefined = context.undefined()
    let jsValue = undefined.toJSValue()
    return jsValue
}
```

## class JSValue

```cangjie
public class JSValue {}
```

**Function:** An ArkTS variable (weakly typed, short lifecycle).

JSValue is the unified type in ArkTS runtime and serves as the data type for direct interaction with the ArkTS runtime.

Only interoperation interfaces can create JSValue. Its lifecycle ends when it goes out of scope (the stack where it was created). It cannot be copied, captured, or returned in non-interoperation functions. If you need to pass this variable, you must first convert it and then pass it as a Cangjie type or safe reference.

**Initial Version:** 22

### func asArray()

```cangjie
public func asArray(): JSArray
```

**Function:** Converts a JSValue to JSArray.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSArray](#class-jsarray)|A reference to an ArkTS array.|

**Exceptions:**

- BusinessException: Error codes are listed below.

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asArrayBuffer()

```cangjie
public func asArrayBuffer(): JSArrayBuffer
```

**Function:** Converts a JSValue to JSArrayBuffer.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSArrayBuffer](#class-jsarraybuffer)|A reference to an ArkTS ArrayBuffer.|

**Exceptions:**

- BusinessException: Error codes are listed below.

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asBigInt()

```cangjie
public func asBigInt(): JSBigInt
```

**Function:** Converts a JSValue to JSBigInt.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSBigInt](#class-jsbigint)|A reference to an ArkTS bigint.|

**Exceptions:**

- BusinessException: Error codes are listed below.

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asBoolean()

```cangjie
public func asBoolean(): JSBoolean
```

**Function:** Converts a JSValue to JSBoolean.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSBoolean](#class-jsboolean)|An ArkTS boolean.|

**Exceptions:**

- BusinessException: Error codes are listed below.

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asClass()

```cangjie
public func asClass(): JSClass
```

**Function:** Converts a JSValue to JSClass.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSClass](#class-jsclass)|A reference to an ArkTS class.|

**Exceptions:**

- BusinessException: Error codes are listed below.

| Error Code ID | Error Message                               |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asExternal()

```cangjie
public func asExternal(): JSExternal
```

**Function:** Converts a JSValue to JSExternal.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSExternal](#class-jsexternal)|A reference to a Cangjie object in ArkTS.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asFunction()

```cangjie
public func asFunction(): JSFunction
```

**Function:** Converts a JSValue to JSFunction.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSFunction](#class-jsfunction)|A reference to an ArkTS function.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asNull()

```cangjie
public func asNull(): JSNull
```

**Function:** Converts a JSValue to JSNull.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSNull](#class-jsnull)|An ArkTS null value.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asNumber()

```cangjie
public func asNumber(): JSNumber
```

**Function:** Converts a JSValue to JSNumber.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSNumber](#class-jsnumber)|An ArkTS number value.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asObject()

```cangjie
public func asObject(): JSObject
```

**Function:** Converts a JSValue to JSObject.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSObject](#class-jsobject)|A reference to an ArkTS object.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asPromise()

```cangjie
public func asPromise(): JSPromise
```

**Function:** Converts a JSValue to JSPromise.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSPromise](#class-jspromise)|A reference to an ArkTS promise.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asString()

```cangjie
public func asString(): JSString
```

**Function:** Converts a JSValue to JSString.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSString](#class-jsstring)|A reference to an ArkTS string.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asSymbol()

```cangjie
public func asSymbol(): JSSymbol
```

**Function:** Converts a JSValue to JSSymbol.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSSymbol](#class-jssymbol)|A reference to an ArkTS symbol.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func asUndefined()

```cangjie
public func asUndefined(): JSUndefined
```

**Function:** Converts a JSValue to JSUndefined.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSUndefined](#class-jsundefined)|An ArkTS undefined value.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func bindObject(JSValue)

```cangjie
public func bindObject(external: JSValue): Unit
```

**Function:** Binds a Cangjie object to an ArkTS object.

**Initial Version:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|external|[JSValue](#class-jsvalue)|Yes|-|ArkTS reference to a Cangjie object.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
class Data <: SharedObject {
}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsObJ = callInfo[0]
    let data = Data()
    let external = context.external(data)
    jsObJ.bindObject(external.toJSValue())
    return jsObJ
}
```

>

### func bindObject(SharedObject)

```cangjie
public func bindObject(data: SharedObject): Unit
```

**Function:** Binds a Cangjie object to an ArkTS object.

**Initial Version:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|data|[SharedObject](#class-sharedobject)|Yes|-|Cangjie object.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
class Data <: SharedObject {
}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsObJ = callInfo[0]
    let data = Data()
    jsObJ.bindObject(data)
    return jsObJ
}
```

>

### func getBindingObject()

```cangjie
public func getBindingObject(): ?SharedObject
```

**Function:** Retrieves the Cangjie object bound to an ArkTS object.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|?[SharedObject](#class-sharedobject)|The bound Cangjie object.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.　             |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
class Data <: SharedObject {
    func doSth() {}
}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsObJ = callInfo[0]
    if (let Some(shareData) <- jsObJ.getBindingObject()) {
        if (let Some(data) <- (shareData as Data)) {
            data.doSth()
        }
    }
    return jsObJ
}
```

### func getElement(Int64)

```cangjie
public func getElement(index: Int64): JSValue
```

**Function:** Retrieves an element from an ArkTS array.

**Initial Version:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|index|Int64|Yes|-|Array element index.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](#class-jsvalue)|An ArkTS value.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                              |
|:------|:-------------------------------------|
| 34300001   | The accessing index is out of range. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsArr = callInfo[0]
    let element = jsArr.getElement(0)
    return element
}
```

### func getProperty(JSKeyable)

```cangjie
public func getProperty(key: JSKeyable): JSValue
```

**Function:** Reads a property from an ArkTS object.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [JSKeyable](#interface-jskeyable) | Yes | - | The property key, which can be a String, JSString, or JSSymbol. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | The retrieved value |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsObJ = callInfo[0]
    let element = jsObJ.getProperty("a")
    let element1 = jsObJ.getProperty(context.string("a"))
    let element2 = jsObJ.getProperty(context.symbol())
    return element
}
```

>

### func isArray()

```cangjie
public func isArray(): Bool
```

**Function:** Determines whether a JSValue is of Array type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the type is Array. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it is an object
    let result = arg0.isArray()
    // Return the result
    return context.boolean(result).toJSValue()
}
```

### func isArrayBuffer()

```cangjie
public func isArrayBuffer(): Bool
```

**Function:** Determines whether a JSValue is of ArrayBuffer type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the type is ArrayBuffer. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it is an ArrayBuffer
    let result = arg0.isArrayBuffer()
    // Return the result
    return context.boolean(result).toJSValue()
}
```

### func isBigInt()

```cangjie
public func isBigInt(): Bool
```

**Function:** Determines whether a JSValue is of bigint type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the type is bigint. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it is a bigint
    let result = arg0.isBigInt()
    // Return the result
    return context.boolean(result).toJSValue()
}
```

### func isBoolean()

```cangjie
public func isBoolean(): Bool
```

**Function:** Determines whether a JSValue is of boolean type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the type is boolean. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it is a boolean
    let result = arg0.isBoolean()
    // Return the result
    return context.boolean(result).toJSValue()
}
```

### func isClass()

```cangjie
public func isClass(): Bool
```

**Function:** Determines whether a JSValue is an ArkTS class (constructor).

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the type is an ArkTS class (constructor). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it is an ArkTS class (constructor)
    let result = arg0.isClass()
    // Return the result
    return context.boolean(result).toJSValue()
}
```

### func isExternal()

```cangjie
public func isExternal(): Bool
```

**Function:** Determines whether a JSValue is an external object (ArkTS reference of a Cangjie object).

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the type is an external object (ArkTS reference of a Cangjie object). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it is an external object (ArkTS reference of a Cangjie object)
    let result = arg0.isExternal()
    // Return the result
    return context.boolean(result).toJSValue()
}
```

### func isFunction()

```cangjie
public func isFunction(): Bool
```

**Function:** Determines whether a JSValue is of function type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the type is function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it is a function
    let result = arg0.isFunction()
    // Return the result
    return context.boolean(result).toJSValue()
}
```

### func isNull()

```cangjie
public func isNull(): Bool
```

**Function:** Determines whether a JSValue is null.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the type is null. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it is null
    let result = arg0.isNull()
    // Return the result
    return context.boolean(result).toJSValue()
}
```

### func isNumber()

```cangjie
public func isNumber(): Bool
```

**Function:** Determines whether a JSValue is of number type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the type is number. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it is a number
    let result = arg0.isNumber()
    // Return the result
    return context.boolean(result).toJSValue()
}
```

### func isObject()

```cangjie
public func isObject(): Bool
```

**Function:** Determines whether a JSValue is of object type.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the type is object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below.

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it is an object
    let result = arg0.isObject()
    // Return the result
    return context.boolean(result).toJSValue()
}
```

### func isPromise()

```cangjie
public func isPromise(): Bool
```

**Function:** Determines whether a JSValue is of Promise type.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the type is Promise.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it's a Promise
    let result = arg0.isPromise()
    // Return result
    return context.boolean(result).toJSValue()
}
```

### func isString()

```cangjie
public func isString(): Bool
```

**Function:** Determines whether a JSValue is of string type.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the type is string.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it's a string
    let result = arg0.isString()
    // Return result
    return context.boolean(result).toJSValue()
}
```

### func isSymbol()

```cangjie
public func isSymbol(): Bool
```

**Function:** Determines whether a JSValue is of Symbol type.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the type is Symbol.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it's a Symbol
    let result = arg0.isSymbol()
    // Return result
    return context.boolean(result).toJSValue()
}
```

### func isUndefined()

```cangjie
public func isUndefined(): Bool
```

**Function:** Determines whether a JSValue is undefined.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the type is undefined.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get input parameter
    let arg0 = callInfo[0]
    // Check if it's undefined
    let result = arg0.isUndefined()
    // Return result
    return context.boolean(result).toJSValue()
}
```

### func setElement(Int64, JSValue)

```cangjie
public func setElement(index: Int64, value: JSValue): Unit
```

**Function:** Writes an element to an ArkTS array.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|index|Int64|Yes|-|Array write index.|
|value|[JSValue](#class-jsvalue)|Yes|-|Value to write to the array.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300001   | The accessing index is out of range. |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsArr = callInfo[0]
    let setValue = context.number(1.0)
    jsArr.setElement(0, setValue.toJSValue())
    let element = jsArr.getElement(0)
    return element
}
```

### func setProperty(JSKeyable, JSValue)

```cangjie
public func setProperty(key: JSKeyable, setValue: JSValue): Unit
```

**Function:** Writes a property to an ArkTS object.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|key|[JSKeyable](#interface-jskeyable)|Yes|-|Property key.|
|setValue|[JSValue](#class-jsvalue)|Yes|-|Property value.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.                |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let jsObJ = context.object()
    let setValue = context.number(1.0)
    jsObJ.setProperty("a", setValue.toJSValue())
    return jsObJ.toJSValue()
}
```

### func strictEqual(JSValue)

```cangjie
public func strictEqual(target: JSValue): Bool
```

**Function:** Performs strict equality comparison between two JSValues (type consistency + value equality).

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|target|[JSValue](#class-jsvalue)|Yes|-|Target value for comparison|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two values are identical|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get two input parameters
    let arg0 = callInfo[0]
    let arg1 = callInfo[1]
    // Perform strict equality comparison
    let isStrictEqual = arg0.strictEqual(arg1)
    // Return the comparison result
    return context.boolean(isStrictEqual).toJSValue()
}
```

### func toBigInt()

```cangjie
public func toBigInt(): BigInt
```

**Function:** Converts a JSValue to BigInt.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|BigInt|Cangjie BigInt.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let value = callInfo[0].toBigInt()
    Hilog.info(0, "test", "value is ${value}")
    return context.undefined().toJSValue()
}
```

### func toBoolean()

```cangjie
public func toBoolean(): Bool
```

**Function:** Converts a JSValue to Bool.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Cangjie Bool value.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let value = callInfo[0].toBoolean()
    Hilog.info(0, "test", "value is ${value}")
    return context.undefined().toJSValue()
}
```

### func toNumber()

```cangjie
public func toNumber(): Float64
```

**Function:** Converts a JSValue to Float64.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Float64|Cangjie Float64 value.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let value = callInfo[0].toNumber()
    Hilog.info(0, "test", "value is ${value}")
    return context.undefined().toJSValue()
}
```

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts a JSValue to String.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|Cangjie string.|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300002   | Outside error occurred.　             |
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

**Example:**

<!--compile-->
```cangjie
// Checks if the first parameter is a number; if yes, returns true; otherwise returns the data type as a string
func checkIsNumber(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get parameter
    let value: JSValue = callInfo[0]
    // Get parameter type
    let valueType: JSType = value.typeof()
    // Type check
    if (valueType == JSType.NUMBER) {
        // Return true
        return context.boolean(true).toJSValue()
    }
    // Return type string
    return context.string(valueType.toString()).toJSValue()
}
```

### func toUtf16String()

```cangjie
public func toUtf16String(): Utf16String
```

**Function:** Converts a JSValue to Utf16String.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[Utf16String](#class-utf16string)|Converted Utf16String object.|
**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |
| 34300005   | The ArkTS data types do not match.   |

### func typeof()

```cangjie
public func typeof(): JSType
```

**Function:** Gets the type of a JSValue, which is basically consistent with the types enumerated by ArkTS's typeof syntax.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[JSType](#struct-jstype)|ArkTS type|

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                                |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |
| 34300004   | Thread mismatch.                     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get first parameter
    let arg0 = callInfo[0]
    // Get parameter type
    let valueType = arg0.typeof()
    // Print parameter type
    Hilog.info(0, "test", "arg type is ${valueType.toString()}")
    arg0
}
``````markdown
## type ClassRegister

```cangjie
public type ClassRegister =(JSContext) -> JSClass
```

**Function:** ClassRegister is a type alias for ([JSContext](#class-jscontext)) -> [JSClass](#class-jsclass).

**Since:** 22

## class SharedObject

```cangjie
public open class SharedObject {
    public init()
}
```

**Function:** Base class for Cangjie objects that can be referenced by ArkTS.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
// Create a class inheriting from SharedObject
class MyObject <: SharedObject {
    let name: String = "MyObject"
}

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Instantiate a MyObject
    let data = MyObject()
    // Create a JSExternal object from data
    let external = context.external(data)
    // Create a JSObject
    let object = context.object()
    // Bind external to object
    object.attachCJObject(external)
    // Create a publicly visible function that accesses object properties
    object["name"] = context.function { context, callInfo =>
        // Get this object
        let object = callInfo.thisArg.asObject()
        // Retrieve the bound MyObject instance from object
        let external = object.getAttachInfo().getOrThrow()
        // Convert data.name to JSString
        let name = context.string(external.cast<MyObject>().getOrThrow().name)
        return name.toJSValue()
    }.toJSValue()
    return object.toJSValue()
}
```

### prop nativeId

```cangjie
public prop nativeId: Int64
```

**Function:** Unique identifier of the object.

**Initial Version:** 22

**Type:** Int64

**Access:** Read-only

### init()

```cangjie
public init()
```

**Function:** Creates a SharedObject instance.

**Initial Version:** 22

## class Utf16String

```cangjie
public class Utf16String <: ToString & Equatable<Utf16String> & Hashable & JSKeyable & JSInteropType<Utf16String> {
    public static let EMPTY: Utf16String
    public init(src: String)
}
```

**Function:** A string stored in UTF-16 encoding format, which offers better performance than String when converting to/from ArkTS strings.

**Since:** 22

**Parent Types:**

- ToString
- Equatable\<Utf16String>
- Hashable
- [JSKeyable](#interface-jskeyable)
- [JSInteropType\<Utf16String>](#interface-jsinteroptypet)

### prop accessible

```cangjie
public prop accessible: Bool
```

**Function:** Determines whether the string content is accessible. The string content of this object can be manually released using dispose. Accessing it after release will throw an exception.

**Since:** 22

**Type:** Bool

**Access:** Read-only

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func checkStringAccessibility(context: JSContext): JSValue {
    let utf16Str = Utf16String("Test String")

    if (utf16Str.accessible) {
        Hilog.info(0, "test", "String content is accessible")
        // Safely use the string content
        let length = utf16Str.size
        Hilog.info(0, "test", "String length: ${length}")
    } else {
        Hilog.info(0, "test", "String content is not accessible")
    }

    return context.boolean(utf16Str.accessible).toJSValue()
}
```

### prop size

```cangjie
public prop size: Int64
```

**Function:** Represents the total length of code units in this string (UTF-16 encoding format). In UTF-16 encoding, each code unit occupies 2 bytes, and each character consists of 1-2 code units.

**Since:** 22

**Type:** Int64

**Access:** Read-only

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getStringSize(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello 世界")  // Contains mixed Chinese and English characters
    let size = utf16Str.size  // Total length of UTF-16 code units

    Hilog.info(0, "test", "UTF-16 string size: ${size}")

    return context.number(Float64(size)).toJSValue()
}
```

### prop totalChars

```cangjie
public prop totalChars: Int64
```

**Function:** The total number of characters in this string.

**Since:** 22

**Type:** Int64

**Access:** Read-only

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getStringTotalChars(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello 世界")  // Contains mixed Chinese and English characters
    let totalChars = utf16Str.totalChars  // Total number of characters

    Hilog.info(0, "test", "Total characters: ${totalChars}")

    return context.number(Float64(totalChars)).toJSValue()
}
```

### static let EMPTY

```cangjie
public static let EMPTY: Utf16String
```

**Function:** An empty string.

**Since:** 22

**Type:** Utf16String

**Access:** Read-only

### init(String)

```cangjie
public init(src: String)
```

**Function:** Creates a Utf16String from a standard library String.

**Since:** 22

**Parameters:**

| Parameter | Type   | Required | Default | Description          |
|:----------|:-------|:---------|:--------|:---------------------|
| src       | String | Yes      | -       | The target string.   |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:---------------------------------------|
| 34300002          | Outside error occurred.                |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createUtf16String(context: JSContext): JSValue {
    // Create Utf16String from a string
    let utf16Str = Utf16String("Hello World")
    Hilog.info(0, "test", "Created Utf16String with content: ${utf16Str.toString()}")

    // Create Utf16String from JSValue
    let jsString = context.string("Test String")
    let utf16Str2 = Utf16String(jsString.toString())
    Hilog.info(0, "test", "Created Utf16String from JSValue: ${utf16Str2.toString()}")

    return context.string(utf16Str.toString()).toJSValue()
}
```

### static func fromJSValue(JSContext, JSValue)

```cangjie
public static func fromJSValue(_: JSContext, value: JSValue): Utf16String
```

**Function:** Converts a JSValue to a Utf16String object.

**Since:** 22

**Parameters:**

| Parameter | Type               | Required | Default | Description                     |
|:----------|:-------------------|:---------|:--------|:--------------------------------|
| _         | [JSContext](#class-jscontext) | Yes      | -       | ArkTS interoperability context. |
| value     | [JSValue](#class-jsvalue)    | Yes      | -       | ArkTS unified type.             |

**Return Value:**

| Type                     | Description            |
|:-------------------------|:-----------------------|
| [Utf16String](#class-utf16string) | A Utf16String object.  |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |
| 34300004          | Thread mismatch.                       |
| 34300005          | The ArkTS data types do not match.     |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func createFromJSValue(context: JSContext): JSValue {
    let jsString = context.string("Hello from JS")
    let jsValue = jsString.toJSValue()

    // Create Utf16String from JSValue
    let utf16Str = Utf16String.fromJSValue(context, jsValue)

    Hilog.info(0, "test", "Created from JSValue: ${utf16Str.toString()}")

    return context.string(utf16Str.toString()).toJSValue()
}
```

### static func toArktsType()

```cangjie
public static func toArktsType(): String
```

**Function:** The corresponding ArkTS type name.

**Since:** 22

**Return Value:**

| Type   | Description                     |
|:-------|:--------------------------------|
| String | The corresponding ArkTS type name. |

### func compare(Utf16String)

```cangjie
public func compare(target: Utf16String): Ordering
```

**Function:** Compares strings lexicographically based on Unicode characters.

**Since:** 22

**Parameters:**

| Parameter | Type                     | Required | Default | Description                     |
|:----------|:-------------------------|:---------|:--------|:--------------------------------|
| target    | [Utf16String](#class-utf16string) | Yes      | -       | The Utf16String to compare with. |

**Return Value:**

| Type    | Description                |
|:--------|:---------------------------|
| Ordering | The comparison result.     |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |

### func contains(Utf16String)

```cangjie
public func contains(target: Utf16String): Bool
```

**Function:** Checks whether the string contains the target string.

**Since:** 22

**Parameters:**

| Parameter | Type                     | Required | Default | Description                                                 |
|:----------|:-------------------------|:---------|:--------|:------------------------------------------------------------|
| target    | [Utf16String](#class-utf16string) | Yes      | -       | The target string. Returns false if target string is empty. |

**Return Value:**

| Type | Description                          |
|:-----|:-------------------------------------|
| Bool | Whether the target string is contained. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |

### func count(Utf16String)

```cangjie
public func count(src: Utf16String): Int64
```

**Function:** Counts the occurrences of the target string.

**Since:** 22

**Parameters:**

| Parameter | Type                     | Required | Default | Description                     |
|:----------|:-------------------------|:---------|:--------|:--------------------------------|
| src       | [Utf16String](#class-utf16string) | Yes      | -       | The target string.               |

**Return Value:**

| Type  | Description                     |
|:------|:--------------------------------|
| Int64 | The count of target string occurrences. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message                          |
|:-------------|:---------------------------------------|
| 34300003          | Accessing reference is beyond reach.   |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func countSubstring(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello World Hello Hello")
    let target = Utf16String("Hello")

    let count = utf16Str.count(target)

    Hilog.info(0, "test", "Count of 'Hello': ${count}")

    return context.number(Float64(count)).toJSValue()
}
```

### func dispose()

```cangjie
public func dispose(): Unit
```

**Function:** Releases the memory storing the string content. Accessing the string content after the first dispose will cause an exception.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func disposeString(context: JSContext): JSValue {
    let utf16Str = Utf16String("Test String")

    // Using string content
    let content = utf16Str.toString()
    Hilog.info(0, "test", "String content before dispose: ${content}")

    // Manually release string content memory
    utf16Str.dispose()

    // Access after dispose will throw exception
    // let contentAfterDispose = utf16Str.toString() // This line will throw exception

    return context.string("String disposed").toJSValue()
}
```

### func endsWith(Utf16String)

```cangjie
public func endsWith(target: Utf16String): Bool
```

**Function:** Determines whether the string ends with the target string.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description                                             |
|:---|:---|:---|:---|:--------------------------------------------------------|
| target | [Utf16String](#class-utf16string) | Yes | - | Target string. Returns false if target string is empty. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the string ends with the target string. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func checkEndsWith(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello World")
    let target = Utf16String("World")

    let endsWithResult = utf16Str.endsWith(target)

    Hilog.info(0, "test", "String ends with 'World': ${endsWithResult}")

    return context.boolean(endsWithResult).toJSValue()
}
```

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Function:** Computes the hash value of the string.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Hash value of the string.<br>**Note:** This hash value is not guaranteed to match the hash of a String with identical content. Nor is it guaranteed to match the hash of an ArkTS string with identical content. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getStringHashCode(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello World")
    let hashCode = utf16Str.hashCode()

    Hilog.info(0, "test", "String hash code: ${hashCode}")

    return context.number(Float64(hashCode)).toJSValue()
}
```

### func indexOf(Utf16String)

```cangjie
public func indexOf(target: Utf16String): ?Int64
```

**Function:** Searches backward for the position of the target string (character index).

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| target | [Utf16String](#class-utf16string) | Yes | - | Target string. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?Int64 | Returns the position index when the target string is first found, or None if not found. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func findSubstring(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello World Hello")
    let target = Utf16String("World")

    let index = utf16Str.indexOf(target)

    if (index != None) {
        Hilog.info(0, "test", "Found 'World' at index: ${index}")
    } else {
        Hilog.info(0, "test", "Substring not found")
    }

    return context.number(Float64(index.getOrDefault({=> -1}))).toJSValue()
}
```

### func indexOf(Utf16String, Int64)

```cangjie
public func indexOf(target: Utf16String, fromIndex: Int64): ?Int64
```

**Function:** Searches backward for the position of the target string (code unit index).

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| target | [Utf16String](#class-utf16string) | Yes | - | Target string. |
| fromIndex | Int64 | Yes | - | Starting position for search in the current string. Default is 0 if not specified. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?Int64 | Returns the position index when the target string is first found, or None if not found. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

### func isEmpty()

```cangjie
public func isEmpty(): Bool
```

**Function:** Determines whether the string is empty.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the string is empty. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func checkIsEmpty(context: JSContext): JSValue {
    let emptyStr = Utf16String("")
    let nonEmptyStr = Utf16String("Hello")

    let isEmpty1 = emptyStr.isEmpty()
    let isEmpty2 = nonEmptyStr.isEmpty()

    Hilog.info(0, "test", "Empty string is empty: ${isEmpty1}")
    Hilog.info(0, "test", "Non-empty string is empty: ${isEmpty2}")

    return context.boolean(isEmpty1).toJSValue()
}
```

### func isCompressed()

```cangjie
public func isCompressed(): Bool
```

**Function:** Determines whether the content is compressed.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the content is compressed. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func checkIsCompressed(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello World")

    let isCompressed = utf16Str.isCompressed()

    Hilog.info(0, "test", "String is compressed: ${isCompressed}")

    return context.boolean(isCompressed).toJSValue()
}
```

### func lastIndexOf(Utf16String)

```cangjie
public func lastIndexOf(target: Utf16String): ?Int64
```

**Function:** Searches forward for the position of the target string.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| target | [Utf16String](#class-utf16string) | Yes | - | Target string. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?Int64 | Returns the position index when the target string is first found, or None if not found. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func findLastSubstring(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello World Hello")
    let target = Utf16String("Hello")

    let index = utf16Str.lastIndexOf(target)

    if (index != None) {
        Hilog.info(0, "test", "Last 'Hello' found at index: ${index}")
    } else {
        Hilog.info(0, "test", "Substring not found")
    }

    return context.number(Float64(index.getOrDefault({=> -1}))).toJSValue()
}
```

### func lastIndexOf(Utf16String, Int64)

```cangjie
public func lastIndexOf(target: Utf16String, fromIndex: Int64): ?Int64
```

**Function:** Searches forward for the position of the target string.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description                                                                                                                                              |
|:---|:---|:---|:---|:---------------------------------------------------------------------------------------------------------------------------------------------------------|
| target | [Utf16String](#class-utf16string) | Yes | - | Target string.                                                                                                                                           |
| fromIndex | Int64 | Yes | - | Starting position for search in the current string. Default is size - 1 if not specified.If the value is less than 0 or greater than size, returns None. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?Int64 | Returns the position index when the target string is first found, or None if not found. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func findLastSubstringFromIndex(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello World Hello")
    let target = Utf16String("Hello")

    // Search forward starting from index 10
    let index = utf16Str.lastIndexOf(target, 10)

    if (index != None) {
        Hilog.info(0, "test", "Last 'Hello' found at index: ${index}")
    } else {
        Hilog.info(0, "test", "Substring not found")
    }

    return context.number(Float64(index.getOrDefault({=> -1}))).toJSValue()
}
```

### func lazySplit(Utf16String, Bool)

```cangjie
public func lazySplit(separator: Utf16String, removeEmpty!: Bool = false): Iterator<Utf16String>
```

**Function:** Lazily splits the string.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| separator | [Utf16String](#class-utf16string) | Yes | - | Separator. When the separator is an empty string, each character is treated as a separate element. |
| removeEmpty | Bool | No | false | Whether to remove empty elements. |

**Return Value:**

| Type | Description |
|:----|:----|
| Iterator\<[Utf16String](#class-utf16string)> | Iterator of split elements. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func lazySplitString(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello,World,Test,Example")
    let separator = Utf16String(",")

    // Lazily split the string, removing empty elements
    let splitIterator = utf16Str.lazySplit(separator, removeEmpty: true)

    var count = 0
    for (part in splitIterator) {
        Hilog.info(0, "test", "Lazy split part ${count}: ${part.toString()}")
        count = count + 1
    }

    return context.number(Float64(count)).toJSValue()
}
```

### func lazySplit(Utf16String, Int64, Bool)

```cangjie
public func lazySplit(separator: Utf16String, maxSplit: Int64, removeEmpty!: Bool = false): Iterator<Utf16String>
```

**Function:** Lazy string splitting.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description                                                                                        |
|:---|:---|:---|:---|:---------------------------------------------------------------------------------------------------|
| separator | [Utf16String](#class-utf16string) | Yes | - | Delimiter. When the delimiter is an empty string, each character is treated as a separate element. |
| maxSplit | Int64 | Yes | - | Maximum number of splits. Treat as 0 when less than 0.                                             |
| removeEmpty | Bool | No | false | Whether to remove empty elements.                                                                  |

**Return Value:**

| Type | Description |
|:----|:----|
| Iterator\<[Utf16String](#class-utf16string)> | Iterator of split elements. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |

### func lines()

```cangjie
public func lines(): Iterator<Utf16String>
```

**Function:** Get line iterator.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Iterator\<[Utf16String](#class-utf16string)> | Line iterator. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func getLines(context: JSContext): JSValue {
    let utf16Str = Utf16String("Line 1\nLine 2\nLine 3")

    // Get line iterator
    let lineIterator = utf16Str.lines()

    var count = 0
    for (line in lineIterator) {
        Hilog.info(0, "test", "Line ${count}: ${line.toString()}")
        count = count + 1
    }

    return context.number(Float64(count)).toJSValue()
}
```

### func replace(Utf16String, Utf16String, Int64)

```cangjie
public func replace(old: Utf16String, new: Utf16String, count!: Int64 = Int64.Max): Utf16String
```

**Function:** Replace string.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| old | [Utf16String](#class-utf16string) | Yes | - | Element to be replaced |
| new | [Utf16String](#class-utf16string) | Yes | - | Replacement element |
| count | Int64 | No | Int64.Max | Number of replacements |

**Return Value:**

| Type | Description |
|:----|:----|
| [Utf16String](#class-utf16string) | Replaced string |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func replaceString(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello World Hello")
    let target = Utf16String("Hello")
    let replacement = Utf16String("Hi")

    // Replace at most once
    let replacedStr = utf16Str.replace(target, replacement, count: 1)

    Hilog.info(0, "test", "Original string: ${utf16Str.toString()}")
    Hilog.info(0, "test", "Replaced string: ${replacedStr.toString()}")

    return context.string(replacedStr.toString()).toJSValue()
}
```

### func runes()

```cangjie
public func runes(): Iterator<Rune>
```

**Function:** Get character iterator.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Iterator\<Rune> | Character iterator. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |

### func split(Utf16String, Bool)

```cangjie
public func split(separator: Utf16String, removeEmpty!: Bool = false): Array<Utf16String>
```

**Function:** Split string.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| separator | [Utf16String](#class-utf16string) | Yes | - | Delimiter. When the delimiter is an empty string, each character is treated as a separate element. |
| removeEmpty | Bool | No | false | Whether to remove empty elements. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[Utf16String](#class-utf16string)> | Array of split elements. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func splitString(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello,World,Test")
    let separator = Utf16String(",")

    // Split string into max 3 parts, keeping empty elements
    let splitResult = utf16Str.split(separator, 3, removeEmpty: false)

    Hilog.info(0, "test", "Split result size: ${splitResult.size}")

    for (i in 0..splitResult.size) {
        Hilog.info(0, "test", "Part ${i}: ${splitResult[i].toString()}")
    }

    return context.number(Float64(splitResult.size)).toJSValue()
}
```

### func split(Utf16String, Int64, Bool)

```cangjie
public func split(separator: Utf16String, maxSplit: Int64, removeEmpty!: Bool = false): Array<Utf16String>
```

**Function:** Split string.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description                                                                                        |
|:---|:---|:---|:---|:---------------------------------------------------------------------------------------------------|
| separator | [Utf16String](#class-utf16string) | Yes | - | Delimiter. When the delimiter is an empty string, each character is treated as a separate element. |
| maxSplit | Int64 | Yes | - | Maximum number of splits. Unlimited when set to 0. Throws exception when less than 0.              |
| removeEmpty | Bool | No | false | Whether to remove empty elements.                                                                  |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[Utf16String](#class-utf16string)> | Array of split elements. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 1 | The accessing index is out of range. |
| 3 | Accessing reference is beyond reach. |

### func startsWith(Utf16String)

```cangjie
public func startsWith(target: Utf16String): Bool
```

**Function:** Check if string starts with target string.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description                                      |
|:---|:---|:---|:---|:-------------------------------------------------|
| target | [Utf16String](#class-utf16string) | Yes | - | Target string. Returns false if target is empty. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the string starts with the target string. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func checkStartsWith(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello World")
    let target = Utf16String("Hello")

    let startsWithResult = utf16Str.startsWith(target)

    Hilog.info(0, "test", "String starts with 'Hello': ${startsWithResult}")

    return context.boolean(startsWithResult).toJSValue()
}
```

### func toJSValue(JSContext)

```cangjie
public func toJSValue(context: JSContext): JSValue
```

**Function:** Convert Utf16String object to JSValue.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](#class-jsvalue) | ArkTS unified type. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |
| 4 | Thread mismatch. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToJSValue(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello from Utf16String")

    // Convert to JSValue
    let jsValue = utf16Str.toJSValue(context)

    Hilog.info(0, "test", "Converted to JSValue")

    return jsValue
}
```

### func toString()

```cangjie
public func toString(): String
```

**Function:** Convert to String.

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Converted String object. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func convertToString(context: JSContext): JSValue {
    let utf16Str = Utf16String("Hello Utf16String")
    let stringResult = utf16Str.toString()

    Hilog.info(0, "test", "Converted to string: ${stringResult}")

    return context.string(stringResult).toJSValue()
}
```

### operator func !=(Utf16String)

```cangjie
public operator func !=(target: Utf16String): Bool
```

**Function:** Check if strings are not equal.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| target | [Utf16String](#class-utf16string) | Yes | - | Target string for comparison. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if strings are not equal, otherwise false. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |

### operator func +(Utf16String)

```cangjie
public operator func +(right: Utf16String): Utf16String
```

**Function:** Concatenate strings.

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| right | [Utf16String](#class-utf16string) | Yes | - | Target string to concatenate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Utf16String](#class-utf16string) | Concatenated string. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 3 | Accessing reference is beyond reach. |

### operator func \<(Utf16String)

```cangjie
public operator func <(target: Utf16String): Bool
```

**Function:** Determines whether the string is less than the target string (based on Unicode lexicographical order).

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| target | [Utf16String](#class-utf16string) | Yes | - | The target string for comparison. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if less than the target string, otherwise `false`. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

### operator func <(Utf16String)

```cangjie
public operator func <(target: Utf16String): Bool
```

**Function:** Determines whether the string is less than or equal to the target string (based on Unicode lexicographical order).

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| target | [Utf16String](#class-utf16string) | Yes | - | The target string for comparison. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if less than or equal to the target string, otherwise `false`. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

### operator func ==(Utf16String)

```cangjie
public operator func ==(target: Utf16String): Bool
```

**Function:** Determines whether the string is equal to the target string.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| target | [Utf16String](#class-utf16string) | Yes | - | The target string for comparison. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the strings are equal, otherwise `false`. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

### operator func >(Utf16String)

```cangjie
public operator func >(target: Utf16String): Bool
```

**Function:** Determines whether the string is greater than the target string (based on Unicode lexicographical order).

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| target | [Utf16String](#class-utf16string) | Yes | - | The target string for comparison. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if greater than the target string, otherwise `false`. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

### operator func >=(Utf16String)

```cangjie
public operator func >=(target: Utf16String): Bool
```

**Function:** Determines whether the string is greater than or equal to the target string (based on Unicode lexicographical order).

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| target | [Utf16String](#class-utf16string) | Yes | - | The target string for comparison. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if greater than or equal to the target string, otherwise `false`. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300003   | Accessing reference is beyond reach. |

### operator func \[](Int64)

```cangjie
public operator func [](index: Int64): UInt16
```

**Function:** Retrieves a character based on the element index.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | The subscript index. |

**Return Value:**

| Type | Description |
|:-------|:----|
| UInt16 | The retrieved character. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300001   | The accessing index is out of range. |
| 34300003   | Accessing reference is beyond reach. |

### operator func \[](Range\\<Int64>)

```cangjie
public operator func [](range: Range<Int64>): Utf16String
```

**Function:** Extracts a substring from the string.

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| range | Range\<Int64> | Yes | - | The range for extraction. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Utf16String](#class-utf16string) | The extracted Utf16String substring. |

**Exceptions:**

- BusinessException: Error codes as follows，see[Interoperation Error Codes](./cj-errorcode-ark_interop.md)

| Error Code ID | Error Message |
|:------|:-------------------------------------|
| 34300001   | The accessing index is out of range. |
| 34300003   | Accessing reference is beyond reach. |

## struct JSType

```cangjie
public struct JSType {
    public static let UNDEFINED: JSType = JSType(0)
    public static let NULL: JSType = JSType(1)
    public static let NUMBER: JSType = JSType(2)
    public static let BOOLEAN: JSType = JSType(3)
    public static let BIGINT: JSType = JSType(4)
    public static let STRING: JSType = JSType(5)
    public static let SYMBOL: JSType = JSType(6)
    public static let OBJECT: JSType = JSType(7)
    public static let FUNCTION: JSType = JSType(8)
    public static let EXTERNAL: JSType = JSType(9)
}
```

**Function:** Enumeration of ArkTS data types.

In ArkTS, the `typeof` operator can enumerate the general type of data. JSType lists these types and includes the EXTERNAL type.

**Initial Version:** 22

**Example:**

<!--compile-->
```cangjie
import ohos.hilog.Hilog

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get the first argument
    let firstArg = callInfo[0]
    // Get the argument type
    let typeInfo = firstArg.typeof()
    // Check the argument type
    if (typeInfo == JSType.STRING) {
        Hilog.info(0, "test", "input is string: ${firstArg.toString()}")
    } else {
        // Get the type name
        let typeName = typeInfo.toString()
        Hilog.info(0, "test", "input is unexpected type: ${typeName}")
    }
    return context.undefined().toJSValue()
}
```

### static let BIGINT

```cangjie
public static let BIGINT: JSType = JSType(4)
```

**Function:** bigint type.

**Initial Version:** 22

**Type:** [JSType](#struct-jstype)

### static let BOOLEAN

```cangjie
public static let BOOLEAN: JSType = JSType(3)
```

**Function:** bool type.

**Initial Version:** 22

**Type:** [JSType](#struct-jstype)

### static let EXTERNAL

```cangjie
public static let EXTERNAL: JSType = JSType(9)
```

**Function:** external type.

**Initial Version:** 22

**Type:** [JSType](#struct-jstype)

### static let FUNCTION

```cangjie
public static let FUNCTION: JSType = JSType(8)
```

**Function:** function type.

**Initial Version:** 22

**Type:** [JSType](#struct-jstype)

### static let NULL

```cangjie
public static let NULL: JSType = JSType(1)
```

**Function:** null type.

**Initial Version:** 22

**Type:** [JSType](#struct-jstype)

### static let NUMBER

```cangjie
public static let NUMBER: JSType = JSType(2)
```

**Function:** number type.

**Initial Version:** 22

**Type:** [JSType](#struct-jstype)

### static let OBJECT

```cangjie
public static let OBJECT: JSType = JSType(7)
```

**Function:** object type.

**Initial Version:** 22

**Type:** [JSType](#struct-jstype)

### static let STRING

```cangjie
public static let STRING: JSType = JSType(5)
```

**Function:** string type.

**Initial Version:** 22

**Type:** [JSType](#struct-jstype)

### static let SYMBOL

```cangjie
public static let SYMBOL: JSType = JSType(6)
```

**Function:** symbol type.

**Initial Version:** 22

**Type:** [JSType](#struct-jstype)

### static let UNDEFINED

```cangjie
public static let UNDEFINED: JSType = JSType(0)
```

**Function:** undefined type.

**Initial Version:** 22

**Type:** [JSType](#struct-jstype)

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string description of JSType.

**Initial Version:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|String description.|

### operator func !=(JSType)

```cangjie
public operator func !=(target: JSType): Bool
```

**Function:** Performs inequality comparison between two JSTypes.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|target|[JSType](#struct-jstype)|Yes|-|Target type for comparison.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the types are not equal.|

### operator func ==(JSType)

```cangjie
public operator func ==(target: JSType): Bool
```

**Function:** Performs equality comparison between two JSTypes.

**Initial Version:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|target|[JSType](#struct-jstype)|Yes|-|Target type for comparison.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the types are equal.|

## type FuncRegister

```cangjie
public type FuncRegister =(JSContext) -> JSFunction
```

**Function:** FuncRegister is a type alias for ([JSContext](#class-jscontext)) -> [JSFunction](#class-jsfunction).

## type JSBufferFinalizer

```cangjie
public type JSBufferFinalizer =(CPointer<Byte>) -> Unit
```

**Function:** JSBufferFinalizer is a type alias for (CPointer\<Byte>) -> Unit.

## type JSLambda

```cangjie
public type JSLambda =(JSContext, JSCallInfo) -> JSValue
```

**Function:** JSLambda is a type alias for ([JSContext](#class-jscontext), [JSCallInfo](#class-jscallinfo)) -> [JSValue](#class-jsvalue).

## type ModuleRegister

```cangjie
public type ModuleRegister =(JSContext, JSObject) -> Unit
```

**Function:** ModuleRegister is a type alias for ([JSContext](#class-jscontext), [JSObject](#class-jsobject)) -> Unit.

## type napi_env

```cangjie
public type napi_env = CPointer<Unit>
```

**Function:** napi_env is a type alias for CPointer\<Unit>.

## type napi_value

```cangjie
public type napi_value = CPointer<Unit>
```

**Function:** napi_value is a type alias for CPointer\<Unit>.
