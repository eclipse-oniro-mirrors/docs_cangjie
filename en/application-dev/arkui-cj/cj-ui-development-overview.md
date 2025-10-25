# Overview of UI Development (Cangjie Declarative Development Paradigm)

The ArkUI development framework based on the Cangjie declarative development paradigm is a minimalist, high-performance, cross-device UI development framework that provides essential capabilities for building application UIs, including:

- **Cangjie**

  The Cangjie language is the primary application development language, covering declarative UI description, custom components, dynamic UI element extension, state management, and rendering control in the application development domain. As a distinctive feature of the Cangjie development paradigm, state management is based on declarative programming concepts, offering developers clear page update rendering processes and pipelines through versatile decorators. State management encompasses both UI component states and application states, enabling developers to comprehensively handle data updates and UI rendering. For foundational knowledge about the Cangjie language, refer to [Introduction to Cangjie Language](https://developer.huawei.com/consumer/cn/doc/cangjie-guides-V5/basic-V5) for more information.

- **Layout**

  Layout is a fundamental UI element that defines component positioning on the interface. The ArkUI framework provides various layout methods, including basic linear, stack, flex, relative, and grid layouts, as well as more complex list, grid, and carousel layouts.

- **Components**

  Components are essential UI elements that form the visual appearance of the interface. Those provided directly by the framework are called **system components**, while those defined by developers are called **custom components**. Built-in system components include buttons, radio buttons, progress bars, text, etc. Developers can set rendering effects for system components through chained calls. System components can be combined into custom components, modularizing pages into independent UI units for separate creation, development, and reuse, enhancing engineering efficiency.

- **Page Routing and Component Navigation**

  Applications may contain multiple pages, with page routing enabling navigation between them. Within a single page, component navigation (e.g., typical tab bars) can be implemented using navigation components.

- **Graphics**

  The ArkUI framework provides capabilities for displaying various types of images and custom drawing to meet developers' needs, supporting shape drawing, color filling, text rendering, transformations, clipping, and image embedding.

- **Animation**

  Animation is a key UI element. Well-designed animations significantly enhance user experience. The framework offers rich animation capabilities, including built-in component animations, property animations, explicit animations, custom transition animations, and animation APIs. Developers can implement custom animation trajectories using encapsulated physical models or animation APIs.

- **Interaction Events**

  Interaction events are essential for UI-user interaction. The ArkUI framework provides various interaction events, including general events like touch, mouse, keyboard, and focus events, as well as gesture events derived from these general events. Gesture events include single gestures (e.g., tap, long press, drag, pinch, rotate, swipe) and composite gestures combining single gestures.

- **Customization Capabilities**

  Customization capabilities allow developers to tailor UI interfaces, including custom combinations, extensions, nodes, and rendering.

## Features

- High Development Efficiency and Excellent Developer Experience

    - Concise Code: Describes UIs in a near-natural semantic manner, freeing developers from worrying about framework-level UI drawing and rendering.

    - Data-Driven UI Changes: Enables developers to focus on business logic. When UIs change, developers only need to modify the data causing the changes, leaving the UI updates to the framework.

    - Enhanced Developer Experience: Treating interfaces as code improves programming experience.

- Superior Performance

    - Layered Declarative UI Frontend and Backend: The UI backend, built in C++, provides foundational components, layouts, animations, interaction events, component state management, and rendering pipelines for the frontend.

    - Optimized Language Compiler and Runtime: Features include unified bytecode, efficient FFI (Foreign Function Interface), AOT (Ahead Of Time), minimized engine footprint, and type optimization.

- Rapid Ecosystem Advancement:
  Leverages mainstream language ecosystems for quick adoption, with a relatively neutral and friendly language design and support from standard organizations for gradual evolution.

## Development Process

When developing applications with the UI development framework, the following processes are primarily involved.

| Task          | Description                                  | Related Guides                                     |
| :----------- | :----------------------------------- | :---------------------------------------- |
|Learn Cangjie|Introduces basic Cangjie syntax, state management, and rendering control scenarios.| - [Basic Syntax](./paradigm/cj-basic-syntax-overview.md)<br> - [State Management](./state_management/cj-state-management-overview.md)<br> - [Rendering Control](./rendering_control/cj-rendering-control-overview.md)|
| Develop Layout| Introduces several common layout methods.| - [Common Layouts](./cj-layout-development-overview.md)<br/> |
| Add Components| Introduces usage methods for several common system components. | - [Common Components](cj-common-components-button.md)<br/> - [Custom Components](./paradigm/cj-create-custom-components.md)|
| Use Text | Introduces usage methods for text components like input fields and rich text.| - [Text](cj-text-introduction.md)<br/>- [Text Display](cj-common-components-text-display.md) <br/>- [Text Input](cj-common-components-text-input.md)<br/> - [Rich Text](./cj-common-components-richeditor.md)<br>|
| Use Dialogs | Introduces application scenarios and usage methods for dialogs. | - [Dialogs](cj-dialog-overview.md)<br/>- [Popup Dialogs](cj-dialog-base-overview.md)<br> - [Menu Control](./cj-popup-and-menu-components-menu.md)<br/>- [Global Custom Dialogs Independent of UI Components](cj-uicontext-custom-dialog.md)<br/>- [Fixed-Style Dialogs](cj-fixes-style-dialog.md)<br/>- [Tooltips](cj-popup-and-menu-components-popup.md)<br> - [Modal Page Binding](./cj-modal-overview.md)<br> - [Instant Feedback](./cj-create-toast.md)|
| Display Graphics| Introduces how to display images, draw custom geometric shapes, and use canvases for custom graphics.| - [Geometric Shapes](cj-shape-drawing.md)<br/>- [Canvas](cj-drawing-customization-on-canvas.md) |
| Use Animation| Introduces typical scenarios for component and page animations.| - [Animation](cj-animation.md)<br>- [Property Animation](cj-attribute-animation-overview.md)<br>- [Implementing Property Animation](cj-attribute-animation-apis.md)<br>- [Transition Animation](cj-transition-overview.md)<br>- [Enter/Exit Transition](cj-enter-exit-transition.md)<br>- [Modal Transition](cj-modal-transition.md)<br>- [Component Animation](cj-component-animation.md)<br>- [Animation Curves](cj-curve-overview.md)<br>- [Traditional Curves](cj-traditional-curve.md)<br>- [Animation Smoothing](cj-animation-smoothing.md)<br>- [Blur](cj-blur-effect.md)<br>- [Shadow](cj-shadow-effect.md)<br>- [Color](cj-color-effect.md)<br> - [Frame Animation](cj-animator.md)|
|Bind Events| Introduces basic event concepts and how to use general and gesture events.| - [Interaction Events](cj-event-overview.md)<br/>- [Event Distribution](cj-common-events-distribute.md)<br/>-&nbsp;[Touch Events](cj-common-events-touch-screen-event.md)<br/>- [Keyboard/Mouse Events](cj-common-events-device-input-event.md)<br/>- [Focus Events](cj-common-events-focus-event.md)<br/>- [Drag Events](../../../en/application-dev/reference/arkui-cj/cj-universal-event-drag.md)|
|Use Mirroring Capabilities|Introduces basic concepts and usage of mirroring capabilities.| - [Using Mirroring Capabilities](./cj-mirroring-display.md)|
|Support Aging-Friendly Design|Introduces scenarios and methods for aging-friendly design.| - Support Aging-Friendly Design |
|Theme Settings|Introduces application-level and page-level theme setting capabilities.| - [Dark/Light Theme Adaptation](./cj-ui-dark-light-color-adaptation.md)|

## General Rules

- **Default Units**

  Length parameters default to vp (virtual pixels), meaning parameters of type Int32 and [Length](../../../en/application-dev/reference/arkui-cj/cj-common-types.md#interface-length) types (Int64, Float64) are in vp.

- **Invalid Value Handling**

  For invalid input parameters, the following rules apply:

    - If the parameter has a default value, the default is used.

    - If the parameter has no default value, the corresponding property or interface is ignored.