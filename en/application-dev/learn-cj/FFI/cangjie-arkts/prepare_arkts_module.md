# Obtaining Interoperability Module Names in ArkTS

The Cangjie application supports adding ArkTS modules but does not support adding ArkTS pages. The following primarily introduces how to add ArkTS modules.

ArkTS modules are mainly divided into NAPI (Node.js API) modules and third-party library modules. Cangjie only supports calling NAPI modules.

Before detailing the specific loading process, we first introduce the mapping specifications between Cangjie's import names and ArkTS module names, as follows:

| ArkTS Module Name            | Cangjie Import Name                        | Description                                                                 |
| :--------------------------- | :---------------------------------------- | :-------------------------------------------------------------------------- |
| @ohos.file.photoAccessHelper | ("file.photoAccessHelper")               | If the ArkTS module name starts with @ohos, the Cangjie import name simply removes the prefix "@ohos." |
| @hms.core.push.pushService   | ("core.push.pushService", prefix: "hms") | If the ArkTS module name starts with @xxx (where xxx is not ohos), there are two import names: the first is the module name with "@xxx." removed, and the second parameter is `prefix: "xxx"`. For this example, the Cangjie import name is `"core.push.pushService", prefix: "hms"`. |

The project configuration for using ArkTS modules in a Cangjie application is no different from a standard Cangjie project. You can refer to [Creating a New Project](https://docs.openharmony.cn/pages/v6.0/en/application-dev/quick-start/start-with-ets-stage.md). The only additional requirement is loading the NAPI module in the code. Taking the OpenHarmony [Photo Access Helper](https://docs.openharmony.cn/pages/v6.0/en/application-dev/reference/apis-media-library-kit/arkts-apis-photoAccessHelper.md) module as an example: after reviewing the ArkTS documentation, its module name is "@ohos.file.photoAccessHelper". This provides the module name on the ArkTS side, which can then be called from the Cangjie side.