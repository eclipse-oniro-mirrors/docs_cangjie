# Page Transition (pageTransition)

When switching routes, you can customize the transition effects for page entry and exit by defining them in the `pageTransition` function.

> **Note:**
>
> For better transition effects, it is recommended to use the Navigation component and [Modal Transition](../../../en/application-dev/arkui-cj/cj-modal-transition.md).

## Import Module

```cangjie
import kit.ArkUI.*
```

## class CommonTransition

```cangjie
sealed abstract class CommonTransition {}
```

**Function:** Base class for common page transition effects.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func opacity(Float64)

```cangjie
public func opacity(value: Float64): This
```

**Function:** Sets the starting opacity value for entry or the ending opacity value for exit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type      | Required | Default | Description                                      |
|:----------|:---------|:--------|:--------|:------------------------------------------------|
| value     | Float64  | Yes     | -       | Starting opacity value for entry or ending opacity value for exit.<br>Range: [0.0, 1.0]. |

### func scale(Float32, Float32, Float32, Length, Length)

```cangjie
public func scale(
    x!: Float32 = 1.0,
    y!: Float32 = 1.0,
    z!: Float32 = 1.0,
    centerX!: Length = 50.percent,
    centerY!: Length = 50.percent
): This
```

**Function:** Sets the scaling effect during page transitions.

> **Note:**
>
> The parameters represent the starting values for entry and ending values for exit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type                                              | Required | Default        | Description                                                                 |
|:----------|:-------------------------------------------------|:--------|:---------------|:----------------------------------------------------------------------------|
| x         | Float32                                          | No      | 1.0            | **Named parameter.** Horizontal scaling factor (or shrinking ratio).        |
| y         | Float32                                          | No      | 1.0            | **Named parameter.** Vertical scaling factor (or shrinking ratio).         |
| z         | Float32                                          | No      | 1.0            | **Named parameter.** Depth scaling factor (or shrinking ratio).             |
| centerX   | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No      | 50.percent     | **Named parameter.** X-axis scaling center point. Defaults to the page center.<br>(0, 0) represents the top-left corner of the page. |
| centerY   | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No      | 50.percent     | **Named parameter.** Y-axis scaling center point. Defaults to the page center.<br>(0, 0) represents the top-left corner of the page. |

### func slide(SlideEffect)

```cangjie
public func slide(value: SlideEffect): This
```

