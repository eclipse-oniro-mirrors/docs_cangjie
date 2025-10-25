# Introduction to Performance Analysis Kit  

Performance Analysis Kit provides developers with tools for application event, log, and trace analysis, enabling observation of application runtime states. It supports behavior analysis, fault analysis, security analysis, and statistical analysis, helping developers continuously improve application performance.  

## Usage Scenarios  

- **Application Debugging**: Provides streaming log functionality to help developers record and retrieve logs for issue analysis.  
- **Fault Localization**: Offers fault scenarios across various contexts, including logs, events, and traces related to reliability, performance, power consumption, and distributed faults.  
- **Online Monitoring**: Provides interfaces for logs, events, and traces required for building online observability, facilitating developers in recording and analyzing application runtime conditions.  

## Capabilities  

- **HiLog Streaming Logs**: Enables developers to record and retrieve streaming logs.  
- **HiTraceMeter Tracing**: Provides developers with trace measurement and distributed tracing capabilities across threads and processes.  
- **HiAppEvent Application Events**: Allows developers to record fault, behavior, security, and statistical events, subscribe to system events, and configure data handlers for data upload.  
- **FaultLogger Fault Log Management**: Offers developers a channel to proactively query fault logs.  

## Highlights/Features  

**Convenient APM System Construction**  

- Provides interfaces (HiAppEvent, HiLog) to build custom client-side APM SDKs and integrate with vendor-developed APM solutions.  
- Enables quick recording and collection of operational and maintenance events through custom events and system event subscription based on HiAppEvent.  

**Robust Exception Handling Mechanism**  

- Delivers concise, standardized, and comprehensive exception logs, supporting precise recording of exception propagation paths.  
- Features a comprehensive exception detection mechanism for real-time exception awareness, application notification, and automatic recovery.  

**Comprehensive Basic Diagnostic Capabilities**  

- Logs support hierarchical classification, multi-language compatibility, privacy processing, and traffic control.  
- Offers a complete event framework with mechanisms for event tagging, recording, and reporting.  
- Supports process trajectory tracing for program performance analysis.  

## Fault Analysis  

Based on the Performance Analysis Kit, developers are equipped with comprehensive fault detection and exception handling capabilities. Given the vast diversity of fault types, varying causes, and manifestations across different products and software businesses, diagnosing complex issues tests engineers' experience, skills, and ingenuity. Stability is a critical quality attribute of applications, significantly influencing development efficiency, delivery costs, and overall application quality and user experience. Typically, fault management design during development and runtime can enhance version quality, encompassing fault detection, analysis, localization, recovery, and quality measurement.  

To assist developers in quickly and effectively identifying and resolving application stability faults, this section also introduces general localization methods for faults such as **Cangjie Crash**, **CppCrash**, **AppFreeze**, and **resource leaks**, along with common analysis cases. Relevant content assumes developers have foundational knowledge of programming languages and operating systems. Case analyses may also involve basic usage and practices of DevEco Studio capabilities and SDK-related suites.