# Introduction to Performance Analysis Kit  

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The Performance Analysis Kit provides developers with tools for application event, log, and trace analysis, enabling observation of application runtime states. It supports behavior analysis, fault analysis, security analysis, and statistical analysis, helping developers continuously improve application performance.  

## Use Cases  

- **Application Debugging**: Provides streaming log functionality to help developers record and retrieve logs for issue analysis.  
- **Fault Localization**: Offers failure scenarios across various contexts, including logs, events, and traces related to reliability, performance, power consumption, and distributed faults.  
- **Online Monitoring**: Provides interfaces for logs, events, and traces required for building online observability, facilitating developers in recording and analyzing application runtime conditions.  

## Capabilities  

- **HiLog Streaming Logs**: Enables developers to record and retrieve streaming logs.  
- **HiTraceMeter and HiTraceChain Tracing**: Provides developers with trace measurement and distributed tracing capabilities across threads and processes.  
- **HiAppEvent Application Events**: Allows developers to record fault, behavior, security, and statistical events, subscribe to system events, and configure data handlers for data upload.  

## Highlights/Features  

**Convenient APM System Construction**  

- Provides interfaces (HiAppEvent, HiLog) for building custom client-side APM SDKs and integrating with vendor-developed APM solutions.  
- Enables quick recording and collection of operational and maintenance events through custom event definitions and system event subscriptions based on HiAppEvent.  

**Robust Exception Handling Mechanism**  

- Offers concise, standardized, and comprehensive exception logs with support for precise recording of exception propagation paths.  
- Features a comprehensive exception detection mechanism for real-time exception awareness, application notification, and automatic recovery.  

**Comprehensive Basic Diagnostic Capabilities**  

- Logs support hierarchical classification, multi-language compatibility, privacy processing, and traffic control.  
- Provides a complete event framework with mechanisms for event marking, recording, and reporting.  
- Supports process trajectory tracking for program performance analysis.  

## Fault Analysis  

The Performance Analysis Kit equips developers with robust fault detection and exception handling capabilities. Given the vast diversity of faults—varying by product and software business—their causes and manifestations differ widely. Thus, diagnosing complex issues tests engineers' experience, skills, and ingenuity. Stability is a critical quality attribute of applications, significantly influencing development efficiency, delivery costs, and overall user experience. Fault management during development and runtime—including detection, analysis, localization, recovery, and quality measurement—can enhance version quality.  

To help developers quickly and effectively identify and resolve stability-related faults, this section also introduces general diagnostic methods for issues such as **Cangjie Crash**, **CppCrash**, **AppFreeze**, **AppKilled (Application Termination)**, and **resource leaks**, along with common analysis cases. These topics require foundational knowledge of programming languages and operating systems. Case analyses may involve the use of **DevEco Studio** capabilities and basic applications of SDK-related suites.