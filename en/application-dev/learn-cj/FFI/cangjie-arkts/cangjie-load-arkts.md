# Importing ArkTS Modules in Cangjie Code

## Scenario Introduction

The `JSContext.requireArkModule` interface in the ArkTS interop library can load ArkTS modules. Once a module is loaded, exported variables can be accessed and exported interfaces can be invoked through interop interfaces.

## Function Description

```cangjie
public func requireArkModule(path: String): JSValue
```

## Usage Restrictions

* This interface can only be used in the ArkTS-bound thread.
* It is prohibited to use this interface during global variable initialization and module export processes.
* Some system modules (e.g., ohos.router) are only available in the main runtime; importing them in worker threads will result in an error.

> **Note:**
> Currently, directly calling this interface in the callback of `spawn(UIThread)` or `context.postJSTask` will fail. This restriction is planned to be removed in subsequent versions.

## Supported Scenarios

| Scenario                | path Format                                                     | Description                                                                                                   |
|:---------------------- |:-------------------------------------------------------------- |:--------------------------------------------------------------------------------------------------------------|
| System Modules          | @ohos.\*, @system.\*, @hms.\* and @kit.\*, e.g.: "@ohos.hilog"   | /                                                                                                             |
| Files in HAP Modules    | Module name/path under the module, e.g.: "entry/src/main/ets/Index" | Supports files in .ets, .ts and .js formats. The path does not include a suffix (applicable to all scenarios). |
| Files in HAR Modules    | Module name/path under the module, e.g.: "myhar/src/main/ets/Index" | Supports (local \| remote \| ohpm) (source code \| binary) HAR (additional configuration required).           |
| Files in HSP Modules    | Module name/path under the module, e.g.: "@ohos/lottie/src/main/js/main" | Supports (remote \| ohpm) HSP.                                                                                |
| Native Modules          | lib\<module name>.so, e.g.: "libentry.so"                        | Supports (napi \| Cangjie) modules included in (HAR \| local HSP \| HAP).                                     |

### Loading System Modules

<!-- compile -->
```cangjie
func loadModule(context: JSContext): Unit {
    // 1. Import the module "@ohos.hilog" using requireArkModule
    let module = context.requireArkModule("@ohos.hilog")
    // 2. Convert the imported module to JSObject
    let hilog = module.asObject()
    // 3. Call the info method of the object
    hilog.callMethod("info", [
        context.number(0).toJSValue(),
        context.string("test").toJSValue(),
        context.string("load hilog success").toJSValue()
    ])
}
```

### Loading Files in HAP Modules

When loading files in a HAP, take the following ArkTS code as an example:

```typescript
// entry/src/main/ets/Test.ets
export function test() {
    console.log("call hap file")
}
export let value = 123
```

1. Configure the following in the module's `build-profile.json5`:

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

2. Import the `Test.ets` file and invoke the exported interfaces:

    <!-- compile -->
    ```cangjie
    func loadModule(context: JSContext): Unit {
        // 1. Import the module using requireArkModule
        let module = context.requireArkModule("entry/src/main/ets/Test")
        // 2. Convert the imported content to JSObject
        let test = module.asObject()
        // 3. Read the exported value variable
        let value = test["value"].toNumber()
        Hilog.info("value is ${value}")
        // 4. Write to the value variable
        test["value"] = context.number(2).toJSValue()
        // 5. Call the exported test method
        test.callMethod("test")
    }
    ```

### Loading Files in HAR Modules

1. Module Dependency Configuration

    ```json5
    // oh-package.json5 under the module
    {
      "name": "entry",
      "version": "1.0.0",
      "dependencies": {
        "localhar": "file:../localhar",                 // Local HAR in the same project, use a relative path to point to the module root directory
        "remotehar": "file:../prebuilts/remotehar.har", // Remote HAR, precompiled into a HAR (regardless of source code HAR or binary HAR), use a path to point to the HAR file
        "@ohos/lottie": "^2.0.0"                        // OHPM HAR, published to OHPM, just specify the version
      },
    }
    ```

2. Configure the following in the module's `build-profile.json5`:

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

3. Import and invoke the exported interfaces:

    <!-- compile -->
    ```cangjie
    func loadModule(context: JSContext): Unit {
        // 1. Import the module using requireArkModule
        let module = context.requireArkModule("localhar/src/main/ets/Test")     // Import files in the local HAR
        let module = context.requireArkModule("remotehar/src/main/ets/Test")    // Import files in the remote HAR
        let module = context.requireArkModule("@ohos/lottie/src/main/js/main")  // Import files in the OHPM HAR
        // 2. Convert the imported content to JSObject
        let test = module.asObject()
        // 3. Read the exported value variable
        let value = test["value"].toNumber()
        Hilog.info("value is ${value}")
        // 4. Write to the value variable
        test["value"] = context.number(2).toJSValue()
        // 5. Call the exported test method
        test.callMethod("test")
    }
    ```

> **Note:**
> There is a full-package import mechanism in ArkTS static imports, for example: `import * as localhar from "localhar"`.
> Essentially, this import mechanism still imports a single file. Each (HAR | HSP) module's `oh-package.json` contains a `main` field,
> which points to a source code file. Full-package import actually imports this file.
> For example, if the `oh-package.json` of `localhar` is configured with `main: "Index.ets"`, this interface should be used to import it as follows: `context.importArkModule("localhar/Index")`.

### Loading Files in HSP Modules
No configuration is required in `build-profile.json5`. The import and invocation methods are as follows:

<!-- compile -->
```cangjie
func loadModule(context: JSContext): Unit {
    // 1. Import the module using requireArkModule
    let module = context.requireArkModule("localhsp/src/main/ets/Test")     // Import files in the local HSP
    // 2. Convert the imported content to JSObject
    let test = module.asObject()
    // 3. Read the exported value variable
    let value = test["value"].toNumber()
    Hilog.info("value is ${value}")
    // 4. Write to the value variable
    test["value"] = context.number(2).toJSValue()
    // 5. Call the exported test method
    test.callMethod("test")
}
```

### Loading Native Modules
Native (napi | Cangjie) modules defined in HAP, HAR, and local HSP can all be loaded by their generated binary names.

<!-- compile -->
```cangjie
func loadModule(context: JSContext): Unit {
    // 1. Import the module using requireArkModule
    let module = context.requireArkModule("libentry.so")     // Import the native module
    // 2. Convert the imported content to JSObject
    let test = module.asObject()
    // 3. Read the exported value variable
    let value = test["value"].toNumber()
    Hilog.info("value is ${value}")
    // 4. Write to the value variable
    test["value"] = context.number(2).toJSValue()
    // 5. Call the exported test method
    test.callMethod("test")
}
```