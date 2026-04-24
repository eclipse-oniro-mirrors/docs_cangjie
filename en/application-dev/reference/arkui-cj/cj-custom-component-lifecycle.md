# Custom Component Lifecycle

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The lifecycle callback functions of custom components are used to notify users about the lifecycle of the custom component. These callback functions are invoked by the development framework at specific times during runtime and cannot be manually called from the application. Do not reuse the same custom component node across multiple windows, as this may cause lifecycle disorder.

> **Note:**
>
> - Asynchronous functions are allowed in lifecycle functions, such as network resource fetching, timer setup, etc.

## func build()

```cangjie
public func build(): Unit
```

**Description:** The `build()` function is used to define the declarative UI description of a custom component. A custom component must define the `build()` function.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## func aboutToAppear()

```cangjie
protected open func aboutToAppear(): Unit
```

**Description:** The `aboutToAppear` function is called after a new instance of the custom component is created and before its `build()` function is executed. State variables can be modified in the `aboutToAppear` function, and the changes will take effect in the subsequent execution of the `build()` function.

> **Note:**
>
> * In this callback function, it is recommended to only perform initialization logic for the current node component and avoid time-consuming operations that may block the main thread. For time-consuming operations, caching or asynchronous solutions are recommended.
> * In scenarios where components are frequently created and destroyed, this callback function will be called frequently.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## func onDidBuild()

```cangjie
protected open func onDidBuild(): Unit
```

**Description:** The `onDidBuild` function is called after the `build()` function of the custom component is executed. Developers can perform non-UI-affecting tasks such as data reporting during this phase. It is not recommended to modify state variables or use functions like `animateTo` in the `onDidBuild` function, as this may lead to unstable UI behavior.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## func aboutToDisappear()

```cangjie
protected open func aboutToDisappear(): Unit
```

**Description:** The `aboutToDisappear` function is executed when the custom component is destructed and destroyed. Modifying state variables in the `aboutToDisappear` function is not allowed, especially changes to `@Link` variables, as this may cause unstable application behavior.

> **Note:**
>
> In scenarios where components are frequently created and destroyed, this callback function will be called frequently.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## func onPageShow()

```cangjie
protected open func onPageShow(): Unit
```

**Description:** Triggered once every time a router page (only for custom components decorated with [`@Entry`](../../arkui-cj/paradigm/cj-create-custom-components.md#entry)) is displayed, including scenarios such as route navigation or the application coming to the foreground.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## func onPageHide()

```cangjie
protected open func onPageHide(): Unit
```

**Description:** Triggered once every time a router page is hidden, including scenarios such as route navigation or the application going to the background.

> **Note:**
>
> In this callback function, it is recommended to avoid time-consuming operations that may block the main thread and cause lag. For time-consuming operations such as camera resource release, asynchronous solutions are recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## func onBackPress()

```cangjie
protected open func onBackPress(): Bool
```

**Description:** Triggered when the user clicks the back button (only effective for router pages). Returning `true` indicates that the page handles the back logic itself without performing page routing. Returning `false` indicates using the default routing back logic. If no return value is set, it is treated as `false`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` to indicate the page handles the back logic itself without performing page routing. Returns `false` to use the default routing back logic. If no return value is set, it is treated as `false`. |

## func aboutToReuse(ReuseParams)

```cangjie
protected open func aboutToReuse(_: ReuseParams): Unit
```

**Description:** When a reusable custom component is re-added to the node tree from the reuse cache, the `aboutToReuse` lifecycle callback is triggered, and the component's construction parameters are passed to `aboutToReuse`.

> **Note:**
>
> - Avoid repeatedly updating state variables that are automatically updated, such as [\@Link](../../arkui-cj/state_management/cj-macro-link.md), [\@Prop](../../arkui-cj/state_management/cj-macro-prop.md) decorated variables, within aboutToReuse().
> - In scrolling scenarios where component reuse is implemented, this callback is typically required to update the component's state variables. As such, avoid performing time-consuming operations within this callback to prevent frame drops and UI stuttering during scrolling animations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [ReuseParams](./cj-common-types.md#class-reuseparams) | Yes | - | The construction parameters of the custom component. |

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
public class EntryView {
    @State
    var switch: Bool = true
    public func build(): Unit {
        Column() {
            Button("Switch")
            .fontSize(50)
            .onClick({e=>
                this.switch = !this.switch
            })
            if (this.switch) {
                Child(message: "Child")
            }
        }
    }
}

@Reusable
@Component
class Child {
    @State
    var message: String = ""

    protected override func aboutToReuse(params: ReuseParams) {
        Hilog.info(0, "TEST", "Child reused")
        if (let Some(value) <- params.get<String>("message")) {
            message = value
        }
    }

    func build() {
        Column(space: 20) {
            Text(this.message).fontSize(20)
        }
    }
}
```

## func aboutToRecycle()

```cangjie
protected open func aboutToRecycle(): Unit
```

**Description:** The lifecycle callback of the component, called before a reusable component is added to the reuse cache from the component tree.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
public class EntryView {
    @State
    var switch: Bool = true
    public func build(): Unit {
        Column() {
            Button("Switch")
            .fontSize(50)
            .onClick({e=>
                this.switch = !this.switch
            })
            if (this.switch) {
                Child(message: "Child")
            }
        }
    }
}

@Reusable
@Component
class Child {
    @State
    var message: String = ""

    protected override func aboutToRecycle(): Unit {
        // This is where you can release memory-intensive content or other non-essential resource references to avoid continuous memory usage that could lead to memory leaks.
        Hilog.info(0, "TEST", "The child enters the recycle pool.")
    }
    
    protected override func aboutToReuse(params: ReuseParams) {
        if (let Some(value) <- params.get<String>("message")) {
            message = value
        }
    }

    func build() {
        Column(space: 20) {
            Text(this.message).fontSize(20)
        }
    }
}
```

## func pageTransition()

```cangjie
protected open func pageTransition(): Unit
```

**Description:** Implements animations when entering this page or navigating to another page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22