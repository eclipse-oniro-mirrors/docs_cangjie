# ohos.ark_interop_macro (ArkTS Interoperability Macros)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Provides declarative interoperability macros between Cangjie and ArkTS, used to automatically generate ArkTS declaration files and interoperation layer code, simplifying cross-language call development work.

## Import Module

```cangjie
import ohos.ark_interop_macro.*
```

To use the `@Interop` macro of this module, the macro package `ohos.ark_interop_macro` must be imported directly. Macros are expanded at compile time, and the compiler only recognizes directly imported macro packages; importing through a Kit package (re-export) is not supported.

## @Interop macro

```cangjie
public macro Interop(attrTokens: Tokens, input: Tokens): Tokens
```

**Function:** Automatically generates ArkTS declaration files and interop layer code by parsing annotated Cangjie code, see [Cangjie-ArkTS Declarative Interop Macros](../../learn-cj/FFI/cangjie-arkts/interoperability_macro.md).

**Example:**

<!-- compile -->
```cangjie
import ohos.ark_interop_macro.*

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
