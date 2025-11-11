# Cangjie-ArkTS Interoperability Development Specifications

## Context Sensitivity in Multi-Engine Instances

**【Rule】** Cross-engine instance access to JS objects is prohibited.

In multi-engine instance scenarios, each JS object (e.g., instances of `JSValue` and its subclasses) is bound to the engine instance (`JSContext`) that created it. Different engine instances operate independently and cannot share JS objects. Accessing a JS object from a non-owning engine may cause program crashes.

In the Cangjie-ArkTS interoperability library, early interfaces for accessing JS objects required developers to manually pass a `JSContext`. When calling these interfaces, ensure the correct instance is passed. Such interfaces are now marked as "deprecated." It is recommended to use the newer interfaces without `JSContext` parameters, which automatically select the correct engine instance.

**Incorrect Example:**

Cangjie code:

<!--compile.error-->
```cangjie
// Import interoperability library
import ohos.ark_interop.*

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Create a new runtime instance
    let newRuntime = JSRuntime()
    let newContext = newRuntime.mainContext

    // Create a new object on the new runtime
    let newObjValue = newContext.object().toJSValue()

    // Error: Converting the new object's JSValue using the old runtime instance
    let newObj = newObjValue.asObject(context)

    // Error: Using the old runtime instance as a parameter when setting a property on the new object
    newObjValue.setProperty(context, newContext.string("a"), newContext.boolean(false).toJSValue())

    // Error: Using a string key created by the old runtime when getting a property from the object
    newObjValue.getProperty(newContext, context.string("a"))

    return newObjValue
}

let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports => exports["doSth"] = runtime.function(doSth).toJSValue()
}
```

**Correct Example:**

Cangjie code:

<!--compile-->
```cangjie
// Import interoperability library
import ohos.ark_interop.*

func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Create a new runtime instance
    let newRuntime = JSRuntime()
    let newContext = newRuntime.mainContext

    // Create a new object on the new runtime
    let newObjValue = newContext.object().toJSValue()

    // Correct: Converting the new object's JSValue using the new runtime instance
    let newObj = newObjValue.asObject()

    // Correct: Using the non-deprecated interface (no explicit context passing) when setting a property
    newObjValue.setProperty(newContext.string("a"), newContext.boolean(false).toJSValue())

    // Correct: Using a string key created by the new runtime when getting a property
    newObjValue.getProperty(newContext.string("a"))

    return newObjValue
}

let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports => exports["doSth"] = runtime.function(doSth).toJSValue()
}
```

## Exception Handling

**【Rule】** Use `try` statements to catch and handle cross-language call exceptions.

In cross-language function calls, exceptions thrown by the callee are automatically converted into exceptions catchable by the caller through the interoperability library. The caller should use `try` statements to catch and handle exceptions to prevent program errors or crashes.

**Correct Example (Catching Cangjie Exceptions on the ArkTS Side):**

Cangjie-side code:

<!--compile-->
```cangjie
// Import interoperability library
import ohos.ark_interop.*

func doSthWithException(context: JSContext, callInfo: JSCallInfo): JSValue {
    if (callInfo.count > 0) {
        throw Exception("should not pass any argument")
    }
    context.undefined().toJSValue()
}

let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports => exports["doSthWithException"] = runtime.function(doSthWithException).toJSValue()
}
```

ArkTS-side code:

```javascript
interface CJLib {
    doSthWithException(src?: string): void
}

function doSth(lib: CJLib): void {
    // Use try...catch to catch cross-language exceptions when calling cross-language interfaces
    try {
        lib.doSthWithException("xxx")
    } catch (err) {
        // ...
    }
}
```

**Correct Example (Catching ArkTS Exceptions on the Cangjie Side):**

Cangjie-side code:

<!--compile-->
```cangjie
// Import interoperability library
import ohos.ark_interop.*

func callArktsWithExp(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Use try...catch to catch cross-language exceptions when calling cross-language interfaces
    try {
        callInfo[0].asFunction().call()
    } catch (err: JSCodeError) {
        // ...
    }
    context.undefined().toJSValue()
}

let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports => exports["callArktsWithExp"] = runtime.function(callArktsWithExp).toJSValue()
}
```

