# Development Preparation

This document is intended for beginners in OpenHarmony application development. By using the Cangjie language to build a simple application with page navigation/return functionality (as shown in the figure below), you can quickly understand the main files in the project directory and familiarize yourself with the OpenHarmony application development process.

<!-- Cangjie diff -->

![cangjieFirstDemo](../../figures/cangjieFirstDemo.png)

Before getting started, you need to understand some basic concepts about OpenHarmony applications: a brief introduction to the UI framework and the fundamental concepts of the application model.

## Basic Concepts

### UI Framework

OpenHarmony provides a UI development framework called the ArkUI framework. The ArkUI framework offers developers essential capabilities for application UI development, such as various components, layout calculations, animation capabilities, UI interactions, and drawing.

The ArkUI framework provides three development paradigms for developers with different purposes and technical backgrounds: the declarative development paradigm based on ArkTS, the web-like development paradigm compatible with JS (referred to as "web-like development paradigm"), and the declarative development paradigm based on Cangjie. Below is a simple comparison of these three development paradigms.

| **Development Paradigm Name** | **Language Ecosystem** | **UI Update Method** | **Applicable Scenarios** | **Target Audience** |
| ---------------------------- | --------------------- | -------------------- | ------------------------ | ------------------ |
| ArkTS Declarative Development Paradigm | ArkTS Language | Data-driven updates | Programs with high complexity and team collaboration | Mobile system application developers, system application developers |
| Web-like Development Paradigm | JS Language | Data-driven updates | Applications and cards with relatively simple interfaces | Web front-end developers |
| Cangjie Declarative Development Paradigm | Cangjie Language | Data-driven updates | Programs with high complexity and team collaboration | Mobile system application developers, system application developers |

For more content and guidance on UI framework development, please refer to [UI Development](../../../arkui-cj/cj-ui-development-overview.md).

### Application Model

The application model is an abstraction of the capabilities required by applications provided by OpenHarmony for developers. It offers essential components and operational mechanisms for applications. With the application model, developers can build applications based on a unified model, making application development simpler and more efficient.

As the system evolves, OpenHarmony has introduced two application models:

- **FA (Feature Ability) Model:** Supported since OpenHarmony API 7, this model is no longer the primary focus, and no further development guidance will be provided.
- **Stage Model:** Introduced in OpenHarmony API 9, this is currently the primary and long-term evolving model. In this model, classes such as AbilityStage and WindowStage serve as the "stage" for application components and Window windows, hence the name Stage model. For Stage model development, please refer to [Stage Model Development Overview](../../../application-models/cj-application-models.md). **The Quick Start guide provides development guidance based on this model.**

> **Note:**
>
> OpenHarmony API 22 introduces Cangjie language APIs (only supporting the Stage model).

The Quick Start guide provides a development example with two pages, building the first OpenHarmony application using the Cangjie language based on the Stage model, helping developers understand the above basic concepts and the application development process.

Additionally, the Cangjie language supports interoperability with the ArkTS language. Therefore, the Quick Start guide also provides instructions for building the first OpenHarmony application using a mix of Cangjie and ArkTS languages, helping developers gain a preliminary understanding of mixed development with Cangjie and ArkTS.

## Tool Preparation

Please install the [latest version of DevEco Studio](https://developer.huawei.com/consumer/en/download).

After completing the above steps and understanding the basic concepts, you can proceed to the next step for hands-on experience and learning.
