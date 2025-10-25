# Development Preparation

This document is intended for beginners in Cangjie application development. By building a simple application with page navigation/return functionality (as shown in the figure below), you can quickly understand the main files in the project directory and familiarize yourself with the Cangjie application development process.

![cangjieFirstDemo](../../figures/cangjieFirstDemo.png)

Before getting started, you need to understand two fundamental concepts about Cangjie applications: the UI framework and the application model.

## Basic Concepts

### UI Framework

Cangjie provides a UI development framework that offers developers essential capabilities for application UI development, such as various components, layout calculations, UI interactions, rendering, and more.

### Application Model

The application model is an abstraction provided by OpenHarmony for developers, encapsulating the necessary capabilities for applications. It includes essential components and runtime mechanisms. With the application model, developers can build applications based on a unified framework, making development simpler and more efficient.

Cangjie applications use the Stage model. In this model, classes like AbilityStage and WindowStage serve as the "stage" for application components and window management, hence the name Stage model. For details on Stage model development, refer to [Stage Model Development Overview](https://developerlf.hwcloudtest.cn/consumer/cn/doc/cangjie-guides/cj-stage-model-development-overview).

The quick start guide provides several development examples with different types of pages, all built on the Stage model to help developers understand the above concepts and the application development process.

- [Build Your First Cangjie Application](./cj-quick-start-first-cangjie-app.md): Create a simple pure Cangjie application with page navigation/return functionality.
- [Build Your First Cangjie and ArkTS Hybrid Application](./cj-quick-start-first-cangjie-hybrid-app.md): Create a simple hybrid application with page navigation/return functionality using both Cangjie and ArkTS.
- [Incrementally Adopt Cangjie in an Existing ArkTS Project](./cj-quick-start-first-cangjie-hybrid-module.md): Based on a simple pure ArkTS application with page navigation/return functionality, introduce Cangjie to develop incremental features.
- [Cangjie Calling ArkTS Third-Party Modules](./cj-quick-start-dts2cj-plugin-usage.md): Call ArkTS third-party library functions in Cangjie code.

After understanding these basic concepts, proceed to [Build Your First Cangjie Application](cj-quick-start-first-cangjie-app.md) for further exploration and learning.