ArkTS-side code:

```javascript
interface CJLib {
    callArkTSWithExp(callback: () => void): void
}

function doSth(lib: CJLib): void {
    lib.callArkTSWithExp(() => {
        throw new Error("this is an error")
    })
}
```

## Proper Usage of JS Objects Created via `JSContext.external`

**【Rule】** Properly use JS objects created via the `JSContext.external` interface.

JS objects created via `JSContext.external` (`JSExternal` objects) are of type `undefined` on the ArkTS side and should not be directly used as interface parameters. It is recommended to bind `JSExternal` objects to a `JSObject` to encapsulate internal data, improving interface security and maintainability.

**Incorrect Example:**

Cangjie-side code:

<!--compile.error-->
```cangjie
// Import interoperability library
import ohos.ark_interop.*

// Define shared class (SharedObject is a class from the interoperability library)
class Data <: SharedObject {
    Data(
        // Define two properties
        var id: Int64,
        let name: String
    ) {}

    static init() {
        // Register functions to export to ArkTS
        JSModule.registerFunc("createData", createData)
        JSModule.registerFunc("setDataId", setDataId)
        JSModule.registerFunc("getDataId", getDataId)
    }

    // Create shared object
    static func createData(context: JSContext, _: JSCallInfo): JSValue {
        // Create Cangjie object
        let data = Data(1, "abc")
        // Create JS reference to the Cangjie object
        let jsExternal = context.external(data)
        // Return JS reference to the Cangjie object
        return jsExternal.toJSValue()
    }

    // Set object's ID
    static func setDataId(context: JSContext, callInfo: JSCallInfo): JSValue {
        // Read arguments
        let arg0 = callInfo[0]
        let arg1 = callInfo[1]

        // Convert argument 0 to a JS reference to the Cangjie object
        let jsExternal = arg0.asExternal(context)
        // Get the Cangjie object
        let data: Data = jsExternal.cast<Data>().getOrThrow()
        // Convert argument 1 to Float64
        let value = arg1.toNumber()

        // Modify the Cangjie object's property
        data.id = Int64(value)

        // Return undefined
        let result = context.undefined().toJSValue()
        return result
    }

    // Get object's ID
    static func getDataId(context: JSContext, callInfo: JSCallInfo): JSValue {
        let arg0 = callInfo[0]

        let jsExternal = arg0.asExternal(context)

        let data: Data = jsExternal.cast<Data>().getOrThrow()

        let result = context.number(Float64(data.id)).toJSValue()
        return result
    }
}
```

ArkTS interface declaration corresponding to Cangjie-side code:

```javascript
export declare function createData(): undefined;
export declare function setDataId(data: undefined, value: number): void;
export declare function getDataId(data: undefined): number;
```

ArkTS-side code:

```javascript
import { createData, setDatId, getDataId } from "libohos_app_cangjie_entry.so";

// Create shared object
let data = createData();
// Modify object property
setDataId(data, 3);
let id = getDataId(data);

console.log("id is " + id);
```

**Correct Example:**

Cangjie-side code:

