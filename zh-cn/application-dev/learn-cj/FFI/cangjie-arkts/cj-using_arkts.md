# 仓颉应用中使用 ArkTS

在开发仓颉应用时，可以通过互操作调用 ArkTS 已有库，复用 ArkTS 丰富的库生态。仓颉应用中不支持增加 ArkTS 页面，但支持增加 ArkTS 模块。

ArkTS 库主要分为 NAPI（Node.js API）系统模块与三方库模块两类，仓颉侧均已支持调用：

| ArkTS 库类型 | 说明 | 调用方式 |
|:--- |:--- |:--- |
| NAPI 系统模块 | 以 `@ohos.*` 开头的系统模块，如相册管理模块 `@ohos.file.photoAccessHelper` | 通过互操作库的 `requireArkModule` / `requireSystemNativeModule` 接口加载后直接调用，参见[在仓颉代码里导入ArkTS模块](./cangjie-load-arkts.md)与[仓颉侧调用 ArkTS 模块](./cj-using_arkts_module.md) |
| 三方库模块 | 发布在 ohpm 仓的 ArkTS 三方库，如 lz4js | 通过 DevEco Studio 仓颉插件的代码生成工具（在类型声明文件上右键选择 **Generate... > Cangjie Bindings**）生成仓颉封装层后调用，参见[仓颉调用ArkTS三方模块](./cj-quick-start-dts2cj-plugin-usage.md) |

> **说明：**
>
> - 部分常用系统模块已提供仓颉原生 API（例如相册管理模块的仓颉 API 可参见 [ohos.file.photoAccessHelper](../../../reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md)）。若目标模块已有仓颉原生 API，建议优先直接使用仓颉原生 API，无需通过互操作调用。
> - 调用需要传入 context 入参的 ArkTS 接口（如相机选择器的 pick 方法）时，context 需由 ArkTS 侧传入仓颉侧，参见[仓颉-ArkTS 互操作辅助库](./cj-arkts_auxiliary_lib.md)。
