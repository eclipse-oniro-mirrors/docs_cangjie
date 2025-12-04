# Cangjie Side Calling ArkTS Module

Taking the example of calling the ArkTS-side module "@ohos.file.photoAccessHelper", the code example and analysis for using this module are as follows:

```cangjie
// Import interoperation library
import ohos.ark_interop.*
func tryLoadArkTSSo() {
    // Create new ArkTS runtime
    let runtime = JSRuntime()
    // Get interoperation context
    let context = runtime.mainContext
    // Import corresponding module based on ArkTS module name, the imported module is a JSValue
    let module = context.requireSystemNativeModule("file.photoAccessHelper")
    // Use this module following JSValue operation methods
    let obj = module.asObject()
    // Call photoAccessHelper methods through callMethod
    // obj.callMethod(...)
}
```

For methods to operate ArkTS data, please refer to [Cangjie Using ArkTS Data](./operating_ArkTS_data.md).