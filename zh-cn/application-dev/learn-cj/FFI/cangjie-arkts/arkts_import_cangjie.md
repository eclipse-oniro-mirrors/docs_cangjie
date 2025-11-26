# ArkTS 侧使用互操作代码

此章节介绍如何在 ArkTS 中使用互操作代码，有两种方式：

- 使用 import 语法加载仓颉模块使用。
- 使用 loadNativeModule 接口加载仓颉模块使用。

## 方式一：使用 import 语法加载仓颉模块

### 使用 import 语法加载仓颉模块并调用接口

> **说明：**
>
> 使用 import 语法加载仓颉模块的方式和使用 import 语法加载 native 模块方式一致，详细介绍请参见：[静态方式加载 native 模块](https://docs.openharmony.cn/pages/v6.0/zh-cn/application-dev/arkts-utils/arkts-import-native-module.md)。

下面为使用 import 语法加载仓颉 ohos_app_cangjie_entry 模块并调用 addNumber 接口的示例：

1. 在 ArkTS 工程中创建仓颉模块，详情请参见[在 ArkTS 工程中添加仓颉模块](./add_cangjie_module.md)。

2. 仓颉侧互操作接口的实现：

    - 实现互操作接口 addNumber：

        <!--compile-->
        ```cangjie
        // entry/src/main/cangjie/index.cj

        // 定义包名，该包名需要和 cjpm.toml 的 package name 保持一致
        package ohos_app_cangjie_entry

        // 导入互操作库
        import ohos.ark_interop.*

        // 定义互操作函数，该函数参数类型必须为(JSContext,JSCallInfo)，返回值类型必须为JSValue
        func addNumber(context: JSContext, callInfo: JSCallInfo): JSValue {
            // 从JSCallInfo获取参数列表
            let arg0: JSValue = callInfo[0]
            let arg1: JSValue = callInfo[1]

            // 把JSValue转换为仓颉类型
            let a: Float64 = arg0.toNumber()
            let b: Float64 = arg1.toNumber()

            // 实际仓颉函数行为
            let value = a + b

            // 把结果转换为JSValue
            let result: JSValue = context.number(value).toJSValue()

            // 返回 JSValue
            return result
        }
        // 必须注册该函数到JSModule中
        let EXPORT_MODULE = JSModule.registerModule {
            runtime, exports =>
                exports["addNumber"] = runtime.function(addNumber).toJSValue()
        }
        ```

    - 在 types->libohos_app_cangjie_entry 文件夹下的 Index.d.ts 文件中，提供 ArkTS 侧接口声明：

        ```typescript
        // entry/src/main/cangjie/types/libohos_app_cangjie_entry/Index.d.ts
        export declare function addNumber(a: number, b: number): number;
        ```

    - 在 types->libohos_app_cangjie_entry 文件夹下的 oh-package.json5 文件中将 Index.d.ts 与仓颉模块对应的 so 库关联起来：

        > **说明：**
        >
        > 以下代码无须复制，创建仓颉模块以后在工程中已配置好。

        ```json
        // entry/src/main/cangjie/types/libohos_app_cangjie_entry/oh-package.json5
        {
            "name": "libohos_app_cangjie_entry.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. 在 ArkTS 模块内的 oh-package.json5 文件中的 dependencies 字段配置对仓颉模块对应的 so 库的依赖：

    > **说明：**
    >
    > 以下代码无须复制，创建仓颉模块以后在工程中已配置好。

    ```json
    // entry/oh-package.json5
    {
        "dependencies": {
            // ...
            "libohos_app_cangjie_entry.so": "file:./src/main/cangjie/types/libohos_app_cangjie_entry"
            // ...
        }
    }
    ```

4. ArkTS 侧使用 import 语法直接导入仓颉模块，并调用仓颉 addNumber 接口：

    ```typescript
    // 导入仓颉动态库，该动态库名称为仓颉包名的名称，该名称需要和互操作接口所在的包名一致
    import { addNumber } from "libohos_app_cangjie_entry.so";

    // 调用仓颉接口
    let result = addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```

### 使用 import 语法加载仓颉三方库并调用接口

下面为使用 import 语法加载仓颉三方库 libapplication.so 并调用 addNumber 接口的示例：

> **说明：**
>
> 假设仓颉三方库 libapplication.so 已经实现了 addNumber 接口可供 ArkTS 侧调用。

1. 在 ArkTS 工程新建 libs->arm64-v8a 目录，将仓颉三方库 libapplication.so 拷贝到 ArkTS 工程的 libs->arm64-v8a 目录下。

2. 在 ArkTS 侧创建仓颉三方库 libapplication.so 接口声明。

    - 在 types->libapplication 文件夹下新建 Index.d.ts 文件，提供 ArkTS 侧接口声明：

        ```typescript
        // entry/src/main/cangjie/types/libapplication/Index.d.ts
        export declare function addNumber(a: number, b: number): number;
        ```

    - 在 types->libapplication 文件夹下新建 oh-package.json5 文件，将 Index.d.ts 与仓颉三方库 libapplication.so 关联起来：

        ```json
        // entry/src/main/cangjie/types/libapplication/oh-package.json5
        {
            "name": "libapplication.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. 在 ArkTS 模块内的 oh-package.json5 文件中声明 so 库的根目录路径。

    ```json
    // entry/oh-package.json5
    {
        "dependencies": {
            // ...
            "libapplication.so": "file:./src/main/cangjie/types/libapplication"
            // ...
        }
    }
    ```

4. ArkTS 侧使用 import 语法直接导入仓颉三方库 libapplication.so，并调用仓颉 addNumber 接口：

    ```typescript
    // 导入仓颉动态库，该动态库名称为仓颉三方库的名称，该名称需要和互操作接口所在的包名一致
    import { addNumber } from "libapplication.so";

    // 调用仓颉接口
    let result = addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```

### 使用 import 语法加载仓颉静态库模块并调用接口

1. 在 ArkTS 工程中创建仓颉静态库模块 cangjielib，详情请参见[添加仓颉静态库模块](./add_cangjie_module.md)。

2. 仓颉侧互操作接口的实现：

    - 实现互操作接口 addNumber：

        <!--compile-->
        ```cangjie
        // cangjielib/src/main/cangjie/index.cj
        // 包名
        package ohos_app_cangjie_cangjielib

        // 导入文件
        internal import ohos.ark_interop.JSModule
        internal import ohos.ark_interop.JSContext
        internal import ohos.ark_interop.JSCallInfo
        internal import ohos.ark_interop.JSValue

        // 互操作函数
        func addNumber(context: JSContext, callInfo: JSCallInfo): JSValue {
            // 从JSCallInfo获取参数列表
            let arg0: JSValue = callInfo[0]
            let arg1: JSValue = callInfo[1]

            // 把JSValue转换为仓颉类型
            let a: Float64 = arg0.toNumber()
            let b: Float64 = arg1.toNumber()

            // 实际仓颉函数行为
            let value = a + b

            // 把结果转换为JSValue
            let result: JSValue = context.number(value).toJSValue()

            // 返回 JSValue
            return result
        }

        let EXPORT_MODULE = JSModule.registerModule {
            runtime, exports => exports["addNumber"] = runtime.function(addNumber).toJSValue()
        }
        ```

    - 在 cangjielib->src->main->cangjie->types->libohos_app_cangjie_cangjielib 文件夹下的 Index.d.ts 文件中，提供 ArkTS 侧接口声明：

        ```typescript
        // cangjielib/src/main/cangjie/types/libohos_app_cangjie_cangjielib/Index.d.ts
        export declare function addNumber(a: number, b: number): number;
        ```

    - 在 cangjielib->src->main->cangjie->types->libohos_app_cangjie_cangjielib 文件夹下的 oh-package.json5 文件中将 Index.d.ts 与仓颉模块对应的 so 库关联起来：

        > **说明：**
        >
        > 以下代码无须复制，创建仓颉模块以后在工程中已配置好。

        ```json
        // cangjielib/src/main/cangjie/types/libohos_app_cangjie_cangjielib/oh-package.json5
        {
            "name": "libohos_app_cangjie_cangjielib.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. 在 ArkTS 模块内的 oh-package.json5 文件中的 dependencies 字段配置对仓颉静态库模块的依赖：

    ```json
    // entry/oh-package.json5
    {
        "dependencies": {
            // ...
            "cangjielib": "../cangjielib",
            "libohos_app_cangjie_cangjielib.so": "file:../cangjielib/src/main/cangjie/types/ohos_app_cangjie_cangjielib"
            // ...
        }
    }
    ```

4. ArkTS 侧使用 import 语法直接导入仓颉模块，并调用仓颉 addNumber 接口：

    ```typescript
    // 导入仓颉动态库，该动态库名称为仓颉包名的名称，该名称需要和互操作接口所在的包名一致
    import { addNumber } from "libohos_app_cangjie_cangjielib.so";

    // 调用仓颉接口
    let result = addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```

### 使用 import 语法加载本地 HAR 包并调用仓颉接口

> **说明：**
>
> 假设有本地 HAR 包 cangjielib.har 中包含 libohos_app_cangjie_cangjielib.so，在该 so 中已经实现了 addNumber 接口可供 ArkTS 侧调用。

1. 将本地 HAR 包 cangjielib.har 拷贝到 ArkTS 工程的 libs 目录下。

2. 在 ArkTS 侧创建 libohos_app_cangjie_cangjielib.so 接口声明。

    - 在 types->libohos_app_cangjie_cangjielib 文件夹下新建 Index.d.ts 文件，提供 ArkTS 侧接口声明：

        ```typescript
        // entry/src/main/cangjie/types/libohos_app_cangjie_cangjielib/Index.d.ts
        export declare function addNumber(a: number, b: number): number;
        ```

    - 在 types->libohos_app_cangjie_cangjielib 文件夹下新建 oh-package.json5 文件，将 Index.d.ts 与仓颉库 libohos_app_cangjie_cangjielib.so 关联起来：

        ```json
        // entry/src/main/cangjie/types/libohos_app_cangjie_cangjielib/oh-package.json5
        {
            "name": "libohos_app_cangjie_cangjielib.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. 在 ArkTS 模块内的 oh-package.json5 文件中声明 HAR 包和 so 的根目录路径。

    ```json
    // entry/oh-package.json5
    {
        "dependencies": {
            // ...
            "cangjielib": "file:libs/cangjielib.har",
            "libohos_app_cangjie_cangjielib.so": "file:src/main/cangjie/types/ohos_app_cangjie_cangjielib"
            // ...
        }
    }
    ```

4. ArkTS 侧使用 import 语法直接导入仓颉模块，并调用仓颉 addNumber 接口：

    ```typescript
    // 导入仓颉动态库，该动态库名称为仓颉包名的名称，该名称需要和互操作接口所在的包名一致
    import { addNumber } from "libohos_app_cangjie_cangjielib.so";

    // 调用仓颉接口
    let result = addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```

## 方式二：使用 loadNativeModule 接口加载仓颉模块

> **说明：**
>
> loadNativeModule 接口详细介绍请参考：[同步方式动态加载 native 模块](https://docs.openharmony.cn/pages/v6.0/zh-cn/application-dev/arkts-utils/js-apis-load-native-module.md)

下面为使用 loadNativeModule 接口加载仓颉 ohos_app_cangjie_entry 模块并调用 addNumber 函数的示例：

1. 在 ArkTS 工程中创建仓颉模块，详情请参见[在 ArkTS 工程中添加仓颉模块](./add_cangjie_module.md)。

2. 仓颉侧互操作接口的实现：

    - 实现互操作接口 addNumber：

        <!--compile-->
        ```cangjie
        // entry/src/main/cangjie/index.cj

        // 定义包名，该包名需要和 cjpm.toml 的 package name 保持一致
        package ohos_app_cangjie_entry

        // 导入互操作库
        import ohos.ark_interop.*

        // 定义互操作函数，该函数参数类型必须为(JSContext,JSCallInfo)，返回值类型必须为JSValue
        func addNumber(context: JSContext, callInfo: JSCallInfo): JSValue {
            // 从JSCallInfo获取参数列表
            let arg0: JSValue = callInfo[0]
            let arg1: JSValue = callInfo[1]

            // 把JSValue转换为仓颉类型
            let a: Float64 = arg0.toNumber()
            let b: Float64 = arg1.toNumber()

            // 实际仓颉函数行为
            let value = a + b

            // 把结果转换为JSValue
            let result: JSValue = context.number(value).toJSValue()

            // 返回 JSValue
            return result
        }
        // 必须注册该函数到JSModule中
        let EXPORT_MODULE = JSModule.registerModule {
            runtime, exports =>
                exports["addNumber"] = runtime.function(addNumber).toJSValue()
        }
        ```

    - 在 types->libohos_app_cangjie_entry 文件夹下的 Index.d.ts 文件中，提供 ArkTS 侧接口声明：

        ```typescript
        // entry/src/main/cangjie/types/libohos_app_cangjie_entry/Index.d.ts
        export declare function addNumber(a: number, b: number): number;
        ```

    - 在 types->libohos_app_cangjie_entry 文件夹下的 oh-package.json5 文件中将 Index.d.ts 与仓颉模块对应的 so 库关联起来：

        > **说明：**
        >
        > 以下代码无须复制，创建仓颉模块以后在工程中已配置好。

        ```json
        // entry/src/main/cangjie/types/libohos_app_cangjie_entry/oh-package.json5
        {
            "name": "libohos_app_cangjie_entry.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. 在 ArkTS 模块内的 oh-package.json5 文件中的 dependencies 字段配置对仓颉模块对应的 so 库的依赖：

    > **说明：**
    >
    > 以下代码无须复制，创建仓颉模块以后在工程中已配置好。

    ```json
    // entry/oh-package.json5
    {
        "dependencies": {
            // ...
            "libohos_app_cangjie_entry.so": "file:./src/main/cangjie/types/libohos_app_cangjie_entry"
            // ...
        }
    }
    ```

4. ArkTS 侧使用 loadNativeModule 加载 libohos_app_cangjie_entry.so，调用仓颉 addNumber 接口：

    ```typescript
    // 使用 loadNativeModule 接口加载仓颉动态库
    let module: ESObject = loadNativeModule("libohos_app_cangjie_entry.so");

    // 调用仓颉接口
    let result: number = module.addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```
