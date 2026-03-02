# Framework Interfaces

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This page describes the public interfaces used by the UI framework.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func bind((CustomView) -> ViewBuilder, CustomView)

```cangjie
public func bind(builder: (CustomView) -> ViewBuilder, thisView: CustomView): () -> Unit
```

**Function:** Used to bind an @Builder decorated function with a custom component object. For details, see bind function usage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| builder | ([CustomView](#class-customview))->ViewBuilder | Yes | - | [@Builder](../../arkui-cj/paradigm/cj-macro-builder.md) decorated function type. |
| thisView | [CustomView](#class-customview) | Yes | - | Current custom component object (usually `this`). |

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| () -> Unit | Returns the bind function, can used as a builder. |

> **Note:**
>
> bind is recommended when using the [title](./cj-navigation-switching-navdestination.md#func-titlecustombuilder-navigationtitleoptions)、[tabBar](./cj-navigation-switching-tabcontent.md#func-tabbarcustombuilder) attributes, or when constructing [MenuItemGroup](./cj-menu-menuitemgroup.md#initcustombuilder-custombuilder----unit) objects.

## func bind\<T1>((CustomView,ObservedProperty\<T1>) -> ViewBuilder, CustomView)

```cangjie
public func bind<T1>(builder: (CustomView, ObservedProperty<T1>) -> ViewBuilder, thisView: CustomView): (T1) -> Unit
```

**Function:** Used to bind an @Builder decorated function with a custom component object. For details, see bind function usage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| builder | ([CustomView](#class-customview),ObservedProperty\<T1>)->ViewBuilder | Yes | - | [@Builder](../../arkui-cj/paradigm/cj-macro-builder.md) decorated function type. |
| thisView | [CustomView](#class-customview) | Yes | - | Current custom component object (usually `this`). |

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| () -> Unit | Returns the bind function, can used as a builder. |

> **Note:**
>
> bind is recommended when using the [title](./cj-navigation-switching-navdestination.md#func-titlecustombuilder-navigationtitleoptions)、[tabBar](./cj-navigation-switching-tabcontent.md#func-tabbarcustombuilder) attributes, or when constructing [MenuItemGroup](./cj-menu-menuitemgroup.md#initcustombuilder-custombuilder----unit) objects.

## func bind\<T1, T2>((CustomView,ObservedProperty\<T1>,ObservedProperty\<T2>) -> ViewBuilder, CustomView)

```cangjie
public func bind<T1, T2>(
    builder: (CustomView, ObservedProperty<T1>, ObservedProperty<T2>) -> ViewBuilder,
    thisView: CustomView
): (T1, T2) -> Unit
```

**Function:** Used to bind an @Builder decorated function with a custom component object. For details, see bind function usage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| builder | ([CustomView](#class-customview),ObservedProperty\<T1>,ObservedProperty\<T2>)->ViewBuilder | Yes | - | [@Builder](../../arkui-cj/paradigm/cj-macro-builder.md) decorated function type. |
| thisView | [CustomView](#class-customview) | Yes | - | Current custom component object (usually `this`). |

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| () -> Unit | Returns the bind function, can used as a builder. |

> **Note:**
>
> bind is recommended when using the [title](./cj-navigation-switching-navdestination.md#func-titlecustombuilder-navigationtitleoptions)、[tabBar](./cj-navigation-switching-tabcontent.md#func-tabbarcustombuilder) attributes, or when constructing [MenuItemGroup](./cj-menu-menuitemgroup.md#initcustombuilder-custombuilder----unit) objects.

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
| builder | ([CustomView](#class-customview),ObservedProperty\<T1>,ObservedProperty\<T2>,ObservedProperty\<T3>)->ViewBuilder | Yes | - | [@Builder](../../arkui-cj/paradigm/cj-macro-builder.md) decorated function type. |
| thisView | [CustomView](#class-customview) | Yes | - | Current custom component object (usually `this`). |

> **Note:**
>
> bind is recommended when using the [title](./cj-navigation-switching-navdestination.md#func-titlecustombuilder-navigationtitleoptions)、[tabBar](./cj-navigation-switching-tabcontent.md#func-tabbarcustombuilder) attributes, or when constructing [MenuItemGroup](./cj-menu-menuitemgroup.md#initcustombuilder-custombuilder----unit) objects.

## class RemoteView

```cangjie
public abstract class RemoteView {
    public init()
}
```

**Function:** Base class for components used by the UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

> **Note:**
>
> This type is for framework internal use only. Application developers should not use it, as doing so may lead to unexpected behavior.

### init()

```cangjie
public init()
```

**Function:** Construct an object of type RemoteView, which is only effective in UI framework scenarios.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

> **Note:**
>
> This interface is for framework internal use only. Application developers should not call it, as doing so may lead to unexpected behavior.

### func build()

```cangjie
public func build(): Unit
```

**Function:** Used to define the declarative UI description of a custom component. Custom components must define a build() function.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## class CustomView

```cangjie
public abstract class CustomView <: RemoteView {
}
```

**Function:** Base class for components used by the UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Class:**

- [RemoteView](#class-remoteview)

> **Note:**
>
> This type is for framework internal use only. Application developers should not use it, as doing so may lead to unexpected behavior.

### func getLocalStorage()

```cangjie
public func getLocalStorage(): LocalStorage
```

**Function:** Retrieves the LocalStorage instance. For UI framework use only.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [LocalStorage](./cj-state-rendering-appstatemanagement.md#class-localstorage) | Persistent storage object. |

> **Note:**
>
> This interface is for framework internal use only. Application developers should not call it, as doing so may lead to unexpected behavior.

### func build()

```cangjie
public func build(): Unit
```

**Function:** Used to define the declarative UI description of a custom component. Custom components must define a build() function.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func aboutToBeDeleted()

```cangjie
public func aboutToBeDeleted(): Unit
```

**Function:** Automatically triggered by the framework during the component destruction phase. For UI framework use only.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

> **Note:**
>
> This interface is for framework internal use only. Application developers should not call it, as doing so may lead to unexpected behavior.

### func getUIContext()

```cangjie
public func getUIContext(): UIContext
```

**Function:** Obtains the UIContext object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [UIContext](./cj-apis-uicontext-uicontext.md#class-uicontext) | UI context. |

> **Note:**
>
> This interface is for framework internal use only. Application developers should not call it, as doing so may lead to unexpected behavior.