<!--compile-->
```cangjie
// Import interoperability library
import ohos.ark_interop.*

// Define shared class
class Data <: SharedObject {
    Data(
        // Define two properties
        var id: Int64,
        let name: String
    ) {}

    static init() {
        // Register function to export to ArkTS
        JSModule.registerFunc("createData", createData)
    }

    // Create shared object
    static func createData(context: JSContext, _: JSCallInfo): JSValue {
        let data = Data(1, "abc")
        let jsExternal = context.external(data)

        // Create empty JSObject
        let object = context.object()
        // Attach JS reference to the Cangjie object as a hidden property of the JSObject
        object.attachCJObject(jsExternal)

        // Add two methods to the JS object
        object["setId"] = context.function(setDataId).toJSValue()
        object["getId"] = context.function(getDataId).toJSValue()

        return object.toJSValue()
    }

    // Set object's ID
    static func setDataId(context: JSContext, callInfo: JSCallInfo): JSValue {
        // Get this pointer
        let thisArg = callInfo.thisArg
        let arg0 = callInfo[0]

        // Convert this pointer to JSObject
        let thisObject = thisArg.asObject(context)
        // Get hidden property from JSObject
        let jsExternal = thisObject.getAttachInfo().getOrThrow()
        // Get Cangjie object from JS reference
        let data = jsExternal.cast<Data>().getOrThrow()
        // Convert argument 0 to Float64
        let value = arg0.toNumber()

        // Modify Cangjie object's property
        data.id = Int64(value)

        let result = context.undefined()
        return result.toJSValue()
    }

    // Get object's ID
    static func getDataId(context: JSContext, callInfo: JSCallInfo): JSValue {
        let thisArg = callInfo.thisArg
        let thisObject = thisArg.asObject(context)
        let jsExternal = thisObject.getAttachInfo().getOrThrow()
        let data = jsExternal.cast<Data>().getOrThrow()

        let result = context.number(Float64(data.id)).toJSValue()
        return result
    }
}
```

ArkTS interface declaration corresponding to Cangjie-side code:

```javascript
export declare interface Data {
    setId(value: number): void;
    getId(): number;
}

export declare function createData(): Data;
```

ArkTS-side code:

```javascript
import { createData } from "libohos_app_cangjie_entry.so";

// Create shared object
let data = createData();
// Modify object property
data.setId(3);
let id = data.getId();

console.log("id is " + id);
```

## Cross-Language Object References

**【Rule】** When passing objects across languages, developers should avoid having local proxy objects hold references to native objects or ensure such references are nullified after use to prevent memory leaks.

During cross-language interoperability, circular references between cross-language objects may occur, preventing related objects from being released and causing memory leaks. The root cause of circular references lies in the ring-shaped dependency between proxy objects (typically parameters or return values of cross-language methods) and native objects. Since their respective garbage collection (GC) mechanisms cannot automatically identify and handle such cross-runtime references, developers must manage them manually.

![interop-circle](../../figures/interop-circle.png)

As shown above, to avoid such issues, it is recommended that developers avoid having proxy objects directly reference native objects during design. If the business scenario requires proxy objects to hold references to native objects, ensure the references are released after use to break the circular dependency.

**Circular Reference Incorrect Example:**

Cangjie-side code:

<!--compile.error-->
```cangjie
import ohos.ark_interop.*

class CJData <: SharedObject {
    let name: String
    var callback: ?()->Unit = None
    init(name: String) {
        this.name = name
    }
}

func createCJData(context: JSContext, callInfo: JSCallInfo): JSValue {
    let object = context.object()
    let data = CJData(callInfo[0].toString())
    object.attachCJObject(context.external(data))
    object.defineOwnAccessor("name", getter: { context, callInfo =>
        context.string(data.name).toJSValue()
    })
    object.defineOwnAccessor("callback", setter: {context, callInfo =>
        let callback = callInfo[0].asFunction()
        data.callback = { =>
            callback.call()
        }
        context.undefined().toJSValue()
    })

    object.toJSValue()
}

let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports => exports["createCJData"] = runtime.function(createCJData).toJSValue()
}
```

ArkTS interface declaration corresponding to Cangjie-side code:

```javascript
export declare interface CJData {
    name: string;
    callback: () => void;
}

export declare function createCJData(): CJData;
```

ArkTS-side code:

```javascript
import { createCJData, CJData } from "libohos_app_cangjie_entry.so"

const data: CJData = createCJData("123")
data.callback = () => {
    console.log(data.name)
}
```

The circular reference in the above example occurs as follows:

1. The `CJData` object **data** created on the ArkTS side holds a reference to the Cangjie object via `external`.
2. The Cangjie object (of type `CJData`) holds the **callback** variable.
3. **callback** captures the ArkTS-side callback function.
4. The ArkTS-side callback function captures the ArkTS-side `CJData` object **data**.

