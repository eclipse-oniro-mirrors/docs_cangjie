# Using ArkTS APIs in Cangjie Applications

## Overview

Cangjie supports cross-language interoperability with ArkTS, enabling developers to call application development APIs and standard libraries provided by ArkTS within applications developed using the Cangjie language.

> **Note:**
>
> The application development APIs and language libraries provided by Cangjie are continuously being improved. If Cangjie application developers encounter scenarios where required APIs are not yet available in Cangjie, they can utilize ArkTS APIs to complete their application development.

## Usage Guide

This section explains how to use ArkTS APIs in applications developed with Cangjie.

### Creating an ArkTS Runtime

Developers can create a JSRuntime object in Cangjie applications, which represents an ArkTS runtime instance. Through the JSRuntime object, ArkTS modules can be loaded, and via the mainContext interoperation context within the JSRuntime object, developers can create and access ArkTS data objects. Currently, ArkTS runtimes can only be created on the main thread.

The following example demonstrates creating a JSRuntime object and obtaining the interoperation context through its mainContext:

```cangjie
import ohos.ark_interop.*

func tryLoadArkTSSo() {
    // Create a new ArkTS runtime
    let runtime = JSRuntime()
    // Obtain the interoperation context
    let context = runtime.mainContext
    ...
}
```

### Loading ArkTS Modules

After successfully creating a JSRuntime object, Cangjie can load and run precompiled ArkTS modules. The main types of precompiled ArkTS modules are:

- Dynamic library (.so) files compiled from NAPI modules (C/C++)
- ABC bytecode files compiled from ArkTS modules

> **Note:**
>
> Currently, Cangjie only supports loading and running a subset of ArkTS modules. Attempting to call unsupported ArkTS modules will cause the program to fail.

Assuming there is an ArkTS system module named someModule (.so file), it can be loaded in Cangjie using the `requireSystemNativeModule` method, as shown in the following example:

```cangjie
// Obtain the interoperation context
let context = runtime.mainContext

let module = context.requireSystemNativeModule("someModule")
```

### Calling ArkTS Interfaces

After successfully loading and running an ArkTS module, developers can call the APIs provided by the module using the call method.

Assuming the ArkTS module someModule exports a parameterless ArkTS interface named someFunc, it can be called as follows:

```cangjie
let jsFunc: JSFunction = module["someFunc"].asFunction(context)

let result = jsFunc.call()
```