# Accessing ArkTS Data from Cangjie

This chapter details the usage of ArkTS data through the JSValue type.

## Usage Methods

1. Obtain the ArkTS type corresponding to JSValue

   Parameters passed from ArkTS are of the anonymous type `JSValue`. To use them, you first need to determine their type. There are two ways to obtain the type:

   - Use `JSValue.typeof()` to get the type enumeration `JSType`.
   - Know the type through other means (including but not limited to reading ArkTS source code, referencing documentation, etc.) and then verify it using type-checking interfaces, such as `JSValue.isNumber()` to check if it's a number type.

2. Using JSValue

   After obtaining the JSValue type, you can convert `JSValue` to the corresponding Cangjie type or ArkTS reference.

   - Convert to Cangjie type: The Cangjie data will be a copy of the ArkTS data, and the ArkTS data may be released during the lifecycle of the Cangjie variable. For example, converting an ArkTS string to a Cangjie String: `var a:String = JSValue.toString(JSContext)`.
   - Convert to ArkTS reference: The Cangjie data will be a reference to the ArkTS data, and the ArkTS data must not be released during the lifecycle of the Cangjie variable. For example, converting an ArkTS string to JSString: `var b:JSString = JSValue.asString(JSContext)`.

3. Constructing ArkTS Data from Cangjie Types

   Constructing ArkTS data from Cangjie types is done using methods from JSContext. For example, to create a `number`: `var a : Float64 = JSContext.number(Float64)`.

   The mapping of major ArkTS data types to Cangjie types is as follows:

| ArkTS Type | Reference Type | typeof Type      |
| ---------- | -------------- | ---------------- |
| undefined  | JSUndefined    | JSType.UNDEFINED |
| null       | JSNull         | JSType.NULL      |
| boolean    | JSBoolean      | JSType.BOOL      |
| number     | JSNumber       | JSType.NUMBER    |
| string     | JSString       | JSType.STRING    |
| object     | JSObject       | JSType.OBJECT    |
| Array      | JSArray        | JSType.OBJECT    |
| bigint     | JSBigInt       | JSType.BIGINT    |
| function   | JSFunction     | JSType.FUNCTION  |
| symbol     | JSSymbol       | JSType.SYMBOL    |

## Example Usage

### Manipulating Ordinary ArkTS Objects

Example implementation of an interoperation function:

1. Cangjie function implementation:

    ```cangjie
    // Define the package name, which must match the package name in cjpm.toml
    package ohos_app_cangjie_entry

    // Import the interoperation library ark_interop and interoperation macros
    import ohos.ark_interop.*

    // Define the interoperation function. The parameter types must be (JSContext, JSCallInfo), and the return type must be JSValue.
    func addByObject(context: JSContext, callInfo: JSCallInfo): JSValue {
        // callInfo records the function call parameters. Below is how to get the first parameter:
        let arg0 = callInfo[0]
        // Verify if parameter 0 is an object; otherwise, return undefined
        if (!arg0.isObject()) {
            return context.undefined().toJSValue()
        }
        // Convert JSValue to Float64
        let a = arg0.asObject()["a"].toNumber()
        let b = arg0.asObject()["b"].toNumber()

        let result = a + b
        return context.number(result).toJSValue()
    }

    // The function must be registered in JSModule
    let EXPORT_MODULE = JSModule.registerModule {
        runtime, exports =>
            exports["addByObject"] = runtime.function(addByObject).toJSValue()
    }
    ```

2. Interoperation interface declaration:

    ```typescript
    // Index.d.ts corresponding to libohos_app_cangjie_entry.so
    export declare interface CustomObject {
        a: number;
        b: number;
    }
    // Defined Cangjie interoperation function, with the same name as registered on the Cangjie side
    export declare function addByObject(args: CustomObject): number;
    ```

3. ArkTS function call:

    ```typescript
    // Import the Cangjie dynamic library. The library name is the Cangjie package name, which must match the package name of the interoperation interface.
    import { addByObject } from "libohos_app_cangjie_entry.so";
    
    // Call the Cangjie interface
    let result = addByObject({a: 1, b: 2});
    console.log("result = " + result);
    ```