**Function:** Sets the slide-in/slide-out effect during page transitions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type                               | Required | Default | Description                   |
|:----------|:----------------------------------|:--------|:--------|:------------------------------|
| value     | [SlideEffect](#enum-slideeffect)  | Yes     | -       | Slide-in/slide-out effect for page transitions. |

### func translate(Length, Length, Length)

```cangjie
public func translate(x!: Length = 0.vp, y!: Length = 0.vp, z!: Length = 0.vp): This
```

**Function:** Sets the translation effect during page transitions.

> **Note:**
>
> The parameters represent the starting values for entry and ending values for exit. If both `slide` and `translate` are set, `slide` takes precedence by default.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type                                              | Required | Default | Description               |
|:----------|:-------------------------------------------------|:--------|:--------|:--------------------------|
| x         | [Length](../BasicServicesKit/cj-apis-base.md#interface-length)| No      | 0.vp    | **Named parameter.** X-axis translation distance. |
| y         | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No      | 0.vp    | **Named parameter.** Y-axis translation distance. |
| z         | [Length](../BasicServicesKit/cj-apis-base.md#interface-length)| No      | 0.vp    | **Named parameter.** Z-axis translation distance. |

## class PageTransitionEnter

```cangjie
public class PageTransitionEnter <: CommonTransition {
    public init(
        routeType!: RouteType = RouteType.None,
        duration!: Int32 = 1000,
        curve!: Curve = Curve.Linear,
        delay!: Int32 = 0
    )
}
```

**Function:** Custom entry animation type for the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [CommonTransition](#class-commontransition)

### init(RouteType, Int32, Curve, Int32)

```cangjie
public init(
    routeType!: RouteType = RouteType.None,
    duration!: Int32 = 1000,
    curve!: Curve = Curve.Linear,
    delay!: Int32 = 0
)
```

**Function:** Creates a custom entry animation object for the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter  | Type                                       | Required | Default          | Description                                                                                                      |
|:-----------|:------------------------------------------|:--------|:----------------|:-----------------------------------------------------------------------------------------------------------------|
| routeType  | [RouteType](#enum-routetype)              | No      | RouteType.None  | **Named parameter.** Route type for which the transition effect applies.                                         |
| duration   | Int32                                     | No      | 1000            | **Named parameter.** Animation duration.<br>Unit: milliseconds.<br>Range: [0, +∞).                              |
| curve      | [Curve](./cj-common-types.md#enum-curve)  | No      | Curve.Linear    | **Named parameter.** Animation curve.                                                                            |
| delay      | Int32                                     | No      | 0               | **Named parameter.** Animation delay duration.<br>Unit: milliseconds.<br>**Note:**<br>If no match is found, the system default page transition effect is used (may vary by device). To disable the default effect, set `duration` to 0. |

### func onEnter(PageTransitionCallback)

```cangjie
public func onEnter(event: PageTransitionCallback)
```

**Function:** Frame-by-frame callback until the entry animation completes, with `progress` ranging from 0 to 1.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type                                                          | Required | Default | Description                                |
|:----------|:-------------------------------------------------------------|:--------|:--------|:-------------------------------------------|
| event     | [PageTransitionCallback](#type-pagetransitioncallback) | Yes     | -       | Frame-by-frame callback until the entry animation completes, with `progress` ranging from 0 to 1. |

## class PageTransitionExit

```cangjie
public class PageTransitionExit <: CommonTransition {
    public init(
        routeType!: RouteType = RouteType.None,
        duration!: Int32 = 1000,
        curve!: Curve = Curve.Linear,
        delay!: Int32 = 0
    )
}
```

**Function:** Custom exit animation type for the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [CommonTransition](#class-commontransition)

### init(RouteType, Int32, Curve, Int32)

```cangjie
public init(
    routeType!: RouteType = RouteType.None,
    duration!: Int32 = 1000,
    curve!: Curve = Curve.Linear,
    delay!: Int32 = 0
)
```

**Function:** Creates a custom exit animation object for the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter  | Type                                       | Required | Default          | Description                                                                                                      |
|:-----------|:------------------------------------------|:--------|:----------------|:-----------------------------------------------------------------------------------------------------------------|
| routeType  | [RouteType](#enum-routetype)              | No      | RouteType.None  | **Named parameter.** Route type for which the transition effect applies.                                         |
| duration   | Int32                                     | No      | 1000            | **Named parameter.** Animation duration.<br>Unit: milliseconds.<br>Range: [0, +∞).                              |
| curve      | [Curve](./cj-common-types.md#enum-curve)  | No      | Curve.Linear    | **Named parameter.** Animation curve.                                                                            |
| delay      | Int32                                     | No      | 0               | **Named parameter.** Animation delay duration.<br>Unit: milliseconds.<br>**Note:**<br>If no match is found, the system default page transition effect is used (may vary by device). To disable the default effect, set `duration` to 0. |

### func onExit(PageTransitionCallback)

```cangjie
public func onExit(event: PageTransitionCallback)
```

**Function:** Frame-by-frame callback until the exit animation completes, with `progress` ranging from 0 to 1.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type      | Required | Default | Description                                |
|:----------|:-------------------------------------------------------------|:--------|:--------|:-------------------------------------------|
| event     | [PageTransitionCallback](#type-pagetransitioncallback) | Yes     | -       | Frame-by-frame callback until the exit animation completes, with `progress` ranging from 0 to 1. |

## enum RouteType

```cangjie
public enum RouteType {
    | None
    | Push
    | Pop
}
```

**Function:** Page route types.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### None

```cangjie
None
```

**Function:** Indicates the page is not redirected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Pop

```cangjie
Pop
```

**Function:** Redirects to a specified page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Push

```cangjie
Push
```

**Function:** Navigates to the next page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

## enum SlideEffect

```cangjie
public enum SlideEffect {
    | Left
    | Right
    | Top
    | Bottom
}
```

**Function:** Page slide effect types.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Bottom

```cangjie
Bottom
```

**Function:** For entry, slides in from the bottom; for exit, slides out to the bottom.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Left

```cangjie
Left
```

**Function:** For entry, slides in from the left; for exit, slides out to the left.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Right

```cangjie
Right
```

**Function:** For entry, slides in from the right; for exit, slides out to the right.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Top

```cangjie
Top
```

**Function:** For entry, slides in from the top; for exit, slides out to the top.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

## type PageTransitionCallback

```cangjie
public type PageTransitionCallback = (RouteType, Float64) -> Unit
```

**Function:** [PageTransitionCallback](#type-pagetransitioncallback) is an alias for [(RouteType, Float64) -> Unit](#type-pagetransitioncallback).

## Example Code

### Example Code 1 (Setting Entry/Exit Animations)

Configure different entry and exit animations based on different route types.

<!-- run -->

```cangjie
//index.cj
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*
import ohos.arkui.ui_context.*

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
        .onClick {
                e => getUIContext().getRouter().pushUrl(url: "Page1")
            }
    }

    protected func onTransition(): Unit {
        PageTransitionEnter(duration: 1200, curve: Curve.Linear,).onEnter {
            ty: RouteType, progress: Float64 => match (ty) {
                case RouteType.Push | RouteType.Pop =>
                    scale2 = Float32(progress)
                    opacity2 = progress
                case _ => ()
            }
        }
        PageTransitionExit(duration: 1200, curve: Curve.Ease, ).onExit {
            ty: RouteType, progress: Float64 => match (ty) {
                case RouteType.Push =>
                    this.scale2 = Float32(1.0 - progress)
                    this.opacity2 = 1.0 - progress
                case _ => ()
            }
        }
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
import ohos.arkui.ui_context.*

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
        .onClick {
                e => getUIContext().getRouter().pushUrl(url: "EntryView")
            }
    }

    protected func onTransition(): Unit {
        PageTransitionEnter(duration: 1200, curve: Curve.Linear).onEnter {
            ty: RouteType, progress: Float64 => match (ty) {
                case RouteType.Push | RouteType.Pop =>
                    scale1 = Float32(progress)
                    opacity1 = progress
                case _ => ()
            }
        }
        PageTransitionExit(duration: 1200, curve: Curve.Ease).onExit {
            ty: RouteType, progress: Float64 => match (ty) {
                case RouteType.Push =>
                    this.scale1 = Float32(1.0 - progress)
                    this.opacity1 = 1.0 - progress
                case _ => ()
            }
        }
    }
}
```

![page_transition](figures/pagetransition.gif)### Example Code 2 (Setting Exit Transition Slide Effect)

Configure different exit transition slide effects by changing the system language layout mode to RTL.

<!-- run -->

```cangjie
//index.cj
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*
import ohos.arkui.ui_context.*

@Entry
@Component
class EntryView {
    @State var scale2: Float32 = 1.0
    @State var opacity2: Float64 = 1.0

    func build() {
        Column() {
            Button("Page1").onClick {
                e => getUIContext().getRouter().pushUrl(url: "Page1")
            }
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

    protected func onTransition(): Unit {
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
import kit.LocalizationKit.*
import ohos.arkui.ui_context.*

@Entry
@Component
class Page1 {
    @State var scale1: Float32 = 1.0
    @State var opacity1: Float64 = 1.0

    func build() {
        Column() {
            Button("Page2").onClick {
                e => getUIContext().getRouter().pushUrl(url: "EntryView")
            }
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

    protected func onTransition(): Unit {
        PageTransitionEnter(duration: 1200).slide(SlideEffect.Right)
        PageTransitionExit(duration: 1200).slide(SlideEffect.Right)
    }
}
```

![page_transition2](figures/pagetransition2.gif)