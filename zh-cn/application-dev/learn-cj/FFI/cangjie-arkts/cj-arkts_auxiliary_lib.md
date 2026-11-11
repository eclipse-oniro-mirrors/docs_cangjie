# 仓颉-ArkTS 互操作辅助库

为了帮助开发者更加方便地编写仓颉-ArkTS 互操作代码，仓颉还提供了互操作辅助库。辅助库提供了更加丰富的 API 供开发者调用，提供数据类型转换和互操作相关的公共辅助功能函数，其接口列表请参见 [ohos.ark_interop_helper](../../../reference/arkinterop/cj-apis-ark_interop_helper.md)。

在仓颉应用里使用 ArkTS 存量库场景中，当开发者想要调用的 ArkTS 模块中的接口需要传入一个 context 入参时，context 需由 ArkTS 侧传入仓颉侧使用。以 ArkTS <!--RP1-->[相机选择器](https://gitcode.com/openharmony/docs/blob/master/zh-cn/application-dev/reference/apis-camera-kit/js-apis-cameraPicker.md)<!--RP1End--> 模块的 pick 方法为例，其声明如下，第一个参数类型为 common.Context。

```typescript
declare namespace cameraPicker {
  // ...
  function pick(context: Context, mediaTypes: Array<PickerMediaType>, pickerProfile: PickerProfile): Promise<PickerResult>;
}
```

context 经过互操作边界后已经是互操作可用的 JSValue，仓颉侧将其保存为安全引用（JSObject），调用接口时直接作为入参使用即可。

> **说明：**
>
> 仓颉侧持有的 UIAbilityContext 实例无法转换为互操作可用的入参，因此此类带 context 入参的 ArkTS 接口需在仓颉与ArkTS混合工程中调用；纯仓颉工程（如 [Cangjie] Empty Ability 模板，UIAbility 由仓颉侧实现）中没有 ArkTS 侧传入 context，不支持此调用方式。

## 完整使用示例

下面以在仓颉与ArkTS混合工程中调用相机选择器的 pick 方法实现拍照为例，说明完整使用链路。相机选择器属于系统 Picker，由系统独立进程实现，调用 pick 接口**无需申请相机权限**（若使用 Camera Kit 开发自定义相机，则需申请 ohos.permission.CAMERA 权限）。此外，pick 接口必须在界面 UIAbility 中调用（即应用处于前台时），否则无法启动 cameraPicker 应用。

> **说明：**
>
> cameraPicker 是系统模块，其接口声明由系统提供，仓颉侧通过 `requireSystemNativeModule` 导入后即可直接调用，无需手动编写声明文件；只有仓颉侧导出给 ArkTS 使用的接口才需要编写 Index.d.ts 声明文档（参见[ArkTS 访问仓颉数据](./operating_cangjie_objects.md)）。

1. 参照[构建第一个仓颉与ArkTS混合应用](./cj-quick-start-first-cangjie-hybrid-app.md)创建一个仓颉与ArkTS混合工程，或参照[在已有ArkTS工程中增量使用仓颉](./cj-quick-start-first-cangjie-hybrid-module.md)在已有ArkTS工程中使能仓颉。以 entry 混合模块为例，与本示例相关的工程目录结构如下：

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

2. 仓颉侧定义接收 context 的导出函数。打开 **entry > src > main > cangjie > index.cj**，导入依赖模块并注册接收 context 的函数（注册方式与[ArkTS 访问仓颉数据](./operating_cangjie_objects.md)一致）。

   <!-- compile -arkts_auxiliary_lib-example1 -->
   ```cangjie
   // index.cj
   // 定义包名，该包名需要和 cjpm.toml 的 package name 保持一致
   package ohos_app_cangjie_entry

   // 导入互操作库
   import kit.CangjieKit.*
   // 导入日志模块（takePhoto 中使用 Hilog 打印结果）
   import kit.PerformanceAnalysisKit.*

   // 保存 ArkTS 侧传入的 context：转为 JSObject 安全引用后保存
   var globalContextObject: ?JSObject = None

   func setAbilityContext(context: JSContext, callInfo: JSCallInfo): JSValue {
       globalContextObject = Some(callInfo[0].asObject())
       return context.undefined().toJSValue()
   }

   // 在模块顶层注册，仓颉模块加载时即完成导出
   let _ = JSModule.registerFunc("setAbilityContext", setAbilityContext)
   ```

3. 在仓颉模块对应的 `Index.d.ts` 中补充接口声明。

   ```typescript
   // libohos_app_cangjie_entry.so 对应的 Index.d.ts
   import { common } from '@kit.AbilityKit';

   export declare function setAbilityContext(context: common.UIAbilityContext): void;
   ```

4. ArkTS 侧在 UIAbility 的 onCreate 回调中调用，把 context 传给仓颉侧保存（导入的动态库名称需与仓颉包名一致，参见[ArkTS 访问仓颉数据](./operating_cangjie_objects.md)）。

   ```typescript
   // EntryAbility.ets
   import { setAbilityContext } from 'libohos_app_cangjie_entry.so';
   import { UIAbility, AbilityConstant, Want } from '@kit.AbilityKit';

   export default class EntryAbility extends UIAbility {
       onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
           // 把 context 传给仓颉侧保存
           setAbilityContext(this.context);
       }
       // ...
   }
   ```

5. 继续编辑 **index.cj**，添加调用相机选择器的互操作函数并注册。

   <!-- compile -arkts_auxiliary_lib-example1 -->
   ```cangjie
   // 调用相机选择器的 pick 方法拍照
   func takePhoto(context: JSContext, callInfo: JSCallInfo): JSValue {
       // 1. 导入相机选择器模块（模块注册名为 ArkTS 模块名 "@ohos.multimedia.cameraPicker" 去掉前缀 "@ohos."）
       let module = context.requireSystemNativeModule("multimedia.cameraPicker")
       let picker = module.asObject()
       // 2. 使用 ArkTS 侧传入并保存的 context 作为 pick 的第一个入参
       let ctxValue = globalContextObject.getOrThrow().toJSValue()
       // 3. 构造参数：媒体类型数组，"photo" 表示拍照模式
       let mediaTypes = context.array([context.string("photo").toJSValue()]).toJSValue()
       //    构造参数：pickerProfile，指定后置相机（camera.CameraPosition.CAMERA_POSITION_BACK 的值为 1）
       let profile = context.object()
       profile["cameraPosition"] = context.number(1.0).toJSValue()
       // 4. 调用 pick 方法，返回值为 Promise
       let result = picker.callMethod("pick", [ctxValue, mediaTypes, profile.toJSValue()])
       // 5. 通过 then 注册回调，读取拍照结果
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

6. 在 `Index.d.ts` 中补充 takePhoto 的接口声明。

   ```typescript
   export declare function takePhoto(): void;
   ```

7. 在 ArkTS 页面中添加“拍照”按钮触发调用。

   ```typescript
   // Index.ets
   import { takePhoto } from 'libohos_app_cangjie_entry.so';

   @Entry
   @Component
   struct Index {
     build() {
       Row() {
         Column() {
           Button('拍照')
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

8. 点击 DevEco Studio 界面中的运行按钮运行应用，在应用界面点击“拍照”按钮，系统拉起相机界面；完成拍照并确认后返回应用，可在 Log 窗口看到输出的拍照结果 URI（未指定 saveUri 时，拍摄内容默认存入媒体库，resultUri 为公共媒体路径）。

   ```text
   takePhoto resultUri: file://media/Photo/...
   ```
