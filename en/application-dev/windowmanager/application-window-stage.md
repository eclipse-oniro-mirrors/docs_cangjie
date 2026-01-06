# Managing Application Windows

## Basic Concepts

- **Window Immersive Capability**: Refers to the ability to control system windows such as the status bar and navigation bar, reducing the abruptness of these system interfaces to provide users with an optimal experience.  
  The immersive capability only takes effect when the application's main window is in full-screen mode. Typically, application sub-windows (such as pop-ups, floating windows, and other auxiliary windows) and the main window in free-window mode cannot utilize the immersive capability.

- **Floating Window**: A global floating window is a special type of application window that can remain displayed in the foreground even after the main application window and its corresponding Ability are moved to the background.  
  Floating windows can be used for scenarios such as continuing video playback in a small window after the app is moved to the background or creating quick-access floating balls for specific applications. Applications must request the appropriate permissions before creating floating windows.

## Scenario Overview

In the `Stage` model, typical scenarios for managing application windows include:

- Setting properties and target pages for the main application window
- Setting properties and target pages for application sub-windows
- Experiencing window immersive capabilities
- Configuring floating windows
- Monitoring window non-interactive and interactive events

The following sections detail the specific development approaches.

## API Reference

The commonly used APIs for the above scenarios are listed in the table below. For more API details, refer to the [API Reference](../reference/arkui-cj/cj-apis-window.md).

| Instance       | API                                                          | Description                                                  |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| WindowStage    | `func getMainWindow(): Window`                               | Retrieves the main window under the `WindowStage` instance.<br/>This API is only available in the `Stage` model. |
| WindowStage    | `loadContent(path: String): Unit`                            | Loads a specific page into the main window of the current `WindowStage`.<br>`path` specifies the path of the page content to be loaded into the window.<br/>This API is only available in the `Stage` model. |
| WindowStage    | `createSubWindow(name: String): Window`                     | Creates a sub-window.<br/>This API is only available in the `Stage` model. |
| Window static method | `createWindow(config: Configuration): Window`               | Creates a sub-window or system window.<br/>- `config`: Parameters for window creation. |
| Window         | `setWindowBrightness(brightness: Float32): Unit`            | Sets the screen brightness value.                            |
| Window         | `setWindowTouchable(isTouchable: Bool): Unit`               | Sets whether the window is touchable. `true` for touchable; `false` for non-touchable. |
| Window         | `moveWindowTo(x: Int32, y: Int32): Unit`                    | Moves the current window's position.                         |
| Window         | `resize(width: UInt32, height: UInt32): Unit`               | Resizes the current window.                                  |
| Window         | `setWindowLayoutFullScreen(isLayoutFullScreen: Bool): Unit` | Sets whether the main window or sub-window uses an immersive layout. `true` for immersive layout; `false` for non-immersive layout. |
| Window         | `setWindowSystemBarEnable(names: Array<SystemBarType>): Unit` | Sets the visibility mode of the main window's status bar and navigation bar. The status bar is controlled via `status`, and the navigation bar via `navigation`.<br>For example, setting this parameter to `[SystemBarType.Status, SystemBarType.Navigation]` displays both; setting it to `[]` hides both. |
| Window         | `setWindowSystemBarProperties(systemBarProperties: SystemBarProperties): Unit` | Sets properties for the navigation bar and status bar within the window.<br/>`systemBarProperties`: A collection of properties for the navigation bar and status bar. |
| Window         | `func showWindow(): Unit`                                    | Displays the current window.                                 |
| Window         | `func destroyWindow(): Unit`                                 | Destroys the current window.                                 |

## Configuring the Main Application Window

