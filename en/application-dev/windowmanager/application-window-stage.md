# Managing Application Windows

## Basic Concepts

- **Window Immersive Capability**: Refers to the ability to control system windows such as the status bar and navigation bar, reducing the abruptness of these system interfaces, thereby providing users with an optimal experience.
  Immersive capability only takes effect when the application's main window is in full-screen mode. Typically, application sub-windows (pop-ups, floating windows, and other auxiliary windows) and the main application window in free window mode cannot use immersive capabilities.

- **Floating Window**: A global floating window is a special type of application window that has the ability to remain displayed in the foreground even after the main application window and its corresponding Ability move to the background.
  Floating windows can be used for scenarios like continuing video playback in a small window after the app moves to the background, or creating quick access points like floating balls for specific applications. Applications need to apply for corresponding permissions before creating floating windows.

## Scenario Description

In the `Stage` model, typical scenarios for managing application windows include:

- Setting the main application window properties and target page.
- Setting sub-application window properties and target page.
- Experiencing window immersive capability.
- Setting up floating windows.
- Listening for window non-interactive and interactive events.

The specific development methods for each are described below.

## Interface Description

The commonly used interfaces involved in the above scenarios are listed in the table below. For more API descriptions, please refer to the [API Reference](../../../en/application-dev/reference/arkui-cj/cj-apis-window.md).

| Instance      | Interface                                                                  | Description                                                                                                                                       |
| ------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| WindowStage   | `func getMainWindow(): Window`                                             | Gets the main window under the `WindowStage` instance.<br/>This interface can only be used in the `Stage` model.                                   |
| WindowStage   | `loadContent(path: String): Unit`                                          | Loads a specific page for the main window of the current `WindowStage`.<br>`path` is the path to the page content to be loaded into the window.<br/>This interface can only be used in the `Stage` model. |
| WindowStage   | `createSubWindow(name: String): Window`                                    | Creates a sub-window.<br/>This interface can only be used in the `Stage` model.                                                                   |
| window static method | `createWindow(config: Configuration): Window`                              | Creates a sub-window or system window.<br/>- `config`: Parameters for creating the window.                                                        |
| Window        | `setWindowBrightness(brightness: Float32): Unit`                           | Sets the screen brightness value.                                                                                                                 |
| Window        | `setWindowTouchable(isTouchable: Bool): Unit`                              | Sets whether the window is touchable. `true` means touchable; `false` means non-touchable.                                                        |
| Window        | `moveWindowTo(x: Int32, y: Int32): Unit`                                   | Moves the current window position.                                                                                                                |
| Window        | `resize(width: UInt32, height: UInt32): Unit`                              | Changes the current window size.                                                                                                                  |
| Window        | `setWindowLayoutFullScreen(isLayoutFullScreen: Bool): Unit`                | Sets whether the layout of the main window or sub-window is an immersive layout. `true` means immersive layout; `false` means non-immersive layout.|
| Window        | `setWindowSystemBarEnable(names: Array<SystemBarType>): Unit`              | Sets the visibility mode of the status bar and three-key navigation bar for the main window. The status bar is controlled by `status`, and the navigation bar by `navigation`.<br>For example, setting this parameter to `[SystemBarType.Status, SystemBarType.Navigation]` displays both; setting it to `[]` displays neither. |
| Window        | `setWindowSystemBarProperties(systemBarProperties: SystemBarProperties): Unit` | Sets the properties of the navigation bar and status bar within the window.<br/>`systemBarProperties`: The collection of properties for the navigation bar and status bar. |
| Window        | `func showWindow(): Unit`                                                  | Displays the current window.                                                                                                                      |
| Window        | `func destroyWindow(): Unit`                                               | Destroys the current window.                                                                                                                      |

## Setting Up the Main Application Window

