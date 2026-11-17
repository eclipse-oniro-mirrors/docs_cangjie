# 在仓颉代码里导入ArkTS模块

## 场景介绍

ArkTS互操作库里的 `JSContext.requireArkModule` 接口可以加载ArkTS模块，当模块被加载后，可以通过互操作接口来访问导出的变量和调用导出的接口。

## 完整使用示例

下面以仓颉侧加载系统模块 `@ohos.hilog` 并调用其 `info` 接口为例，介绍从工程创建到运行验证的完整流程。

1. 参照[构建第一个仓颉与ArkTS混合应用](./cj-quick-start-first-cangjie-hybrid-app.md)创建一个仓颉与ArkTS混合工程，或参照[在已有ArkTS工程中增量使用仓颉](./cj-quick-start-first-cangjie-hybrid-module.md)在已有ArkTS工程中使能仓颉。以 `entry` 混合模块为例，与本示例相关的工程目录结构如下：

   ```text
   entry
   ├── src
   │    └── main
   │         ├── cangjie
   │         │    ├── types
   │         │    │    └── libohos_app_cangjie_entry
   │         │    │         ├── Index.d.ts
   │         │    │         └── oh-package.json5
   │         │    └── index.cj
   │         ├── ets
   │         │    ├── entryability
   │         │    │    └── EntryAbility.ets
   │         │    └── pages
   │         │         └── Index.ets
   │         ├── resources
   │         └── module.json5
   ├── build-profile.json5
   ├── cjpm.toml
   ├── hvigorfile.ts
   └── oh-package.json5
   ```

2. 在仓颉侧编写互操作代码。打开 `entry > src > main > cangjie > index.cj`，注册一个供ArkTS调用的函数，并在该函数中通过 `requireArkModule` 加载系统模块 `@ohos.hilog`，示例如下：

   <!-- compile -->
   ```cangjie
   // index.cj
   package ohos_app_cangjie_entry

   // 导入互操作库
   import kit.CangjieKit.*

   // 互操作函数：加载系统模块@ohos.hilog并调用其info接口
   func loadHilogModule(context: JSContext, callInfo: JSCallInfo): JSValue {
       // 1. 使用requireArkModule导入系统模块"@ohos.hilog"
       let module = context.requireArkModule("@ohos.hilog")
       // 2. 把导入的模块转换为JSObject
       let hilog = module.asObject()
       // 3. 调用模块的info方法，打印一条日志
       hilog.callMethod(
           "info",
           [
               context.number(0).toJSValue(),
               context.string("test").toJSValue(),
               context.string("load hilog success").toJSValue()
           ]
       )
       // 4. 返回执行结果
       return context.boolean(true).toJSValue()
   }

   // 在模块导出时，将loadHilogModule注册为可被ArkTS调用的函数
   let EXPORT_MODULE = JSModule.registerModule {
       runtime, exports => exports["loadHilogModule"] = runtime.function(loadHilogModule).toJSValue()
   }
   ```

3. 在 `entry > src > main > cangjie > types > libohos_app_cangjie_entry > Index.d.ts` 文件中，补充上述注册函数的接口声明：

   ```typescript
   // Index.d.ts
   export declare function loadHilogModule(): boolean
   ```