In addition to reading properties from objects, you can also assign values to properties or create new properties using `JSObject[key] = value`, where the key can be a Cangjie String, JSString, or JSSymbol type, and the value is a JSValue type.

> **Note:**
>
> When defining properties via `JSObject[key] = value`, the property is writable, enumerable, and configurable.
> For more details, see [JavaScript Standard Built-in Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object).

**Important Notes:**

1. Property assignment may fail in the following scenarios without throwing exceptions or logging:
   1. The target object is a sealed object created by `Object.seal()`, which cannot be modified or have new properties added.
   2. The target property's `writable` is false, as defined by `Object.defineProperty(object, key, {writable: false, value: xxx})`.

2. For an unknown object, you can enumerate its enumerable properties:

   ```cangjie
   func handleUnknownObject(context: JSContext, target: JSObject): Unit {
       // The keys interface enumerates the object's enumerable properties
       let keys = target.keys()
       println("target keys: ${keys}")
   }
   ```

3. Create a new ArkTS object using `JSContext.object()`.

4. The ArkTS runtime has a special global object accessible from any ArkTS code. On the Cangjie side, it can be accessed via `JSContext.global`.

### Manipulating ArkTS Sendable Objects

ArkTS provides sendable object types to support reference passing during concurrent communication, addressing the need for large object transfers.

On the Cangjie side, sendable objects are handled the same way as ordinary ArkTS objects.

Define a sendable object in ArkTS:

```typescript
// Function definition
@Sendable
class SendableTestClass {
  desc: string = "sendable: this is SendableTestClass ";
  num1: number = 5;
  num2: number = 5;
  printName() {
    console.info("sendable: SendableTestClass desc is: " + this.desc);
  }
  get getNum(): number {
    return this.num1;
  }
}
```

Manipulate the sendable object in Cangjie:

```cangjie
// Define the package name, which must match the package name in cjpm.toml
package ohos_app_cangjie_entry

// Import the interoperation library ark_interop and interoperation macros
import ohos.ark_interop.*

// Define the interoperation function. The parameter types must be (JSContext, JSCallInfo), and the return type must be JSValue.
func readNumber(context: JSContext, callInfo: JSCallInfo): JSValue {
    let obj = callInfo[0].asObject()
    // Get properties from JSObject
    let argA = obj["num1"]
    let argB = obj["num2"]
    // Convert JSValue to Float64
    let a = argA.toNumber()
    let b = argB.toNumber()

    let result = a + b
    return context.number(result).toJSValue()
}

// The function must be registered in JSModule
let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports =>
        exports["readNumber"] = runtime.function(readNumber).toJSValue()
}
```

Declare the interoperation interface in Index.d.ts:

```typescript
// Index.d.ts corresponding to libohos_app_cangjie_entry.so
export declare function readNumber(data: SendableTestClass): number;

interface SendableTestClass {}
```

Construct the sendable object in ArkTS:

```typescript
// Import the Cangjie dynamic library. The library name is the Cangjie package name, which must match the package name of the interoperation interface.
import { readNumber } from "libohos_app_cangjie_entry.so"

// Construct the sendable object
let a = new SendableTestClass();
// Call the Cangjie interface
let result = readNumber(a);
console.log("result = " + result);
```

### ArkTS Async Lock

