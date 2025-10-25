# Page Transition Animation (Not Recommended)

For better transition effects, it is recommended to use [Modal Transition](./cj-modal-transition.md).

When navigating between two pages where one disappears and another appears, you can configure custom page transition effects by setting page transition parameters for each page. [Page transition](../../../en/application-dev/reference/arkui-cj/cj-animation-pagetransition.md) effects are defined in the pageTransition function, using [PageTransitionEnter](../../../en/application-dev/reference/arkui-cj/cj-animation-pagetransition.md#class-pagetransitionenter) and [PageTransitionExit](../../../en/application-dev/reference/arkui-cj/cj-animation-pagetransition.md#class-pagetransitionexit) to specify animation effects for page entry and exit.

The pageTransition function is:

```cangjie
protected func pageTransition(): Unit {
    PageTransitionEnter()
    PageTransitionExit()
}
```

The PageTransitionEnter interface is:

```cangjie
PageTransitionEnter(routeType: RouteType.None, duration: 1000)
```

The PageTransitionExit interface is:

```cangjie
PageTransitionExit(routeType: RouteType.None, duration: 1000)
```

These interfaces define PageTransitionEnter and PageTransitionExit components, which can specify different page transition effects through slide, translate, scale, and opacity properties. For PageTransitionEnter, these effects represent the starting values during entry; for PageTransitionExit, they represent the ending values during exit, similar to component transition configurations. Additionally, PageTransitionEnter provides the onEnter callback for custom page entry animations, and PageTransitionExit provides the onExit callback for custom page exit animations.

The type parameter in these interfaces indicates the route type that triggers the effect, which can be confusing for developers. In page transitions, one page always exits while another enters. For example:
- When navigating from Page A to Page B via router.pushUrl, Page A exits (exit animation) and Page B enters (entry animation).
- When returning from Page B to Page A via router.back, Page B exits (exit animation) and Page A enters (entry animation).

Thus, PageTransitionEnter can be triggered either by adding a new page (push, stack operation) or by returning to an existing page (back/pop, unstack operation). The type parameter helps distinguish between these scenarios, allowing developers to fully customize all types of page transition effects.

## type Configured as RouteType.None

When type is RouteType.None, the effect applies to both push and pop operations (default value).

```cangjie
// page A
protected func pageTransition(): Unit {
    // Defines page entry effect: slides in from left (1200ms), applies to both push and pop
    PageTransitionEnter(routeType: RouteType.None, duration: 1200)
        .slide(SlideEffect.Left)
    // Defines page exit effect: slides out to left (1000ms), applies to both push and pop
    PageTransitionExit(routeType: RouteType.None, duration: 1000)
        .slide(SlideEffect.Left)
}
```

```cangjie
// page B
protected func pageTransition(): Unit {
    // Defines page entry effect: slides in from right (1000ms), applies to both push and pop
    PageTransitionEnter(routeType: RouteType.None, duration: 1000)
        .slide(SlideEffect.Right)
    // Defines page exit effect: slides out to right (1200ms), applies to both push and pop
    PageTransitionExit(routeType: RouteType.None, duration: 1200)
        .slide(SlideEffect.Right)
}
```

Assuming multi-instance page navigation (allowing duplicate pages in the stack), the four possible scenarios are:

| Routing Operation | Page A Transition | Page B Transition |
|:---|:---|:---|
| router.pushUrl (A → B) | Page A exits (slides left) | Page B enters (slides right) |
| router.back (B → A) | Page A enters (slides left) | Page B exits (slides right) |
| router.pushUrl (B → A) | Page A enters (slides left) | Page B exits (slides right) |
| router.back (A → B) | Page A exits (slides left) | Page B enters (slides right) |

If you want pages to always slide in from the right during pushUrl and slide out to the right during back, scenarios 3 and 4 won't meet requirements. This requires defining all four transition effects explicitly.

## type Configured as RouteType.Push or RouteType.Pop

RouteType.Push applies only to push operations, while RouteType.Pop applies only to pop operations.

```cangjie
// page A
protected func pageTransition(): Unit {
    // Entry effect for push: slides in from right (1200ms)
    PageTransitionEnter(routeType: RouteType.Push, duration: 1200)
        .slide(SlideEffect.Right)
    // Entry effect for pop: slides in from left (1200ms)
    PageTransitionEnter(routeType: RouteType.Pop, duration: 1200)
        .slide(SlideEffect.Left)
    // Exit effect for push: slides out to left (1000ms)
    PageTransitionExit(routeType: RouteType.Push, duration: 1000)
        .slide(SlideEffect.Left)
    // Exit effect for pop: slides out to right (1000ms)
    PageTransitionExit(routeType: RouteType.Pop, duration: 1000)
        .slide(SlideEffect.Right)
}
```

```cangjie
// page B
protected func pageTransition(): Unit {
    // Entry effect for push: slides in from right (1000ms)
    PageTransitionEnter(routeType: RouteType.Push, duration: 1000)
        .slide(SlideEffect.Right)
    // Entry effect for pop: slides in from left (1000ms)
    PageTransitionEnter(routeType: RouteType.Pop, duration: 1000)
        .slide(SlideEffect.Left)
    // Exit effect for push: slides out to left (1200ms)
    PageTransitionExit(routeType: RouteType.Push, duration: 1200)
        .slide(SlideEffect.Left)
    // Exit effect for pop: slides out to right (1200ms)
    PageTransitionExit(routeType: RouteType.Pop, duration: 1200)
        .slide(SlideEffect.Right)
}
```

This code fully defines all possible page transition scenarios. The four possible cases are:

| Routing Operation | Page A Transition | Page B Transition |
|:---|:---|:---|
| router.pushUrl (A → B) | Page A exits (push exit: slides left) | Page B enters (push entry: slides right) |
| router.back (B → A) | Page A enters (pop entry: slides left) | Page B exits (pop exit: slides right) |
| router.pushUrl (B → A) | Page A enters (push entry: slides right) | Page B exits (push exit: slides left) |
| router.back (A → B) | Page A exits (pop exit: slides right) | Page B enters (pop entry: slides left) |

> **Notes:**
>
> - Since each page's transition can be independently configured, developers should ensure smooth transitions between pages (e.g., matching durations).
> - If no matching transition is defined, the system default transition is used.

## Disabling Page Transition for a Page

Set duration to 0 to disable page transition animations.

```cangjie
protected func pageTransition(): Unit {
    PageTransitionEnter(routeType: RouteType.None, duration: 0)
    PageTransitionExit(routeType: RouteType.None, duration: 0)
}
```

## Example Scenarios

Below are examples demonstrating all four transition types using [router.pushUrl](../../../en/application-dev/reference/arkui-cj/cj-apis-router.md#static-func-pushurlstring-string-optionint32---unit).

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*
import ohos.arkui.ui_context.*

@Entry
@Component
class EntryView {
    func build() {
        Column() {
            Image(@r(app.media.background))
                .width(90.percent).height(80.percent)
                .objectFit(ImageFit.Fill)
                .syncLoad(true) // Sync image loading for immediate display
                .margin(30)

             Row(space: 10){
                Button("pushUrl")
                  .onClick { evt =>
                    getUIContext().getRouter().pushUrl(url: "Page1")
                  }
                Button("back")
                    .onClick { evt =>
                    getUIContext().getRouter().back()
                  }
            }.justifyContent(FlexAlign.Center)
        }
        .width(100.percent).height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }

    protected func pageTransition(): Unit {
        // Push entry: slides right (1000ms)
        PageTransitionEnter(routeType: RouteType.Push, duration: 1000)
            .slide(SlideEffect.Right)
        // Pop entry: slides left (1000ms)
        PageTransitionEnter(routeType: RouteType.Pop, duration: 1000)
            .slide(SlideEffect.Left)
        // Push exit: slides left (1000ms)
        PageTransitionExit(routeType: RouteType.Push, duration: 1000)
            .slide(SlideEffect.Left)
        // Pop exit: slides right (1000ms)
        PageTransitionExit(routeType: RouteType.Pop, duration: 1000)
            .slide(SlideEffect.Right)
    }
}
```

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*
import ohos.arkui.ui_context.*

@Entry
@Component
class Page1 {
    func build() {
        Column() {
            Image(@r(app.media.foreground))
                .width(90.percent).height(80.percent)
                .objectFit(ImageFit.Fill)
                .syncLoad(true) // Sync image loading for immediate display
                .margin(30)

             Row(space: 10){
                Button("pushUrl")
                  .onClick { evt =>
                    getUIContext().getRouter().pushUrl(url: "EntryView")
                  }
                Button("back")
                    .onClick { evt =>
                    getUIContext().getRouter().back()
                  }
            }.justifyContent(FlexAlign.Center)
        }
        .width(100.percent).height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }

    protected func pageTransition(): Unit {
        // Push entry: slides right (1000ms)
        PageTransitionEnter(routeType: RouteType.Push, duration: 1000)
            .slide(SlideEffect.Right)
        // Pop entry: slides left (1000ms)
        PageTransitionEnter(routeType: RouteType.Pop, duration: 1000)
            .slide(SlideEffect.Left)
        // Push exit: slides left (1000ms)
        PageTransitionExit(routeType: RouteType.Push, duration: 1000)
            .slide(SlideEffect.Left)
        // Pop exit: slides right (1000ms)
        PageTransitionExit(routeType: RouteType.Pop, duration: 1000)
            .slide(SlideEffect.Right)
    }
}
```

![transiton-animation](figures/transition-animation1.gif)

Below is an example using RouteType.None transitions.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*
import ohos.arkui.ui_context.*

@Entry
@Component
class EntryView {
    func build() {
        Column() {
            Image(@r(app.media.background))
                .width(90.percent).height(80.percent)
                .objectFit(ImageFit.Fill)
                .syncLoad(true) // Sync image loading for immediate display
                .margin(30)

             Row(space: 10){
                Button("pushUrl")
                  .onClick { evt =>
                    getUIContext().getRouter().pushUrl(url: "Page1")
                  }
                Button("back")
                    .onClick { evt =>
                    getUIContext().getRouter().back()
                  }
            }.justifyContent(FlexAlign.Center)
        }
        .width(100.percent).height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }

    protected func pageTransition(): Unit {
        // Entry: slides left (1000ms), applies to both push and pop
        PageTransitionEnter(duration: 1000)
            .slide(SlideEffect.Left)
        // Exit: translates by (100vp, 100vp) with opacity 0 (1200ms), applies to both
        PageTransitionExit(duration: 1200)
            .translate(x: 100.0, y: 100.0)
            .opacity(0.0)
    }
}
```

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*
import ohos.arkui.ui_context.*

@Entry
@Component
class Page1 {
    func build() {
        Column() {
            Image(@r(app.media.foreground))
                .width(90.percent).height(80.percent)
                .objectFit(ImageFit.Fill)
                .syncLoad(true) // Sync image loading for immediate display
                .margin(30)

             Row(space: 10){
                Button("pushUrl")
                  .onClick { evt =>
                    getUIContext().getRouter().pushUrl(url: "EntryView")
                  }
                Button("back")
                    .onClick { evt =>
                    getUIContext().getRouter().back()
                  }
            }.justifyContent(FlexAlign.Center)
        }
        .width(100.percent).height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }

    protected func pageTransition(): Unit {
        // Entry: slides left (1200ms), applies to both push and pop
        PageTransitionEnter(duration: 1200)
            .slide(SlideEffect.Left)
        // Exit: translates by (100vp, 100vp) with opacity 0 (1000ms), applies to both
        PageTransitionExit(duration: 1000)
            .translate(x: 100.0, y: 100.0)
            .opacity(0.0)
    }
}
```

![transiton-animation](figures/transition-animation2.gif)