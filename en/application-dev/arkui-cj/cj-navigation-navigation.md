# Component Navigation (Navigation) (Recommended)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The Navigation component is primarily used to implement page navigation between pages and within components. It supports passing navigation parameters between different components and provides flexible navigation stack operations, enabling more convenient access and reuse of different pages. This document will provide a detailed introduction to the Navigation component from several aspects, including routing operations, subpage management, and transition animations.

[Navigation](../reference/arkui-cj/cj-navigation-switching-navigation.md) serves as the root view container for route navigation and is typically used as the root container for pages (@Entry). The Navigation component is suitable for route switching within modules, offering a more natural and smooth transition experience through component-level routing capabilities. It also provides various title bar styles to deliver better title and content interaction effects. In the "Write Once, Deploy Anywhere" scenario, the Navigation component can automatically adapt to window display sizes and switch to a split-column display effect in larger window scenarios.

The Navigation component mainly consists of a navigation page and subpages. The navigation page includes a title bar (with a menu bar), content area, and toolbar. The navigation page does not exist in the page stack. Switching between the navigation page and subpages, as well as between subpages, can be achieved through routing operations.

It is recommended to use [NavPathStack](../reference/arkui-cj/cj-navigation-switching-navigation.md#class-navpathstack) for page routing.

## Routing Operations

Navigation routing-related operations are based on methods provided by the page stack [NavPathStack](../reference/arkui-cj/cj-navigation-switching-navigation.md#class-navpathstack). Each Navigation component needs to create and pass a NavPathStack object to manage pages. This primarily involves functions such as page navigation and page return.

> **Note:**
>
> It is not recommended for developers to manage their own page stacks by listening to lifecycle events.

```cangjie
@Entry
@Component
class EntryView {
    // Create a page stack object and pass it to Navigation
    var pageStack: NavPathStack = NavPathStack()
    func build(){
        Navigation(this.pageStack) {
        }
    }
}
```

### Page Navigation

NavPathStack implements page navigation functionality through Push-related interfaces, primarily navigating by page name and optionally carrying parameters.

```cangjie
this.pageStack.pushPath(NavPathInfo(name: 'PageOne', param: 'PageOne Param'))
```

### Page Return

NavPathStack implements page return functionality through Pop-related interfaces.

```cangjie
// Return to the previous page
this.pageStack.pop()
```

## Subpages

[NavDestination](../reference/arkui-cj/cj-navigation-switching-navdestination.md) is the root container for subpages of Navigation, used to carry special attributes and lifecycle events of subpages.

## Page Transitions

Navigation provides default transition animations for page switching. Different transition effects are triggered during page stack operations. Navigation also offers the ability to disable system transitions, customize transitions, and implement shared element transitions.

### Shared Element Transition

When switching between NavDestinations, shared element transitions can be achieved using [geometryTransition](../reference/arkui-cj/cj-animation-geometrytransition.md#func-geometryTransition). Pages configured for shared element transitions must also disable the system's default transition animation.

1. Add the geometryTransition property to the components that require shared element transitions. The id parameter must remain consistent between the two NavDestinations.

    ```cangjie
    // Configure shared element ID on the source page
    // ...
    @Component
    class PageOne {
        func build() {
            NavDestination() {
                Column() {
                    // ...
                    Image(@r(app.media.startIcon))
                        .geometryTransition('sharedId')
                        .width(200)
                        .height(200)
                }
            }
        }
    }

    // Configure shared element ID on the destination page
    // ...  
    @Component
    class PageTwo {
        func build() {
            NavDestination() {
                Column() {
                    // ...
                    Image(@r(app.media.startIcon))
                        .geometryTransition('sharedId')
                        .width(200)
                        .height(200)
                }
            }
        }
    }
    ```

2. Place the page routing operation within the animateTo animation closure and configure the corresponding animation parameters.

    ```cangjie
    @Component
    class PageOne {
        func build() {
            NavDestination() {
                Column() {
                    Button('Navigate to Destination Page')
                    .width(80.percent)
                    .height(40)
                    .margin(20)
                    .onClick({ => animateTo(AnimateParam(duration: 1200),
                        { => this.pageStack.pushPath(NavPathInfo(name: "PageTwo", param: "information"))})
                    })
                }
            }
        }
    }
    ```