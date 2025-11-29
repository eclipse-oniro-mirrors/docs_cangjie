# Page Transition Animation (Not Recommended)

For better transition effects, it is recommended to use [Modal Transition](./cj-modal-transition.md).

When navigating between two pages where one page disappears and another appears, custom page transition effects can be configured by setting page transition parameters for each page. [Page transition](../reference/arkui-cj/cj-animation-pagetransition.md) effects are defined in the `pageTransition` function, using [PageTransitionEnter](../reference/arkui-cj/cj-animation-pagetransition.md#class-pagetransitionenter) and [PageTransitionExit](../reference/arkui-cj/cj-animation-pagetransition.md#class-pagetransitionexit) to specify the animation effects for page entry and exit.

The `pageTransition` function is:

```cangjie
protected func pageTransition(): Unit {
    PageTransitionEnter()
    PageTransitionExit()
}
```

The interface for `PageTransitionEnter` is:

```cangjie
PageTransitionEnter(routeType: RouteType.None, duration: 1000)
```

The interface for `PageTransitionExit` is:

```cangjie
PageTransitionExit(routeType: RouteType.None, duration: 1000)
```

The above interfaces define the `PageTransitionEnter` and `PageTransitionExit` components, which can specify different page transition effects using properties like `slide`, `translate`, `scale`, and `opacity`. For `PageTransitionEnter`, these effects represent the starting values for entry animations, while for `PageTransitionExit`, they represent the ending values for exit animations, similar to the configuration method for component transitions. Additionally, `PageTransitionEnter` provides the `onEnter` callback for custom entry animations, and `PageTransitionExit` provides the `onExit` callback for custom exit animations.

The `routeType` parameter in these interfaces indicates the route type for which the transition takes effect, which can be confusing for developers. In a page transition, one page exits while another enters. For example, when navigating from Page A to Page B via `router.pushUrl`, Page A exits with an exit animation, and Page B enters with an entry animation. Conversely, when returning from Page B to Page A via `router.back`, Page B exits with an exit animation, and Page A enters with an entry animation. Thus, `PageTransitionEnter` can apply to either a new page entering due to a push operation or an existing page re-entering due to a pop operation. The `routeType` parameter distinguishes between these scenarios, allowing developers to fully customize all types of page transitions.

## `routeType` Configured as RouteType.None

Setting `routeType` to `RouteType.None` means the transition applies to both push and pop operations. The default value for `routeType` is `RouteType.None`.

```cangjie
// page A
protected func pageTransition(): Unit {
    // Define the entry effect: slide in from the left with a duration of 1200ms, applicable to both push and pop operations
    PageTransitionEnter(routeType: RouteType.None, duration: 1200)
        .slide(SlideEffect.Left)
    // Define the exit effect: slide out to the left with a duration of 1000ms, applicable to both push and pop operations
    PageTransitionExit(routeType: RouteType.None, duration: 1000)
        .slide(SlideEffect.Left)
}
```

```cangjie
// page B
protected func pageTransition(): Unit {
    // Define the entry effect: slide in from the right with a duration of 1000ms, applicable to both push and pop operations
    PageTransitionEnter(routeType: RouteType.None, duration: 1000)
        .slide(SlideEffect.Right)
    // Define the exit effect: slide out to the right with a duration of 1200ms, applicable to both push and pop operations
    PageTransitionExit(routeType: RouteType.None, duration: 1200)
        .slide(SlideEffect.Right)
}
```

Assuming the page navigation is configured for multi-instance mode (allowing duplicate pages in the stack), the four possible scenarios and their corresponding transition effects are shown below.

| Routing Operation | Page A Transition Effect | Page B Transition Effect |
|:---|:---|:---|
| `router.pushUrl` from Page A to a new Page B | Page exits: `PageTransitionExit` takes effect, sliding out to the left | Page enters: `PageTransitionEnter` takes effect, sliding in from the right |
| `router.back` from Page B to Page A | Page enters: `PageTransitionEnter` takes effect, sliding in from the left | Page exits: `PageTransitionExit` takes effect, sliding out to the right |
| `router.pushUrl` from Page B to a new Page A | Page enters: `PageTransitionEnter` takes effect, sliding in from the left | Page exits: `PageTransitionExit` takes effect, sliding out to the right |
| `router.back` from Page A to Page B | Page exits: `PageTransitionExit` takes effect, sliding out to the left | Page enters: `PageTransitionEnter` takes effect, sliding in from the right |

If the desired behavior is for pages to always slide in from the right during `pushUrl` and slide out to the right during `back`, the third and fourth scenarios above do not meet this requirement. In such cases, all four transition effects must be explicitly defined.

## `routeType` Configured as RouteType.Push or RouteType.Pop

Setting `routeType` to `RouteType.Push` means the transition applies only to push operations, while `RouteType.Pop` means it applies only to pop operations.

```cangjie
// page A
protected func pageTransition(): Unit {
    // Define the entry effect: slide in from the right with a duration of 1200ms, applicable only to push operations
    PageTransitionEnter(routeType: RouteType.Push, duration: 1200)
        .slide(SlideEffect.Right)
    // Define the entry effect: slide in from the left with a duration of 1200ms, applicable only to pop operations
    PageTransitionEnter(routeType: RouteType.Pop, duration: 1200)
        .slide(SlideEffect.Left)
    // Define the exit effect: slide out to the left with a duration of 1000ms, applicable only to push operations
    PageTransitionExit(routeType: RouteType.Push, duration: 1000)
        .slide(SlideEffect.Left)
    // Define the exit effect: slide out to the right with a duration of 1000ms, applicable only to pop operations
    PageTransitionExit(routeType: RouteType.Pop, duration: 1000)
        .slide(SlideEffect.Right)
}
```

```cangjie
// page B
protected func pageTransition(): Unit {
    // Define the entry effect: slide in from the right with a duration of 1000ms, applicable only to push operations
    PageTransitionEnter(routeType: RouteType.Push, duration: 1000)
        .slide(SlideEffect.Right)
    // Define the entry effect: slide in from the left with a duration of 1000ms, applicable only to pop operations
    PageTransitionEnter(routeType: RouteType.Pop, duration: 1000)
        .slide(SlideEffect.Left)
    // Define the exit effect: slide out to the left with a duration of 1200ms, applicable only to push operations
    PageTransitionExit(routeType: RouteType.Push, duration: 1200)
        .slide(SlideEffect.Left)
    // Define the exit effect: slide out to the right with a duration of 1200ms, applicable only to pop operations
    PageTransitionExit(routeType: RouteType.Pop, duration: 1200)
        .slide(SlideEffect.Right)
}
```

The above code explicitly defines all possible page transition styles. Assuming multi-instance mode is enabled, the four scenarios and their effects are as follows.

| Routing Operation | Page A Transition Effect | Page B Transition Effect |
|:---|:---|:---|
| `router.pushUrl` from Page A to a new Page B | Page exits: `PageTransitionExit` with `RouteType.Push` takes effect, sliding out to the left | Page enters: `PageTransitionEnter` with `RouteType.Push` takes effect, sliding in from the right |
| `router.back` from Page B to Page A | Page enters: `PageTransitionEnter` with `RouteType.Pop` takes effect, sliding in from the left | Page exits: `PageTransitionExit` with `RouteType.Pop` takes effect, sliding out to the right |
| `router.pushUrl` from Page B to a new Page A | Page enters: `PageTransitionEnter` with `RouteType.Push` takes effect, sliding in from the right | Page exits: `PageTransitionExit` with `RouteType.Push` takes effect, sliding out to the left |
| `router.back` from Page A to Page B | Page exits: `PageTransitionExit` with `RouteType.Pop` takes effect, sliding out to the right | Page enters: `PageTransitionEnter` with `RouteType.Pop` takes effect, sliding in from the left |

> **Note:**
>
> - Since each page's transition style can be independently configured, and transitions involve two pages, developers should ensure the transition effects between pages are cohesive, such as maintaining consistent durations.
> - If no matching transition style is defined, the system default transition style will be used.

## Disabling Page Transition for a Specific Page

Setting the transition duration to 0 disables the transition animation for that page.

```cangjie
protected func pageTransition(): Unit {
    PageTransitionEnter(routeType: RouteType.None, duration: 0)
    PageTransitionExit(routeType: RouteType.None, duration: 0)
}
```

## Example Scenario

The following example demonstrates page transition animations using all four transition styles with the [router.pushUrl](../reference/arkui-cj/cj-apis-uicontext-router.md#func-pushurlstringstring) navigation capability.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.resource.*

@Entry
@Component
class EntryView {
    func build() {
        Column() {
            Image(@r(app.media.image1))
                .width(90.percent).height(80.percent)
                .objectFit(ImageFit.Fill)
                .syncLoad(true) // Synchronously load the image so it's ready when the page appears
                .margin(30)

             Row(space: 10){
                Button("pushUrl")
                  .onClick ({ evt =>
                    // Navigate to the next page (push operation)
                    getUIContext().getRouter().pushUrl(url: "Page1")
                  })
                Button("back")
                    .onClick ({ evt =>
                    // Return to the previous page (pop operation)
                    getUIContext().getRouter().back()
                  })
            }.justifyContent(FlexAlign.Center)
        }
        .width(100.percent).height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }

    protected func pageTransition(): Unit {
        // Define the entry effect: slide in from the right with a duration of 1000ms, applicable only to push operations
        PageTransitionEnter(routeType: RouteType.Push, duration: 1000)
            .slide(SlideEffect.Right)
        // Define the entry effect: slide in from the left with a duration of 1000ms, applicable only to pop operations
        PageTransitionEnter(routeType: RouteType.Pop, duration: 1000)
            .slide(SlideEffect.Left)
        // Define the exit effect: slide out to the left with a duration of 1000ms, applicable only to push operations
        PageTransitionExit(routeType: RouteType.Push, duration: 1000)
            .slide(SlideEffect.Left)
        // Define the exit effect: slide out to the right with a duration of 1000ms, applicable only to pop operations
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
import ohos.resource.*

@Entry
@Component
class Page1 {
    func build() {
        Column() {
            Image(@r(app.media.image2))
                .width(90.percent).height(80.percent)
                .objectFit(ImageFit.Fill)
                .syncLoad(true) // Synchronously load the image so it's ready when the page appears
                .margin(30)

             Row(space: 10){
                Button("pushUrl")
                  .onClick ({ evt =>
                    // Navigate to the next page (push operation)
                    getUIContext().getRouter().pushUrl(url: "EntryView")
                  })
                Button("back")
                    .onClick( { evt =>
                    // Return to the previous page (pop operation)
                    getUIContext().getRouter().back()
                  })
            }.justifyContent(FlexAlign.Center)
        }
        .width(100.percent).height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }

    protected func pageTransition(): Unit {
        // Define the entry effect: slide in from the right with a duration of 1000ms, applicable only to push operations
        PageTransitionEnter(routeType: RouteType.Push, duration: 1000)
            .slide(SlideEffect.Right)
        // Define the entry effect: slide in from the left with a duration of 1000ms, applicable only to pop operations
        PageTransitionEnter(routeType: RouteType.Pop, duration: 1000)
            .slide(SlideEffect.Left)
        // Define the exit effect: slide out to the left with a duration of 1000ms, applicable only to push operations
        PageTransitionExit(routeType: RouteType.Push, duration: 1000)
            .slide(SlideEffect.Left)
        // Define the exit effect: slide out to the right with a duration of 1000ms, applicable only to pop operations
        PageTransitionExit(routeType: RouteType.Pop, duration: 1000)
            .slide(SlideEffect.Right)
    }
}
```

![transiton-animation](figures/transition-animation1.gif)

The following example demonstrates page transition animations using `routeType` set to `None`.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.resource.*

@Entry
@Component
class EntryView {
    func build() {
        Column() {
            Image(@r(app.media.image1))
                .width(90.percent).height(80.percent)
                .objectFit(ImageFit.Fill)
                .syncLoad(true) // Synchronously load the image so it's ready when the page appears
                .margin(30)

             Row(space: 10){
                Button("pushUrl")
                  .onClick ({ evt =>
                    // Navigate to the next page (push operation)
                    getUIContext().getRouter().pushUrl(url: "Page1")
                  })
                Button("back")
                    .onClick({ evt =>
                    // Return to the previous page (pop operation)
                    getUIContext().getRouter().back()
                  })
            }.justifyContent(FlexAlign.Center)
        }
        .width(100.percent).height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }

    protected func pageTransition(): Unit {
        // Define the entry effect: slide in from the left with a duration of 1000ms, applicable to both push and pop operations
        PageTransitionEnter(duration: 1000)
            .slide(SlideEffect.Left)
        // Define the exit effect: translate 100vp in x and y directions with opacity reduced to 0, duration 1200ms, applicable to both push and pop operations
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
import ohos.resource.*

@Entry
@Component
class Page1 {
    func build() {
        Column() {
            Image(@r(app.media.image2))
                .width(90.percent).height(80.percent)
                .objectFit(ImageFit.Fill)
                .syncLoad(true) // Synchronously load the image so it's ready when the page appears
                .margin(30)

             Row(space: 10){
                Button("pushUrl")
                  .onClick ({ evt =>
                    // Navigate to the next page (push operation)
                    getUIContext().getRouter().pushUrl(url: "EntryView")
                  })
                Button("back")
                    .onClick ({ evt =>
                    // Return to the previous page (pop operation)
                    getUIContext().getRouter().back()
                  })
            }.justifyContent(FlexAlign.Center)
        }
        .width(100.percent).height(100.percent)
        .alignItems(HorizontalAlign.Center)
    }

    protected func pageTransition(): Unit {
        // Define the entry effect: slide in from the left with a duration of 1200ms, applicable to both push and pop operations
        PageTransitionEnter(duration: 1200)
            .slide(SlideEffect.Left)
        // Define the exit effect: translate 100vp in x and y directions with opacity reduced to 0, duration 1000ms, applicable to both push and pop operations
        PageTransitionExit(duration: 1000)
            .translate(x: 100.0, y: 100.0)
            .opacity(0.0)
    }
}
```

![transiton-animation](figures/transition-animation2.gif)