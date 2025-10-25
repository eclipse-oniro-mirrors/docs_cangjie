# ForEach

ForEach接口基于数组类型数据来进行循环渲染。

## 导入模块

```cangjie
import kit.ArkUI.*
```

## class ForEach

```cangjie
public class ForEach<T> <: UINodeBase {
    public init(arr: CollectionEx<T>, itemGenerator!: ItemGenFuncType<T>,
        keyGenerator!: ?KeyGenFuncType<T> = None) {}
    public init(subcomponent: () -> Unit)
}
```

**功能：** 创建一个循环渲染组件。ForEach接口基于数组类型数据来进行循环渲染，需要与容器组件配合使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**父类型：**

- UINodeBase

### init(CollectionEx\<T>, ItemGenFuncType\<T>, ?KeyGenFuncType\<T>)

```cangjie
public init(arr: CollectionEx<T>, itemGenerator!: ItemGenFuncType<T>, keyGenerator!: ?KeyGenFuncType<T> = None)
```

**功能：** 定义ForEach组件。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|arr|CollectionEx\<T>|是|-|用于UI中的数组集合。|
|itemGenerator|ItemGenFuncType\<T>|否|-|项目生成函数。|
|keyGenerator|?KeyGenFuncType\<T>|否|None|键生成函数。|

### init(() -> Unit)

```cangjie
public init(subcomponent: () -> Unit)
```

**功能：** 创建ForEach组件。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|subcomponent|() -> Unit|是|-|子组件构建函数。|

### func pop()

```cangjie
public func pop(): Unit
```

**功能：** 弹出ForEach组件。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22