4. 在ArkTS侧调用仓颉函数。打开 `entry > src > main > ets > pages > Index.ets`，导入并调用 `loadHilogModule`，示例如下：

   ```typescript
   // Index.ets
   // 导入仓颉动态库，该动态库名称为仓颉包名的名称，该名称需要和互操作接口所在的包名一致
   import { loadHilogModule } from 'libohos_app_cangjie_entry.so'

   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World'

     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           // 添加按钮，触发调用
           Button('调用 loadHilogModule')
             .width('80%')
             .height(40)
             .margin(20)
             .onClick(() => {
               // 调用仓颉函数，仓颉内部通过requireArkModule加载@ohos.hilog并打印日志
               let ret = loadHilogModule()
               this.message = `loadHilogModule: ${ret}`
             })
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

5. 使用真机或模拟器运行应用（具体步骤请参见[构建第一个仓颉与ArkTS混合应用](./cj-quick-start-first-cangjie-hybrid-app.md#使用真机或模拟器运行应用)）。单击页面上的**调用 loadHilogModule**按钮后，页面文本更新为"loadHilogModule: true"，并在日志窗口（HiLog，过滤关键字"test"）中可以看到"load hilog success"日志，说明仓颉侧成功加载并调用了ArkTS系统模块。

## 模块方法列表的查询方式

在通过 `requireArkModule` 加载模块后，可以调用模块导出的接口和读取导出的变量。各模块支持的方法列表可通过以下方式查询：

- **系统模块**（@ohos.\*）：系统模块的接口列表可查阅仓颉API参考中对应Kit的接口文档，例如 `@ohos.hilog` 的接口说明（含 `info`、`debug`、`warn`、`error` 等方法）可参见[Hilog接口参考](../../../reference/PerformanceAnalysisKit/cj-apis-hilog.md)；仓颉API参考的总目录参见[仓颉API参考](../../../reference/README_zh.md)。
- **工程内模块**（hap/har/hsp里的文件）：可查阅模块源码或其对应的.d.ts声明文件，其中声明了该模块导出的全部函数、变量及其参数类型。

## 通用调用流程

无论加载哪种模块，调用其导出接口都遵循"加载模块 → 转换为JSObject → 调用方法或读写变量"三步，通用模板如下：

<!-- compile -->
```cangjie
// 1. 使用requireArkModule加载模块，path取值参见“支持场景”章节
let module = context.requireArkModule("模块路径")
// 2. 把导入的模块转换为JSObject
let obj = module.asObject()
// 3. 调用模块的某个方法或读写模块导出的变量，callMethod 的第一个参数为方法名，第二个参数为参数列表
let result = obj.callMethod("方法名", [参数列表])
let value = obj["变量名"].toNumber()
```

## 调用异步方法

若被调用的ArkTS方法为异步方法（返回Promise），其返回值可以通过`asPromise()`转换为JSPromise，再通过`then`/`catchError`注册结果与异常回调。以下示例演示了通用的异步方法调用写法：

<!-- compile -->
```cangjie
func callAsyncMethod(context: JSContext, callInfo: JSCallInfo): JSValue {
    // 1. 加载模块并转换为JSObject
    let module = context.requireArkModule("模块路径")
    let obj = module.asObject()
    // 2. 调用返回Promise的异步方法
    let result = obj.callMethod("异步方法名", [参数列表])
    // 3. 把返回值转换为JSPromise
    let promise = result.asPromise()
    // 4. 注册结果处理回调，回调的callInfo[0]即Promise的执行结果
    let onFulfilled: JSLambda = {context, callInfo =>
        let value = callInfo[0].toNumber()
        Hilog.info(0, "test", "async result: ${value}")
        context.undefined().toJSValue()
    }
    promise.then(context.function(onFulfilled))
    // 5. 如需处理异步调用失败，可通过then的命名参数onRejected或catchError注册异常回调
    return context.undefined().toJSValue()
}
```

> **说明：**
>
> JSLambda的函数签名为`(JSContext, JSCallInfo) -> JSValue`，需要通过`context.function()`包装为JSFunction后才能传给ArkTS侧。JSPromise的更多接口说明请参见互操作库API参考中的[JSPromise](../../../reference/arkinterop/cj-apis-ark_interop.md#class-jspromise)。

## 函数说明

```cangjie
public func requireArkModule(path: String): JSValue
```

## 使用限制

* 只能在ArkTS绑定线程使用该接口
* 禁止在全局变量初始化过程和模块导出流程中使用该接口
* 对于部分系统模块（如：`ohos.router`）只在主运行时上提供，在worker线程导入将产生错误

> **注意：**
>
> 当前在spawn(UIThread)或context.postJSTask的回调里直接调用该接口将失败，该限制计划在后续的版本里移除。

## 支持场景

| 场景        | path 格式                                             | 说明                                         |
|:----------|:----------------------------------------------------|:-------------------------------------------|
| 系统模块      | @ohos.\*，@system.\*，@hms.\*和@kit.\*，如："@ohos.hilog" | /                                          |
| hap模块里的文件 | 模块名/模块下路径，如："entry/src/main/ets/Index"              | 支持.ets、.ts和.js格式的文件。path不带后缀（适用于所有场景）      |
| har模块里的文件 | 模块名/模块下路径，如："myhar/src/main/ets/Index"              | 支持（本地 \| 远程 \| ohpm）（源码 \| 二进制）har（需要额外配置） |
| hsp模块里的文件 | 模块名/模块下路径，如："@ohos/lottie/src/main/js/main"         | 支持（远程 \| ohpm）hsp                          |
| native模块  | lib模块名.so，如："libentry.so"                           | 支持（har\|本地hsp\|hap）里带的（NAPI\|仓颉）模块         |

### 加载系统模块

<!-- compile -->
```cangjie
func loadModule(context: JSContext): Unit {
    // 1. 使用requireArkModule导入模块"@ohos.hilog"
    let module = context.requireArkModule("@ohos.hilog")
    // 2. 把导入的模块转换为JSObject
    let hilog = module.asObject()
    // 3. 调用对象的info方法
    hilog.callMethod(
        "info",
        [
            context.number(0).toJSValue(),
            context.string("test").toJSValue(),
            context.string("load hilog success").toJSValue()
        ]
    )
}
```

> **注意：**
>
> 部分系统模块底层为 NAPI 实现（如：`@ohos.file.photoAccessHelper`），此类模块应使用 `requireSystemNativeModule` 按注册名导入，具体请参见[仓颉侧调用 ArkTS 模块](./cj-using_arkts_module.md)。

### 加载hap模块里的文件

当加载hap里的文件时，如以下ArkTS代码：

```typescript
// entry/src/main/ets/Test.ets
export function test() {
    console.log("call hap file")
}
export let value = 123
```

1. 需要在模块的build-profile.json5里进行以下配置

    ```json5
    {
      "buildOption": {
        "arkOptions": {
          "runtimeOnly": {
            "sources": [
              "./src/main/ets/Test.ets"
            ]
          }
        }
      }
    }
    ```

2. 导入Test.ets文件和调用导出的接口

    <!-- compile -->
    ```cangjie
    import kit.PerformanceAnalysisKit.Hilog

    func loadModule(context: JSContext): Unit {
        // 1. 使用requireArkModule导入模块
        let module = context.requireArkModule("entry/src/main/ets/Test")
        // 2. 把导入内容转换为JSObject
        let test = module.asObject()
        // 3. 读取导出的value变量
        let value = test["value"].toNumber()
        Hilog.info(0, "test", "value is ${value}")
        // 4. 写value变量
        test["value"] = context.number(2).toJSValue()
        // 5. 调用导出的test方法
        test.callMethod("test")
    }
    ```

### 加载har模块里的文件

1. 模块依赖配置

    ```json5
    // 模块下的 oh-package.json5
    {
      "name": "entry",
      "version": "1.0.0",
      "dependencies": {
        "localhar": "file:../localhar",                 // 本地har，在同一个工程下，用相对路径指向模块根目录
        "remotehar": "file:../prebuilts/remotehar.har", // 远程har，预编译为har（不区分源码har和二进制har），用路径指向har文件
        "@ohos/lottie": "^2.0.0"                        // ohpm har，已发布到ohpm的har，指定版本即可
      },
    }
    ```

2. 在模块的build-profile.json5里进行以下配置

    ```json5
    {
      "buildOption": {
        "arkOptions": {
          "runtimeOnly": {
            "packages": [
              "localhar",
              "remotehar",
              "@ohos/lottie"
            ]
          }
        }
      }
    }
    ```

3. 导入和调用导出的接口

    <!-- compile -->
    ```cangjie
    import kit.PerformanceAnalysisKit.Hilog

    func loadModule(context: JSContext): Unit {
        // 1. 使用requireArkModule导入模块
        let module1 = context.requireArkModule("localhar/src/main/ets/Test") // 导入本地har里的文件
        let module2 = context.requireArkModule("remotehar/src/main/ets/Test") // 导入远程har里的文件
        let module3 = context.requireArkModule("@ohos/lottie/src/main/js/main") // 导入ohpm har里的文件

        // 2. 把导入内容转换为JSObject
        let test = module1.asObject()
        // 3. 读取导出的value变量
        let value = test["value"].toNumber()
        Hilog.info(0, "test", "value is ${value}")
        // 4. 写value变量
        test["value"] = context.number(2).toJSValue()
        // 5. 调用导出的test方法
        test.callMethod("test")
    }
    ```

> **注意：**
>
> 在ArkTS静态导入里存在整包导入的机制，例如：`import * as localhar from "localhar"`。
> 这种导入机制本质上仍然是导入一个文件，在每个(har | hsp)模块的oh-package.json里有一个字段main，
> 该字段指向一个源码文件，整包导入时实际上就是导入该文件。
> 例如localhar的oh-package.json配置为`main: "Index.ets"`，那么用该接口应该这样导入：`context.importArkModule("localhar/Index")`

### 加载hsp模块里的文件

build-profile.json5无需配置，导入和调用方式如下：

<!-- compile -->
```cangjie
import kit.PerformanceAnalysisKit.Hilog

