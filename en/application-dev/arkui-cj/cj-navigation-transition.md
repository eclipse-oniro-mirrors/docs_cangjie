# Navigation Transition

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Navigation transition refers to the route transition method between pages, which is the animation effect where one interface disappears and another appears.

It is recommended to use the [Navigation](../reference/arkui-cj/cj-navigation-switching-navigation.md) component for navigation transitions, which can be combined with the [NavDestination](../reference/arkui-cj/cj-navigation-switching-navdestination.md) component to implement navigation functionality.

## Creating Navigation Pages

Implementation steps:

1. Use Navigation to create the main navigation page and establish a route stack NavPathStack to enable jumps between different pages.

2. Add a List component within Navigation to define different primary interfaces on the main navigation page.

3. Add an onClick method to components within the List, and use the pushPath method of the route stack NavPathStack to enable components to jump from the current page to the corresponding page specified by the input parameter name in the route table upon clicking.

<!-- run -navigation -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.arkui.state_management.*

@Builder
func pageMap(name: String, param: Any) {
    if (name == "PageOne") {
        PageOne()
    } else {
        PageTwo()
    }
}

@Entry
@Component
class EntryView {
     @Provide var pathInfos: NavPathStack = NavPathStack()
     @State var listArray1: Array<String> = ['WLAN', 'Bluetooth']
     @State var listArray2: Array<String> = ['Personal Hotspot', 'Connect & Share']
     func build() {
        Column() {
            Navigation(this.pathInfos) {
        // Define primary navigation interfaces via List
                Search(placeholder: 'Enter keywords to search')
                .width(90.percent)
                .height(40)
                .margin(top: 40, bottom: 15)

                List(initialIndex: 0) {
                    ForEach(this.listArray1, itemGeneratorFunc: {item: String, _:Int64 =>
                        ListItem() {
                            Row() {
                                Row() {
                                    Text('${item.split("")[0]}')
                                    .fontColor(Color.White)
                                    .fontSize(14)
                                    .fontWeight(FontWeight.Bold)
                                }
                                .width(30)
                                .height(30)
                                .backgroundColor(Color.Gray)
                                .margin( right: 20 )
                                .borderRadius(20)
                                .justifyContent(FlexAlign.Center)

                                Column() {
                                    Text(item)
                                    .fontSize(16)
                                    .margin(5)
                                }
                                .alignItems(HorizontalAlign.Start)

                                Blank()

                                Row()
                                .width(12)
                                .height(12)
                                .margin(15)
                                .border(width: 2.px, color: 0xCCCCCC)
                            }
                            .borderRadius(15)
                            .shadow(radius: 100.0, color: 0xededed)
                            .width(90.percent)
                            .alignItems(VerticalAlign.Center)
                            .padding( left: 15, top: 15, bottom: 15 )
                            .backgroundColor(Color.White)
                        }
                        .width(100.percent)
                        .margin(top: 12)
                        .onClick({ evt =>
                            this.pathInfos.pushPath(NavPathInfo(name: 'PageOne', param: 'Detail page parameters')) // Push the NaviDestination page info specified by name onto the stack, passing param as parameter
                        })
                    })
                    ForEach(this.listArray2, itemGeneratorFunc: {item: String, _:Int64 =>
                        ListItem() {
                            Row() {
                                Row() {
                                    Text('${item.split("")[0]}')
                                    .fontColor(Color.White)
                                    .fontSize(14)
                                    .fontWeight(FontWeight.Bold)
                                }
                                .width(30)
                                .height(30)
                                .backgroundColor(Color.Gray)
                                .margin( right: 20 )
                                .borderRadius(20)
                                .justifyContent(FlexAlign.Center)

                                Column() {
                                  Text(item)
                                    .fontSize(16)
                                    .margin(5)
                                }
                                .alignItems(HorizontalAlign.Start)
                                Blank()
                                Row()
                                .width(12)
                                .height(12)
                                .margin(15)
                                .border(width: 2.px,color: 0xCCCCCC)
                            }
                            .borderRadius(15)
                            .shadow(radius: 100.0, color: 0xededed)
                            .width(90.percent)
                            .alignItems(VerticalAlign.Center)
                            .padding( left: 15, top: 15, bottom: 15 )
                            .backgroundColor(Color.White)
                        }
                        .width(100.percent)
                        .margin(top: 12)
                        .onClick({ evt =>
                            this.pathInfos.pushPath(NavPathInfo(name: 'PageTwo', param: 'Detail page parameters' )) // Push the NaviDestination page info specified by name onto the stack, passing param as parameter
                        })
                    })
                }
                .listDirection(Axis.Vertical)
                .edgeEffect(EdgeEffect.Spring)
                .sticky(StickyStyle.Header)
                .chainAnimation(false)
                .width(100.percent)
                .height(100.percent)
                .padding(top: 10)
            }
            .navDestination(bind<String, Any>(pageMap, this))
            .width(100.percent).height(100.percent)

        }
        .size( width: 100.percent, height: 100.percent )
        .backgroundColor(Color.White)
    }
}
```

## Creating Navigation Subpages

Implementation steps for Navigation Subpage 1:

1. Use NavDestination to create navigation subpage PageOne.

2. Create a route stack NavPathStack and initialize it during onReady to obtain the current page stack, enabling jumps between different pages.

3. Add onClick to components within the subpage and use the pop method of the route stack NavPathStack to enable components to pop the top element of the route stack upon clicking, thereby returning to the previous page.

<!-- run -navigation -->

```cangjie
@Component
class PageOne {
    var pathInfos1: NavPathStack = NavPathStack()
    var name: String = ''
    @State var value: String = ''

