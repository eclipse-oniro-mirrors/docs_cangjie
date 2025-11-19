# Framework Interfaces

This page documents the public interfaces used by the UI framework. Application developers are prohibited from using these interfaces, as doing so may lead to unexpected results.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func bind((CustomView) -> ViewBuilder, CustomView)

```cangjie
public func bind(builder: (CustomView) -> ViewBuilder, thisView: CustomView)
```

**Function:** Used to bind an @Builder decorated function with a custom component object. For details, see bind function usage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| builder | ([CustomView](#class-customview))->[ViewBuilder](#class-viewbuilder) | Yes | - | @Builder decorated function type. |
| thisView | [CustomView](#class-customview) | Yes | - | Current custom component object (usually `this`). |

## func bind\<T1>((CustomView,ObservedProperty\<T1>) -> ViewBuilder, CustomView)

```cangjie
public func bind<T1>(builder: (CustomView, ObservedProperty<T1>) -> ViewBuilder, thisView: CustomView)
```

**Function:** Used to bind an @Builder decorated function with a custom component object. For details, see bind function usage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| builder | ([CustomView](#class-customview),[ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T1>)->[ViewBuilder](#class-viewbuilder) | Yes | - | @Builder decorated function type. |
| thisView | [CustomView](#class-customview) | Yes | - | Current custom component object (usually `this`). |

## func bind\<T1, T2>((CustomView,ObservedProperty\<T1>,ObservedProperty\<T2>) -> ViewBuilder, CustomView)

```cangjie
public func bind<T1, T2>(builder: (CustomView, ObservedProperty<T1>,
    ObservedProperty<T2>) -> ViewBuilder, thisView: CustomView)
```

**Function:** Used to bind an @Builder decorated function with a custom component object. For details, see bind function usage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| builder | ([CustomView](#class-customview),[ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T1>,[ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T2>)->[ViewBuilder](#class-viewbuilder) | Yes | - | @Builder decorated function type. |
| thisView | [CustomView](#class-customview) | Yes | - | Current custom component object (usually `this`). |

## func bind\<T1, T2, T3>((CustomView,ObservedProperty\<T1>,ObservedProperty\<T2>,ObservedProperty\<T3>) -> ViewBuilder, CustomView)

```cangjie
public func bind<T1, T2, T3>(builder: (CustomView, ObservedProperty<T1>, ObservedProperty<T2>,
    ObservedProperty<T3>) -> ViewBuilder, thisView: CustomView)
```

**Function:** Used to bind an @Builder decorated function with a custom component object. For details, see bind function usage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| builder | ([CustomView](#class-customview),[ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T1>,[ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T2>,[ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T3>)->[ViewBuilder](#class-viewbuilder) | Yes | - | @Builder decorated function type. |
| thisView | [CustomView](#class-customview) | Yes | - | Current custom component object (usually `this`). |

## class RemoteView

```cangjie
public abstract class RemoteView {
    public init()
}
```

**Function:** Base class for components used by the UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init()

```cangjie
public init()
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func build()

```cangjie
public func build(): Unit
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func rerender()

```cangjie
public open func rerender(): Unit
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func purgeVariableDependenciesOnElmtId(Int64)

```cangjie
public func purgeVariableDependenciesOnElmtId(rmElmtId: Int64): Unit
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| rmElmtId | Int64 | Yes | - | - |

### func forceCompleteRerender(Bool)

```cangjie
public func forceCompleteRerender(deep: Bool): Unit
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| deep | Bool | Yes | - | - |

## class CustomView

```cangjie
public abstract class CustomView <: RemoteView {
    public init(parent: Option<CustomView>, localStorage: Option<LocalStorage>)
}
```

**Function:** Base class for components used by the UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Class:**

- [RemoteView](#class-remoteview)

### init(Option\<CustomView>, Option\<LocalStorage>)

```cangjie
public init(parent: Option<CustomView>, localStorage: Option<LocalStorage>)
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| parent | Option\<[CustomView](#class-customview)> | Yes | - | Parent component. |
| localStorage | Option\<[LocalStorage](./cj-state-rendering-appstatemanagement.md#class-localstorage)> | Yes | - | Persistent storage object. |

### func getLocalStorage()

```cangjie
public func getLocalStorage(): LocalStorage
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [LocalStorage](./cj-state-rendering-appstatemanagement.md#class-localstorage) | Persistent storage object. |

### func build()

```cangjie
public func build(): Unit
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func aboutToBeDeleted()

```cangjie
public func aboutToBeDeleted(): Unit
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func getUIContext()

```cangjie
public func getUIContext(): UIContext
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [UIContext](./cj-apis-uicontext-uicontext.md#class-uicontext) | UI context. |

## class ViewBuilder

```cangjie
public class ViewBuilder {
}
```

**Function:** Base class used by the UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## class CJPageEntry

```cangjie
public class CJPageEntry {}
```

**Function:** Used to provide global functions called by Native.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static func getInstance()

```cangjie
public static func getInstance(): CJPageEntry
```

**Function:** Creates and returns a CJPageEntry object.

**Return Value:**

| Type | Description |
|:----|:----|
| [CJPageEntry](#class-cjpageentry) | Corresponding CJPageEntry object. |

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func registerHybridPage(String, CustomView)

```cangjie
public func registerHybridPage(name: String, cjPage: CustomView): Unit
```

**Function:** Registers a hybrid page for UI framework use.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Registration name. |
| cjPage | [CustomView](#class-customview) | Yes | - | Callback function. |

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func removeHybridPage(String)

```cangjie
public func removeHybridPage(name: String): Unit
```

**Function:** Removes the hybrid page with the specified name.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Hybrid page name. |

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22