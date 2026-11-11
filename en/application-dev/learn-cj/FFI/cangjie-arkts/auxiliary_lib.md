# Cangjie-ArkTS Interoperability Helper Library

To help developers write Cangjie-ArkTS interoperability code more conveniently, Cangjie provides an interoperability helper library. The library provides richer APIs for developers to call, offering public helper functions related to data type conversion and interoperability. For the API list, see [ohos.ark_interop_helper](../../../reference/arkinterop/cj-apis-ark_interop_helper.md).

In scenarios where a Cangjie application needs to use existing ArkTS libraries, if the interface in the ArkTS module that the developer wants to call requires a `context` parameter, the context must be passed from the ArkTS side to the Cangjie side. Take the `pick` method of the ArkTS <!--RP1-->[Camera Picker](https://gitcode.com/openharmony/docs/blob/master/en/application-dev/reference/apis-camera-kit/js-apis-cameraPicker.md)<!--RP1End--> module as an example. Its declaration is as follows, and the first parameter type is `common.Context`.

```typescript
declare namespace cameraPicker {
  // ...
  function pick(context: Context, mediaTypes: Array<PickerMediaType>, pickerProfile: PickerProfile): Promise<PickerResult>;
}
```

After crossing the interoperability boundary, the context is already a JSValue that can be used for interoperability. The Cangjie side saves it as a safe reference (JSObject) and uses it directly as a parameter when calling the interface.

> **Note:**
>
> A UIAbilityContext instance held on the Cangjie side cannot be converted into a parameter usable for interoperability. Therefore, ArkTS interfaces with a context parameter must be called in a Cangjie-ArkTS hybrid project. A pure Cangjie project (such as the [Cangjie] Empty Ability template, where UIAbility is implemented on the Cangjie side) has no ArkTS side to pass the context, so this call mode is not supported.

## Complete Example

The following example describes the complete process of calling the `pick` method of the camera picker to take a photo in a Cangjie-ArkTS hybrid project. The camera picker is a system picker implemented by an independent system process, so calling the `pick` interface **does not require the camera permission** (if you develop a custom camera with Camera Kit, the ohos.permission.CAMERA permission is required). In addition, the `pick` interface must be called in a UIAbility in the foreground; otherwise, the cameraPicker application cannot be started.

> **Note:**
>
> cameraPicker is a system module, and its interface declaration is provided by the system. The Cangjie side can call it directly after importing it through `requireSystemNativeModule`, without manually writing a declaration file. Only interfaces exported from the Cangjie side for ArkTS to use require an Index.d.ts declaration file (see [ArkTS Access to Cangjie Data](./operating_cangjie_objects.md)).

1. Create a Cangjie-ArkTS hybrid project by referring to [Building the First Cangjie-ArkTS Hybrid Application](./cj-quick-start-first-cangjie-hybrid-app.md), or enable Cangjie in an existing ArkTS project by referring to [Incrementally Using Cangjie in an Existing ArkTS Project](./cj-quick-start-first-cangjie-hybrid-module.md). Taking the entry hybrid module as an example, the project directory structure related to this example is as follows:

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

2. Define an exported function on the Cangjie side to receive the context. Open **entry > src > main > cangjie > index.cj**, import the dependent modules, and register the function that receives the context (the registration method is the same as that in [ArkTS Access to Cangjie Data](./operating_cangjie_objects.md)):

   <!-- compile -arkts_auxiliary_lib-example1 -->
   ```cangjie
   // index.cj
   // Define the package name, which must match the package name in cjpm.toml
   package ohos_app_cangjie_entry

   // Import the interoperability library
   import kit.CangjieKit.*
   // Import the logging module (Hilog is used in takePhoto to print the result)
   import kit.PerformanceAnalysisKit.*

   // Save the context passed from the ArkTS side: convert it into a JSObject safe reference and save it
   var globalContextObject: ?JSObject = None

   func setAbilityContext(context: JSContext, callInfo: JSCallInfo): JSValue {
       globalContextObject = Some(callInfo[0].asObject())
       return context.undefined().toJSValue()
   }

   // Register at the top level of the module so that the export is complete when the Cangjie module is loaded
   let _ = JSModule.registerFunc("setAbilityContext", setAbilityContext)
   ```

3. Add the interface declaration to the Index.d.ts corresponding to the Cangjie module:

   ```typescript
   // Index.d.ts corresponding to libohos_app_cangjie_entry.so
   import { common } from '@kit.AbilityKit';

   export declare function setAbilityContext(context: common.UIAbilityContext): void;
   ```

4. On the ArkTS side, call the function in the `onCreate` callback of UIAbility to pass the context to the Cangjie side for saving (the name of the imported dynamic library must be the same as the Cangjie package name. For details, see [ArkTS Access to Cangjie Data](./operating_cangjie_objects.md)):

   ```typescript
   // EntryAbility.ets
   import { setAbilityContext } from 'libohos_app_cangjie_entry.so';
   import { UIAbility, AbilityConstant, Want } from '@kit.AbilityKit';

   export default class EntryAbility extends UIAbility {
       onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
           // Pass the context to the Cangjie side for saving
           setAbilityContext(this.context);
       }
       // ...
   }
   ```

5. Continue editing **index.cj**. Add the interoperation function that calls the camera picker and register it:

   <!-- compile -arkts_auxiliary_lib-example1 -->
   ```cangjie
   // Call the pick method of the camera picker to take a photo
   func takePhoto(context: JSContext, callInfo: JSCallInfo): JSValue {
       // 1. Import the camera picker module (the module registration name is the ArkTS module name "@ohos.multimedia.cameraPicker" with the prefix "@ohos." removed)
       let module = context.requireSystemNativeModule("multimedia.cameraPicker")
       let picker = module.asObject()
       // 2. Use the context passed from the ArkTS side and saved as the first parameter of pick
       let ctxValue = globalContextObject.getOrThrow().toJSValue()
       // 3. Construct the parameter: media type array, where "photo" indicates the photo mode
       let mediaTypes = context.array([context.string("photo").toJSValue()]).toJSValue()
       //    Construct the parameter: pickerProfile, which specifies the rear camera (the value of camera.CameraPosition.CAMERA_POSITION_BACK is 1)
       let profile = context.object()
       profile["cameraPosition"] = context.number(1.0).toJSValue()
       // 4. Call the pick method, which returns a Promise
       let result = picker.callMethod("pick", [ctxValue, mediaTypes, profile.toJSValue()])
       // 5. Read the photo result through the callback registered by then
       result.asPromise().then(context.function { c, i =>
           let pickerResult = i[0].asObject()
           let resultUri = pickerResult["resultUri"].toString()
           Hilog.info(0, "AuxLib", "takePhoto resultUri: ${resultUri}")
           c.undefined().toJSValue()
       })
       return context.undefined().toJSValue()
   }

   let _ = JSModule.registerFunc("takePhoto", takePhoto)
   ```

6. Add the interface declaration of takePhoto to Index.d.ts:

   ```typescript
   export declare function takePhoto(): void;
   ```

7. Add a **Take Photo** button to the ArkTS page to trigger the call:

   ```typescript
   // Index.ets
   import { takePhoto } from 'libohos_app_cangjie_entry.so';

   @Entry
   @Component
   struct Index {
     build() {
       Row() {
         Column() {
           Button('Take Photo')
             .width('80%')
             .height(40)
             .margin(20)
             .onClick(() => {
               takePhoto()
             })
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

8. Click the run button in DevEco Studio to run the application, and click **Take Photo** on the application page. The system starts the camera interface. After taking a photo and confirming it, return to the application, and the URI of the photo result is displayed in the Log window (if saveUri is not specified, the captured content is saved to the media library by default and resultUri is the public media path):

   ```text
   takePhoto resultUri: file://media/Photo/...
   ```
