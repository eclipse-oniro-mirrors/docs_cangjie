# Custom Component Lifecycle

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

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| _ | [ReuseParams](./cj-common-types.md#class-reuseparams) | Yes | - | The construction parameters of the custom component. |

## func aboutToRecycle()

```cangjie
protected open func aboutToRecycle(): Unit
```

**Description:** The lifecycle callback of the component, called before a reusable component is added to the reuse cache from the component tree.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## func pageTransition()

```cangjie
protected open func pageTransition(): Unit
```

**Description:** Implements animations when entering this page or navigating to another page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22