If this scenario is necessary for the business, developers should nullify `data.callback` after execution to break the circular reference. Example:

<!--code_no_check-->
```cangjie
// ...
data.callback()
data.callback = () => {}
// ...
```

## In ArkTS Main Thread, Do Not Block Waiting for Execution Results of spawn(UIThread) in Cangjie Interfaces

**【Rule】** In Cangjie interfaces called from the ArkTS main thread, do not block waiting for the execution results of `spawn(UIThread)`. Otherwise, it will cause a deadlock and trigger an App Freeze failure.

When Cangjie interfaces are called from the ArkTS main thread, the Cangjie code may use the `spawn(UIThread)` expression to dispatch an asynchronous task to the main thread. This operation is typically used to return the execution results of the Cangjie interface to the ArkTS side. Developers must note that they should not block the main thread while waiting for the execution results of `spawn(UIThread)`, as this will cause a deadlock and trigger an App Freeze failure (APP_INPUT_BLOCK). Common blocking behaviors include but are not limited to:

- Using `future.get()` to wait for the return value of the `spawn(UIThread)` expression;
- Using the `lock()` interface of `Mutex` to acquire a lock that will be released in the task of `spawn(UIThread)`.

**Incorrect Example:**

Cangjie-side code:

<!--compile.error-->
```cangjie
import ohos.ark_interop.*
import ohos.ark_interop_macro.*
import ohos.base.UIThread

@Interop[ArkTS]
public func testCJ(): Unit {
    // ...
    let future = spawn(UIThread) {
        // ...
    }
    future.get() // Error: `spawn(UIThread)` dispatches a Cangjie task to the main thread, and `future.get()` waits on the main thread, causing a deadlock
    // ...
}
```

ArkTS-side code:

```javascript
import { testCJ } from "libohos_app_cangjie_entry.so"

@Entry
@Component
struct Index {
   // ...
   testCJ() // Calling a Cangjie interface from the ArkTS main thread
   // ...
}
```

## Cangjie and ArkTS Interoperation Logic Must Execute on System Threads Bound to the ArkTS Runtime

**【Rule】** When Cangjie calls ArkTS, all operations involving ArkTS data access or interface calls must run on system threads bound to the ArkTS runtime. Otherwise, a `JSThreadMisMatch` exception will be triggered.

Cangjie threads are user-mode threads, and the runtime schedules Cangjie threads to execute on system threads. Therefore, Cangjie programs are not bound to specific system threads by default. However, Cangjie and ArkTS interoperation logic must run on system threads bound to the ArkTS runtime. Thus, developers must pay attention to the thread where interoperation occurs. If it is not an ArkTS thread, developers must use the interfaces provided by the interoperation library to switch to the ArkTS thread for execution. Developers can use the following interfaces to ensure correct execution of interoperation logic:

- Use `JSContext.isInBindThread()` to determine whether the current thread can execute interoperation interfaces;
- If thread switching is required, use:
    - `JSContext.postJSTask { ... }` to create a task that executes on the ArkTS thread;
    - If ArkTS is deployed on the main thread, developers can use the `spawn(UIThread)` syntax to schedule the interoperation logic to execute on the main thread.

**Incorrect Example:**

<!--compile.error-->
Cangjie code:

```cangjie
import ohos.ark_interop.*

func addNumberAsync(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get the argument list from JSCallInfo
    let arg0: JSValue = callInfo[0]
    let arg1: JSValue = callInfo[1]
    let arg2: JSValue = callInfo[2]

    // Convert JSValue to Cangjie types
    let a: Float64 = arg0.toNumber()
    let b: Float64 = arg1.toNumber()
    let callback = arg2.asFunction(context)

    // Create a new Cangjie thread
    spawn {
        // Actual Cangjie function behavior
        let value = a + b
        // Create result
        let result = context.number(value).toJSValue() // Error: Not running on a system thread bound to the ArkTS runtime
        // Call the JS callback
        callback.call(result)
    }

    // Return void
    return context.undefined().toJSValue()
}

let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports => exports["addNumberAsync"] = runtime.function(addNumberAsync).toJSValue()
}
```