    func build() {
        NavDestination() {
            Column() {
                Text('${this.name} Settings Page')
                .width(100.percent)
                .fontSize(20)
                .fontColor(0x333333)
                .textAlign(TextAlign.Center)
                .padding( top: 30 )

                Text('${(this.value)}')
                .width(100.percent)
                .fontSize(18)
                .fontColor(0x666666)
                .textAlign(TextAlign.Center)
                .padding( top: 45 )
                Button('Back')
                .width(50.percent)
                .height(40)
                .margin( top: 50 )
                .onClick({e =>
                  // Pop the top element of the route stack to return to the previous page
                  this.pathInfos1.pop()
                })
            }
            .size( width: 100.percent, height: 100.percent )
        }
        .onReady({ctx: NavDestinationContext =>
            // NavDestinationContext obtains the current page stack
            this.pathInfos1 = ctx.pathStack
        })
        .padding(top: 40)
    }
}
```

Implementation steps for Navigation Subpage 2:

1. Use NavDestination to create navigation subpage PageTwo.

2. Create a route stack NavPathStack and initialize it during onReady to obtain the current page stack, enabling jumps between different pages.

3. Add onClick to components within the subpage and use the pushPath method of the route stack NavPathStack to enable components to jump from the current page to the corresponding page specified by the input parameter name in the route table upon clicking.

<!-- run -navigation -->

```cangjie
@Component
class PageTwo {
    var pathInfos2: NavPathStack = NavPathStack()
    var name: String = ''
    private var listArray: Array<String> = ['Projection', 'Print', 'VPN', 'Private DNS', 'NFC']

    func build() {
        NavDestination() {
            Column() {
                List(initialIndex: 0 ) {
                    ForEach(this.listArray, itemGeneratorFunc: {item: String, _: Int64 =>
                        ListItem() {
                            Row() {
                                Row() {
                                    Text('${item.split("")[0]}')
                                    .fontColor(Color.White)
                                    .fontSize(14)
                                    .fontWeight(FontWeight.Bold)
                                }
                                .width(30)
                                .height(30)
                                .backgroundColor(Color.Gray)
                                .margin( right: 20 )
                                .borderRadius(20)
                                .justifyContent(FlexAlign.Center)

                                Column() {
                                    Text(item)
                                    .fontSize(16)
                                    .margin( bottom: 5 )
                                }.alignItems(HorizontalAlign.Start)

                                Blank()

                                Row()
                                .width(12)
                                .height(12)
                                .margin( right: 15 )
                                .border(width: 2.px, color: 0xcccccc )
                            }
                            .borderRadius(15)
                            .shadow(radius: 100.0, color: 0xededed)
                            .width(100.percent)
                            .alignItems(VerticalAlign.Center)
                            .padding( left: 15, top: 15, bottom: 15 )
                            .backgroundColor(Color.White)
                        }
                        .onClick({ evt =>
                            this.pathInfos2.pushPath(NavPathInfo(name: 'PageOne', param: 'Detail page parameters'))
                        })
                        .margin(top: 12, left: 20)
                        .width(90.percent)
                    })
                }
                .listDirection(Axis.Vertical)
                .edgeEffect(EdgeEffect.Spring)
                .sticky(StickyStyle.Header)
                .width(100.percent)
                .height(100.percent)
            }
            .size( width: 100.percent, height: 100.percent )
        }
        .onReady({ctx: NavDestinationContext =>
            // NavDestinationContext obtains the current page stack
            this.pathInfos2 = ctx.pathStack
        })
        .padding(top: 40)
        .width(100.percent)
        .height(100.percent)
    }
}
```

![navigation-transition](./figures/navigation-transition.gif)