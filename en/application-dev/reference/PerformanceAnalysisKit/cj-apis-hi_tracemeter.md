# ohos.hi_trace_meter (Performance Tracing)

This module provides the capability to trace process trajectories and measure program execution performance. The traced data is intended for analysis using the hiTraceMeter tool.

> **Note**
>
> The performance tracing interfaces `startTrace`, `finishTrace`, and `traceByValue` cannot specify the trace output level, which defaults to the COMMERCIAL level.
>
> User-space trace format uses the vertical bar `|` as a separator. Therefore, string parameters passed through performance tracing interfaces should avoid containing this character to prevent trace parsing exceptions.
>
> The total length of user-space traces is limited to 512 characters. Excess characters will be truncated.

## Importing the Module

```cangjie
import kit.PerformanceAnalysisKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a `// index.cj` comment, it indicates the example can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#cangjie-sample-code-instructions).

## class HiTraceMeter

```cangjie
public class HiTraceMeter {}
```

**Description:** This class provides the capability to trace process trajectories and measure program execution performance.

**System Capability:** SystemCapability.HiviewDFX.HiTrace

**Since:** 21

### static func finishTrace(String, Int32)

```cangjie
public static func finishTrace(name: String, taskId: Int32): Unit
```

**Description:** Marks the end of a pre-traced time-consuming task.

The `name` and `taskId` in [finishTrace](#static-func-finishtracestring-int32) must correspond to the parameters in the initiating [startTrace](#static-func-starttracestring-int32).

**System Capability:** SystemCapability.HiviewDFX.HiTrace

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Name of the task to trace. |
| taskId | Int32 | Yes | - | Task ID. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*

func f1(){
    HiTraceMeter.finishTrace("myTestFunc", 1)
}

func f2(){
    // Tracing parallel execution of tasks with the same name
    HiTraceMeter.startTrace("myTestFunc", 1)
    // Business logic code
    HiTraceMeter.startTrace("myTestFunc", 2)  // Second traced task starts while the first traced task with the same name hasn't ended, indicating parallel execution. The taskId must differ.
    // Business logic code
    HiTraceMeter.finishTrace("myTestFunc", 1)
    // Business logic code
    HiTraceMeter.finishTrace("myTestFunc", 2)
}

func f3(){
    // Tracing serial execution of tasks with the same name
    HiTraceMeter.startTrace("myTestFunc", 1)
    // Business logic code
    HiTraceMeter.finishTrace("myTestFunc", 1)  // First traced task ends
    // Business logic code
    HiTraceMeter.startTrace("myTestFunc", 1)   // Second traced task with the same name starts, executing serially.
    // Business logic code
    HiTraceMeter.finishTrace("myTestFunc", 1)
}

f1()
f2()
f3()
```

### static func startTrace(String, Int32)

```cangjie
public static func startTrace(name: String, taskId: Int32): Unit
```

**Description:** Marks the beginning of a pre-traced time-consuming task.

If multiple tasks with the same `name` need to be traced or the same task needs to be traced multiple times while executing concurrently, each call to [startTrace](#static-func-starttracestring-int32) must use a different `taskId`.

If tasks with the same `name` execute serially, the `taskId` can remain the same. Refer to the example in [HiTraceMeter.finishTrace](#static-func-finishtracestring-int32) for details.

**System Capability:** SystemCapability.HiviewDFX.HiTrace

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Name of the task to trace. |
| taskId | Int32 | Yes | - | Task ID. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*

HiTraceMeter.startTrace("myTestFunc", 1)
```