**Correct Example (Usage of `isInBindThread` & `postJSTask`):**

Cangjie code:

<!--compile-->
```cangjie
import ohos.ark_interop.*

func addNumberAsync(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get the argument list from JSCallInfo
    let arg0: JSValue = callInfo[0]
    let arg1: JSValue = callInfo[1]
    let arg2: JSValue = callInfo[2]

    // Convert JSValue to Cangjie types
    let a: Float64 = arg0.toNumber()
    let b: Float64 = arg1.toNumber()
    let callback = arg2.asFunction(context)

    // Create a new Cangjie thread
    spawn {
        // Actual Cangjie function behavior
        let value = a + b
        if (context.isInBindThread()) { // Correct: If the current thread is a system thread bound to the ArkTS runtime, synchronous calls can be made directly
            // Create result
            let result = context.number(value).toJSValue()
            // Call the JS callback
            callback.call(result)
        } else {                        // Correct: Otherwise, use `postJSTask` to dispatch an asynchronous callback to the ArkTS thread
            context.postJSTask {
                // Create result
                let result = context.number(value).toJSValue()
                // Call the JS callback
                callback.call(result)
            }
        }
    }

    // Return void
    return context.undefined().toJSValue()
}

let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports => exports["addNumberAsync"] = runtime.function(addNumberAsync).toJSValue()
}
```

**Correct Example (Usage of `spawn(UIThread)`):**

Cangjie code:

<!--compile-->
```cangjie
import ohos.ark_interop.*
import ohos.base.UIThread

func addNumberAsync(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get the argument list from JSCallInfo
    let arg0: JSValue = callInfo[0]
    let arg1: JSValue = callInfo[1]
    let arg2: JSValue = callInfo[2]

    // Convert JSValue to Cangjie types
    let a: Float64 = arg0.toNumber()
    let b: Float64 = arg1.toNumber()
    let callback = arg2.asFunction(context)

    // Create a new Cangjie thread
    spawn {
        // Actual Cangjie function behavior
        let value = a + b
        spawn(UIThread) { // Correct: Schedule execution on the ArkTS main thread
            // Create result
            let result = context.number(value).toJSValue()
            // Call the JS callback
            callback.call(result)
        }
    }

    // Return void
    return context.undefined().toJSValue()
}

let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports => exports["addNumberAsync"] = runtime.function(addNumberAsync).toJSValue()
}
```

## In Cangjie Applications, ArkTS Runtime Can Only Be Created Using `JSRuntime()` on the Main Thread

**【Rule】** In Cangjie applications, ArkTS runtime can only be created using `JSRuntime()` on the main thread.

Thread environment requirements dictate that `JSRuntime` must be bound to a system thread, and all interoperation interfaces can only be called on this system thread. Otherwise, undefined behavior will occur. However, Cangjie threads are not 1:1 bound to system threads. As a result, creating a `JSRuntime` in a Cangjie thread spawned via `spawn` will appear as a synchronous call from the Cangjie perspective but may involve thread switching from the ArkTS perspective, leading to undefined behavior or crashes. Therefore, `JSRuntime` can only be created on system threads and not in Cangjie threads.

**Incorrect Example:**

Cangjie code:

<!--compile.error-->
```cangjie
import ohos.ark_interop.*

func addNumberAsync(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Get the argument list from JSCallInfo
    let arg0: JSValue = callInfo[0]
    let arg1: JSValue = callInfo[1]
    let arg2: JSValue = callInfo[2]

    // Convert JSValue to Cangjie types
    let a: Float64 = arg0.toNumber()
    let b: Float64 = arg1.toNumber()
    let callback = arg2.asFunction(context)

    // Create a new Cangjie thread
    spawn {
        let runtime = JSRuntime() // Error: ArkTS runtime can only be created using `JSRuntime()` on the main thread
        // ...
    }

    // Return void
    return context.undefined().toJSValue()
}

let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports => exports["addNumberAsync"] = runtime.function(addNumberAsync).toJSValue()
}
```