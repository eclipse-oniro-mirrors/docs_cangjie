# ohos.hi_trace_meter (Performance Tracing)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides the capability to trace process trajectories and measure program execution performance. The traced data is intended for analysis using the hiTraceMeter tool.

> **Note**
>
> The performance tracing interfaces `startTrace`, `finishTrace`, and `traceByValue` cannot specify the trace output level, which defaults to COMMERCIAL level performance tracing.
>
> User-space trace format uses the vertical bar `|` as a separator. Therefore, string parameters passed through performance tracing interfaces should avoid containing this character to prevent trace parsing exceptions.
>
> The total length of user-space traces is limited to 512 characters. Any excess will be truncated.

## Importing the Module

```cangjie
import kit.PerformanceAnalysisKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code begins with a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class HiTraceMeter

```cangjie
public class HiTraceMeter {}
```

**Description:** This class provides the capability to trace process trajectories and measure program execution performance.

**System Capability:** SystemCapability.HiviewDFX.HiTrace

**Since:** 22

### static func finishTrace(String, Int32)

```cangjie
public static func finishTrace(name: String, taskId: Int32): Unit
```

**Description:** Marks the end of a pre-traced time-consuming task.

The `name` and `taskId` parameters in [finishTrace](#static-func-finishtracestring-int32) must correspond to those in the initiating [startTrace](#static-func-starttracestring-int32).

**System Capability:** SystemCapability.HiviewDFX.HiTrace

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | The name of the task to trace. |
| taskId | Int32 | Yes | - | The task ID. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.*
import kit.PerformanceAnalysisKit.*
import kit.CangjieKit.BusinessException

try {
    func f1(){
        HiTraceMeter.finishTrace("myTestFunc", 1)
    }

    func f2(){
        // Trace parallel execution of tasks with the same name
        HiTraceMeter.startTrace("myTestFunc", 1)
        // Business logic code
        HiTraceMeter.startTrace("myTestFunc", 2)  // The second traced task starts while the first traced task with the same name hasn't ended, indicating parallel execution. The taskId must differ for corresponding interfaces.
        // Business logic code
        HiTraceMeter.finishTrace("myTestFunc", 1)
        // Business logic code
        HiTraceMeter.finishTrace("myTestFunc", 2)
    }

    func f3(){
        // Trace serial execution of tasks with the same name
        HiTraceMeter.startTrace("myTestFunc", 1)
        // Business logic code
        HiTraceMeter.finishTrace("myTestFunc", 1)  // The first traced task ends
        // Business logic code
        HiTraceMeter.startTrace("myTestFunc", 1)   // The second traced task with the same name starts, indicating serial execution of tasks with the same name.
        // Business logic code
        HiTraceMeter.finishTrace("myTestFunc", 1)
    }

    f1()
    f2()
    f3()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func startTrace(String, Int32)

```cangjie
public static func startTrace(name: String, taskId: Int32): Unit
```

**Description:** Marks the start of a pre-traced time-consuming task.

If multiple tasks with the same `name` need to be traced or the same task needs to be traced multiple times, and these tasks are executed concurrently, each call to [startTrace](#static-func-starttracestring-int32) must have a different `taskId`.

If tasks with the same `name` are executed serially, the `taskId` can be the same. For specific examples, refer to the sample in [HiTraceMeter.finishTrace](#static-func-finishtracestring-int32).

**System Capability:** SystemCapability.HiviewDFX.HiTrace

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | The name of the task to trace. |
| taskId | Int32 | Yes | - | The task ID. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.*
import kit.PerformanceAnalysisKit.*
import kit.CangjieKit.BusinessException

try {
    HiTraceMeter.startTrace("myTestFunc", 1)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```