In the `Stage` model, the main application window is created and its lifecycle is maintained by the `UIAbility`. In the `onWindowStageCreate` callback of the `UIAbility`, the main application window can be obtained via `WindowStage`, allowing for operations like property setting. Attributes of the main application window, such as `maxWindowWidth`, can also be set in the application configuration file. For details, refer to [abilities tag in the module.json5 configuration file](../../../en/application-dev/cj-start/basic-knowledge/module-configuration-file.md#abilities-tag).

### Development Steps

1.  Get the main application window.
    Use the `getMainWindow` interface to get the main application window.

2.  Set the main window properties.
    Properties such as background color, brightness, and touchability can be set. Developers can choose the corresponding interface as needed. This example sets the "touchable" property.

3.  Load the target page for the main window.
    Use the `loadContent` interface to load the target page for the main window.

```cangjie
package ohos_app_cangjie_entry

internal import kit.AbilityKit.*
internal import kit.ArkUI.*

class MainAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        // 1. Get the main application window.
        let mainWindow: Window = windowStage.getMainWindow()
        // 2. Set main window properties. Using "touchable" property as an example.
        mainWindow.setWindowTouchable(false) // Corrected variable name from 'window' to 'mainWindow'
        // 3. Load the target page for the main window.
        windowStage.loadContent("EntryView")
    }
}
```

## Setting Up Application Sub-Windows

Developers can create application sub-windows, such as pop-ups, as needed, and perform operations like property setting.

> **Note:**
> The following scenarios are not recommended for using sub-windows. It is recommended to prioritize using the control [overlay](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-overlay.md) capability instead.
> - On mobile devices (phones), sub-windows cannot exceed the boundaries of the main window when it is in floating or split-screen mode, similar to controls.
> - In split-screen and free window modes, controls have better real-time following capability regarding changes in the main window's position and size compared to sub-windows.
> - On some device platforms, due to actual system configuration limitations, sub-windows only have system-default animations and rounded corners/shadows, which cannot be set by the application, resulting in low flexibility.

### Development Steps

1.  Create an application sub-window.
    Use the `createSubWindow` interface to create an application sub-window.

2.  Set sub-window properties.
    After the sub-window is successfully created, you can change its size, position, etc., and also set properties like background color and brightness according to application needs.
    It is recommended to set the size and position of the sub-window before calling `showWindow`.
    If the sub-window size is not set, after calling `showWindow`:
    + In free window state, the default sub-window size is the current physical screen size.
    + In non-free window state, the default sub-window size is the main window size.

3.  Load and display the specific content of the sub-window.
    Use the `showWindow` interface to load and display the specific content of the sub-window.

4.  Destroy the sub-window.
    When certain sub-windows are no longer needed, use the `destroyWindow` interface to destroy them based on specific logic.

Complete sample code for creating a sub-window directly within `onWindowStageCreate`:

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
        // Developers can create sub-windows at an appropriate time, such as a button click event on the main window. It doesn't necessarily need to be called in onWindowStageCreate; shown here for demonstration only.
        // 1. Create an application sub-window.
        let subWindow = windowStage.createSubWindow("mySubWindow")
        // 2. After successful creation, set the sub-window's position, size, and related properties.
        subWindow.getOrThrow().moveWindowTo(300, 300)
        subWindow.getOrThrow().resize(500, 500)
        // 3. Show the sub-window.
        subWindow.getOrThrow().showWindow()
    }

    public override func onWindowStageDestroy(): Unit {
        // Developers can destroy the sub-window at an appropriate time, such as a close button click on the sub-window. It doesn't necessarily need to be called in onWindowStageDestroy; shown here for demonstration only.
        // 4. Destroy the sub-window. When it's no longer needed, use destroyWindow to destroy it based on specific logic.
        if (!subWindow.isSome()) {
            return
        }
        subWindow.getOrThrow().destroyWindow()
    }
}
```

Alternatively, you can create a sub-window by clicking a button on a page. Complete sample code:

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
                            // 1. Create an application sub-window.
                            subWindow = windowStage.getOrThrow().createSubWindow("mySubWindow")
                            // 2. After successful creation, set the sub-window's position, size, and related properties.
                            subWindow.getOrThrow().moveWindowTo(300, 300)
                            subWindow.getOrThrow().resize(500, 500)
                            // 3. Show the sub-window.
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
                            // 4. Destroy the sub-window. When it's no longer needed, use destroyWindow to destroy it based on specific logic.
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

In scenarios like watching videos or playing games, users often want to hide unnecessary system windows like the status bar and navigation bar for a more immersive experience. This can be achieved using the window immersive capability (which applies to the main application window). Starting from API version 10, immersive windows are configured by default to full-screen size with the layout controlled by the component module. The status bar and navigation bar background color is transparent, and the text color is black. The application window calls the `setWindowLayoutFullScreen` interface. Setting it to `true` means the component module controls the layout, ignoring the status bar and navigation bar for an immersive full-screen layout. Setting it to `false` means the component module controls the layout, avoiding the status bar and navigation bar for a non-immersive full-screen layout.

> **Note:**
> Current immersive interface development only supports configuration at the window level, not at the Page level. If Page-level switching is needed, you can set the immersive mode at the beginning of the page lifecycle, for example in `onPageShow`, and then restore the default settings when the page exits, for example in `onPageHide`.

### Development Steps

1.  Get the main application window.
    Use the `getMainWindow` interface to get the main application window.

2.  Implement the immersive effect. There are two ways:
    - **Method 1**: When the main application window is in full-screen mode, call the `setWindowSystemBarEnable` interface and set the navigation bar and status bar to not display, thus achieving the immersive effect.
    - **Method 2**: Call the `setWindowLayoutFullScreen` interface to set the main application window to a full-screen layout. Then call the `setWindowSystemBarProperties` interface to set properties like transparency, background/text color, and highlight icons for the navigation bar and status bar, ensuring they coordinate with the main window display, thus achieving the immersive effect.

3.  Load and display the specific content for the immersive window.
    Use the `loadContent` interface to load the specific content for the immersive window.

```cangjie
package ohos_app_cangjie_entry