To address data race issues between concurrent instances, the ArkTS language base library introduces async lock capabilities. For developer efficiency, AsyncLock objects support cross-concurrent instance reference passing. For details, refer to [Async Lock](https://docs.openharmony.cn/pages/v5.1/en/application-dev/arkts-utils/arkts-async-lock-introduction.md). This section focuses on async locks combined with sendable objects.

Cangjie implementation:

```cangjie
// Define the package name, which must match the package name in cjpm.toml
package ohos_app_cangjie_entry

internal import ohos.ark_interop.JSModule
internal import ohos.ark_interop.JSContext
internal import ohos.ark_interop.JSCallInfo
internal import ohos.ark_interop.JSValue

import ohos.hilog.HilogChannel
let logger = HilogChannel(0, 0, "WBT")

func testAsync(context: JSContext, callInfo: JSCallInfo): JSValue {
    // Create PromiseCapability
    let promise = context.promiseCapability()
    spawn {
        // Use a new thread for compute-intensive tasks
        // Return to the ArkTS thread
        context.postJSTask {
            // Return the result to ArkTS
            promise.resolve(context.string("abcdedf").toJSValue())
        }
    }
    // Return Promise
    promise.toJSValue()
}

func readName(context: JSContext, callInfo: JSCallInfo): JSValue {
    let some = callInfo[0].asObject()
    some["lock"].asObject().callMethod("lockAsync", context.function { context, callInfo =>
        return some["name"]
    }.toJSValue())
}

let EXPORT_MODULE = JSModule.registerModule {
    runtime, exports =>
        exports["testAsync"] = runtime.function(testAsync).toJSValue()
        exports["readName"] = runtime.function(readName).toJSValue()
}
```

Declare the interoperation interface in Index.d.ts:

```typescript
// Index.d.ts corresponding to libohos_app_cangjie_entry.so
export declare function testAsync(): Promise<boolean>;
export declare function readName(data: Some): Promise<string>;

interface Some {}
```

Create a file workerTest.ets in entry->src->main->ets. Main thread code:

```typescript
// workerTest.ets
import hilog from '@ohos.hilog';
import worker, {MessageEvents} from '@ohos.worker';
import {ArkTSUtils} from "@kit.ArkTS";

// Import the Cangjie dynamic library. The library name is the Cangjie package name, which must match the package name of the interoperation interface.
import { readName } from "libohos_app_cangjie_entry.so";

// Define the Sendable class
@Sendable
export class Some {
  name: string = "safd";
  type: string = "";
  result: boolean = false;
  lock: ArkTSUtils.locks.AsyncLock;

  constructor() {
    this.lock = new ArkTSUtils.locks.AsyncLock();
  }

  getName(): Promise<string> {
    return this.lock.lockAsync(() => {
      return this.name;
    });
  }

  setName(value: string): Promise<void> {
    return this.lock.lockAsync(() => {
      this.name = value;
    });
  }
}
// Program entry
export async function startTestWorker() {
  hilog.info(0, "test", "worker test begin");
  // Create worker
  const thread = new worker.ThreadWorker("entry/ets/workers/Worker.ets");
  // Create and initialize the event callback table
  const eventHandlers = new Map<string, (msg: MessageEvents) => void>();
  eventHandlers.set("close", (evt) => {
    thread.terminate();
  });
  eventHandlers.set("result", async (evt) => {
    let result = evt.data.value as boolean;
    const name = await a.getName();
    hilog.info(0, "worker", `result is ${result}, name is ${name}`);
  });
  // Listen for worker messages
  thread.onmessage = (evt) => {
    let type = evt.data.type as string;
    if (eventHandlers.has(type)) {
      eventHandlers.get(type)!(evt);
    } else {
      hilog.error(0, "worker", "unknown message type: %{public}s", type);
    }
  };
  // Create the Sendable object
  let a = new Some();
  // Call the Cangjie interface
  hilog.info(0, "test", `name: ${await readName(a)}`);
  // Send the message "begin" to the worker
  a.type = "begin";
  thread.postMessageWithSharedSendable(a);
}
```

Create a workers folder in entry->src->main->ets, and create Workers.ets inside it:

```typescript
// Workers.ets
import {ErrorEvent, MessageEvents, ThreadWorkerGlobalScope, worker} from '@kit.ArkTS';
import hilog from '@ohos.hilog';

// Import the Cangjie dynamic library. The library name is the Cangjie package name, which must match the package name of the interoperation interface.
import { readName, testAsync } from "libohos_app_cangjie_entry.so";

import {Some} from "../workerTest";

// Get the worker thread environment
const workerPort: ThreadWorkerGlobalScope = worker.workerPort;
// Listen for messages from the main thread
workerPort.onmessage = (evt) => {
  let some = evt.data as Some;
  if (some.type == "begin") {
    beginTask(some);
  }
}

async function beginTask(some: Some) {
  // Modify object properties in the worker thread
  await some.setName("modified");
  some.type = "modify";
  hilog.info(0, "worker", `worker name: ${await readName(some)}`);
  // Call the Cangjie function
  testAsync().then(data => {
    hilog.info(0, "worker", `resolved: ${data}`);
    workerPort.postMessage({"type": "result", value: data});
  }).catch((err: Error) => {
    hilog.error(0, "worker", `caught error: ${err.message}`);
    workerPort.postMessage({"type": "result", value: false});
  });
}
```

Start the Worker in ArkTS:

```typescript
// Import the Cangjie dynamic library. The library name is the Cangjie package name, which must match the package name of the interoperation interface.
import { startTestWorker } from "../workerTest"

// Start the Worker
startTestWorker();
```

### Calling ArkTS Functions

#### Ordinary Function Calls

After obtaining an ArkTS function (via parameter passing, global variables, or retrieving from ArkTS data collections like arrays), you can call it directly in Cangjie. This example shows ArkTS calling a Cangjie function, which then calls back an ArkTS function.

1. ArkTS calls Cangjie:

    ```typescript
    // Index.d.ts corresponding to libohos_app_cangjie_entry.so
    export declare function addByCallback(a: number, b: number, callback: (result: number) => void): void;
    ```

    ```typescript
    // 1. Import the Cangjie dynamic library. The library name is the Cangjie package name, which must match the package name of the interoperation interface.
    import { addByCallback } from "libohos_app_cangjie_entry.so";

    // 2. Call the Cangjie interface
    addByCallback(1, 2, (result) => {
        console.log(`1 + 2 = ${result}`);
    });
    ```2. Calling Back ArkTS Functions in Cangjie Code:

    ```cangjie
    package ohos_app_cangjie_entry
    
    internal import ohos.ark_interop.JSModule
    internal import ohos.ark_interop.JSContext
    internal import ohos.ark_interop.JSCallInfo
    internal import ohos.ark_interop.JSValue
    
    func addByCallback(context: JSContext, callInfo: JSCallInfo): JSValue {
        // Get the 1st and 2nd parameters and convert them to Float64
        let a = callInfo[0].toNumber()
        let b = callInfo[1].toNumber()
        // Convert the 3rd parameter to JSFunction
        let callback = callInfo[2].asFunction(context)
        // Calculate the result
        let result = a + b
        // Create ArkTS number from Cangjie Float64
        let retJSValue = context.number(result).toJSValue()
        // Call the callback function
        callback.call(retJSValue)
    }
    
    let EXPORT_MODULE = JSModule.registerModule {
        runtime, exports =>
            exports["addByCallback"] = runtime.function(addByCallback).toJSValue()
    }
    ```

#### Function Calls with this Pointer

The function in this example doesn't have a this pointer. For method calls requiring a this pointer, it can be specified via the named parameter `thisArg`.

```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let callback = callInfo[0].asFunction(context)
    let thisArg = callInfo[1]

    callback.call(thisArg: thisArg)
}
```

In ArkTS code, you can use `object.method(...)` for invocation, which implicitly passes the this pointer.

```typescript
class Someone {
    id: number = 0;
    doSth(): void {
        console.log(`someone ${this.id} have done something`);
    }
}

let target = new Someone();

// This implicitly passes the this pointer and works correctly
target.doSth();

let doSth = target.doSth;
// This doesn't pass the this pointer and will throw `can't read property of undefined` error
doSth.call();
```

The corresponding Cangjie implementation is as follows:

```cangjie
func doSth(context: JSContext, callInfo: JSCallInfo): JSValue {
    let object = callInfo[0].asObject(context)
    // Implicitly passes the this pointer and works correctly
    object.callMethod("doSth")

    let doSth = object["doSth"].asFunction(context)
    // Doesn't pass the this pointer, will throw `can't read property of undefined` error
    doSth.call()
    // Explicitly passes the this pointer and works correctly
    doSth.call(thisArg: object.toJSValue())
}
```