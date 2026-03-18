# Lifecycle Development Using the Interop Library

## Introduction

In the interop library, JSValue is an abstract type that represents an ArkTS value. It can represent any ArkTS value, including primitive types (such as numbers, strings, booleans) and complex object types (such as arrays, functions, objects, etc.).
The lifecycle of a JSValue is tightly bound to the lifecycle of its corresponding ArkTS value. When the ArkTS value is garbage-collected, the associated JSValue becomes invalid. It is critical not to attempt to use a JSValue after its underlying ArkTS value no longer exists.
Framework-managed scopes are typically used to manage the lifecycle of JSValue instances. In the interop library, you can use JSContext.newScope to create and destroy scopes. By creating JSValue instances inside a scope, you ensure they are automatically released when the scope ends, preventing memory leaks.
JSHeapObject is an interop type designed to manage the lifecycle of JSValue. JSHeapObject lets you hold a reference to a JSValue beyond its original context scope. This allows sharing JSValue across different contexts and ensures proper memory release when the value is no longer needed.

## Basic Concepts

The interop library provides a set of capabilities for creating and manipulating ArkTS objects, managing references and lifecycles, and registering garbage-collection callbacks within interop modules. Key concepts include:

* Scope: Manages the lifecycle of ArkTS objects. Object handles created within a scope are only usable inside that scope by default. Once the scope is closed, objects created within it can no longer be accessed.
* Reference Management: The interop library provides functions to create, delete, and manage object references to extend object lifecycles, avoid use-after-free errors, and prevent memory leaks.
* Garbage-Collection Callback: Lets you register a callback to perform custom cleanup when an ArkTS object is garbage-collected.

These concepts enable developers to safely and efficiently work with ArkTS objects in interop modules and ensure proper lifecycle management.

## Scenarios and API Overview

The following interop-library APIs are used for ArkTS object reference management and correct lifecycle handling in interop modules.

| API	| Description |
| ---- | ----|
| JSContext.newScope|	Manages ArkTS object lifecycle to ensure proper memory management when using ArkTS objects in interop code. Creates a temporary scope to hold object references for safe access during execution and automatic cleanup when finished.
| JSValue.asObject, JSValue.asArray, JSValue.asFunction |	Creates safe references to ArkTS objects in interop modules, ensuring the object lifecycle matches module requirements.
| JSHeapObject (e.g., JSObject, JSArray, JSFunction)	| Safe references that can escape the handle scope. The ArkTS object lifecycle outlives the Cangjie object lifecycle.

## Usage Example

Use JSContext.newScope to create a context and pass a custom callback that runs within the scope. This API manages ArkTS object lifecycles and prevents invalid handle releases.

<!--compile-->
```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    context.postJSTask {
        context.newScope {
            let callback = context.function { c, _ =>
                Hilog.info(0, "test", "newScope called")
                c.undefined().toJSValue()
            }
            callback.call()
        }
    }
    context.undefined().toJSValue()
}
```

## Memory Leak Scenarios
Memory leaks occur when created JSValue instances are not managed by a handle scope. The interop library detects such cases and prints the call stack.

Typical leak scenarios:

* Asynchronous tasks implemented via libuv, event handler, FFRT, or similar mechanisms on the C side, with interop calls inside callbacks.
* Interop API calls within Cangjie tasks submitted via spawn(UIThread).