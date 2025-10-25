# Using Display for Screen Property Queries and Status Monitoring

## Scenario Description

[Display](../../../en/application-dev/reference/arkui-cj/cj-apis-display.md) screen properties provide basic capabilities for managing device screens, such as obtaining information about the default display device, getting information about all display devices, and additionally listening for the plugging and unplugging of display devices. Applications can adapt their UI display based on corresponding screen information, screen status changes, screen folding status, etc.

Common usage scenarios for screen properties include the following:

- Querying screen information: Includes screen resolution, physical pixel density, logical pixel density, refresh rate, screen size, screen rotation direction, screen rotation angle, etc. For details, refer to [Display Properties](../../../en/application-dev/reference/arkui-cj/cj-apis-display.md).
- Monitoring screen status changes, including screen rotation changes, screen resolution changes, screen refresh rate changes, etc.
- Querying whether the current device is a foldable device, while supporting listening for changes in the folding status (expanded/folded).

## Interface Description

The commonly used interfaces for screen properties are listed in the table below. For more features, interface descriptions, and usage, please refer to [@ohos.display (Screen Properties)](../../../en/application-dev/reference/arkui-cj/cj-apis-display.md).

| Interface                                                                 | Description                                                                                  |
| ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `getAllDisplays(): Array<Display>`                                        | Gets all current Display objects.                                                            |
| `getDefaultDisplaySync(): Display`                                        | Gets the current default Display object.                                                     |
| `func isFoldable(): Bool`                                                 | Checks if the device is foldable. `true` means the device is foldable, `false` means it is not. |
| `on(listenerType: ListenerType, callback: Callback1Argument<FoldStatus>): Unit` | Starts listening for fold status changes on foldable devices.                                |
| `off(listenerType: ListenerType, callback: Callback1Argument<FoldStatus>): Unit` | Stops listening for fold status changes on foldable devices.                                 |

## Obtaining a Display Object

The Display object, i.e., a screen instance, provides interfaces related to screen properties and listening for changes. Currently, there are several ways to obtain a Display object. Developers can choose based on specific scenario needs.

- Get the current default Display object: Use the `getDefaultDisplaySync()` interface.
- Get all current Display objects: Use the `getAllDisplays()` interface.

Here is an example using `getDefaultDisplaySync()` to get the current default Display object:

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
// Ensure the Display object (i.e., displayClass) is obtained before proceeding with subsequent queries for related screen property information and event/status change monitoring.
```

## Obtaining Screen-Related Properties

1. After ensuring the Display object is obtained (details can be found in [Obtaining a Display Object](#obtaining-a-display-object)), you can query some basic screen information through its related properties.

    ```cangjie
    import ohos.display.*

    func getDefaultDisplaySyncExample() {
        try {
            let displayClass: Display = getDefaultDisplaySync()
            // Get the screen ID
            Hilog.info(0, "AppLogCj", "The screen Id is ${displayClass.id}.")
            // Get the screen refresh rate
            Hilog.info(0, "AppLogCj", "The screen refresh rate is ${displayClass.refreshRate}.")
            // Get the screen width
            Hilog.info(0, "AppLogCj", "The screen width is ${displayClass.width}.")
            // Get the screen height
            Hilog.info(0, "AppLogCj", "The screen height is ${displayClass.height}.")
            // ...
        } catch (exception: Exception) {
            Hilog.error(0, "AppLogCj", exception.toString())
        }
    }
    ```

2. You can also use `getCutoutInfo()` to get information about unusable screen areas like punch-hole screens, notch screens, waterfall screens, etc., to better avoid these areas during UI layout.

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

## Monitoring Foldable Device Status Changes

1. You can use the `display.isFoldable()` interface to query whether the current device is a foldable device.

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

2. If the current device is a foldable device, you can use `display.on('foldStatusChange')` to start listening for fold status changes. Use `display.off('foldStatusChange')` to stop the corresponding listening.

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
    // The callback parameter for registration should be passed as an object.
    on(ListenerTypeFoldStatusChange, testCallback)

    // If multiple callbacks are registered via `on`, turn off all callback listeners simultaneously with:
    off(ListenerTypeFoldStatusChange);

    // Turn off a single callback listener with:
    off(ListenerTypeFoldStatusChange, testCallback);
    ```