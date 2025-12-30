# ohos.ark_interop_macro (ArkTS Interoperability Macros)

Provide macros for interoperability between the Cangjie language and ArkTS language.

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
