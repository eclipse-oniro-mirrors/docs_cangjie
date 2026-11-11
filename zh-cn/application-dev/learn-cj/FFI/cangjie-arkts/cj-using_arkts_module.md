# 仓颉侧调用 ArkTS 模块

以调用 ArkTS 侧的系统 NAPI 模块 `@ohos.file.photoAccessHelper`（相册管理模块）为例，介绍仓颉侧从导入模块到调用接口的完整流程。

> **说明：**
>
> 部分常用系统模块已提供仓颉原生 API（例如相册管理模块的仓颉 API 可参见 [ohos.file.photoAccessHelper](../../../reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md)）。若目标模块已有仓颉原生 API，建议优先直接使用仓颉原生 API；本章节介绍的互操作导入方式，适用于暂无仓颉原生 API 的 ArkTS 模块。

## 导入系统 NAPI 模块：requireSystemNativeModule 与 requireArkModule 的区别

两者都用于在仓颉侧加载 ArkTS 模块，区别在于入参与适用范围：

| 接口 | 适用范围 |
|:---|:---|
| [requireArkModule(path)](./cangjie-load-arkts.md#支持场景) | 加载系统 ArkTS 模块（@ohos.\*、@system.\*、@hms.\*、@kit.\*）、工程内 hap/har/hsp 模块文件、native 模块（lib\*.so）。 |
| [requireSystemNativeModule(moduleName)](../../../reference/arkinterop/cj-apis-ark_interop.md) | 专门用于加载系统内置的 ArkTS NAPI 模块，入参为 NAPI 模块的注册名称，如 "file.photoAccessHelper"、"hilog"。 |

> **注意：**
>
> 部分 ArkTS 系统模块底层为 NAPI 实现（如 `@ohos.file.photoAccessHelper`），若通过 `requireArkModule` 导入，应用可能在运行时崩溃。此类模块应使用 `requireSystemNativeModule` 按注册名导入。

`requireSystemNativeModule` 的模块注册名与 ArkTS 模块名的映射规范（如 `@ohos.file.photoAccessHelper` 对应 "file.photoAccessHelper"），请参见 [ArkTS 侧获取互操作模块名](./cj-prepare_arkts_module.md)。

## 完整使用示例

`photoAccessHelper` 模块的 `getPhotoAccessHelper` 接口需要传入 `context` 入参，`context` 需由 ArkTS 侧传入仓颉侧使用，完整链路如下：

1. 参照[仓颉-ArkTS 互操作辅助库](./cj-arkts_auxiliary_lib.md)完整使用示例中的步骤 1 至步骤 4，在仓颉与ArkTS混合工程中把 ArkTS 侧的 context 传给仓颉侧保存（仓颉侧保存 context 的全局变量为 `globalContextObject`）。

2. 在仓颉代码中导入模块并调用其接口（以互操作函数的形式编写，由 ArkTS 侧触发调用）：

   <!-- compile -->
   ```cangjie
   // 导入互操作库
   import kit.CangjieKit.*

   func usePhotoAccessHelper(context: JSContext, callInfo: JSCallInfo): JSValue {
       // 1. 导入系统 NAPI 模块：模块注册名为 ArkTS 模块名去掉前缀 "@ohos."
       let module = context.requireSystemNativeModule("file.photoAccessHelper")
       // 2. 把导入的模块转换为 JSObject
       let obj = module.asObject()
       // 3. 使用 ArkTS 侧传入并保存的 context 作为入参
       let ctxValue = globalContextObject.getOrThrow().toJSValue()
       // 4. 调用模块的 getPhotoAccessHelper 方法，返回值即 PhotoAccessHelper 实例
       let helper = obj.callMethod("getPhotoAccessHelper", [ctxValue])
       // 5. 后续通过 callMethod 继续调用该实例的方法（如 getAssets 等），
       //    操作返回的 JSValue 的方式参见"仓颉访问 ArkTS 数据"
       return context.undefined().toJSValue()
   }
   ```

3. 调用 photoAccessHelper 的接口前，需确认已申请对应权限。该模块的读接口需要 ohos.permission.READ_IMAGEVIDEO 权限，写接口需要 ohos.permission.WRITE_IMAGEVIDEO 权限（详见[权限列表](../../../reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md#权限列表)）。这两个权限均为受控权限，申请方式请参见[申请受控权限](../../../security/AccessToken/cj-declare-permissions-in-acl.md)。

操作 ArkTS 数据的方法请参考[仓颉访问 ArkTS 数据](./cj-operating_ArkTS_data.md)。若被调用的接口为异步接口（返回 Promise），处理方式请参见[调用异步方法](./cangjie-load-arkts.md#调用异步方法)。

## 将类中的函数注册给 ArkTS 侧

在混合工程中，若需要把包含上述 ArkTS 模块调用的仓颉类函数暴露给 ArkTS 侧调用，需注意：`JSModule.registerFunc` / `registerModule` 只能注册顶层函数或 `JSLambda`，不能直接注册类的成员函数。可根据函数是否依赖实例状态，选择以下两种方式：

- 方式一：不依赖实例状态的函数声明为静态成员函数（函数签名需满足 (JSContext, JSCallInfo) -> JSValue），并在静态初始化器 `static init` 中注册：

  <!-- compile -->
  ```cangjie
  // 导入互操作库
  import kit.CangjieKit.*

  class Data {
      static init() {
          // 注册导出到 ArkTS 的函数
          JSModule.registerFunc("createData", createData)
      }

      // 静态成员函数：签名需满足互操作函数要求
      static func createData(context: JSContext, _: JSCallInfo): JSValue {
          context.number(1.0).toJSValue()
      }
  }
  ```

- 方式二：依赖实例状态的成员函数，通过捕获类实例的 `JSLambda` 包装后注册：

  <!-- compile -->
  ```cangjie
  // 导入互操作库
  import kit.CangjieKit.*

  class Calculator {
      var factor: Float64 = 2.0

      // 实例成员函数：实际的计算逻辑
      public func multiply(a: Float64, b: Float64): Float64 {
          a * b * factor
      }
  }

  // 创建类实例
  let calculator = Calculator()

  // 用捕获实例的 JSLambda 包装类成员函数，再注册给 ArkTS 侧
  let multiplyLambda: JSLambda = { context, callInfo =>
      let a = callInfo[0].toNumber()
      let b = callInfo[1].toNumber()
      // 在 JSLambda 内调用类成员函数
      context.number(calculator.multiply(a, b)).toJSValue()
  }

  let _ = JSModule.registerFunc("multiply", multiplyLambda)
  ```

注册后，ArkTS 侧需在 Index.d.ts 中补充对应的接口声明，并通过具名导入方式调用，具体参见[ArkTS 访问仓颉数据](./operating_cangjie_objects.md)。
