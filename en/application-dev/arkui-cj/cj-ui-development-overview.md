# Overview of UI Development (Cangjie Declarative Development Paradigm)

The ArkUI development framework based on the Cangjie declarative development paradigm is a minimalist, high-performance, cross-device UI development framework that provides essential capabilities for building application UIs, including:

- **Cangjie**

  Cangjie language is the primary application development language, covering declarative UI description, custom components, dynamic UI element extension, state management, and rendering control in application development. As a distinctive feature of the Cangjie development paradigm, state management follows declarative programming principles, offering developers clear page update and rendering pipelines through versatile decorators. State management encompasses both UI component states and application states, enabling developers to comprehensively handle data updates and UI rendering. For foundational knowledge about Cangjie language, refer to [Introduction to Cangjie Language](https://gitcode.com/Cangjie/cangjie_docs/blob/dev/docs/dev-guide/source_zh_cn/first_understanding/basic.md) for more information.

- **Layout**

  Layout is a fundamental UI element that defines component positioning. The ArkUI framework provides various layout methods, including basic linear, stack, flex, relative, and grid layouts, as well as more complex list, grid, and carousel layouts.

- **Components**

  Components are essential UI elements that form the visual interface. Those provided by the framework are called **system components**, while those defined by developers are called **custom components**. Built-in system components include buttons, radio buttons, progress bars, text, etc. Developers can chain method calls to configure rendering effects of system components. System components can be combined into custom components, modularizing pages into independent UI units for separate creation, development, and reuse, enhancing engineering efficiency.

- **Page Routing and Component Navigation**

  Applications may contain multiple pages, with navigation between them achieved through page routing. Within a page, component navigation (e.g., tabs) can be implemented using navigation components.

- **Graphics**

  The ArkUI framework supports displaying various image types and provides extensive custom drawing capabilities, including shape drawing, color filling, text rendering, transformations, clipping, and image embedding.

- **Animation**

  Animation is a key UI element. Well-designed animations significantly enhance user experience. The framework offers rich animation capabilities, including built-in component animations, property animations, explicit animations, custom transition animations, and animation APIs. Developers can create custom animation trajectories using encapsulated physical models or animation APIs.

- **Interaction Events**

  Interaction events are essential for UI-user interaction. The ArkUI framework provides various events, including general touch, mouse, keyboard, and focus events, as well as gesture events derived from them. Gesture events include single gestures (tap, long press, drag, pinch, rotate, swipe) and composite gestures combining single gestures.

- **Customization Capabilities**

  Customization capabilities empower developers to tailor UI interfaces, including custom composition, extension, nodes, and rendering.

## Features

- **High Development Efficiency and Excellent Developer Experience**

  - Concise Code: UI is described using near-natural semantics, freeing developers from framework implementation details.
  
  - Data-Driven UI Changes: Developers focus on business logic. When UI changes, they only need to modify data—UI updates are handled by the framework.
  
  - Enhanced Developer Experience: UI-as-code improves programming workflow.

- **Superior Performance**

  - Layered Declarative UI Frontend and Backend: The C++-based UI backend provides foundational components, layouts, animations, events, state management, and rendering pipelines.
  
  - Compiler and Runtime Optimizations: Unified bytecode, efficient FFI (Foreign Function Interface), AOT (Ahead Of Time), minimized engine footprint, and type optimizations.

- **Rapid Ecosystem Advancement:**
  Leverages mainstream language ecosystems, maintains language neutrality, and evolves through standardization bodies.

## Development Process

When developing applications with the UI framework, the main workflow includes:

| Task          | Description                                  | Guides                                     |
| :----------- | :----------------------------------- | :---------------------------------------- |
| Learn Cangjie | Covers basic syntax, state management, and rendering control. | - [Basic Syntax](./paradigm/cj-basic-syntax-overview.md)<br> - [State Management](./state_management/cj-state-management-overview.md)<br> - [Rendering Control](./rendering_control/cj-rendering-control-overview.md)|
| Develop Layout | Introduces common layout methods. | - [Common Layouts](./cj-layout-development-overview.md)<br/> |
| Add Components | Explains usage of common system components. | - [Common Components](cj-common-components-button.md)<br/> - [Custom Components](./paradigm/cj-create-custom-components.md)|
| Use Text | Describes text components like input fields and rich text. | - [Text](cj-text-introduction.md)<br/>- [Text Display](cj-common-components-text-display.md) <br/>- [Text Input](cj-common-components-text-input.md)<br/> - [Rich Text](./cj-common-components-richeditor.md)<br>|
| Use Dialogs | Covers dialog scenarios and usage. | - [Dialogs](cj-dialog-overview.md)<br/>- [Popup](cj-dialog-base-overview.md)<br> - [Menu Control](./cj-popup-and-menu-components-menu.md)<br/>- [Global Custom Dialogs](cj-uicontext-custom-dialog.md)<br/>- [Fixed-Style Dialogs](cj-fixes-style-dialog.md)<br/>- [Tooltips](cj-popup-and-menu-components-popup.md)<br> - [Modal Pages](./cj-modal-overview.md)<br> - [Instant Feedback](./cj-create-toast.md)|
| Display Graphics | Explains image display, custom shapes, and canvas drawing. | - [Shapes](cj-shape-drawing.md)<br/>- [Canvas](cj-drawing-customization-on-canvas.md) |
| Use Animation | Demonstrates animation scenarios for components and pages. | - [Animation](cj-animation.md)<br>- [Property Animation](cj-attribute-animation-overview.md)<br>- [Implement Property Animation](cj-attribute-animation-apis.md)<br>- [Transition Animation](cj-transition-overview.md)<br>- [Enter/Exit Transition](cj-enter-exit-transition.md)<br>- [Modal Transition](cj-modal-transition.md)<br>- [Component Animation](cj-component-animation.md)<br>- [Animation Curves](cj-curve-overview.md)<br>- [Traditional Curves](cj-traditional-curve.md)<br>- [Animation Smoothing](cj-animation-smoothing.md)<br>- [Blur](cj-blur-effect.md)<br>- [Shadow](cj-shadow-effect.md)<br>- [Color](cj-color-effect.md)<br> - [Frame Animation](cj-animator.md)|
| Bind Events | Introduces event concepts and usage of general and gesture events. | - [Interaction Events](cj-event-overview.md)<br/>- [Event Distribution](cj-common-events-distribute.md)<br/>-&nbsp;[Touch Events](cj-common-events-touch-screen-event.md)<br/>- [Keyboard/Mouse Events](cj-common-events-device-input-event.md)<br/>- [Focus Events](cj-common-events-focus-event.md)|
| Use Mirroring | Explains mirroring concepts and usage. | - [Mirroring](./cj-mirroring-display.md)|
| Support Aging-Friendly | Covers aging-friendly scenarios and implementation. | - Aging-Friendly Support |
| Theme Settings | Describes application- and page-level theme configuration. | - [Dark/Light Mode Adaptation](./cj-ui-dark-light-color-adaptation.md)|

## General Rules

- **Default Units**

  Length parameters default to `vp` (virtual pixels). This applies to `Int32` inputs and `Int64`/`Float64` values in the [`Length`](../reference/arkui-cj/cj-common-types.md#interface-length) type.

- **Invalid Value Handling**

  For invalid inputs:
  
    - If the parameter has a default value, the default is used.
  
    - If no default exists, the associated property or API is ignored.