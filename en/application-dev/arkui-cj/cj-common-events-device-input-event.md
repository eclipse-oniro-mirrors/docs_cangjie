# Keyboard and Mouse Events

Keyboard and mouse events refer to input events triggered by external devices such as keyboards and mice.

## Mouse Events

Supported mouse events include those triggered by external mice and touchpads.

The mouse can trigger the following events:

| Name                                       | Description                                       |
|:---------------------------------------- |:---------------------------------------- |
|  onHover(callback: (isHover: Bool)->Unit) | Triggered when the mouse enters or exits a component.<br>isHover: Indicates whether the mouse is hovering over the component. It is true when the mouse enters and false when it exits. |
|  onMouse(callback: (event: MouseEvent)->Unit) | Triggered when the current component is clicked by a mouse button or when the mouse hovers and moves over the component.<br>The event return value includes the timestamp when the event was triggered, the mouse button, the action, the mouse coordinates on the entire screen, and the coordinates relative to the current component. |

The principle of mouse events is illustrated below:

![Hover](./figures/Hover_mouse.png)

After a mouse event is passed to ArkUI, it first determines whether the mouse event is a left button press/release/move and then responds differently:

- Yes: The mouse event is first converted into a touch event at the same position, and the touch event's collision test, gesture judgment, and callback response are executed. Then, the mouse event's collision test and callback response are performed.

- No: The event is only used to perform the mouse event's collision test and callback response.

> **Note:**
>
> All single-finger touch events/gesture events can be operated and responded to via the left mouse button. For example, if we need to develop a feature where clicking a Button navigates to a page and needs to support both finger clicks and left mouse button clicks, binding a single click event (onClick) can achieve this effect. If different effects are required for finger clicks and left mouse button clicks, the source field in the callback parameters can be used within the onClick callback to determine whether the event was triggered by a finger or the mouse.

### onHover

```cangjie
public func onHover(callback: (Bool)->Unit): This
```

Mouse hover event. The parameter type is Bool, indicating whether the mouse enters or exits the component. This event does not support custom bubbling settings and defaults to parent-child bubbling.

If a component is bound to this interface, the event is triggered the moment the mouse pointer moves from outside the component into the component, with the parameter value being true. The event is also triggered the moment the mouse pointer leaves the component, with the parameter value being false.

> **Note:**
>
> Event bubbling: In a tree structure, after a child node processes an event, the event is passed to its parent node for processing.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State
    var hoverText: String = 'Not Hover'
    @State
    var color: Color = Color.Gray

    func build() {
        Column() {
            Button(this.hoverText)
                .width(200)
                .height(100)
                .backgroundColor(this.color)
                .onHover(
                    {
                        isHover => // Use the onHover interface to monitor whether the mouse is hovering over the Button component
                        if (isHover) {
                            this.hoverText = 'Hovered!'
                            this.color = Color.Green
                        } else {
                            this.hoverText = ' Hover'
                            this.color = Color.Gray
                        }
                    })
        }
            .width(100.percent)
            .height(100.percent)
            .justifyContent(FlexAlign.Center)
    }
}

```

This example creates a Button component with an initial background color of gray and the text "Not Hover." The Button component in the example is bound to the onHover callback.

When the mouse moves from outside the Button to inside the Button, the callback is triggered with the parameter value true, changing the component's background color to Color.Green and the text to "Hovered!".

When the mouse moves from inside the Button to outside the Button, the callback is triggered with the parameter value false, restoring the component to its initial style.

![onHover](./figures/onHover.gif)

### onMouse

```cangjie
public func onMouse(callback: (MouseEvent)->Unit): This
```

Mouse event callback. Whenever the mouse pointer performs an action (MouseAction) within a component bound to this API, the event callback is triggered. The parameter is a [MouseEvent](../../../en/application-dev/reference/arkui-cj/cj-universal-event-mouse.md#class-mouseevent) object, representing the mouse event that triggered this action. This event supports custom bubbling settings and defaults to parent-child bubbling. It is commonly used for developer-defined mouse behavior logic.

Developers can obtain the coordinates (screenX/screenY/x/y), button ([MouseButton](../../../en/application-dev/reference/arkui-cj/cj-common-types.md#enum-mousebutton)), action ([MouseAction](../../../en/application-dev/reference/arkui-cj/cj-common-types.md#enum-mouseaction)), timestamp (timestamp), interactive component area ([EventTarget](../../../en/application-dev/reference/arkui-cj/cj-universal-event-click.md#class-eventtarget)), and event source ([SourceType](../../../en/application-dev/reference/arkui-cj/cj-common-types.md#enum-sourcetype)) from the MouseEvent object in the callback.

> **Note:**
>
> The values for the button (MouseButton): Left/Right/Middle/Back/Forward correspond to physical buttons on the mouse. Events for these buttons are triggered when they are pressed or released. None indicates no button, which appears in events triggered by moving the mouse without any button pressed or released.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var buttonText: String = ''
    @State var columnText: String = ''
    @State var hoverText: String = 'Not Hover'
    @State var color: Color = Color.Gray

    func build() {
        Column(space: 20) {
            Button(this.hoverText)
                .width(200)
                .height(100)
                .backgroundColor(this.color)
                .onHover({isHover =>
                    if (isHover) {
                        this.hoverText = 'Hovered!'
                        this.color = Color.Green
                    } else {
                        this.hoverText = 'Not Hover'
                        this.color = Color.Gray
                    }
                })
                .onMouse({event =>
                this.buttonText = "Button onMouse:\n" +
                    "x,y = (${event.x},${event.y})\n" +
                    "windowXY=(${event.screenX},${event.screenY})"
                })
            Divider()
            Text(this.buttonText).fontColor(Color.Green)
            Divider()
            Text(this.columnText).fontColor(Color.Red)
        }
        .width(100.percent)
        .height(100.percent)
        .justifyContent(FlexAlign.Center)
        .borderWidth(2.px)
        .borderColor(Color.Red)
        .onMouse({event =>
                this.columnText = "Column onMouse:\n" +
                    "x,y = (${event.x},${event.y})\n" +
                    "windowXY=(${event.screenX},${event.screenY})"
        })
    }
}
```

