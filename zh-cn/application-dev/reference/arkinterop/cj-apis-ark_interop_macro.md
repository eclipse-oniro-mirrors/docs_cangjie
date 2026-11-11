# ohos.ark_interop_macro（ArkTS互操作宏）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

提供仓颉与ArkTS之间的声明式互操作宏，用于自动生成ArkTS声明文件及互操作层代码，简化跨语言调用的开发工作。

## 导入模块

```cangjie
import ohos.ark_interop_macro.*
```

使用本模块的 `@Interop` 宏时，必须直接导入宏包 `ohos.ark_interop_macro`。宏在编译期展开，编译器仅识别直接导入的宏包，不支持通过 Kit 包重新导出后使用。

## @Interop 宏

```cangjie
public macro Interop(attrTokens: Tokens, input: Tokens): Tokens
```

**功能：** 自动生成 ArkTS 声明文件及互操作层代码，详见[仓颉-ArkTS 声明式互操作宏](../../learn-cj/FFI/cangjie-arkts/cj-arkts_interoperability_macro.md)。

**示例：**

<!-- compile -->
```cangjie
import kit.CangjieKit.*
import ohos.ark_interop_macro.*

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
