# ohos.ark_interop_macro（ArkTS互操作宏）

提供仓颉语言与 ArkTS 语言的互操作宏。

## @Interop 宏

```cangjie
public macro Interop(attrTokens: Tokens, input: Tokens): Tokens
```

**功能：** 自动生成 ArkTS 声明文件及互操作层代码，详见[仓颉-ArkTS 声明式互操作宏](../../learn-cj/FFI/cangjie-arkts/interoperability_macro.md)。

**示例：**

<!--compile-->
```cangjie
@Interop[ArkTS]
public class MyCustomClass {
    public let name: String   // String 实现了 JSInteropType<String>，可以用在这里。
    public let age: Int64     // Int64 实现了 JSInteropType<Int64>，可以用在这里。

    public init(name: String, age: Int64) {
        this.name = name
        this.age = age
    }
}
```
