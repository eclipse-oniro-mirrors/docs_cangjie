# 线程控制

## 背景

仓颉开发HarmonyOS应用的过程中，代码逻辑主要分为两部分：UI 相关逻辑代码和 UI 无关逻辑代码。

- UI 相关逻辑代码：UI 布局描述代码，UI 状态声明及修改代码。
- UI 无关逻辑代码：除 UI 相关逻辑代码以外的其他代码。

UI 相关逻辑代码必须运行在拥有独立 OS 线程的 UI 线程中，UI 无关逻辑代码可以跑在任意 OS 线程中。由于仓颉代码运行于仓颉用户态线程，与 OS 线程不存在显式的绑定关系，进而无法保证 UI 代码逻辑运行在 UI 线程上，容易引发应用卡顿和安全风险等问题。

## 开发范式

支持指定代码逻辑可以自定义调度到UI线程或者非UI线程上运行。

## 导入模块

```cangjie
import kit.ArkUI.*
```

## var UIThread

```cangjie
public let UIThread: MainThreadContext = MainThreadContext.instance_
```

**功能：** UI线程上下文实例。

**类型：** MainThreadContext

**读写能力：** 只读

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

## func launch(() -> Unit)

```cangjie
public func launch(task: () -> Unit): Unit
```

**功能：** 提交任务到主线程执行。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|task|() -> Unit|是|-|执行任务。|

## class MainThreadContext

```cangjie
public class MainThreadContext <: ThreadContext {}
```

**功能：** 主线程上下文类。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**父类型：**

- ThreadContext

### func end()

```cangjie
public func end(): Unit
```

**功能：** 结束线程。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

### func hasEnded()

```cangjie
public func hasEnded(): Bool
```

**功能：** 检查线程是否已结束。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**返回值：**

|类型|说明|
|:---|:---|
|Bool|线程是否已结束。|
