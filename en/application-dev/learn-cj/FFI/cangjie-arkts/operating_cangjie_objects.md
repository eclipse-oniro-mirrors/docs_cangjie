# ArkTS Access to Cangjie Data

This chapter introduces three methods for manipulating Cangjie objects in ArkTS:

1. **Custom Functions**: Utilize ArkTS runtime's memory management mechanism to control the lifecycle of Cangjie objects and access them through relevant interoperability interfaces.
2. **JSExternal**: Store Cangjie objects in JSExternal and bind them to JSObject, hiding JSExternal data to enhance interface security.
3. **JSClass**: For performance-critical scenarios, define a JSClass to accelerate object creation and reduce memory footprint.

## Custom Functions

This example demonstrates sharing Cangjie objects to the ArkTS runtime, using ArkTS runtime's memory management to control their lifecycle and accessing them through interoperability interfaces:

1. Define Cangjie functions:

    <!--compile-->
    ```cangjie
    // Import interoperability libraries
    import ohos.ark_interop.*
    import ohos.ark_interop_macro.*
    // Define shared class (SharedObject is a class from the interoperability library)
    class Data <: SharedObject {
        Data(
            // Define two properties
            var id: Int64,
            let name: String
        ) {}

        static init() {
            // Register functions to be exported to Ark
            JSModule.registerFunc("createData", createData)
            JSModule.registerFunc("setDataId", setDataId)
            JSModule.registerFunc("getDataId", getDataId)
        }

        // Create shared object
        static func createData(context: JSContext, _: JSCallInfo): JSValue {
            // Create Cangjie object
            let data = Data(1, "abc")
            // Create JS reference to Cangjie object
            let jsExternal = context.external(data)
            // Return JS reference to Cangjie object
            return jsExternal.toJSValue()
        }

        // Set object's ID
        static func setDataId(context: JSContext, callInfo: JSCallInfo): JSValue {
            // Read parameters
            let arg0 = callInfo[0]
            let arg1 = callInfo[1]

            // Convert parameter 0 to JS reference of Cangjie object
            let jsExternal = arg0.asExternal()
            // Get Cangjie object
            let data: Data = jsExternal.cast<Data>().getOrThrow()
            // Convert parameter 1 to Float64
            let value = arg1.toNumber()

            // Modify Cangjie object property
            data.id = Int64(value)

            // Return undefined
            let result = context.undefined().toJSValue()
            return result
        }

        // Get object's ID
        static func getDataId(context: JSContext, callInfo: JSCallInfo): JSValue {
            let arg0 = callInfo[0]

            let jsExternal = arg0.asExternal()

            let data: Data = jsExternal.cast<Data>().getOrThrow()

            let result = context.number(Float64(data.id)).toJSValue()
            return result
        }
    }
    ```

2. Provide interface declarations in Index.d.ts:

    ```typescript
    // Index.d.ts corresponding to libohos_app_cangjie_entry.so
    export declare function createData(): undefined;
    export declare function setDataId(data: undefined, value: number): void;
    export declare function getDataId(data: undefined): number;
    ```

3. ArkTS calls Cangjie functions:

    ```typescript
    // Import Cangjie dynamic library (library name should match the package name containing interoperability interfaces)
    import cjLib from "libohos_app_cangjie_entry.so";

    // Create shared object
    let data = cjLib.createData();
    // Manipulate object properties
    cjLib.setDataId(data, 3);
    let id = cjLib.getDataId(data);

    console.log("id is " + id);
    ```

JSExternal objects are recognized as `undefined` in ArkTS. Directly using `undefined` as parameters may lead to runtime errors when incorrect arguments are passed:

```typescript
// ...
// Create shared object
let data = cjLib.createData();
// Manipulate object properties
cjLib.setDataId(undefined, 3); // Wrong parameter (should be Cangjie reference), but compiler won't catch this
let id = cjLib.getDataId(data);
// ...
```

## JSExternal

In actual development, you can bind JSExternal objects to JSObject to hide JSExternal data and improve interface security.

Example implementation:

### Define Cangjie functions

