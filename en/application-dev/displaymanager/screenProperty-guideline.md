# Using Display to Implement Screen Property Queries and State Monitoring

## Scenario Introduction

[Display](../reference/arkui-cj/cj-apis-display.md) screen properties provide basic capabilities for managing device screens, such as obtaining information about the default display device, retrieving information about all display devices, and monitoring plug-and-play behaviors of display devices. Applications can adapt their UI displays based on corresponding screen information, screen state changes, and foldable screen states.

Common usage scenarios for screen properties include:

- Querying screen information: Including screen resolution, physical pixel density, logical pixel density, refresh rate, screen size, screen rotation direction, screen rotation angle, etc. For details, see [Display Properties](../reference/arkui-cj/cj-apis-display.md).
- Monitoring screen state changes, including screen rotation changes, screen resolution changes, and screen refresh rate changes.
- Querying whether the current device is foldable, while supporting monitoring of fold state changes (expanded/folded).

## Interface Description

The commonly used interfaces for screen properties are listed in the table below. For more functions, interface descriptions, and usage, refer to [@ohos.display (Screen Properties)](../reference/arkui-cj/cj-apis-display.md).

| Interface                                                         | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| getAllDisplays(): Array\<Display>                   | Retrieves all current Display objects.             |
| getDefaultDisplaySync(): Display                             | Retrieves the current default Display object.                                  |
| func isFoldable(): Bool                                        | Checks whether the device is foldable. Returns true if the device is foldable, false otherwise.                          |
| on(listenerType: ListenerType, callback: Callback1Argument\<FoldStatus>): Unit | Enables monitoring of fold state changes for foldable devices.                             |
| off(listenerType: ListenerType, callback: Callback1Argument\<FoldStatus>): Unit | Disables monitoring of fold state changes for foldable devices.                             |

## Obtaining Display Objects

A Display object, or screen instance, provides interfaces for screen-related properties and monitoring changes. Currently, there are several ways to obtain a Display object. Developers can choose the appropriate method based on specific scenarios.

- Obtaining the current default Display object: Use the getDefaultDisplaySync() interface.
- Obtaining all current Display objects: Use the getAllDisplays() interface.

Here, we use getDefaultDisplaySync() to obtain the current default Display object as an example:

```cangjie
import ohos.display.*
func getDefaultDisplaySyncExample() {
    try {
        let displayClass: Display = getDefaultDisplaySync()
        println(displayClass.name)
    } catch (exception: Exception) {
        Hilog.error(0, "AppLogCj", exception.toString())
    }
}
// Ensure the Display object (displayClass) is obtained before proceeding with subsequent screen property queries and event/state change monitoring.
```

## Obtaining Screen-Related Properties

1. After ensuring the Display object is obtained (see [Obtaining Display Objects](#obtaining-display-objects)), you can query basic screen information through related properties.

    ```cangjie
    import ohos.display.*

    func getDefaultDisplaySyncExample() {
        try {
            let displayClass: Display = getDefaultDisplaySync()
            // Get screen ID
            Hilog.info(0, "AppLogCj", "The screen Id is ${displayClass.id}.")
            // Get screen refresh rate
            Hilog.info(0, "AppLogCj", "The screen Id is ${displayClass.refreshRate}.")
            // Get screen width
            Hilog.info(0, "AppLogCj", "The screen Id is ${displayClass.width}.")
            // Get screen height
            Hilog.info(0, "AppLogCj", "The screen Id is ${displayClass.height}.")
            // ...
        } catch (exception: Exception) {
            Hilog.error(0, "AppLogCj", exception.toString())
        }
    }
    ```

2. You can also use getCutoutInfo() to obtain information about unusable screen areas such as punch-hole screens, notched screens, and waterfall screens, to better avoid these areas during UI layout.

    ```cangjie
    import ohos.display.*

    func getCutoutInfoExample() {
        try {
            let displayClass = getDefaultDisplaySync()
            let cutout = displayClass.getCutoutInfo()
            println(cutout.boundingRects.size)
        } catch (exception: Exception) {
            Hilog.error(0, "AppLogCj", exception.toString())
        }
    }
    ```

## Monitoring Foldable Device State Changes

1. You can use the display.isFoldable() interface to query whether the current device is foldable.

    ```cangjie
    import ohos.display.*
    func isFoldableExample() {
        try {
            let displayClass = getDefaultDisplaySync()
            var ret: Bool = false
            try {
                ret = isFoldable()
            } catch (exception: Exception) {
                Hilog.error(0, "AppLogCj", exception.toString())
            }
            if (ret) {
                Hilog.info(0, "AppLogCj", "The device is foldable.")
            } else {
                Hilog.info(0, "AppLogCj", "The device is not foldable.")
            }
        } catch (exception: Exception) {
            Hilog.error(0, "AppLogCj", exception.toString())
        }
    }
    ```

2. If the current device is foldable, you can use display.on('foldStatusChange') to enable monitoring of fold state changes. You can use display.off('foldStatusChange') to disable the corresponding monitoring.

    ```cangjie
    import ohos.display.*
    class TestCallback <: Callback1Argument<FoldStatus> {
        public init() {}
        public open func invoke(value: FoldStatus): Unit {
            Hilog.info(0, "AppLogCj", 
                "Display fold status changed, current fold status: " + match (value) {
                    case FoldStatusUnknown => "FoldStatusUnknown"
                    case FoldStatusExpanded => "FoldStatusExpanded"
                    case FoldStatusFolded => "FoldStatusFolded"
                    case FoldStatusHalfFolded => "FoldStatusHalfFolded"
                    case _ => "Failed to get fold status."
                })
        }
    }
    let testCallback = TestCallback()
    // The callback parameter for registering a listener must be passed as an object.
    on(ListenerTypeFoldStatusChange, testCallback)

    // If multiple callbacks are registered via on, disable all callback monitoring simultaneously.
    off(ListenerTypeFoldStatusChange);

    // Disable single callback monitoring.
    off(ListenerTypeFoldStatusChange, testCallback);
    ```