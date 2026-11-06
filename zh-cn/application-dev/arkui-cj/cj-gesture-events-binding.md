# 绑定手势方法

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

通过给各个组件绑定不同的手势事件，并设计事件的响应方式，当手势识别成功时，ArkUI框架将通过事件回调通知组件手势识别的结果。

当前版本支持的手势绑定方法包括[gesture](#gesture常规手势绑定方法)（常规手势绑定方法）和[parallelGesture](#parallelgesture并行手势绑定方法)（并行手势绑定方法），绑定的手势类型当前仅支持滑动手势[PanGesture](../reference/arkui-cj/cj-basic-gestures-pangesture.md)。

## gesture（常规手势绑定方法）

```cangjie
.gesture(gesture: GestureType)
.gesture(gesture: GestureType, mask: ?GestureMask)
```

gesture为通用的一种手势绑定方法，可以将手势绑定到对应的组件上。

例如，可以将滑动手势PanGesture通过gesture方法绑定到Text组件上。

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State
    var offsetX: Float64 = 0.0

    func build() {
        Column {
            Text('offsetX: ' + this.offsetX.toString()).fontSize(28)
                // 采用gesture手势绑定方法绑定PanGesture
                .gesture(
                    PanGesture(direction: PanDirection.Horizontal)
                        .onActionUpdate({ event =>
                            this.offsetX = event.offsetX
                        })
                    )
        }
        .height(200)
        .width(250)
    }
}
```

绑定手势时，还可以通过mask参数（[GestureMask](../reference/arkui-cj/cj-common-types.md#enum-gesturemask)）控制是否屏蔽子组件的手势：

- GestureMask.Normal：不屏蔽子组件的手势，按照默认手势识别顺序进行识别，为默认值。

- GestureMask.IgnoreInternal：屏蔽子组件的手势，包括子组件上系统内置的手势，如子组件为List组件时，内置的滑动手势同样会被屏蔽。

## parallelGesture（并行手势绑定方法）

```cangjie
.parallelGesture(gesture: GestureType)
.parallelGesture(gesture: GestureType, mask: ?GestureMask)
```

parallelGesture是并行的手势绑定方法，可以在父子组件上绑定可以同时响应的相同手势。

在默认情况下，手势事件为非冒泡事件，当父子组件绑定相同的手势时，父子组件绑定的手势事件会发生竞争，最多只有一个组件的手势事件能够获得响应。而当父组件绑定了并行手势parallelGesture时，父子组件相同的手势事件都可以触发，实现类似冒泡效果。

例如，当父组件Column和子组件Text同时绑定PanGesture手势时，父组件以并行手势parallelGesture的形式进行绑定时，在子组件区域内滑动，父组件和子组件绑定的PanGesture都可以触发。

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State
    var childText: String = 'child: idle'
    @State
    var parentText: String = 'parent: idle'

    func build() {
        Column {
            Text(this.parentText).fontSize(15)
                .margin(bottom: 10)
            Column {
                Text(this.childText).fontSize(20)
            }
            .height(120)
            .width(200)
            .backgroundColor(0x4682B4)
            .borderRadius(8)
            // 子组件通过gesture绑定滑动手势
            .gesture(
                PanGesture()
                    .onActionUpdate({ event =>
                        this.childText = 'child offsetX: ' + event.offsetX.toString()
                    }))
        }
        .height(200)
        .width(250)
        // 设置为parallelGesture时，在子组件区域内滑动，父组件Column与子组件Text的PanGesture手势事件会同时触发
        .parallelGesture(
            PanGesture()
                .onActionUpdate({ event =>
                    this.parentText = 'parent offsetX: ' + event.offsetX.toString()
                }), GestureMask.Normal)
    }
}
```