![onMouse1](./figures/onMouse1.gif)

## Key Events

### onKeyEvent

```cangjie
public func onKeyEvent(callback: (KeyEvent)->Unit): This
```

When the component bound to this method is in a focused state, key events from an external keyboard will trigger this method. The callback parameter is [KeyEvent](../../../en/application-dev/reference/arkui-cj/cj-universal-event-key.md#class-keyevent), from which the current key event's key action ([KeyType](../../../en/application-dev/reference/arkui-cj/cj-common-types.md#enum-keytype)), key text (keyText), event source device type ([KeySource](../../../en/application-dev/reference/arkui-cj/cj-common-types.md#enum-keysource)), event source device ID (deviceId), meta key press state (metaKey), and timestamp (timestamp) can be obtained.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var buttonText: String = ''
    @State var buttonType: String = ''
    @State var columnText: String = ''
    @State var columnType: String = ''

    func build() {
        Column() {
            Button('onKeyEvent')
                .defaultFocus(true)
                .width(140)
                .height(70)
                .onKeyEvent({ event =>
                    if (event.keyType == KeyType.Down) {
                        this.buttonType = 'Down'
                    }
                    if (event.keyType == KeyType.Up) {
                        this.buttonType = 'Up'
                    }
                    this.buttonText = """
                        Button:
                        KeyType: ${this.buttonType}
                        KeyCode: ${event.keyCode.toString()}
                        KeyText: ${event.keyText.toString()}
                    """
                })

            Divider()
            Text(this.buttonText).fontColor(Color.Green)

            Divider()
            Text(this.columnText).fontColor(Color.Red)
        }
        .width(100.percent)
        .height(100.percent)
        .justifyContent(FlexAlign.Center)
        .onKeyEvent({ event =>
            if (event.keyType == KeyType.Down) {
                this.columnType = 'Down'
            }
            if (event.keyType == KeyType.Up) {
                this.columnType = 'Up'
            }
            this.columnText = """
                Column:
                KeyType: ${this.columnType}
                KeyCode: ${event.keyCode.toString()}
                KeyText: ${event.keyText.toString()}
            """
        })
    }
}
```

In the above example, the onKeyEvent is bound to the Button component and its parent container Column. When the application opens and the page loads, the first non-container component in the component tree that can be focused automatically gains focus. The Button is set as the default focus for the current page. Since the Button is a child node of the Column, the Button gaining focus also means the Column gains focus. For the focus mechanism, refer to [Focus Events](./cj-common-events-focus-event.md).

![KeyEvent](./figures/KeyEvent.gif)

After opening the application, press the following keys in sequence on the keyboard: Space, Enter, Left Ctrl, Left Shift, Letter A, Letter Z.

> **Note:**
>
> - Since the onKeyEvent event bubbles by default, both the Button and Column's onKeyEvent can respond.
> - Each key press triggers two callbacks, corresponding to KeyType.Down and KeyType.Up, indicating the key is pressed and then released.

To prevent bubbling, i.e., only the Button responds to keyboard events and the Column does not, add the event.stopPropagation() method to the Button's onKeyEvent callback, as shown below:

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var buttonText: String = ''
    @State var buttonType: String = ''
    @State var columnText: String = ''
    @State var columnType: String = ''

    func build() {
        Column() {
            Button('onKeyEvent')
                .defaultFocus(true)
                .width(140)
                .height(70)
                .onKeyEvent({ event =>
                    // Prevent event bubbling with stopPropagation
                    event.stopPropagation()
                    if (event.keyType == KeyType.Down) {
                        this.buttonType = 'Down'
                    }
                    if (event.keyType == KeyType.Up) {
                        this.buttonType = 'Up'
                    }
                    this.buttonText = """
                        Button:
                        KeyType: ${this.buttonType}
                        KeyCode: ${event.keyCode.toString()}
                        KeyText: ${event.keyText.toString()}
                    """
                })

            Divider()
            Text(this.buttonText).fontColor(Color.Green)

            Divider()
            Text(this.columnText).fontColor(Color.Red)
        }
        .width(100.percent)
        .height(100.percent)
        .justifyContent(FlexAlign.Center)
        .onKeyEvent({ event =>
            if (event.keyType == KeyType.Down) {
                this.columnType = 'Down'
            }
            if (event.keyType == KeyType.Up) {
                this.columnType = 'Up'
            }
            this.columnText = """
                Column:
                KeyType: ${this.columnType}
                KeyCode: ${event.keyCode.toString()}
                KeyText: ${event.keyText.toString()}
            """
        })
    }
}
```

![KeyEventStop](./figures/KeyEventStop.gif)