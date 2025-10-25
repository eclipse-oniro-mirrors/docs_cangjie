# Full-Screen Modal Transition

The `bindContentCover` property allows components to be bound to a full-screen modal page. Transition effects can be displayed during component insertion and removal by configuring the `ModalTransition` parameter.

> **Note:**
>
> - Does not support landscape/portrait switching.
> - Does not support route navigation.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func bindContentCover(Bool, CustomBuilder, ContentCoverOptions)

```cangjie
public func bindContentCover(isShow: Bool, builder: CustomBuilder,
    options!: ContentCoverOptions = ContentCoverOptions()): This
```

**Function:** Binds a content overlay layer.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| isShow | Bool | Yes | - | Whether to display. |
| builder | [CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | Custom builder. |
| options | [ContentCoverOptions](#class-contentcoveroptions)) | No | ContentCoverOptions() | Content overlay options. |

## Basic Type Definitions

### class ContentCoverOptions

```cangjie
public class ContentCoverOptions <: BindOptions {
    public init(
        modalTransition!: ModalTransition = ModalTransition.Default,
        onWillDismiss!: ?(DismissContentCoverAction) -> Unit = Option.None,
        transition!: ?TransitionEffect = Option.None,
        backgroundColor!: ?ResourceColor = Option.None,
        onAppear!: ?() -> Unit = Option.None,
        onDisappear!: ?() -> Unit = Option.None,
        onWillAppear!: ?() -> Unit = Option.None,
        onWillDisappear!: ?() -> Unit = Option.None
    )
}
```

**Function:** Full-screen modal page transition.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [BindOptions](./cj-universal-attribute-sheettransition.md#class-bindoptions)

#### init(ModalTransition, ?(DismissContentCoverAction) -> Unit, ?TransitionEffect, ?ResourceColor, ?() -> Unit, ?() -> Unit, ?() -> Unit, ?() -> Unit)

```cangjie
public init(
    modalTransition!: ModalTransition = ModalTransition.Default,
    onWillDismiss!: ?(DismissContentCoverAction) -> Unit = Option.None,
    transition!: ?TransitionEffect = Option.None,
    backgroundColor!: ?ResourceColor = Option.None,
    onAppear!: ?() -> Unit = Option.None,
    onDisappear!: ?() -> Unit = Option.None,
    onWillAppear!: ?() -> Unit = Option.None,
    onWillDisappear!: ?() -> Unit = Option.None
)
```

**Function:** Constructs a `ContentCoverOptions` object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| modalTransition | [ModalTransition](./cj-common-types.md#enum-modaltransition) | No | ModalTransition.Default | **Named parameter.** Transition method for the full-screen modal page. |
| onWillDismiss | ?([DismissContentCoverAction](./cj-common-types.md#class-dismisscontentcoveraction))->Unit | No | Option.None | **Named parameter.** Callback function for interactive dismissal of the full-screen modal page. |
| transition | ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | Option.None | **Named parameter.** Custom transition method for the full-screen modal page. |
| backgroundColor | ?[ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Option.None | **Named parameter.** Background color of the full-modal page. |
| onAppear | ?()->Unit | No | Option.None | **Named parameter.** Callback function after the full-modal page is displayed (after animation ends). |
| onDisappear | ?()->Unit | No | Option.None | **Named parameter.** Callback function after the full-modal page is dismissed (after animation ends). |
| onWillAppear | ?()->Unit | No | Option.None | **Named parameter.** Callback function before the full-modal page is displayed (before animation starts). |
| onWillDisappear | ?()->Unit | No | Option.None | **Named parameter.** Callback function before the full-modal page is dismissed (before animation starts). |