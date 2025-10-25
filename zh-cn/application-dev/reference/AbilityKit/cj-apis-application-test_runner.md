# ohos.application.test_runner

本模块提供了框架测试的能力。

## 导入模块

```cangjie
import kit.AbilityKit.*
```

## 权限列表

ohos.permission.DISTRIBUTED_DATASYNC

ohos.permission.PREPARE_APP_TERMINATE

ohos.permission.PRIVACY_WINDOW

## 使用说明

API示例代码使用说明：

- 若示例代码首行有"// index.cj"注释，表示该示例可在仓颉模板工程的"index.cj"文件中编译运行。
- 若示例需获取[Context](./cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的"main_ability.cj"文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## class TestRunner

```cangjie
public open class TestRunner {}
```

**功能：** 提供了框架测试的能力。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### static func registerCreator(String, () -> TestRunner)

```cangjie
public static func registerCreator(name: String, creator: () -> TestRunner): Unit
```

**功能：** 注册构建[TestRunner](#class-testrunner)对象的函数。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|构建函数标识。|
|creator|()->[TestRunner](#class-testrunner)|是|-|构建[TestRunner](#class-testrunner)对象的函数。|

**示例：**

<!-- compile -->
```cangjie
import kit.TestKit.*

let TESTRUNNER_REGISTER_RESULT = TestRunner.registerCreator("test", () -> MyTestRunner)

class MyTestRunner <: TestRunner {
    public override func onPrepare(): Unit {
    }
}

### func onPrepare()

```cangjie
public open func onPrepare(): Unit
```

**功能：** 运行测试用例。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.TestKit.*

let TESTRUNNER_REGISTER_RESULT = TestRunner.registerCreator("test", () -> MyTestRunner)

class MyTestRunner <: TestRunner {
    public override func onPrepare(): Unit {
    }
}

### func onRun()

```cangjie
public open func onRun(): Unit
```

**功能：** 为运行测试用例准备单元测试环境。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.TestKit.*

let TESTRUNNER_REGISTER_RESULT = TestRunner.registerCreator("test", () -> MyTestRunner)

class MyTestRunner <: TestRunner {
    public override func onRun(): Unit {
    }
}
