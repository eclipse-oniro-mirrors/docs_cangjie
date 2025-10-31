# Using Interoperability Code in ArkTS

This chapter describes three methods for using interoperability code in ArkTS:

- Loading Cangjie modules via `import` syntax: Supported from API version 18.
- Loading Cangjie modules via the `loadNativeModule` interface: Supported from API version 18.

## Method 1: Loading Cangjie Modules via `import` Syntax

> **Note:**
>
> - This loading method is supported from API version 18. Minimum compatible version: OpenHarmony 5.1.0(18).
> - The method for loading Cangjie modules via `import` syntax is consistent with loading native modules via `import`. For details, refer to: [Statically Loading Native Modules](https://docs.openharmony.cn/pages/v5.1/zh-cn/application-dev/arkts-utils/arkts-import-native-module.md).

Below is an example of loading the Cangjie module `ohos_app_cangjie_entry` via `import` syntax and calling the `addNumber` interface:

1. Create a Cangjie module in the ArkTS project. For details, refer to [Adding a Cangjie Module to an ArkTS Project](./add_cangjie_module.md).

2. Implementation of the interoperability interface on the Cangjie side:

    - Implement the interoperability interface `addNumber`:

        ```cangjie
        // entry/src/main/cangjie/index.cj

        // Define the package name, which must match the package name in cjpm.toml
        package ohos_app_cangjie_entry

        // Import the interoperability library
        import ohos.ark_interop.*

        // Define the interoperability function. The parameter type must be (JSContext, JSCallInfo), and the return type must be JSValue.
        func addNumber(context: JSContext, callInfo: JSCallInfo): JSValue {
            // Get the argument list from JSCallInfo
            let arg0: JSValue = callInfo[0]
            let arg1: JSValue = callInfo[1]

            // Convert JSValue to Cangjie types
            let a: Float64 = arg0.toNumber()
            let b: Float64 = arg1.toNumber()

            // Actual Cangjie function behavior
            let value = a + b

            // Convert the result to JSValue
            let result: JSValue = context.number(value).toJSValue()

            // Return JSValue
            return result
        }
        // The function must be registered to JSModule
        let EXPORT_MODULE = JSModule.registerModule {
            runtime, exports =>
                exports["addNumber"] = runtime.function(addNumber).toJSValue()
        }
        ```

    - Provide the interface declaration for the ArkTS side in the `Index.d.ts` file under the `types->libohos_app_cangjie_entry` folder:

        ```typescript
        // entry/src/main/cangjie/types/libohos_app_cangjie_entry/Index.d.ts
        export declare function addNumber(a: number, b: number): number;
        ```

    - Associate `Index.d.ts` with the corresponding `.so` library of the Cangjie module in the `oh-package.json5` file under the `types->libohos_app_cangjie_entry` folder:

        > **Note:**
        >
        > The following code does not need to be copied, as it is already configured in the project after creating the Cangjie module.

        ```json
        // entry/src/main/cangjie/types/libohos_app_cangjie_entry/oh-package.json5
        {
            "name": "libohos_app_cangjie_entry.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. Configure the dependency on the `.so` library corresponding to the Cangjie module in the `dependencies` field of the `oh-package.json5` file in the ArkTS module:

    > **Note:**
    >
    > The following code does not need to be copied, as it is already configured in the project after creating the Cangjie module.

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

4. Use `import` syntax in ArkTS to directly import the Cangjie module and call the `addNumber` interface:

    ```typescript
    // Import the Cangjie dynamic library. The library name must match the package name of the interoperability interface.
    import { addNumber } from "libohos_app_cangjie_entry.so";
    
    // Call the Cangjie interface
    let result = addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```

## Method 2: Loading Cangjie Modules via the `loadNativeModule` Interface

> **Note:**
>
> - This loading method is supported from API version 18. Minimum compatible version: OpenHarmony 5.1.0(18).
> - For detailed information about the `loadNativeModule` interface, refer to: [Dynamically Loading Native Modules in Synchronous Mode](https://docs.openharmony.cn/pages/v5.1/zh-cn/application-dev/arkts-utils/js-apis-load-native-module.md).

Below is an example of loading the Cangjie module `ohos_app_cangjie_entry` via the `loadNativeModule` interface and calling the `addNumber` function:

1. Create a Cangjie module in the ArkTS project. For details, refer to [Adding a Cangjie Module to an ArkTS Project](./add_cangjie_module.md).

2. Implementation of the interoperability interface on the Cangjie side:

    - Implement the interoperability interface `addNumber`:

        ```cangjie
        // entry/src/main/cangjie/index.cj

        // Define the package name, which must match the package name in cjpm.toml
        package ohos_app_cangjie_entry

        // Import the interoperability library
        import ohos.ark_interop.*

        // Define the interoperability function. The parameter type must be (JSContext, JSCallInfo), and the return type must be JSValue.
        func addNumber(context: JSContext, callInfo: JSCallInfo): JSValue {
            // Get the argument list from JSCallInfo
            let arg0: JSValue = callInfo[0]
            let arg1: JSValue = callInfo[1]

            // Convert JSValue to Cangjie types
            let a: Float64 = arg0.toNumber()
            let b: Float64 = arg1.toNumber()

            // Actual Cangjie function behavior
            let value = a + b

            // Convert the result to JSValue
            let result: JSValue = context.number(value).toJSValue()

            // Return JSValue
            return result
        }
        // The function must be registered to JSModule
        let EXPORT_MODULE = JSModule.registerModule {
            runtime, exports =>
                exports["addNumber"] = runtime.function(addNumber).toJSValue()
        }
        ```

    - Provide the interface declaration for the ArkTS side in the `Index.d.ts` file under the `types->libohos_app_cangjie_entry` folder:

        ```typescript
        // entry/src/main/cangjie/types/libohos_app_cangjie_entry/Index.d.ts
        export declare function addNumber(a: number, b: number): number;
        ```

    - Associate `Index.d.ts` with the corresponding `.so` library of the Cangjie module in the `oh-package.json5` file under the `types->libohos_app_cangjie_entry` folder:

        > **Note:**
        >
        > The following code does not need to be copied, as it is already configured in the project after creating the Cangjie module.

        ```json
        // entry/src/main/cangjie/types/libohos_app_cangjie_entry/oh-package.json5
        {
            "name": "libohos_app_cangjie_entry.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. Configure the dependency on the `.so` library corresponding to the Cangjie module in the `dependencies` field of the `oh-package.json5` file in the ArkTS module:

    > **Note:**
    >
    > The following code does not need to be copied, as it is already configured in the project after creating the Cangjie module.

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

4. Use `loadNativeModule` in ArkTS to load `libohos_app_cangjie_entry.so` and call the `addNumber` interface:

    ```typescript
    // Load the Cangjie dynamic library using the loadNativeModule interface
    let module: ESObject = loadNativeModule("libohos_app_cangjie_entry.so");
    
    // Call the Cangjie interface
    let result: number = module.addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```