# PDF Document Preview Capability Using Web Components

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Web components provide the ability to preview PDF documents within web pages. Applications can load PDF documents by passing PDF files through the [src](../reference/arkui-cj/cj-web-web.md#web) parameter interface of web components. Depending on the source of the PDF document, there are three common scenarios: loading network PDF documents, loading local PDF documents, and loading in-app resource PDF documents.

During the PDF document preview loading process, if network document retrieval is involved, please configure network access permissions in module.json5. For adding methods, refer to [Declaring Permissions in Configuration Files](../security/AccessToken/cj-declare-permissions.md).

```json
"requestPermissions":[
  {
    "name" : "ohos.permission.INTERNET"
  }
]
```

In the following example, the web component specifies the default loading of a network PDF document `www.example.com/test.pdf` upon creation. This address is for demonstration purposes only and should be replaced with a real accessible address during actual use:

<!-- compile -->

```cangjie
// index.cj
import ohos.arkui.state_macro_manage.*
import kit.ArkWeb.WebviewController
import kit.ArkUI.Web

@Entry
@Component
class EntryView {
    let webController = WebviewController()

    func build() {
        Column {
            /*
            * src setting methods:
            * Method 1: Load network PDF document: "https://www.example.com/test.pdf"
            * Method 2: Load local application sandbox PDF document: abilityContext.filesDirectory + "/test.pdf"
            * Method 3: In-app resource PDF document: "resource://rawfile/test.pdf"
            * Method 4: In-app resource PDF document: @rawfile(“test.pdf”)
            */
            Web(src: "https://www.example.com/test.pdf", controller: this.webController)
                .domStorageAccess(true)
        }
    }
}
```

In the above example, since the PDF preview page persistently records whether the sidebar navigation is expanded based on user operations using `window.localStorage`, the Document Object Model storage [domStorageAccess](../reference/arkui-cj/cj-web-web.md#func-domstorageaccessbool) permission needs to be enabled:

<!-- compile -->

```cangjie
Web().domStorageAccess(true)
```

When creating the web component, specify the default PDF document to load. The first parameter variable src of the [Web component](../reference/arkui-cj/cj-web-web.md#web) cannot be dynamically changed via state variables (e.g., @State).

It includes three PDF document loading and preview scenarios:

- Preview and load network PDF files.

    <!-- compile -->

    ```cangjie
    Web(src: "https://www.example.com/test.pdf", controller: this.webController)
        .domStorageAccess(true)
    ```

- Preview and load PDF files within the application sandbox. This requires enabling the [fileAccess](../reference/arkui-cj/cj-web-web.md#func-fileaccessbool) permission for accessing the application's file system.

    1. Obtain context

        <!-- compile -->

        ```cangjie
        // main_ability.cj
        import kit.AbilityKit.UIAbilityContext
        import kit.PerformanceAnalysisKit.Hilog
        
        func loggerInfo(str: String) {
            Hilog.info(0, "CangjieTest", str)
        }

        var globalAbilityContext: Option<UIAbilityContext> = Option<UIAbilityContext>.None

        class MainAbility <: UIAbility {
            public init() {
                super()
                registerSelf()
            }

            public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
                Hilog.info(1, "info", "MainAbility OnCreated.${want.abilityName}")

                // Obtain context
                globalAbilityContext = Option<UIAbilityContext>.Some(this.context)

                match (launchParam.launchReason) {
                    case LaunchReason.StartAbility => Hilog.info(1, "info", "StartAbility")
                    case _ => ()
                }
            }

            // ...
        }
        ```

    2. Enable access to the application's file system

        <!-- compile -->

        ```cangjie
        Web(src: globalAbilityContext.getOrThrow().filesDirectory + "/test.pdf", controller: this.webController)
            .domStorageAccess(true)
            .fileAccess(true)
        ```

- Preview and load in-app PDF resource files. There are two usage forms. The `@rawfile("test.pdf")` form cannot specify the preview parameters described below.

    <!-- compile -->

    ```cangjie
    import kit.LocalizationKit.*

    Web(src: @rawfile("test.pdf"), controller: this.webController)
        .domStorageAccess(true)
    ```

    <!-- compile -->

    ```cangjie
    Web(src: "resource://rawfile/test.pdf", controller: this.webController)
        .domStorageAccess(true)
    ```

Additionally, by configuring PDF file preview parameters, you can control the page state when opening the preview.

Currently supported parameters:

| Syntax  | Description  |
| :--------- | :---------- |
| nameddest=destination  |  Specifies a named destination within the PDF document. |
| page=pagenum  | Uses an integer to specify the page number in the document, where the first page has a pagenum value of 1. |
| zoom=scale    zoom=scale,left,top | Uses floating-point or integer values to set zoom and scroll factors. For example, a zoom value of 100 indicates 100% zoom. Left and top scroll values are in a coordinate system where 0,0 represents the top-left corner of the visible page, regardless of document rotation. |
| toolbar=1 \| 0 | Turns the top toolbar on or off. |
| navpanes=1 \| 0 | Turns the sidebar navigation pane on or off. |

URL examples:

```text
https://example.com/test.pdf#Chapter6
https://example.com/test.pdf#page=3
https://example.com/test.pdf#zoom=50
https://example.com/test.pdf#page=3&zoom=200,250,100
https://example.com/test.pdf#toolbar=0
https://example.com/test.pdf#navpanes=0
```