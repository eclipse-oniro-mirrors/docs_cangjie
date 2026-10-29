# Gesture Binding Methods

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

After you bind different gesture events to components and design how the events are responded to, the ArkUI framework notifies the component of the gesture recognition result through event callbacks when a gesture is successfully recognized.

The gesture binding methods supported in the current version include [gesture](#gesture-regular-gesture-binding-method) (regular gesture binding method) and [parallelGesture](#parallelgesture-parallel-gesture-binding-method) (parallel gesture binding method). The only gesture type that can be bound is the pan gesture [PanGesture](../reference/arkui-cj/cj-basic-gestures-pangesture.md).

## gesture (Regular Gesture Binding Method)

```cangjie
.gesture(gesture: GestureType)
.gesture(gesture: GestureType, mask: ?GestureMask)
```

gesture is a general gesture binding method that binds a gesture to a component.

For example, you can bind the pan gesture PanGesture to a Text component through the gesture method.

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
                // Binds PanGesture through the gesture gesture binding method
                .gesture(
                    PanGesture(direction: PanDirection.Horizontal)
                        .onActionUpdate({ event =>
                            this.offsetX = event.offsetX
                        }))
        }
            .height(200)
            .width(250)
    }
}
```

When binding a gesture, you can also use the mask parameter ([GestureMask](../reference/arkui-cj/cj-common-types.md#enum-gesturemask)) to control whether to block child component gestures:

- GestureMask.Normal: does not block child component gestures; gestures are recognized according to the default gesture recognition order. This is the default value.

- GestureMask.IgnoreInternal: blocks child component gestures, including system-built-in gestures on child components (e.g., the built-in pan gesture of a List component).

## parallelGesture (Parallel Gesture Binding Method)

```cangjie
.parallelGesture(gesture: GestureType)
.parallelGesture(gesture: GestureType, mask: ?GestureMask)
```

parallelGesture is a parallel gesture binding method that binds the same gesture to parent and child components so that they can respond at the same time.

By default, gesture events are non-bubbling events. When the parent and child components are bound to the same gesture, the gesture events bound to them compete with each other, and at most one component's gesture event can be responded to. However, when the parent component is bound to a parallel gesture through parallelGesture, the same gesture events of both the parent and child components can be triggered, implementing a quasi-bubbling effect.

For example, when both the parent component Column and the child component Text are bound to the PanGesture gesture, and the parent component is bound in the form of the parallel gesture parallelGesture, panning within the area of the child component triggers the PanGesture bound to both the parent and child components.

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
                // The child component binds a pan gesture through gesture
                .gesture(
                    PanGesture()
                        .onActionUpdate({ event =>
                            this.childText = 'child offsetX: ' + event.offsetX.toString()
                        }))
        }
            .height(200)
            .width(250)
            // When parallelGesture is set, panning within the area of the child component triggers the PanGesture events of both the parent component Column and the child component Text at the same time
            .parallelGesture(
                PanGesture()
                    .onActionUpdate({ event =>
                        this.parentText = 'parent offsetX: ' + event.offsetX.toString()
                    }), GestureMask.Normal)
    }
}
```