<!--compile-->
```cangjie
// Import interoperability libraries
import ohos.ark_interop.*
import ohos.ark_interop_macro.*
// Define shared class
class Data <: SharedObject {
    Data(
        // Define two properties
        var id: Int64,
        let name: String
    ) {}

    static init() {
        // Register function to be exported to Ark
        JSModule.registerFunc("createData", createData)
    }

    // Create shared object
    static func createData(context: JSContext, _: JSCallInfo): JSValue {
        let data = Data(1, "abc")
        let jsExternal = context.external(data)

        // Create empty JSObject
        let object = context.object()
        // Attach JS reference of Cangjie object as hidden property
        object.attachCJObject(jsExternal)

        // Add two methods to JS object
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
        let thisObject = thisArg.asObject()
        // Get hidden property from JSObject
        let jsExternal = thisObject.getAttachInfo().getOrThrow()
        // Get Cangjie object from JS reference
        let data = jsExternal.cast<Data>().getOrThrow()
        // Convert parameter 0 to Float64
        let value = arg0.toNumber()

        // Modify Cangjie object property
        data.id = Int64(value)

        let result = context.undefined()
        return result.toJSValue()
    }

    // Get object's ID
    static func getDataId(context: JSContext, callInfo: JSCallInfo): JSValue {
        let thisArg = callInfo.thisArg
        let thisObject = thisArg.asObject()
        let jsExternal = thisObject.getAttachInfo().getOrThrow()
        let data = jsExternal.cast<Data>().getOrThrow()

        let result = context.number(Float64(data.id)).toJSValue()
        return result
    }
}
```

### Provide interface declarations

In Index.d.ts file:

```typescript
// Index.d.ts corresponding to libohos_app_cangjie_entry.so
interface Data {
    setId(value: number): void;
    getId(): number;
}

export declare function createData(): Data;
```

### ArkTS calls Cangjie functions

```typescript
// Import Cangjie dynamic library
import cjLib from "libohos_app_cangjie_entry.so";

// Create shared object
let data = cjLib.createData();
// Manipulate object properties
data.setId(3);
let id = data.getId();

console.log("id is " + id);
```

## JSClass

Attaching all object operation methods directly to objects consumes more memory and increases object creation overhead. For performance-critical scenarios, define a JSClass to accelerate object creation and reduce memory usage:

1. Define Cangjie functions:

    <!--compile-->
    ```cangjie
    // Import interoperability libraries
    import ohos.ark_interop.*
    import ohos.ark_interop_macro.*
    // Define shared class
    class Data <: SharedObject {
        Data(
            // Define two properties
            var id: Int64,
            let name: String
        ) {}

        static init() {
            // Register class to be exported to Ark
            JSModule.registerClass("Data") { context =>
                // Create JSClass
                let clazz = context.clazz(jsConstructor)
                // Add methods
                clazz.addMethod(context.string("setId"), context.function(setDataId))
                clazz.addMethod(context.string("getId"), context.function(getDataId))

                return clazz
            }
        }

        // JS constructor
        static func jsConstructor(context: JSContext, callInfo: JSCallInfo): JSValue {
            // Get this pointer
            let thisArg = callInfo.thisArg
            // Convert to JSObject
            let thisObject = thisArg.asObject()
            // Create object
            let data = Data(1, "abc")
            // Create JS reference to Cangjie object
            let jsExternal = context.external(data)
            // Set JSObject property
            thisObject.attachCJObject(jsExternal)
            return thisObject.toJSValue()
        }

        // Set object's ID
        static func setDataId(context: JSContext, callInfo: JSCallInfo): JSValue {
            // Get this pointer
            let thisArg = callInfo.thisArg
            // Convert this pointer to JSObject
            let thisObject = thisArg.asObject()
            // Get hidden property from JSObject
            let jsExternal = thisObject.getAttachInfo().getOrThrow()
            // Get Cangjie object from JS reference
            let data = jsExternal.cast<Data>().getOrThrow()

            let arg0 = callInfo[0]
            // Convert parameter 0 to Float64
            let value = arg0.toNumber()

            // Modify Cangjie object property
            data.id = Int64(value)

            let result = context.undefined()
            return result.toJSValue()
        }

        // Get object's ID
        static func getDataId(context: JSContext, callInfo: JSCallInfo): JSValue {
            let thisArg = callInfo.thisArg
            let thisObject = thisArg.asObject()
            let jsExternal = thisObject.getAttachInfo().getOrThrow()
            let data = jsExternal.cast<Data>().getOrThrow()

            let result = context.number(Float64(data.id)).toJSValue()
            return result
        }
    }
    ```

2. Provide interface declarations in Index.d.ts:

    ```typescript
    // Index.d.ts corresponding to libohos_app_cangjie_entry.so
    export declare class Data {
        setId(value: number): void;
        getId(): number;
        constructor();
    }
    ```

3. ArkTS calls Cangjie functions:

    ```typescript
    // Import Cangjie dynamic library
    import cjLib from "libohos_app_cangjie_entry.so";

    // Create shared object
    let data = new cjLib.Data();
    // Manipulate object properties
    data.setId(3);
    let id = data.getId();

    console.log("id is " + id);
    ```