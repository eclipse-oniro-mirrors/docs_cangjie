# Cangjie Side Calling ArkTS Module

Taking the system NAPI module `@ohos.file.photoAccessHelper` (media library management module) on the ArkTS side as an example, this topic describes the complete process from importing a module to calling its interfaces on the Cangjie side.

> **Note:**
>
> Cangjie native APIs are available for some common system modules (for example, the Cangjie API of the media library management module, see [ohos.file.photoAccessHelper](../../../reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md)). If the target module already has a Cangjie native API, you are advised to use the Cangjie native API directly. The interoperation import method described in this section applies to ArkTS modules that do not have a Cangjie native API.

## Importing System NAPI Modules: Difference Between requireSystemNativeModule and requireArkModule

Both are used to load ArkTS modules on the Cangjie side. They differ in parameters and applicable scope:

| Interface | Applicable Scope |
|:---|:---|
| [requireArkModule(path)](./cangjie-load-arkts.md#supported-scenarios) | Loads system ArkTS modules (@ohos.\*, @system.\*, @hms.\*, @kit.\*), module files of hap/har/hsp in the project, and native modules (lib\*.so). |
| [requireSystemNativeModule(moduleName)](../../../reference/arkinterop/cj-apis-ark_interop.md) | Dedicated to loading ArkTS NAPI modules built in the system. The parameter is the registration name of the NAPI module, such as "file.photoAccessHelper" and "hilog". |

> **Caution:**
>
> Some ArkTS system modules are implemented based on NAPI at the bottom layer (for example, `@ohos.file.photoAccessHelper`). If such a module is imported through `requireArkModule`, the application may crash at runtime. Such modules should be imported by registration name using `requireSystemNativeModule`.

For the mapping rule between the module registration name of `requireSystemNativeModule` and the ArkTS module name (for example, `@ohos.file.photoAccessHelper` corresponds to "file.photoAccessHelper"), see [Obtaining the Interoperation Module Name on the ArkTS Side](./prepare_arkts_module.md).

## Complete Example

The `getPhotoAccessHelper` interface of the `photoAccessHelper` module requires a `context` parameter, which must be passed from the ArkTS side to the Cangjie side. The complete process is as follows:

1. Referring to steps 1 to 4 in the complete example of [Cangjie-ArkTS Interoperability Helper Library](./auxiliary_lib.md), pass the context on the ArkTS side to the Cangjie side for saving in a Cangjie-ArkTS hybrid project (the global variable that saves the context on the Cangjie side is `globalContextObject`).

2. Import the module and call its interfaces in Cangjie code (write it as an interoperation function, which is triggered by the ArkTS side):

   <!-- compile -->
   ```cangjie
   // Import the interoperability library
   import kit.CangjieKit.*

   func usePhotoAccessHelper(context: JSContext, callInfo: JSCallInfo): JSValue {
       // 1. Import the system NAPI module: the module registration name is the ArkTS module name with the prefix "@ohos." removed
       let module = context.requireSystemNativeModule("file.photoAccessHelper")
       // 2. Convert the imported module into a JSObject
       let obj = module.asObject()
       // 3. Use the context passed from the ArkTS side and saved as the parameter
       let ctxValue = globalContextObject.getOrThrow().toJSValue()
       // 4. Call the getPhotoAccessHelper method of the module; the return value is a PhotoAccessHelper instance
       let helper = obj.callMethod("getPhotoAccessHelper", [ctxValue])
       // 5. Subsequently call the methods of the instance (such as getAssets) through callMethod.
       //    For how to operate the returned JSValue, see "Cangjie Accessing ArkTS Data"
       return context.undefined().toJSValue()
   }
   ```

3. Before calling the interfaces of photoAccessHelper, ensure that the required permissions have been requested. The read interfaces of this module require the ohos.permission.READ_IMAGEVIDEO permission, and the write interfaces require the ohos.permission.WRITE_IMAGEVIDEO permission (for details, see [Permission List](../../../reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md#permission-list)). Both permissions are controlled permissions. For the request method, see [Requesting Controlled Permissions](../../../security/AccessToken/cj-declare-permissions-in-acl.md).

For how to operate ArkTS data, see [Cangjie Accessing ArkTS Data](./operating_ArkTS_data.md).

## Registering Class Functions with ArkTS Side

In a hybrid project, if you need to expose Cangjie class functions that contain the preceding ArkTS module calls to the ArkTS side, note that `JSModule.registerFunc` / `registerModule` can only register top-level functions or `JSLambda`, and cannot directly register class member functions. Choose one of the following methods based on whether the function depends on instance state:

- Method 1: Declare functions that do not depend on instance state as static member functions (the function signature must be (JSContext, JSCallInfo) -> JSValue), and register them in the static initializer `static init`:

  <!-- compile -->
  ```cangjie
  // Import the interoperability library
  import kit.CangjieKit.*

  class Data {
      static init() {
          // Register the function exported to ArkTS
          JSModule.registerFunc("createData", createData)
      }

      // Static member function: the signature must meet the interoperation function requirements
      static func createData(context: JSContext, _: JSCallInfo): JSValue {
          context.number(1.0).toJSValue()
      }
  }
  ```

- Method 2: For member functions that depend on instance state, wrap them with a `JSLambda` that captures the class instance, and then register the JSLambda:

  <!-- compile -->
  ```cangjie
  // Import the interoperability library
  import kit.CangjieKit.*

  class Calculator {
      var factor: Float64 = 2.0

      // Instance member function: the actual calculation logic
      public func multiply(a: Float64, b: Float64): Float64 {
          a * b * factor
      }
  }

  // Create a class instance
  let calculator = Calculator()

  // Wrap the class member function with a JSLambda that captures the instance, and register it with the ArkTS side
  let multiplyLambda: JSLambda = { context, callInfo =>
      let a = callInfo[0].toNumber()
      let b = callInfo[1].toNumber()
      // Call the class member function in the JSLambda
      context.number(calculator.multiply(a, b)).toJSValue()
  }

  let _ = JSModule.registerFunc("multiply", multiplyLambda)
  ```

After registration, add the corresponding interface declaration to Index.d.ts on the ArkTS side and call it through named imports. For details, see [ArkTS Access to Cangjie Data](./operating_cangjie_objects.md).