func loadModule(context: JSContext): Unit {
    // 1. 使用requireArkModule导入模块
    let module = context.requireArkModule("localhsp/src/main/ets/Test") // 导入本地hsp里的文件

    // 2. 把导入内容转换为JSObject
    let test = module.asObject()
    // 3. 读取导出的value变量
    let value = test["value"].toNumber()
    Hilog.info(0, "test", "value is ${value}")
    // 4. 写value变量
    test["value"] = context.number(2).toJSValue()
    // 5. 调用导出的test方法
    test.callMethod("test")
}
```

### 加载native模块

针对hap、har和本地hsp里定义的native（NAPI | 仓颉）模块，都可以通过生成的二进制名称进行加载。

<!-- compile -->
```cangjie
import kit.PerformanceAnalysisKit.Hilog

func loadModule(context: JSContext): Unit {
    // 1. 使用requireArkModule导入模块
    let module = context.requireArkModule("libentry.so") // 导入native模块

    // 2. 把导入内容转换为JSObject
    let test = module.asObject()
    // 3. 读取导出的value变量
    let value = test["value"].toNumber()
    Hilog.info(0, "test", "value is ${value}")
    // 4. 写value变量
    test["value"] = context.number(2).toJSValue()
    // 5. 调用导出的test方法
    test.callMethod("test")
}
```