internal import kit.AbilityKit.*
internal import kit.ArkUI.*

class MainAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        // 1. Get the main application window.
        let mainWindow: Window = windowStage.getMainWindow()
        // 2. Implement immersive effect. Method 1: Set the navigation bar and status bar to not display.
        mainWindow.setWindowSystemBarEnable([])
        // 2. Implement immersive effect. Method 2: Set the window to full-screen layout, and coordinate the properties of the navigation bar and status bar.
        mainWindow.setWindowLayoutFullScreen(true)
        let sysBarProps: SystemBarProperties = SystemBarProperties(
                                                statusBarColor: "#ff00ff",
                                                navigationBarColor: "#00ff00",
                                                statusBarContentColor: "#ffffff",
                                                navigationBarContentColor: "#ffffff")
        mainWindow.setWindowSystemBarProperties(sysBarProps)
        // 3. Load the target page for the immersive window.
        windowStage.loadContent("EntryView")
    }
}
```

## Setting Up Floating Windows

A floating window can create a window that always stays in the foreground on top of an existing task. Even if the task that created the floating window moves to the background, the floating window can still be displayed in the foreground. Typically, floating windows are located above all application windows. Developers can create floating windows and perform operations like property setting.

### Development Steps

**Prerequisite:** Creating a window of type `WindowType.TypeFloat` (i.e., a floating window) requires applying for the `ohos.permission.SYSTEM_FLOAT_WINDOW` permission. For configuration methods, please refer to [How system_basic level applications apply for permissions](../../../en/application-dev/security/AccessToken/cj-determine-application-mode.md#how-system_basic-level-applications-apply-for-permissions).

1.  Create a floating window.
    Use the `createWindow` interface to create a window of the floating type.

2.  Perform operations like property setting on the floating window.
    After the floating window is successfully created, you can change its size, position, etc., and also set properties like background color and brightness according to application needs.

3.  Load and display the specific content of the floating window.
    Use the `showWindow` interface to load and display the specific content of the floating window.

4.  Destroy the floating window.
    When the floating window is no longer needed, use the `destroyWindow` interface to destroy it based on specific logic.

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
        // 2. After successful creation, set the floating window's position, size, and related properties.
        windowClass.moveWindowTo(300, 300)
        windowClass.resize(500, 500)
        // 3. Show the floating window.
        windowClass.showWindow()
        // 4. Destroy the floating window. When it's no longer needed, use destroyWindow to destroy it based on specific logic.
        windowClass.destroyWindow()
    }
}
```