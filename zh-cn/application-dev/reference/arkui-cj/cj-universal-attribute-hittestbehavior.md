# 触摸测试控制

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

设置组件的[触摸测试](../../arkui-cj/cj-common-events-distribute.md#触摸测试)模式。在ArkUI开发框架中，处理触屏事件和鼠标事件时，会在事件触发前进行按压点与组件响应热区的触摸测试，以收集需响应事件的组件。基于测试结果，框架会向通过触摸测试的组件分发事件。当组件存在重叠、穿透等触摸响应冲突时，可通过hitTestBehavior属性设置不同的触摸测试响应模式，影响触摸测试收集结果及后续事件分发，避免不必要的触摸响应。具体影响参考[HitTestMode](./cj-common-types.md#enum-hittestmode)枚举说明。

> **说明：**
>
> - 当Stack组件中有多个节点触摸区域重叠时，如果最上层节点的子组件命中，则默认只会对显示在最上层的节点做触摸测试。此时只有给显示在最上层的节点设置hitTestBehavior为HitTestMode.Transparent时，才能使显示在下层的节点触发触摸测试。

## 导入模块

```cangjie
import kit.ArkUI.*
```

## func hitTestBehavior(?HitTestMode)

```cangjie
func hitTestBehavior(value: ?HitTestMode): T
```

**功能：** 设置组件的触摸测试类型。如果组件不设置hitTestBehavior，其默认触摸测试类型为HitTestMode.Default。value为None时，保持默认触摸测试类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?[HitTestMode](./cj-common-types.md#enum-hittestmode)|是|-|设置当前组件的触摸测试模式。|

**返回值：**

|类型|说明|
|:---|:---|
|T|返回调用此接口的组件实例本身。|

## 示例代码

### 示例1（触摸测试模式为Block和Transparent的触摸测试效果）

该示例通过设置不同的[HitTestMode](./cj-common-types.md#enum-hittestmode)值演示了Block和Transparent的触摸测试效果。

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
        // 外层Stack
        Stack {
            Button('outer button')
                .onTouch({ event =>
                    Hilog.info(0, 'cangjie', 'outer button touched')
                })
            // 内层Stack
            Stack {
                Button('inner button')
                    .onTouch({ event =>
                        Hilog.info(0, 'cangjie', 'inner button touched')
                    })
            }
                .width(100.percent).height(100.percent)
                // 设置触摸测试类型为Block，自身响应触摸测试但阻止兄弟节点参与触摸测试
                .hitTestBehavior(HitTestMode.Block)
                .onTouch({ event =>
                    Hilog.info(0, 'cangjie', 'stack touched')
                })

            Text('Transparent')
                // 设置触摸测试类型为Transparent，自身不拦截触摸测试，允许下层节点响应触摸测试
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

### 示例2（触摸测试类型为BlockHierarchy时的触摸测试效果）

从API version 26.1.0开始，该示例演示了设置触摸测试类型为BlockHierarchy时的触摸测试效果。

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
        // 外层Stack
        Stack {
            Stack {
                Button('outer button')
                    .onTouch({ event =>
                        Hilog.info(0, 'cangjie', 'outer button touched')
                    })
                    .width(200)
                    .height(200)
                    .backgroundColor(0xD5D5D5)
                // 内层Stack
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
                    // 设置触摸测试模式为BlockHierarchy，自身和子节点响应触摸测试，阻止所有优先级较低的兄弟节点和父节点参与触摸测试
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

### 示例3（触摸测试类型为BlockDescendants时的触摸测试效果）

从API version 26.1.0开始，该示例演示了设置触摸测试类型为BlockDescendants时的触摸测试效果。

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
        // 外层Stack
        Stack {
            Stack {
                Button('outer button')
                    .onTouch({ event =>
                        Hilog.info(0, 'cangjie', 'outer button touched')
                    })
                    .width(200)
                    .height(200)
                    .backgroundColor(0xD5D5D5)
                // 内层Stack
                Stack {
                    Button('inner button')
                        .width(100)
                        .height(100)
                        .onTouch({ event =>
                            Hilog.info(0, 'cangjie', 'inner button touched')
                        })
                }
                    .width(100.percent).height(100.percent)
                    // 设置触摸测试模式为BlockDescendants，自身不响应触摸测试，所有的后代（孩子、孙子等）也不响应触摸测试，不影响祖先节点的触摸测试
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

### 示例4（Stack组件中多节点重合时的触摸测试效果）

该示例演示了在Stack组件中存在多节点触摸区域重叠时的触摸测试效果。此时设置[HitTestMode](./cj-common-types.md#enum-hittestmode)为None时，重叠的背景区域无法响应触摸测试；只有设置为Transparent时，背景区域才能响应触摸测试。

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
                // 点击按钮进行触摸测试
                Button('HitTest')
                // 点击按钮切换不同的触摸测试模式
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
                // 只有上层节点的HitTestMode设置为Transparent时，下层节点才能响应触摸测试
                .hitTestBehavior(this.mode)
        }
            .height(100.percent)
            .width(100.percent)
    }
}
```
