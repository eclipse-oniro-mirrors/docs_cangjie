# Introduction to ArkGraphics 2D

ArkGraphics 2D (Ark 2D Graphics Service) primarily provides capabilities related to graphics rendering and display. Developers can build applications based on a unified set of graphics APIs, making application development simpler and more efficient.

## Capabilities

- Provides the ability to specify frame rates for different types of content, which can be used for developer-customized rendering. For details, refer to [Variable Frame Rate Introduction](./cj-displaysync-overview.md).

## Usage Scenarios

Custom Frame Rate Scenarios: Supports developers in customizing frame rates for rendering based on different content and requirements. For example, setting different frame rates for various game scenes and interfaces to enhance user experience smoothness while achieving balanced power consumption.

## Key Features

- Multiple Frame Rates in a Single Window: Supports setting different rendering frame rates for different content within the same window, such as animations or custom-drawn UIs, with each content running independently.

- Dynamic Frame Rate Configuration for Balancing Performance and Power Consumption: Supports third-party frameworks in dynamically requesting rendering frame rates based on UI scenarios, such as gaming and video applications, to balance smooth performance and power efficiency.