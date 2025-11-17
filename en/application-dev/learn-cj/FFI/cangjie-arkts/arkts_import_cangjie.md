# Using Interoperability Code in ArkTS

This chapter introduces two methods for using interoperability code in ArkTS:

- Loading Cangjie modules using the `import` syntax.
- Loading Cangjie modules using the `loadNativeModule` interface.

## Method 1: Loading Cangjie Modules Using the `import` Syntax

### Loading Cangjie Modules Using the `import` Syntax and calling its interface

> **Note:**
>
> The method for loading Cangjie modules using the `import` syntax is consistent with loading native modules via `import`. For detailed information, refer to: [Statically Loading Native Modules](https://docs.openharmony.cn/pages/v6.0/en/application-dev/arkts-utils/arkts-import-native-module.md).

Below is an example of loading the Cangjie module `ohos_app_cangjie_entry` using the `import` syntax and calling the `addNumber` interface:

1. Create a Cangjie module in the ArkTS project. For details, refer to [Adding a Cangjie Module to an ArkTS Project](./add_cangjie_module.md).

2. Implementation of the interoperability interface on the Cangjie side:

    - Implement the interoperability interface `addNumber`:

        <!--compile-->
        ```cangjie
        // entry/src/main/cangjie/index.cj

        // Define the package name, which must match the package name in cjpm.toml
        package ohos_app_cangjie_entry

        // Import the interoperability library
        import ohos.ark_interop.*

        // Define the interoperability function. The parameter type must be (JSContext, JSCallInfo), and the return type must be JSValue
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
        // The function must be registered in JSModule
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
        > The following code does not need to be copied; it is already configured in the project after creating the Cangjie module.

        ```json
        // entry/src/main/cangjie/types/libohos_app_cangjie_entry/oh-package.json5
        {
            "name": "libohos_app_cangjie_entry.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. Configure the dependency on the `.so` library of the Cangjie module in the `dependencies` field of the `oh-package.json5` file in the ArkTS module:

    > **Note:**
    >
    > The following code does not need to be copied; it is already configured in the project after creating the Cangjie module.

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

4. Use the `import` syntax in ArkTS to directly import the Cangjie module and call the `addNumber` interface:

    ```typescript
    // Import the Cangjie dynamic library. The library name must match the package name of the interoperability interface
    import { addNumber } from "libohos_app_cangjie_entry.so";

    // Call the Cangjie interface
    let result = addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```

### Loading Cangjie third-party library Using the `import` Syntax and calling its interface

Below is an example of loading the Cangjie third-party library `libapplication.so` by using `import` syntax and calling the `addNumber` interface:

> **Note：**
>
> Assuming that the Cangjie third-party library `libapplication.so` has already implemented the `addNumber` interface for ArkTS to call.

1. In the ArkTS project, create the directory `libs->arm64-v8a`, and copy the Cangjie third-party library `libapplication.so` into the `libs->arm64-v8a` directory of the ArkTS project.

2. Create interface declaration for the Cangjie third-party library `libapplication.so` on the ArkTS side.

    - Create a new Index.d.ts file in the `types->libapplication` folder to provide interface declarations for ArkTS:

        ```typescript
        // entry/src/main/cangjie/types/libapplication/Index.d.ts
        export declare function addNumber(a: number, b: number): number;
        ```

    - In the `types->libapplication` folder, create a new `oh-package.json5` file to associate `Index.d.ts` with the Cangjie third-party library `libapplication.so`.

        ```json
        // entry/src/main/cangjie/types/libapplication/oh-package.json5
        {
            "name": "libapplication.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. Declare the root directory path of the so library in the `oh-package.json5` file within the ArkTS module.

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

4. On the ArkTS side, use `import` syntax to import the third-party Cangjie library `libapplication.so` and call the Cangjie `addNumber` interface:

    ```typescript
    // Import the Cangjie dynamic library. The library name must match the package name of the interoperability interface
    import { addNumber } from "libapplication.so";

    // Call the Cangjie interface
    let result = addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```

### Loading Cangjie static library module Using the `import` Syntax and calling its interface

1. Create a Cangjie Static Library Module `cangjielib` in the ArkTS project. For details, refer to [Adding a Cangjie Static Library Module](./add_cangjie_module.md).

2. Implementation of the interoperability interface on the Cangjie side:

    - Implement the interoperability interface `addNumber`：

        <!--compile-->
        ```cangjie
        // cangjielib/src/main/cangjie/index.cj

        // package name
        package ohos_app_cangjie_cangjielib

        // Import the interoperability library
        internal import ohos.ark_interop.JSModule
        internal import ohos.ark_interop.JSContext
        internal import ohos.ark_interop.JSCallInfo
        internal import ohos.ark_interop.JSValue

        // Define the interoperability function. The parameter type must be (JSContext, JSCallInfo), and the return type must be JSValue
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
        // The function must be registered in JSModule
        let EXPORT_MODULE = JSModule.registerModule {
            runtime, exports => exports["addNumber"] = runtime.function(addNumber).toJSValue()
        }
        ```

    - Provide the interface declaration for the ArkTS side in the `Index.d.ts` file under the `cangjielib->src->main->cangjie->types->libohos_app_cangjie_cangjielib` folder:

        ```typescript
        // cangjielib/src/main/cangjie/types/libohos_app_cangjie_cangjielib/Index.d.ts
        export declare function addNumber(a: number, b: number): number;
        ```

    - Associate `Index.d.ts` with the corresponding `.so` library of the Cangjie module in the `oh-package.json5` file under the `cangjielib->src->main->cangjie->types->libohos_app_cangjie_cangjielib` folder:

        > **Note：**
        >
        > The following code does not need to be copied; it is already configured in the project after creating the Cangjie module.

        ```json
        // cangjielib/src/main/cangjie/types/libohos_app_cangjie_cangjielib/oh-package.json5
        {
            "name": "libohos_app_cangjie_cangjielib.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. Declare the dependencies on the Cangjie static library module in the `dependencies` field of the `oh-package.json5` file within the ArkTS module:

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

4. On the ArkTS side, use `import` syntax to import the Cangjie module and call the Cangjie `addNumber` interface:

    ```typescript
    // Import the Cangjie dynamic library. The library name must match the package name of the interoperability interface
    import { addNumber } from "libohos_app_cangjie_cangjielib.so";

    // Call the Cangjie interface
    let result = addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```

### Loading the local HAR package by using `import` syntax and calling its interface

> **Note：**
>
> Assuming that there is a local HAR package `cangjielib.har` that contains `libohos_app_cangjie_cangjielib.so`, in which the `addNumber` interface has already been implemented and is available for ArkTS to call.

1. Copy the local HAR package `cangjielib.har` to the libs directory of the ArkTS project.

2. Create interface declaration for the Cangjie library `libohos_app_cangjie_cangjielib.so` on the ArkTS side.

    - Create a new Index.d.ts file in the `types->libohos_app_cangjie_cangjielib` folder to provide interface declarations for ArkTS:

        ```typescript
        // entry/src/main/cangjie/types/libohos_app_cangjie_cangjielib/Index.d.ts
        export declare function addNumber(a: number, b: number): number;
        ```

    - In the `types->libohos_app_cangjie_cangjielib` folder, create a new `oh-package.json5` file to link `Index.d.ts` with the Cangjie library `libohos_app_cangjie_cangjielib.so`

        ```json
        // entry/src/main/cangjie/types/libohos_app_cangjie_cangjielib/oh-package.json5
        {
            "name": "libohos_app_cangjie_cangjielib.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. Declare the path of the HAR package and so in the `oh-package.json5` file within the ArkTS module.

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

4. On the ArkTS side, use the `import` syntax to directly import the third-party Cangjie library `libapplication.so` and call the Cangjie `addNumber` interface:

    ```typescript
    // Import the Cangjie dynamic library. The library name must match the package name of the interoperability interface
    import { addNumber } from "libohos_app_cangjie_cangjielib.so";

    // Call the Cangjie interface
    let result = addNumber(1, 2);
    console.log(`1 + 2 = ${result}`);
    ```

## Method 2: Loading Cangjie Modules Using the `loadNativeModule` Interface

> **Note:**
>
> For detailed information about the `loadNativeModule` interface, refer to: [Dynamically Loading Native Modules in Synchronous Mode](https://docs.openharmony.cn/pages/v6.0/en/application-dev/arkts-utils/js-apis-load-native-module.md)

Below is an example of loading the Cangjie module `ohos_app_cangjie_entry` using the `loadNativeModule` interface and calling the `addNumber` function:

1. Create a Cangjie module in the ArkTS project. For details, refer to [Adding a Cangjie Module to an ArkTS Project](./add_cangjie_module.md).

2. Implementation of the interoperability interface on the Cangjie side:

    - Implement the interoperability interface `addNumber`:

        <!--compile-->
        ```cangjie
        // entry/src/main/cangjie/index.cj

        // Define the package name, which must match the package name in cjpm.toml
        package ohos_app_cangjie_entry

        // Import the interoperability library
        import ohos.ark_interop.*

        // Define the interoperability function. The parameter type must be (JSContext, JSCallInfo), and the return type must be JSValue
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
        // The function must be registered in JSModule
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
        > The following code does not need to be copied; it is already configured in the project after creating the Cangjie module.

        ```json
        // entry/src/main/cangjie/types/libohos_app_cangjie_entry/oh-package.json5
        {
            "name": "libohos_app_cangjie_entry.so",
            "types": "./Index.d.ts",
            "version": "1.0.0",
            "description": ""
        }
        ```

3. Configure the dependency on the `.so` library of the Cangjie module in the `dependencies` field of the `oh-package.json5` file in the ArkTS module:

    > **Note:**
    >
    > The following code does not need to be copied; it is already configured in the project after creating the Cangjie module.

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