In the `Stage` model, the main application window is created and managed by [UIAbility](../reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability). In the [onWindowStageCreate](../reference/AbilityKit/cj-apis-app-ability-ui_ability.md#func-onwindowstagecreatewindowstage) callback of [UIAbility](../reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability), the main window can be retrieved via `WindowStage` for property configuration. Additionally, main window properties such as `maxWindowWidth` can be set in the application configuration file. For details, refer to [abilities tag in module.json5 configuration file](../cj-start/basic-knowledge/module-configuration-file.md#abilities-tag).

### Development Steps

1. Retrieve the main application window.  
   Use the [getMainWindow](../reference/arkui-cj/cj-apis-window.md#func-getmainwindow) API to obtain the main window.

2. Set main window properties.  
   Multiple properties such as background color, brightness, and touchability can be configured as needed. This example demonstrates setting the "touchable" property.

3. Load the target page into the main window.  
   Use the [loadContent](../reference/arkui-cj/cj-apis-window.md#func-loadcontentstring) API to load the target page.

```cangjie
package ohos_app_cangjie_entry

internal import kit.AbilityKit.*
internal import kit.ArkUI.*

class MainAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        // 1. Retrieve the main application window.
        let mainWindow: Window = windowStage.getMainWindow()
        // 2. Set main window properties. Example: Set "touchable" property.
        window.setWindowTouchable(false)
        // 3. Load the target page into the main window.
        windowStage.loadContent("EntryView")
    }
}
```

## Configuring Application Sub-Windows

Developers can create sub-windows (e.g., pop-ups) as needed and configure their properties.

> **Note:**  
> The following scenarios are not recommended for sub-windows. Instead, prioritize using the [overlay](../reference/arkui-cj/cj-universal-attribute-overlay.md) capability of controls:  
> - On mobile devices (phones), sub-windows cannot exceed the bounds of the main window in floating or split-screen mode, similar to controls.  
> - In split-screen or free-window mode, controls adapt to changes in the main window's position and size more effectively than sub-windows.  
> - On some platforms, sub-windows may only support default system animations and rounded corners, limiting customization options.

### Development Steps

1. Create a sub-window.  
   Use the `createSubWindow` API to create a sub-window.

2. Configure sub-window properties.  
   After creation, properties such as size, position, background color, and brightness can be set.  
   It is recommended to set the size and position before calling `showWindow`.  
   If size is not specified:  
   - In free-window mode, the default size matches the physical screen.  
   - In non-free-window mode, the default size matches the main window.

3. Load and display sub-window content.  
   Use the `showWindow` API to display the sub-window content.

4. Destroy the sub-window.  
   Use the `destroyWindow` API to remove the sub-window when no longer needed.

Example code for creating a sub-window within `onWindowStageCreate`:

```cangjie
package ohos_app_cangjie_entry

internal import kit.ArkUI.*
internal import kit.AbilityKit.*

var windowStage: ?WindowStage = None
var subWindow: ?Window = None

class MainAbility <: UIAbility {
    public init() {
        super()
        registerSelf()
    }

    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        // Sub-windows can be created at appropriate times (e.g., button clicks). This example shows creation in onWindowStageCreate for demonstration.
        // 1. Create a sub-window.
        let subWindow = windowStage.createSubWindow("mySubWindow")
        // 2. Set sub-window properties (position, size, etc.).
        subWindow.getOrThrow().moveWindowTo(300, 300)
        subWindow.getOrThrow().resize(500, 500)
        // 3. Display the sub-window.
        subWindow.getOrThrow().showWindow()
    }

    public override func onWindowStageDestroy(): Unit {
        // Sub-windows can be destroyed at appropriate times (e.g., close button clicks). This example shows destruction in onWindowStageDestroy for demonstration.
        // 4. Destroy the sub-window when no longer needed.
        if (!subWindow.isSome()) {
            return
        }
        subWindow.getOrThrow().destroyWindow()
    }
}
```

Alternatively, sub-windows can be created via button clicks in a page:

```cangjie
// main_ability.cj
package ohos_app_cangjie_entry

internal import kit.ArkUI.*
internal import kit.AbilityKit.*
internal import ohos.arkui.state_management.AppStorage

var windowStage: ?WindowStage = None
var subWindow: ?Window = None

class MainAbility <: UIAbility {
    public init() {
        super()
        registerSelf()
    }

    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        AppStorage.setOrCreate("windowStage", windowStage)
        windowStage.loadContent("EntryView")
    }
}
```

```cangjie
// index.cj
package ohos_app_cangjie_entry

import kit.ArkUI.*
import kit.UIKit.*
import ohos.arkui.state_management.AppStorage

var windowStage: ?WindowStage = None
var subWindow: ?Window = None

@Entry
@Component
class EntryView{

    @State
    var message: String = "Hello World"

    func build() {
        Row() {
            Column() {
                Text(this.message)
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
                Button() {
                    Text("CreateSubWindow")
                        .fontSize(30)
                        .fontWeight(FontWeight.Normal)
                }
                    .margin(top: 20.px)
                    .backgroundColor(0x0D9FFB)
                    .width(220)
                    .height(68)
                    .onClick {
                        evt =>
                            windowStage = AppStorage.get('windowStage')
                            // 1. Create a sub-window.
                            subWindow = windowStage.getOrThrow().createSubWindow("mySubWindow")
                            // 2. Set sub-window properties (position, size, etc.).
                            subWindow.getOrThrow().moveWindowTo(300, 300)
                            subWindow.getOrThrow().resize(500, 500)
                            // 3. Display the sub-window.
                            subWindow.getOrThrow().showWindow()
                    }
                Button() {
                    Text("destroySubWindow")
                        .fontSize(30)
                        .fontWeight(FontWeight.Normal)
                }
                    .margin(top: 20.px)
                    .backgroundColor(0x0D9FFB)
                    .width(220)
                    .height(68)
                    .onClick {
                        evt =>
                            // 4. Destroy the sub-window when no longer needed.
                            if (!subWindow.isSome()) {
                                return
                            }
                            subWindow.getOrThrow().destroyWindow()
                    }
            }.width(100.percent)
        }.height(100.percent)
    }
}
```

## Experiencing Window Immersive Capability

In scenarios like video playback or gaming, users often prefer to hide system windows (e.g., status bar, navigation bar) for a more immersive experience. The window immersive capability (applicable only to the main window) can achieve this effect. Starting from API version 10, immersive windows default to full-screen size with layout controlled by the component module. The status bar and navigation bar have transparent backgrounds with black text. The `setWindowLayoutFullScreen` API can be used to toggle between immersive (`true`) and non-immersive (`false`) layouts.

> **Note:**  
> Currently, immersive mode configuration is only supported at the window level, not the Page level. For Page-level switching, immersive mode can be set in lifecycle callbacks like `onPageShow` and reverted in `onPageHide`.

### Development Steps

1. Retrieve the main application window.  
   Use the `getMainWindow` API to obtain the main window.

2. Implement immersive effects via one of two methods:  
   - Method 1: Hide the status bar and navigation bar using `setWindowSystemBarEnable` when the main window is in full-screen mode.  
   - Method 2: Set the main window to full-screen layout via `setWindowLayoutFullScreen`, then configure the transparency, colors, and highlight icons of the status bar and navigation bar via `setWindowSystemBarProperties` to harmonize with the main window.

3. Load and display immersive window content.  
   Use the `loadContent` API to load the content.

```cangjie
package ohos_app_cangjie_entry

internal import kit.AbilityKit.*
internal import kit.ArkUI.*

class MainAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        // 1. Retrieve the main application window.
        let mainWindow: Window = windowStage.getMainWindow()
        // 2. Implement immersive effects. Method 1: Hide the status bar and navigation bar.
        mainWindow.setWindowSystemBarEnable([])
        // 2. Implement immersive effects. Method 2: Set full-screen layout and configure system bar properties.
        mainWindow.setWindowLayoutFullScreen(true)
        let sysBarProps: SystemBarProperties = SystemBarProperties(
                                                statusBarColor: "#ff00ff", 
                                                navigationBarColor: "#00ff00", 
                                                statusBarContentColor: "#ffffff",
                                                navigationBarContentColor: "#ffffff")
        mainWindow.setWindowSystemBarProperties(sysBarProps)
        // 3. Load the target page into the immersive window.
        windowStage.loadContent("EntryView")
    }
}
```

## Configuring Floating Windows

Floating windows can remain displayed in the foreground even after the creating task moves to the background. Typically, floating windows appear above all other application windows. Developers can create and configure floating windows as needed.

### Development Steps

**Prerequisite:** To create a `WindowType.TypeFloat` (floating window), the `ohos.permission.SYSTEM_FLOAT_WINDOW` permission must be requested. For configuration details, refer to [Permission Request for system_basic-Level Applications](../security/AccessToken/cj-determine-application-mode.md#system_basic-level-application-permission-request-methods).

1. Create a floating window.  
   Use the `createWindow` API with `WindowType.TypeFloat`.

2. Configure floating window properties.  
   After creation, properties such as size, position, background color, and brightness can be set.

3. Load and display floating window content.  
   Use the `showWindow` API to display the content.

4. Destroy the floating window.  
   Use the `destroyWindow` API to remove the window when no longer needed.

```cangjie
package ohos_app_cangjie_entry

internal import kit.AbilityKit.*
internal import kit.ArkUI.*

class MainAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        // 1. Create a floating window.
        let config: Configuration = Configuration(
            name: "floatWindow", windowType: WindowType.TypeFloat, ctx: this.context
        )
        let windowClass: Window = createWindow(config)
        // 2. Configure floating window properties (position, size, etc.).
        windowClass.moveWindowTo(300, 300)
        windowClass.resize(500, 500)
        // 3. Display the floating window.
        windowClass.showWindow()
        // 4. Destroy the floating window when no longer needed.
        windowClass.destroyWindow()
    }
}
```