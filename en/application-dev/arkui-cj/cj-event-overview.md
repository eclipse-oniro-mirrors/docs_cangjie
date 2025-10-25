# Overview of Interaction Events

Common events are categorized by their trigger types, including touch screen events, keyboard/mouse events, focus events, and drag events.

- [Touch Screen Events](./cj-common-events-touch-screen-event.md): Single-finger or single-stylus operations on a touch screen.

- [Keyboard/Mouse Events](./cj-common-events-device-input-event.md): Includes operation events from peripheral mice or touchpads and key events from peripheral keyboards.
    - Mouse events refer to events triggered by connecting and using peripheral mice/touchpads.
    - Key events refer to events triggered by connecting and using peripheral keyboards.

- [Focus Events](./cj-common-events-focus-event.md): The ability to control component focus through the above methods and the corresponding events.

- [Drag Events](../../../en/application-dev/reference/arkui-cj/cj-universal-event-drag.md): Initiated by touch screen events or keyboard/mouse events, including long-press-and-drag operations with fingers/stylus on components and mouse dragging.

- [Event Distribution](./cj-common-events-distribute.md): Describes the hit collection process of the response chain for touch-related events (excluding key and focus events).

Gesture events consist of bound gesture methods and the gestures themselves. Bound gestures can be divided into two types based on complexity: single gestures and composite gestures.