# Environment: Device Environment Query

Developers may need to query the environmental parameters of the device running the application to make different scenario judgments, such as multilingual support or light/dark mode. This requires the use of the Environment device environment query.

Environment is a singleton object created by the ArkUI framework when the application starts. It provides AppStorage with a series of properties describing the application's runtime state. All properties of Environment are immutable (i.e., applications cannot write to them), and all properties are of simple types.

Environment offers the capability to read certain system environment variables (see [Environment Built-in Parameters](#environment-built-in-parameters)) and writes their values into AppStorage. Therefore, developers need to access AppStorage to obtain the values of these environment variables.

Before reading this document, it is recommended to first review: [AppStorage](./cj-appstorage.md).

## Environment Built-in Parameters

| Key | Data Type | Description |
|:---|:---|:---|
| accessibilityEnabled | Bool | Indicates whether screen reader accessibility is enabled. |
| colorMode | ColorMode | Color model type: options are ColorMode.LIGHT (light mode) and ColorMode.DARK (dark mode). |
| fontScale | Float64 | Font size scaling factor. Range: [0.85, 1.45]. |
| fontWeightScale | Float64 | Font weight scaling factor. Range: [0.6, 1.6]. |
| layoutDirection | LayoutDirection | Layout direction type: includes LayoutDirection.Ltr (left-to-right) and LayoutDirection.Rtl (right-to-left). |
| languageCode | String | Current system language value, which must be in lowercase letters (e.g., "zh"). |

## Usage Scenarios

### Accessing Environment Parameters from UI

- Use `Environment.envProp` to store device environment variables in AppStorage.

    ```cangjie
    // Store the device's language code in AppStorage, with a default value of "en"
    Environment.envProp<String>("languageCode", "en")
    ```

- Use `@StorageProp` to link to a Component.

    ```cangjie
    @StorageProp["languageCode"] let languageCode: String = "en"
    ```

The update chain from device environment to Component: Environment --> AppStorage --> Component.

> **Note:**
>
> Environment parameters linked via `@StorageProp` can be modified locally but cannot be synchronized back to AppStorage because the application cannot write to environment variables. They can only be queried in Environment.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    let SysLanguageCode = Environment.envProp<String>("languageCode", "en")
    @StorageProp["languageCode"]
    let languageCode: String = "en"
    func build() {
        Row() {
            Column() {
                // Display the current device's languageCode
                Text(this.languageCode)
            }
        }
    }
}
```

### Using Environment in Application Logic

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    // Use Environment.EnvProp to store the device's languageCode in AppStorage
    let SysLanguageCode = Environment.envProp<String>("languageCode", "en")
    // Retrieve the languageCode variable from AppStorage with one-way binding
    let lang: ObservedProperty<String> = AppStorage.`prop`<String>('languageCode').getOrThrow()
    func build() {
        Row() {
            Column() {
                Button("lang")
                .onClick {
                    evt =>
                        if (lang.get()=='zh') {
                            Hilog.info(0, "Chinese", "Hello")
                        } else {
                            Hilog.info(0, "En", "Hello")
                        }

                }
            }
        }
    }
}
```