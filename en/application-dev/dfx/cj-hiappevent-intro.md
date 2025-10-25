# Introduction to HiAppEvent

HiAppEvent is an event tracking mechanism provided at the system level for application developers, helping applications record fault information, statistical data, security events, and user behavior information during runtime. It supports developers in analyzing application performance to further conduct statistical analysis on metrics such as visit counts, daily active users, user behavior patterns, and other key factors affecting product usage.

## Basic Concepts

**Tracking:** Recording changes triggered by user operations to provide business data information for analysis by development, product, and operations teams.

## Event Design Specifications

- **Event Domain:** Identifies the domain of the event. It is recommended to set this as the business module name to distinguish between different business modules.

- **Event Name:** Specifies the name of the event. It is recommended to use specific business names to accurately describe the actual business significance.

- **Event Type:** Specifies the type of event. The following four types are supported:
    - **Behavioral Events:** Record routine user operations, such as button clicks, page navigation, etc.
    - **Fault Events:** Identify and analyze application failures, such as UI freezes, network disconnections, or call drops.
    - **Statistical Events:** Measure and quantify key application behaviors, such as usage duration, visit counts, etc.
    - **Security Events:** Document security-related actions, such as password changes, user authorizations, etc.

- **Event Parameters:** Define the parameters for each event. An event can include a set of parameters, which are recommended to represent event attributes or contextual information to provide detailed descriptions of the event.