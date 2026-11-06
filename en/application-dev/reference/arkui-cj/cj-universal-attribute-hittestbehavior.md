# Touch Test Control

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Sets the [touch test](../../arkui-cj/cj-common-events-distribute.md#touch-testing) mode of a component. In the ArkUI development framework, when handling touch and mouse events, a touch test is performed between the press point and the component's responsive hot zone before the event is triggered, in order to collect the components that need to respond to the event. Based on the test result, the framework distributes events to the components that pass the touch test. When components have touch response conflicts such as overlapping or penetration, you can set different touch test response modes through the hitTestBehavior attribute to affect the touch test collection results and subsequent event distribution, avoiding unnecessary touch responses. For details about the effects, see the [HitTestMode](./cj-common-types.md#enum-hittestmode) enum description.

> **Note:**
>
> - When multiple nodes in a Stack component have overlapping touch areas, if a child component of the topmost node is hit, only the topmost node will undergo touch testing by default. In this case, touch testing for lower-layer nodes can be triggered only by setting the hitTestBehavior of the topmost node to HitTestMode.Transparent.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func hitTestBehavior(?HitTestMode)

```cangjie
func hitTestBehavior(value: ?HitTestMode): T
```

**Description:** Sets the touch test type of a component. If hitTestBehavior is not set, the default touch test type of the component is HitTestMode.Default. When value is None, the default touch test type is retained.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[HitTestMode](./cj-common-types.md#enum-hittestmode) | Yes | - | Sets the touch test mode of the current component. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## Sample Code

### Example 1 (Touch Test Effects of Block and Transparent Modes)

This example demonstrates the touch test effects of Block and Transparent by setting different [HitTestMode](./cj-common-types.md#enum-hittestmode) values.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    func build() {
        // Outer stack
        Stack {
            Button('outer button')
                .onTouch({ event =>
                    Hilog.info(0, 'cangjie', 'outer button touched')
                })
            // Inner stack
            Stack {
                Button('inner button')
                    .onTouch({ event =>
                        Hilog.info(0, 'cangjie', 'inner button touched')
                    })
            }
                .width(100.percent).height(100.percent)
                // Set the touch test type to Block: the component itself responds to touch testing but blocks sibling nodes from participating in touch testing
                .hitTestBehavior(HitTestMode.Block)
                .onTouch({ event =>
                    Hilog.info(0, 'cangjie', 'stack touched')
                })

            Text('Transparent')
                // Set the touch test type to Transparent: the component itself does not block touch testing, allowing lower-layer nodes to respond to touch testing
                .hitTestBehavior(HitTestMode.Transparent)
                .width(100.percent).height(100.percent)
                .onTouch({ event =>
                    Hilog.info(0, 'cangjie', 'text touched')
                })
        }
            .width(300).height(300)
    }
}
```

### Example 2 (Touch Test Effect When the Touch Test Type Is BlockHierarchy)

Since API version 26.1.0, this example demonstrates the touch test effect when the touch test type is set to BlockHierarchy.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    func build() {
        // Outer stack
        Stack {
            Stack {
                Button('outer button')
                    .onTouch({ event =>
                        Hilog.info(0, 'cangjie', 'outer button touched')
                    })
                    .width(200)
                    .height(200)
                    .backgroundColor(0xD5D5D5)
                // Inner stack
                Stack {
                    Button()
                        .id('button150')
                        .backgroundColor(0xF7F7F7)
                        .width(150)
                        .height(150)
                        .onTouch({ event =>
                            Hilog.info(0, 'cangjie', 'button150 touched')
                        })
                        .hitTestBehavior(HitTestMode.Transparent)
                    Button()
                        .id('button100')
                        .backgroundColor(0x707070)
                        .width(100)
                        .height(100)
                        .onTouch({ event =>
                            Hilog.info(0, 'cangjie', 'button100 touched')
                        })
                        .hitTestBehavior(HitTestMode.Transparent)
                    Button()
                        .id('button050')
                        .backgroundColor(0xD5D5D5)
                        .width(50)
                        .height(50)
                        .onTouch({ event =>
                            Hilog.info(0, 'cangjie', 'button050 touched')
                        })
                        .hitTestBehavior(HitTestMode.Transparent)
                }
                    .width(100.percent).height(100.percent)
                    // Set the touch test type to BlockHierarchy: the component itself and its child nodes respond to touch testing, preventing all sibling nodes and parent nodes with lower priority from participating in touch testing
                    .hitTestBehavior(HitTestMode.BlockHierarchy)
                    .onTouch({ event =>
                        Hilog.info(0, 'cangjie', 'stack touched')
                    })

                Text('Transparent')
                    .hitTestBehavior(HitTestMode.Transparent)
                    .width(100.percent).height(100.percent)
                    .onTouch({ event =>
                        Hilog.info(0, 'cangjie', 'text touched')
                    })
            }
                .width(300).height(300)
                .borderWidth(2)
                .onTouch({ event =>
                    Hilog.info(0, 'cangjie', 'father stack touched')
                })
        }
            .width(500).height(500)
            .borderWidth(2)
            .onTouch({ event =>
                Hilog.info(0, 'cangjie', 'grandfather stack touched')
            })
    }
}
```

### Example 3 (Touch Test Effect When the Touch Test Type Is BlockDescendants)

Since API version 26.1.0, this example demonstrates the touch test effect when the touch test type is set to BlockDescendants.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    func build() {
        // Outer stack
        Stack {
            Stack {
                Button('outer button')
                    .onTouch({ event =>
                        Hilog.info(0, 'cangjie', 'outer button touched')
                    })
                    .width(200)
                    .height(200)
                    .backgroundColor(0xD5D5D5)
                // Inner stack
                Stack {
                    Button('inner button')
                        .width(100)
                        .height(100)
                        .onTouch({ event =>
                            Hilog.info(0, 'cangjie', 'inner button touched')
                        })
                }
                    .width(100.percent).height(100.percent)
                    // Set the touch test type to BlockDescendants: the component itself does not respond to touch testing, and all its descendants (children, grandchildren, and more) do not respond to touch testing either, without affecting the touch testing of ancestor nodes
                    .hitTestBehavior(HitTestMode.BlockDescendants)
                    .onTouch({ event =>
                        Hilog.info(0, 'cangjie', 'stack touched')
                    })

                Text('Transparent')
                    .hitTestBehavior(HitTestMode.Transparent)
                    .width(100.percent).height(100.percent)
                    .onTouch({ event =>
                        Hilog.info(0, 'cangjie', 'text touched')
                    })
            }
                .width(300).height(300)
                .borderWidth(2)
                .onTouch({ event =>
                    Hilog.info(0, 'cangjie', 'father stack touched')
                })
        }
            .width(500).height(500)
            .borderWidth(2)
            .onTouch({ event =>
                Hilog.info(0, 'cangjie', 'grandfather stack touched')
            })
    }
}
```

### Example 4 (Touch Test Effect When Multiple Nodes Overlap in the Stack Component)

This example demonstrates the touch test effect when multiple nodes in the Stack component overlap in touch area. In this case, when [HitTestMode](./cj-common-types.md#enum-hittestmode) is set to None, the overlapped background area cannot respond to touch testing; only when it is set to Transparent can the background area respond to touch testing.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    @State
    @Watch[onModeChange]
    var mode: HitTestMode = HitTestMode.None
    @State
    var modeStr: String = 'None'

    func onModeChange(): Unit {
        if (this.mode == HitTestMode.None) {
            this.modeStr = 'None'
        } else {
            this.modeStr = 'Transparent'
        }
    }

    func build() {
        Stack {
            Column()
                .height(100.percent)
                .width(100.percent)
                .onTouch({ _ =>
                    Hilog.info(0, 'cangjie', 'background hit test!')
                })
            Stack {
                // Tap the button to perform touch testing
                Button('HitTest')
                // Tap the button to switch between different touch test modes
                Button('HitTestMode: ' + this.modeStr)
                    .margin(top: 100)
                    .onClick({ _ =>
                        if (this.mode == HitTestMode.None) {
                            this.mode = HitTestMode.Transparent
                        } else {
                            this.mode = HitTestMode.None
                        }
                    })
            }
                .height(100.percent)
                .width(100.percent)
                // Only when the HitTestMode of the upper-layer node is set to Transparent can lower-layer nodes respond to touch testing
                .hitTestBehavior(this.mode)
        }
            .height(100.percent)
            .width(100.percent)
    }
}
```
