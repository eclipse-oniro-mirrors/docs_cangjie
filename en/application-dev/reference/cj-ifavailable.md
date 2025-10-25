# API Tagging Control

## Overview

Typically, developers need to tag certain APIs to restrict their usage in different locations of the source code based on these tags. Global tags are obtained from the Cangjie project created by Deveco Studio. For example, if the created project is version 5.1.0, its global API level will be 18. Tagged APIs must comply with the global tag configuration to be legally used.

To achieve API tagging control, the Cangjie language introduces the `@IfAvailable` macro expression. It provides finer-grained control over the usage of tagged APIs based on global tag settings. `@IfAvailable` needs to be used in conjunction with the custom annotation `APILevel`. This chapter will introduce the functionality and usage of `@IfAvailable`.

## Syntax of `@IfAvailable`

<!-- compile -->

```cangjie
@IfAvailable(<label>: <value>, <lambda1>, <lambda2>)
```

Where:

- `<label>` is the parameter name of the custom annotation `APILevel`;
- `<value>` is the parameter of the annotation type, supporting only literal expressions;
- `<label>: <value>` constitutes the condition of `@IfAvailable`;
- `<lambda1>` and `<lambda2>` must comply with Lambda expression syntax and are restricted to parameterless forms. The return types of `<lambda1>` and `<lambda2>` are inferred by the compiler as `Unit`.

## Semantics of `@IfAvailable`

If the condition of `@IfAvailable` holds at runtime, the function body of `<lambda1>` will be executed; otherwise, the function body of `<lambda2>` will be executed. All symbols called in `<lambda1>` will be marked as weak symbols, meaning they are not required to be found during compilation and linking.

In a Cangjie project, using the `@IfAvailable` expression implicitly imports the dependency packages `ohos.device_info` and `ohos.base` by default, without requiring manual import.

### `level` Check

When `<label>` is specified as `level` in the `@IfAvailable` macro expression, this check takes effect.

In any scope, calling APIs with a higher Level than the current scope is prohibited. That is, `<lambda1>` must not call APIs higher than the value specified by `<value>` in `level: <value>`, and `<lambda2>` must not call APIs higher than the Level of the current project.

### `syscap` Check

When `<label>` is specified as `syscap` in the `@IfAvailable` macro expression, this check takes effect.

> **Note:**
>
> - **Intersection**: The set of capabilities shared by all devices;
> - **Union**: The set of capabilities possessed by at least one device.

**Check Rules:**

- No error is reported when the called API satisfies the **intersection**;
- A compilation warning is issued when the called API does not satisfy the **intersection** but satisfies the **union**;
- A compilation error is reported when the called API satisfies neither the **intersection** nor the **union**.

In any scope, calling APIs not supported by any device is prohibited, while calling APIs with syscap in the **intersection** or **union** is allowed. `@IfAvailable` can add capabilities to the **intersection** and **union**, meaning `<lambda1>` can call APIs with the syscap specified by `<value>` in `syscap: <value>`, while `<lambda2>` cannot.

## Examples of `@IfAvailable` Usage

### Using `IfAvailable` to Control `APILevel`

Prerequisite dependencies, providing APIs with different tags:

<!-- compile -pkg0 -->

```cangjie
package ohos.sample

@!APILevel[17]
public func f17() {
    println("level-17")
}

@!APILevel[18]
public func f18() {
    println("level-18")
}

@!APILevel[19]
public func f19() {
    println("level-19")
}
```

Assuming `ohos.sample` is a package provided by the SDK, users can select the desired level when using the Cangjie project in Deveco Studio:

![image-Create-Project-With-Level](./figures/image-Create-Project-With-Level.png)

When using `@IfAvailable`, `<label>: <value>` is `level: xx`, where `xx` is a numeric literal.

<!-- compile -pkg0 -->

```cangjie
import ohos.sample.*

func demo() {
    @IfAvaliable(level: 19, { =>
        // Compile-time: This scope allows calling APIs with level 19 or lower. That is, this branch can use f17, f18, f19, while calling higher-level interfaces will result in a compilation error.
        // Runtime: If the execution device supports level 19, this branch will be executed.
        f17();
        f18();
        f19();
    }, { =>
        // Compile-time: This scope uses the capabilities provided by the project, allowing calls to APIs with level 18 or lower. That is, this branch can use f17, f18, while calling higher-level interfaces will result in a compilation error (e.g., f19).
        // Runtime: If the execution device supports level 18, this branch will be executed.
        f17();
        f18();
        f19(); // compile error
    })
}
```

### Using `IfAvailable` to Control `syscap`

Prerequisite dependencies, providing APIs with different `syscap` tags:

<!-- compile -pkg1 -->

```cangjie
package ohos.sample

@!APILevel[18, syscap: "SystemCapability.A"]
public func f1() {
    println("SystemCapability.A")
}

@!APILevel[18, syscap: "SystemCapability.B"]
public func f2() {
    println("SystemCapability.B")
}

@!APILevel[18, syscap: "SystemCapability.C"]
public func f3() {
    println("SystemCapability.C")
}

@!APILevel[18, syscap: "SystemCapability.D"]
public func f4() {
    println("SystemCapability.D")
}
```

Deveco Studio reads the SystemCapability supported by all devices by default to check whether the scope allows the use of tagged APIs.

Assuming `ohos.sample` is the SDK, Device 1's syscap is `["SystemCapability.A", "SystemCapability.B"]`, and Device 2's syscap is `["SystemCapability.B", "SystemCapability.C"]`.

When using `@IfAvailable`, `<label>: <value>` is `syscap: "SystemCapability.xx"`, where `"SystemCapability.xx"` is a string literal.

<!-- compile -pkg1 -->

```cangjie
import ohos.sample.*

func demo() {
    @IfAvaliable(syscap: "SystemCapability.D", { =>
        // This scope allows the highest usage of ["SystemCapability.A", "SystemCapability.B", "SystemCapability.C", "SystemCapability.D"], where:
        // ["SystemCapability.B", "SystemCapability.D"] will not trigger warnings;
        // ["SystemCapability.A", "SystemCapability.C"] will trigger warnings;
        // Anything not in ["SystemCapability.A", "SystemCapability.B", "SystemCapability.C", "SystemCapability.D"] will trigger errors.
        f1();  // warning
        f2();  // ok
        f3();  // warning
        f4();  // ok
    }, { =>
        // This scope allows the highest usage of ["A", "B", "C"], where:
        // ["B"] will not trigger warnings;
        // ["A", "C"] will trigger warnings;
        // Anything not in ["A", "B", "C"] will trigger errors.
        f1();  // warning
        f2();  // ok
        f3();  // warning
        f4();  // error
    })
}
```