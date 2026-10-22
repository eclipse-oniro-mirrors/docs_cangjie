# Page Transition (pageTransition)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

When switching routes ([Router](./cj-apis-uicontext-router.md)), you can customize the page entrance and page exit transition animations in the [pageTransition](./cj-custom-component-lifecycle.md#func-pagetransition) function. For detailed guidance, see [Page Transition Animation](../../arkui-cj/cj-page-transition-animation.md).

> **Note:**
>
> For better transition effects, it is recommended to use the Navigation component and [Modal Transition](../../arkui-cj/cj-modal-transition.md).

## Import Module

```cangjie
import kit.ArkUI.*
```

## class CommonTransition

```cangjie
abstract sealed class CommonTransition {}
```

**Function:** Common page transition animation effects.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### func slide(SlideEffect)

```cangjie
public func slide(value: SlideEffect): This
```

**Function:** Sets the slide-in and slide-out effect for page transition.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [SlideEffect](#enum-slideeffect) | Yes | - | Slide-in and slide-out effect during page transition. |

### func translate(?Length, ?Length, ?Length)

```cangjie
public func translate(x!: ?Length = None, y!: ?Length = None, z!: ?Length = None): This
```

**Function:** Sets the translation effect during page transitions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The translation distance on the x-axis. <br>Value range: (−∞, +∞).<br>Initial value: 0.0.vp. |
| y | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The translation distance on the y-axis. <br>Value range: (−∞, +∞).<br>Initial value: 0.0.vp. |
| z | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The translation distance on the z-axis. <br>Value range: (−∞, +∞).<br>Initial value: 0.0.vp. |

### func scale(?Float32, ?Float32, ?Float32, ?Length, ?Length)

```cangjie
public func scale(
    x!: ?Float32 = None,
    y!: ?Float32 = None,
    z!: ?Float32 = None,
    centerX!: ?Length = None,
    centerY!: ?Length = None
): This
```

**Function:** Sets the scaling effect during page transitions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | ?Float32 | No | None | **Named parameter.** The scaling ratio on the x-axis. When x>1, scale up along the x-axis; when 0<x<1, scale down along the x-axis; when x<0, reflect and scale along the x-axis.<br>Initial value: 1.0. |
| y | ?Float32 | No | None | **Named parameter.** The scaling ratio on the y-axis. When y>1, scale up along the y-axis; when 0<y<1, scale down along the y-axis; when y<0, reflect and scale along the y-axis.<br>Initial value: 1.0. |
| z | ?Float32 | No | None | **Named parameter.** The scaling ratio on the z-axis. When z>1, scale up along the z-axis; when 0<z<1, scale down along the z-axis; when z<0, reflect and scale along the z-axis.<br>Initial value: 1.0. |
| centerX | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The x-coordinate of the transformation center point.<br>Initial value: 50.percent. |
| centerY | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The y-coordinate of the transformation center point.<br>Initial value: 50.percent. |

### func opacity(Float64)

```cangjie
public func opacity(value: Float64): This
```

**Function:** Sets the opacity value at the start of the entrance or at the end of the exit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Sets the opacity value at the start of the entrance or at the end of the exit. Value range: [0.0, 1.0]. 0.0 means fully transparent, 1.0 means fully opaque. |

## class PageTransitionEnter

```cangjie
public class PageTransitionEnter <: CommonTransition {
    public init(
        routeType!: ?RouteType = Option.None,
        duration!: ?Int32 = None,
        curve!: ?Curve = None,
        delay!: ?Int32 = None
    )
}
```

**Function:** The custom entrance animation type for the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parent Type:**

- [CommonTransition](#class-commontransition)

### init(?RouteType, ?Int32, ?Curve, ?Int32)

```cangjie
public init(
    routeType!: ?RouteType = Option.None,
    duration!: ?Int32 = None,
    curve!: ?Curve = None,
    delay!: ?Int32 = None
)
```

**Function:** Creates a custom entrance animation object for the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| routeType | ?[RouteType](#enum-routetype) | No | Option.None | **Named parameter.** The route type for which the page transition effect is applied.<br>Initial value: RouteType.None. |
| duration | ?Int32 | No | None | **Named parameter.** The duration of the animation.<br>Unit: milliseconds.<br>Value range: [0, +∞).<br>Initial value: 1000. |
| curve | ?[Curve](./cj-common-types.md#enum-curve) | No | None | **Named parameter.** The animation curve.<br>Curve.Linear |
| delay | ?Int32 | No | None | **Named parameter.** The delay time of the animation.<br>Unit: milliseconds.<br>Initial value: 1000. |

### func onEnter(?PageTransitionCallback)

```cangjie
public func onEnter(event: ?PageTransitionCallback)
```

**Function:** Frame-by-frame callback until the entrance animation ends, with the transition progress changing from 0 to 1.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | ?[PageTransitionCallback](#type-pagetransitioncallback) | Yes | - | The frame-by-frame callback for the entrance animation until it ends, with the transition progress changing from 0 to 1. |

## class PageTransitionExit

```cangjie
public class PageTransitionExit <: CommonTransition {
    public init(
        routeType!: ?RouteType = Option.None,
        duration!: ?Int32 = None,
        curve!: ?Curve = None,
        delay!: ?Int32 = None
    )
}
```

**Function:** The custom exit animation type for the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parent Type:**

- [CommonTransition](#class-commontransition)

### init(?RouteType, ?Int32, ?Curve, ?Int32)

```cangjie
public init(
    routeType!: ?RouteType = Option.None,
    duration!: ?Int32 = None,
    curve!: ?Curve = None,
    delay!: ?Int32 = None
)
```

**Function:** Creates a custom exit animation object for the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| routeType | ?[RouteType](#enum-routetype) | No | Option.None | **Named parameter.** The route type for which the page transition effect is applied.<br>Initial value: RouteType.None. |
| duration | ?Int32 | No | None | **Named parameter.** The duration of the animation.<br>Unit: milliseconds.<br>Value range: [0, +∞).<br>Initial value: 1000. |
| curve | ?[Curve](./cj-common-types.md#enum-curve) | No | None | **Named parameter.** The animation curve.<br>Curve.Linear |
| delay | ?Int32 | No | None | **Named parameter.** The delay time of the animation.<br>Unit: milliseconds.<br>Initial value: 1000. |

### func onExit(?PageTransitionCallback)

```cangjie
public func onExit(event: ?PageTransitionCallback)
```

**Function:** Frame-by-frame callback until the exit animation ends, with the transition progress changing from 0 to 1.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | ?[PageTransitionCallback](#type-pagetransitioncallback) | Yes | - | The frame-by-frame callback for the exit animation until it ends, with the transition progress changing from 0 to 1. |

## enum RouteType

```cangjie
public enum RouteType <: Equatable<RouteType> {
    | None
    | Push
    | Pop
    | ...
}
```

**Function:** The type of page routing.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parent Type:**

- Equatable\<[RouteType](#enum-routetype)>

### None

```cangjie
None
```

**Function:** The page is not redirected. When RouteType is None as described in Push and Pop, the PageTransitionEnter transition effect applies when the page enters, and the PageTransitionExit transition effect applies when the page exits.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### Push

```cangjie
Push
```

**Function:** Navigates to the next page. PageA navigates to a new page PageB. For PageA, the PageTransitionExit component style with RouteType set to None or Push takes effect; for PageB, the PageTransitionEnter component style with RouteType set to None or Push takes effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### Pop

```cangjie
Pop
```

**Function:** Redirects to the specified page. When returning from PageB to the previous page PageA. For PageB, the PageTransitionExit component style with RouteType set to None or Pop takes effect; for PageA, the PageTransitionEnter component style with RouteType set to None or Pop takes effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### operator func !=(RouteType)

```cangjie
public operator func !=(other: RouteType): Bool
```

**Function:** Compares whether two enumeration values are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RouteType](#enum-routetype) | Yes | - | The other enumeration value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are not equal, otherwise returns false. |

### operator func ==(RouteType)

```cangjie
public operator func ==(other: RouteType): Bool
```

**Function:** Compares whether two enumeration values are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RouteType](#enum-routetype) | Yes | - | The other enumeration value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

## enum SlideEffect

```cangjie
public enum SlideEffect <: Equatable<SlideEffect> {
    | Left
    | Right
    | Top
    | Bottom
    | ...
}
```

**Function:** Slide-in and slide-out effect during page transition.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parent Type:**

- Equatable\<[SlideEffect](#enum-slideeffect)>

### Left

```cangjie
Left
```

**Function:** For entrance, it means sliding in from the left; for exit, it means sliding out to the left.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### Right

```cangjie
Right
```

**Function:** For entrance, it means sliding in from the right; for exit, it means sliding out to the right.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### Top

```cangjie
Top
```

**Function:** For entrance, it means sliding in from the top; for exit, it means sliding out to the top.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### Bottom

```cangjie
Bottom
```

**Function:** For entrance, it means sliding in from the bottom; for exit, it means sliding out to the bottom.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### operator func !=(SlideEffect)

```cangjie
public operator func !=(other: SlideEffect): Bool
```

**Function:** Compares whether two enumeration values are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SlideEffect](#enum-slideeffect) | Yes | - | The other enumeration value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are not equal, otherwise returns false. |

### operator func ==(SlideEffect)

```cangjie
public operator func ==(other: SlideEffect): Bool
```

**Function:** Compares whether two enumeration values are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SlideEffect](#enum-slideeffect) | Yes | - | The other enumeration value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

## type PageTransitionCallback

```cangjie
public type PageTransitionCallback = (RouteType, Float64) -> Unit
```

**Function:** Callback for reporting page transition events.

**Type:** ([RouteType](#enum-routetype), Float64) -> Unit

| Type Parameter | Description |
|:---|:---|
| [RouteType](#enum-routetype) | Page transition type. |
| Float64 | Transition progress, which changes from 0 to 1. |

## Example Code

### Example Code 1 (Configuring Exit/Enter Animations)

Configure different exit and enter animations through different transition types.

<!-- run -->

```cangjie
//index.cj
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    @State var scale2: Float32 = 1.0
    @State var opacity2: Float64 = 1.0

    func build() {
        Column() {
            Image(@r(app.media.background))
                .width(100.percent)
                .height(100.percent)
        }
        .width(100.percent)
        .height(100.percent)
        .scale(x: scale2, y: 1.0)
        .opacity(this.opacity2)
        .onClick({
                e => getUIContext().getRouter().pushUrl(url: "Page1")
            })
    }

    protected func pageTransition(): Unit {
        PageTransitionEnter(duration: 1200, curve: Curve.Linear).onEnter({
            ty: RouteType, progress: Float64 => 
                if (ty == RouteType.Push || ty ==  RouteType.Pop) {
                    scale2 = Float32(progress)
                    opacity2 = progress
                }
        })
        PageTransitionExit(duration: 1200, curve: Curve.Ease).onExit({
            ty: RouteType, progress: Float64 =>
                if (ty == RouteType.Push) {
                    this.scale2 = Float32(1.0 - progress)
                    this.opacity2 = 1.0 - progress
                }
        })
    }
}
```

<!-- run -->

```cangjie
//page1.cj
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*

@Entry
@Component
class Page1 {
    @State var scale1: Float32 = 1.0
    @State var opacity1: Float64 = 1.0

    func build() {
        Column() {
            Image(@r(app.media.background))
                .width(50.percent)
                .height(50.percent)
        }
        .width(100.percent)
        .height(100.percent)
        .scale(x: scale1, y: 1.0)
        .opacity(opacity1)
        .onClick({
                e => getUIContext().getRouter().pushUrl(url: "EntryView")
            })
    }

    protected func pageTransition(): Unit {
        PageTransitionEnter(duration: 1200, curve: Curve.Linear).onEnter({
            ty: RouteType, progress: Float64 => 
                if (ty == RouteType.Push || ty ==  RouteType.Pop) {
                    scale1 = Float32(progress)
                    opacity1 = progress
                }
        })
        PageTransitionExit(duration: 1200, curve: Curve.Ease).onExit({
            ty: RouteType, progress: Float64 => 
                if (ty == RouteType.Push) {
                    this.scale1 = Float32(1.0 - progress)
                    this.opacity1 = 1.0 - progress
                }
        })
    }
}
```

![page_transition](figures/pagetransition.gif)

### Example Code 2 (Configuring Exit/Enter Slide Effects)

Configure different exit/enter slide effects by changing the system language layout mode to RTL.

<!-- run -->

```cangjie
//index.cj
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var scale2: Float32 = 1.0
    @State var opacity2: Float64 = 1.0

    func build() {
        Column() {
            Button("Page1").onClick({
                e => getUIContext().getRouter().pushUrl(url: "Page1")
            })
                .width(200)
                .height(60)
                .fontSize(36)
            Text("START")
                .fontSize(36)
                .textAlign(TextAlign.Center)
        }
        .width(100.percent)
        .height(100.percent)
        .scale(x: scale2, y: 1.0)
        .opacity(this.opacity2)
        .justifyContent(FlexAlign.Center)
    }

    protected func pageTransition(): Unit {
        PageTransitionEnter(duration: 1200, curve: Curve.Linear).slide(SlideEffect.Left)
        PageTransitionExit(duration: 1200, curve: Curve.Ease).slide(SlideEffect.Left)
    }
}
```

<!-- run -->

```cangjie

//page1.cj
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class Page1 {
    @State var scale1: Float32 = 1.0
    @State var opacity1: Float64 = 1.0

    func build() {
        Column() {
            Button("Page2").onClick({
                e => getUIContext().getRouter().pushUrl(url: "EntryView")
            })
                .width(200)
                .height(60)
                .fontSize(36)
            Text("END")
                .fontSize(36)
                .textAlign(TextAlign.Center)
        }
        .width(100.percent)
        .height(100.percent)
        .scale(x: scale1, y: 1.0)
        .opacity(this.opacity1)
        .justifyContent(FlexAlign.Center)
    }

    protected func pageTransition(): Unit {
        PageTransitionEnter(duration: 1200).slide(SlideEffect.Right)
        PageTransitionExit(duration: 1200).slide(SlideEffect.Right)
    }
}
```

![page_transition2](figures/pagetransition2.gif)