# Cangjie-ArkTS Declarative Interop Macros

The Cangjie-ArkTS Declarative Interop Macros automatically generate ArkTS declaration files and interop layer code by parsing annotated Cangjie code, providing developers with a near-native calling experience.

## Usage Instructions

For DevEco Studio configuration, refer to [Adding Cangjie Modules to ArkTS Projects](./add_cangjie_module.md). After configuration, interop modules can be implemented.

Currently, for functions (asynchronous functions), interfaces, and classes that need to be called by ArkTS, the interop declaration macro `@Interop` can be used for annotation. The following demonstrates the specific usage of declarative interop macros using a regular function scenario as an example. For examples of asynchronous functions, interfaces, and classes, refer to [Detailed Scenario Descriptions](#detailed-scenario-descriptions).

### Implementing Cangjie Interop Modules

After successfully inserting a Cangjie interop module into an ArkTS project, custom methods can be implemented in the generated index.cj file. For example:

1. Implement a Cangjie function named `addF64` and annotate it with `@Interop[ArkTS]` to mark it as an interop function. Assume the file is named demo.cj, with the following content:

   <!--compile-->
   ```cangjie
   // Define the package name, which must match the package name in cjpm.toml
   package ohos_app_cangjie_entry
   // Import the interop library ark_interop and interop macros
   import ohos.ark_interop.*
   import ohos.ark_interop_macro.*
   // Implement the custom function addF64, which takes two numbers as input and returns their sum
   @Interop[ArkTS]
   public func addF64(a: Float64, b!: Float64): Float64 {
       a + b
   }
   ```

2. In DevEco Studio, right-click the Cangjie file demo.cj, select **Generate... > Cangjie-ArkTS Interop API**. This will generate the Index.d.ts declaration file and oh_package.json5 configuration file in the **cangjie->types->libohos_app_cangjie_entry** directory, as well as the ark_interop_api.d.ts declaration file and oh_package.json5 configuration file in the **cangjie -> ark_interop_api** directory.

    > **Note:**
    >
    > The .d.ts file generated in the ark_interop_api directory is for compatibility with applications running on OpenHarmony 12 Release or later. If there are no compatibility requirements, this folder can be ignored.

   The content of Index.d.ts in the types->libohos_app_cangjie_entry directory is as follows:

   ```typescript
   export declare function addF64(a: number, b: number): number
   ```

   The oh_package.json5 in the types->libohos_app_cangjie_entry directory is as follows:

   ```json
   {
     "name": "libohos_app_cangjie_entry.so",
     "types": "./Index.d.ts",
     "version": "1.0.0",
     "description": ""
   }
   ```

   The content of ark_interop_api.d.ts in the ark_interop directory is as follows:

   ```typescript
   export declare interface CustomLib {
       addF64(a: number, b: number): number
   }
   ```

   The oh_package.json5 in the ark_interop directory is as follows:

   ```json
   {
     "name": "libark_interop_api.so",
     "types": "./ark_interop_api.d.ts",
     "version": "1.0.0",
     "description": ""
   }
   ```

   Dependencies are automatically added to the oh-package.json5 file in the entry:

   ```json
   "dependencies": {
     // ...
     "libohos_app_cangjie_entry.so": "file:./src/main/cangjie/types/libohos_app_cangjie_entry",
     "libark_interop_api.so": "file:./src/main/cangjie/ark_interop_api",
     // ...
   }
   ```

> **Warning:**
>
> In the same Cangjie module (the same package and its sub-packages), the following rules must be followed to avoid compilation errors or symbol conflicts:
>
> - Functions, interfaces, and classes annotated with `@Interop` must not have the same name.
>
>   Incorrect example:
>
>   ```cangjie
>   @Interop[ArkTS]
>   public func addNumber() : Unit {}
>
>   @Interop[ArkTS]
>   public func addNumber(a: Float64) : Unit {} // Compilation error in the same package; symbol conflicts may occur in parent-child packages
>   ```
>
> - Functions, interfaces, and classes annotated with `@Interop` must not have the same name as those registered with JSModule.registerModule, JSModule.registerClass, or JSModule.registerFunc.
>
>   Incorrect example:
>
>   ```cangjie
>   @Interop[ArkTS]
>   public func addNumber() : Unit {}
>
>   func addFloat() {}
>   let EXPORT_MODULE = JSModule.registerModule {
>       runtime, exports => exports["addNumber"] = runtime.function(addFloat).toJSValue() // Will override the addNumber function annotated with @Interop
>   }
>   ```

### Using Cangjie Modules in ArkTS Code

After implementing the Cangjie interop module, import the Cangjie ohos_app_cangjie_entry module in ArkTS code to load the custom Cangjie interop module and call its interfaces.

Example of using the `addF64` function provided by the Cangjie interop module in an ArkTS application:

```typescript
// Import the Cangjie dynamic library. The library name must match the package name of the interop interface.
import { addF64 } from "libohos_app_cangjie_entry.so"

// Call the Cangjie interface
console.log("result " + addF64(1, 2))
```

## Detailed Scenario Descriptions

The declarative interop macros can annotate functions (asynchronous functions), interfaces, and classes. The recommended usage for different scenarios is as follows:

| Scenario | Type | Annotation |
| :--- | :--- | :--- |
| ArkTS calling Cangjie functions | Function | @Interop[ArkTS] |
| ArkTS calling time-consuming Cangjie functions | Asynchronous function | @Interop[ArkTS, Async] |
| Passing objects created on the ArkTS side to Cangjie | Interface | @Interop[ArkTS] |
| Returning objects created on the Cangjie side to ArkTS | Class | @Interop[ArkTS] for the entire class<br>@Interop[ArkTS, Invisible] for members not intended to be exposed |

### Functions

Functions annotated with declarative interop macros must meet the following conditions; otherwise, compilation errors will occur:

- Must be annotated with `public`
- Type parameters are not supported
- Named parameters are supported, but ArkTS calling methods are the same as for non-named parameters
- Default values are not supported

For function interop usage examples, refer to [Usage Instructions](#usage-instructions).

### Asynchronous Functions

Asynchronous functions annotated with declarative interop macros must meet the following conditions; otherwise, compilation errors will occur:

- Must be annotated with `public`
- Type parameters are not supported
- Named parameters are supported, but ArkTS calling methods are the same as for non-named parameters
- Default values are not supported
- The types `JSStringEx`, `JSArrayEx<T>`, and `JSHashMapEx<K, V>` cannot be used in asynchronous functions

Example of asynchronous function interop:

<!--compile-->
```cangjie
// Create an interop function on the Cangjie side
package ohos_app_cangjie_entry

import ohos.ark_interop.*
import ohos.ark_interop_macro.*

@Interop[ArkTS, Async]
public func doAsync(a: Float64, b: Float64): Float64 {
    a + b
}
```

Automatically generated ArkTS interface:

```typescript
// Generated .d.ts after selecting Generate... > Cangjie-ArkTS Interop API
export declare function doAsync(a: number, b: number): Promise<number>
```

Calling the Cangjie module from the ArkTS side:

```typescript
// Import the Cangjie dynamic library. The library name must match the package name of the interop interface.
import { doAsync } from "libohos_app_cangjie_entry.so";

doAsync(1, 2).then(result => {
    console.log("result " + result);
});
```

### Interfaces

Interfaces annotated with declarative interop macros must meet the following conditions; otherwise, compilation errors will occur:

- Must be annotated with `public`
- Type parameters are not supported
- Inheritance from other interfaces is not supported
- Member functions without modifiers are supported, with other restrictions matching those for functions
- Operator overloading is not supported
- Member properties are supported, including the `mut` modifier

Example of interface interop:

<!--compile-->
```cangjie
// Create an interop function on the Cangjie side
package ohos_app_cangjie_entry

import ohos.ark_interop.*
import ohos.ark_interop_macro.*

@Interop[ArkTS]
public interface InterfaceDemo {
    mut prop id: Float64
    func foo(a!: Float64): Float64
}

@Interop[ArkTS]
public func doInterface(a: InterfaceDemo): Float64  {
    return a.foo(a: a.id)
}
```

Automatically generated ArkTS interface:

```typescript
// Generated .d.ts after selecting Generate... > Cangjie-ArkTS Interop API
export declare interface InterfaceDemo {
    id: number;
    foo: (a: number) => number;
}

export declare function doInterface(a: InterfaceDemo): number;
```

Calling the Cangjie module from the ArkTS side:

```typescript
// Import the Cangjie dynamic library. The library name must match the package name of the interop interface.
import { InterfaceDemo, doInterface } from "libohos_app_cangjie_entry.so";

let callbackInterface = (a: number): number => {
  return a + 1;
}
let inter: InterfaceDemo = {foo: callbackInterface, id: 6};
console.log("result " + doInterface(inter));
```

### Classes

Classes annotated with declarative interop macros must meet the following conditions; otherwise, compilation errors will occur:

- Must be annotated with `public`
- Type parameters are not supported
- Inheritance from other classes is supported but not expanded
- Inheritance from interfaces is supported but not expanded
- Static initializers are not supported
- If there is only one regular constructor or primary constructor, it must be annotated with `public`; other modifiers are not supported, member variable parameters are not supported, and default parameter values are not supported
- Member variables can have default values, must be annotated with `public`, other modifiers are not supported, and variable type annotations cannot be omitted
- Operator overloading is not supported
- Member properties must be annotated with `public`

> **Note:**
>
> Class constraints apply only to members intended to be exposed to ArkTS. Members not intended to be exposed can be marked by omitting the `public` modifier or using `@Interop[ArkTS, Invisible]`.

Example of class interop:

<!--compile-->
```cangjie
// Create an interop function on the Cangjie side
package ohos_app_cangjie_entry

import ohos.ark_interop.*
import ohos.ark_interop_macro.*

@Interop[ArkTS]
public class ClassDemo {
    public var value2: Float64 = 1.0
    public let value3: Float64 = 1.0
    @Interop[ArkTS, Invisible]
    public var value4: Float64 = 1.0

    public init(a: Float64) {
        value2 = a
    }

    public func foo(a: Float64 ): Float64 {
        a
    }

    @Interop[ArkTS, Invisible]
    public func foo2(): Float64 {
        1.0
    }

    public mut prop id: Float64 {
        get() {
            value2
        }
        set(value) {
            this.value2 = value
        }
    }

    public prop id2: Float64 {
        get() {
            value3
        }
    }

    @Interop[ArkTS, Invisible]
    public prop id3: Float64 {
        get() {
            value4
        }
    }
}
```

Automatically generated ArkTS interface:

```typescript
// Generated .d.ts after selecting Generate... > Cangjie-ArkTS Interop API
export declare class ClassDemo {
    value2: number
    value3: number
    foo(number): number
    id: number
    id2: number
    constructor (a: number)
}
```

Calling the Cangjie module from the ArkTS side:

```typescript
// Import the Cangjie dynamic library. The library name must match the package name of the interop interface.
import { ClassDemo } from "libohos_app_cangjie_entry.so";

let class1: ClassDemo = new ClassDemo(3);

console.log("result " + class1.foo(5));
console.log("result " + class1.value2);
```

## Type Mapping

The declarative interop macros support the following data type conversions:

| Cangjie Type | ArkTS Corresponding Type | Notes |
| :----------------------------------------------------------- | :------------- | :----------------------------------------------------------- |
| Int8, Int16, Int32, Int64, UInt8, UInt16, UInt32, UInt64, Float16, Float32, Float64 | number | - |
| Bool | boolean | - |
| String, JSStringEx | string | - |
| Unit | undefined | - |
| Option\<T> | T \| undefined | T cannot be of type Option\<T> or function type. If T is a custom type (class or interface), it must be annotated with Interop macros |
| func | function | - |
| JSArrayEx\<T> | Array\<T> | T cannot be a function type. If T is a custom type (class or interface), it must be annotated with Interop macros |
| JSHashMapEx\<K, V> | Map\<K, V> | V cannot be a function type. If V is a custom type (class or interface), it must be annotated with Interop macros |
| Array\<Byte> | ArrayBuffer | - |
| class | class | - |
| interface | interface | - |

> **Warning:**
>
> - In function signatures annotated with `Interop` macros and in type annotations for member variables and properties, syntax sugar (e.g., `?T` for `Option<T>`) is not supported.
>
> - The types `JSStringEx`, `JSArrayEx<T>`, and `JSHashMapEx<K, V>` can only be used in functions, classes, and interfaces annotated with `Interop` macros.