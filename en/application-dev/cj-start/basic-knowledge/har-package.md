# HAR  

HAR (Harmony Archive) is a static shared package that can contain code, C++ libraries, resources, and configuration files. HAR enables the sharing of Cangjie components and resources across multiple modules or projects.  

## Usage Scenarios  

- Supports in-application sharing and can also be published as a second-party library (SDK) or third-party library (SDK) for use by other applications.  

- As a second-party library (SDK), it can be published to the [OHPM Private Repository](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo) for internal use by other applications within the company.  

- As a third-party library (SDK), it can be published to the [OHPM Central Repository](https://ohpm.openharmony.cn/) for use by other applications.  

## Constraints  

- HAR cannot be installed or run independently on a device; it can only be referenced as a dependency of an application module.  

- HAR does not support declaring `pages` in configuration files, but it can contain `pages` and navigate via the `Navigation` method.  

- HAR cannot reference resources in the `AppScope` directory. During compilation and building, content in `AppScope` is not packaged into the HAR, which may cause HAR resource references to fail.  

- When multiple packages (HAPs) reference the same HAR, it results in duplicate copies of code and resources across packages, increasing the application package size.  

- HAR can depend on other HARs, but circular dependencies and transitive dependencies are not supported.  

- When a HAP references a HAR, the system automatically merges their permission configurations during compilation. Therefore, developers do not need to repeatedly request the same permissions in both the HAP and HAR.  

- When integrating a Cangjie binary HAR, the same SDK version used to compile the HAR must be used for compilation.  

- If a module contains custom macros and needs to be used by other modules, the module and other modules cannot be compiled into a binary HAR and must be compiled into a source-code format Cangjie HAR<!-- add link -->.  

- Binary HAR packages require the use of `hapTasks` imported from `@ohos/cangjie-build-support` in the `hvigorfile.ts` of the final integrated HAP module; otherwise, only the source-code format Cangjie HAR can be used.  

> **Note:**  
>  
> **Circular Dependency**: For example, with three HARs—HAR-A, HAR-B, and HAR-C—a circular dependency occurs if HAR-A depends on HAR-B, HAR-B depends on HAR-C, and HAR-C in turn depends on HAR-A.  
>  
> **Transitive Dependency**: For example, with three HARs—HAR-A, HAR-B, and HAR-C—the dependency relationship is HAR-A depends on HAR-B, and HAR-B depends on HAR-C. Non-transitive dependency means HAR-A can use methods and components from HAR-B but cannot directly use methods and components from HAR-C.  

## Creation  

Developers can create a HAR module using DevEco Studio. For details, see [Creating a Library Module](#)<!-- add link -->.  

## Development  

This section explains how to export Cangjie components, interfaces, and resources from a HAR for use by other applications or other modules within the same application.  

Interfaces and other elements to be exported from the HAR can be marked with the `public` modifier.  

> **Note:**  
>  
> When a HAR is compiled with its host application, the HAR's code is directly compiled into the host application. The HAR package is an intermediate compilation artifact, not the final runtime entity. At runtime, the HAR operates under the identity of its host application, and the system distinguishes behavior based on the host application's version. If different behaviors are required in the HAR based on the host application's version, developers can call the [`getBundleInfoForSelf`](../../../../en/application-dev/reference/AbilityKit/cj-apis-bundle_manager.md#static-func-getbundleinfoforselfint32) interface to obtain the host application's `targetVersion` and implement logic accordingly.  

### Exporting Cangjie Components  

Use `public` to export Cangjie components. Example:  

<!-- compile -->  

```cangjie  
// library/src/main/cangjie/mainPage.cj  
package ohos_app_cangjie_library  

import ohos.base.*  
import ohos.arkui.component.Text  
import ohos.arkui.component.Column  
import ohos.arkui.component.CustomView  
import ohos.arkui.state_management.LocalStorage  
import ohos.arkui.state_management.ObservedProperty  
import ohos.arkui.state_management.SubscriberManager  
import ohos.arkui.state_management.ViewStackProcessor  
import ohos.arkui.state_macro_manage.State  
import ohos.arkui.state_macro_manage.Component  
import ohos.arkui.state_macro_manage.r  
import ohos.arkui.component.Flex  
import ohos.arkui.component.Row  
import ohos.arkui.component.FlexParams  
import ohos.arkui.component.FontWeight  
import ohos.arkui.component.ItemAlign  
import ohos.arkui.component.FlexAlign  
import ohos.arkui.component.Image  
import ohos.resource_manager.__GenerateResource__  

@Component  
public class MainPage {  
    @State  
    var message: String = "Hello"  

    public func build() {  
        Column() {  
            Row() {  
                Text(this.message).fontSize(32).fontWeight(FontWeight.Bold)  
            }.margin(32).height(56).width(624)  
            Flex(  
                FlexParams(justifyContent: FlexAlign.Center, alignItems: ItemAlign.Center,  
                    alignContent: FlexAlign.Center)) {  
                    Column() {  
                        Image(@r(app.media.pic_empty)).width(33.percent)  
                        Text(@r(app.string.empty)).fontSize(14).fontColor(@r(app.color.text_color))  
                    }  
            }.width(100.percent).height(90.percent)  
        }.width(100.percent).height(100.percent).backgroundColor(@r(app.color.page_background))  
    }  
}  
```  

### Exporting Classes and Methods  

Use `public` to export classes and methods. Multiple classes and methods can be exported. Example:  

<!-- compile -->  

```cangjie  
// library/src/main/cangjie/classFunc.cj  
package ohos_app_cangjie_library  

public class Log {  
    public static func info(msg: String) {  
        msg  
    }  
}  

public func harFunc() {  
  return 'har func'  
}  

public func harFunc2() {  
  return 'har func2'  
}  
```  

### Exporting Resources  

During HAP compilation, DevEco Studio collects resource files from the HAP module and its dependent modules. If resource files with the same name conflict across modules, DevEco Studio resolves the conflict based on the following priority (from highest to lowest):  

- `AppScope` (only supported in the Stage model).  
- The HAP module itself.  
- Dependent HAR modules. If multiple HARs have resource conflicts, the resolution follows the dependency order in the project's `oh-package.json5` file, where earlier dependencies have higher priority. For example, in the following snippet, if `dayjs` and `lottie` contain files with the same name, resources from `dayjs` will be used first.  

> **Note:**  
>  
> If resources are configured in the internationalization directories of `AppScope`, HAP modules, or HAR modules, the merging priority under the same internationalization qualifiers follows the above rules. Additionally, configurations under internationalization qualifiers take precedence over those in `base`. For example, if a resource field is configured in `base` of `AppScope` and the same field is configured in `en_US` of a HAR module, the HAR module's configuration will be prioritized in an `en_US` context.  

```json5  
// oh-package.json5  
{  
    "dependencies": {  
        "dayjs": "^1.10.4",  
        "lottie": "^2.0.0"  
    }  
}  
```  

## Usage  

This section explains how to configure HAR dependencies and reference Cangjie components, interfaces, and resources from a HAR.  

Before referencing a HAR, you must configure the HAR dependency. For details, see [Referencing HAR Files and Resources](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-har-import).  

### Referencing Cangjie Components from a HAR  

After successfully configuring the HAR dependency, you can reference its Cangjie components. Use `import` to reference exported Cangjie components. Example:  

<!-- compile -->  

```cangjie  
// entry/src/main/cangjie/index.cj  
package ohos_app_cangjie_entry  

import ohos.base.LengthProp  
import ohos.arkui.component.Column  
import ohos.arkui.component.Row  
import ohos.arkui.component.CustomView  
import ohos.arkui.component.CJEntry  
import ohos.arkui.component.loadNativeView  
import ohos.arkui.state_management.ObservedProperty  
import ohos.arkui.state_management.LocalStorage  
import ohos.arkui.state_macro_manage.Entry  
import ohos.arkui.state_macro_manage.Component  
import ohos.arkui.state_management.ViewStackProcessor  
import ohos.arkui.state_management.SubscriberManager  
import ohos.arkui.component.LegalCallCheck  
import ohos.arkui.component.ReuseParams  
import ohos.arkui.component.ViewBuilder  
import ohos.arkui.component.__Recycle__  
import ohos.arkui.component.FakeComponent  
import ohos_app_cangjie_library.MainPage  

@Entry  
@Component  
class EntryView {  
    func build() {  
        Row {  
           // Reference the Cangjie component from the HAR  
           MainPage()  
        }.height(100.percent)  
    }  
}  
```  

### Referencing Classes and Methods from a HAR  

Use `import` to reference exported classes and methods. Example:  

<!-- compile -->  

```cangjie  
// entry/src/main/cangjie/index2.cj  
package ohos_app_cangjie_entry  

import ohos.base.LengthProp  
import ohos.arkui.component.Column  
import ohos.arkui.component.Row  
import ohos.arkui.component.Text  
import ohos.arkui.component.CustomView  
import ohos.arkui.component.CJEntry  
import ohos.arkui.component.loadNativeView  
import ohos.arkui.component.FontWeight  
import ohos.arkui.state_management.SubscriberManager  
import ohos.arkui.state_management.ObservedProperty  
import ohos.arkui.state_management.LocalStorage  
import ohos.arkui.state_macro_manage.Entry  
import ohos.arkui.state_macro_manage.Component  
import ohos.arkui.state_macro_manage.State  
import ohos_app_cangjie_library.Log  
import ohos_app_cangjie_library.harFunc  

@Entry  
@Component  
class EntryView2 {  
    @State  
    var message: String = "Hello World"  

    func build() {  
        Row {  
            Column {  
                Text(this.message)  
                    .fontSize(50)  
                    .fontWeight(FontWeight.Bold)  
                    .onClick {  
                        evt =>  
                        // Reference the class and method from the HAR  
                        Log.info("har msg")  
                        this.message = "func return: ${harFunc()}"  
                    }  
            }.width(100.percent)  
        }.height(100.percent)  
    }  
}  
```  

### Referencing Resources from a HAR  

Use `@r` to reference resources from a HAR. For example, if a string resource (defined in `string.json` with `name: hello_har`) and an image resource (`icon_har.png`) are added to the HAR module's `src/main/resources`, they can be referenced in the Entry module as follows:  

<!-- compile -->  

```cangjie  
// entry/src/main/cangjie/index3.cj  
package ohos_app_cangjie_entry  

import ohos.base.LengthProp  
import ohos.arkui.component.Column  
import ohos.arkui.component.Row  
import ohos.arkui.component.Text  
import ohos.arkui.component.CustomView  
import ohos.arkui.component.CJEntry  
import ohos.arkui.component.loadNativeView  
import ohos.arkui.component.FontWeight  
import ohos.arkui.state_management.SubscriberManager  
import ohos.arkui.state_management.ObservedProperty  
import ohos.arkui.state_management.LocalStorage  
import ohos.arkui.state_macro_manage.Entry  
import ohos.arkui.state_macro_manage.Component  
import ohos.arkui.state_macro_manage.State  
import ohos.arkui.state_macro_manage.r  
import ohos.resource_manager.__GenerateResource__  
import ohos.arkui.component.Image  
import ohos.arkui.component.List  
import ohos.arkui.component.ListItem  
import ohos.arkui.component.ListItemAlign  

@Entry  
@Component  
class EntryView3 {  
    @State  
    var message: String = "Hello World"  

    func build() {  
        Row {  
            Column {  
                // Reference the string resource from the HAR  
                Text(@r(app.string.hello_har))  
                    .fontSize(50)  
                    .fontWeight(FontWeight.Bold)  
                    .onClick {  
                        evt => this.message = "Hello Cangjie"  
                    }  
                List() {  
                    ListItem() {  
                        // Reference the image resource from the HAR  
                        Image(@r(app.media.icon_har)).id('iconHar').borderRadius(48.px)  
                    }.margin(5.percent).width(312.px)  
                }.alignListItem(ListItemAlign.Center)  
            }.width(100.percent)  
        }.height(100.percent)  
    }  
}  
```  

## Compilation  

HARs can be provided to other applications as second-party or third-party libraries.  

## Publishing  

For details, see [Publishing a HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-har-publish).