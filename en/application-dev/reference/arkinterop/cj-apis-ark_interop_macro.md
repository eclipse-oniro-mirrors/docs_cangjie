# ohos.ark_interop_macro (ArkTS Interoperability Macros)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Provides declarative interoperability macros between Cangjie and ArkTS, used to automatically generate ArkTS declaration files and interoperation layer code, simplifying cross-language call development work.

## Import Module

```cangjie
import kit.CangjieKit.*
```

The interface capabilities of this module (ohos.ark_interop_macro) are encapsulated in CangjieKit and can be used after being imported through `import kit.CangjieKit.*`. For more details about importing Kits, see [Interface Usage Notes](../cj-development-intro.md#interface-usage-notes).

## @Interop macro

```cangjie
public macro Interop(attrTokens: Tokens, input: Tokens): Tokens
```

**Function:** Automatically generates ArkTS declaration files and interop layer code by parsing annotated Cangjie code, see [Cangjie-ArkTS Declarative Interop Macros](../../learn-cj/FFI/cangjie-arkts/interoperability_macro.md).

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
