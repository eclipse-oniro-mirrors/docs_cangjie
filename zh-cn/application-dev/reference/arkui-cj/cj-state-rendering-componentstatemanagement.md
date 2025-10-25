# 组件级变量的状态管理

提供ObservedArray和ObservedArrayList作为状态管理的数组类型，当其中数组发生变化时，如修改其中一项的值，删除或添加一项，就会触发UI更新。

## 导入模块

```cangjie
import kit.ArkUI.*
```

## ObservedProperty

用于进行状态管理的属性类型。

### class ObservedProperty

```cangjie
public open class ObservedProperty<T> <: ObservedPropertyAbstract {
    public init(String, T)
    public func createProp(String): ObservedProperty<T>
    public func get(): T
    public func set(T): Unit
    public func subscribeEx(Observer): Unit
    public func unsubscribeEx(Observer): Unit
}
```

**功能：** 表示用于进行状态管理的属性类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**父类型：** 

- ObservedPropertyAbstract

#### init(String, T)

```cangjie
public init(info: String, initValue: T)
```

**功能：** 定义一个ObservedProperty类型的属性。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|info|String|是|-|属性信息。|
|initValue|T|是|-|状态管理属性类型的初始化值。|

#### func get()

```cangjie
public func get(): T
```

**功能：** 获取状态管理的属性值。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|T|获取的状态管理属性值。|

#### func set(T)

```cangjie
public open func set(newValue: T): Unit
```

**功能：** 设置状态管理属性类型的新值。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|newValue|T|是|-|状态管理属性被设置的新值。|

#### func createProp(String)

```cangjie
public func createProp(info: String): ObservedProperty<T>
```

**功能：** 创建一个同步属性。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|info|String|是|-|属性信息。|

**返回值：**

|类型|说明|
|:----|:----|
|ObservedProperty\<T>|创建的同步属性。|

#### func subscribeEx(Observer)

```cangjie
public func subscribeEx(observer: Observer): Unit
```

**功能：** 对状态管理数组的每一项进行递归的观察绑定。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|observer|Observer|是|-|绑定的观察类。|

#### func unsubscribeEx(Observer)

```cangjie
public func unsubscribeEx(observer: Observer): Unit
```

**功能：** 对状态管理数组的每一项进行递归的解绑。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|observer|Observer|是|-|解绑的观察类。|

## ObservedArrayList

用于进行状态管理的数组列表类型。

### class ObservedArrayList

```cangjie
public class ObservedArrayList<T> <: ObservedComplexAbstract & CollectionEx<T> {
    public init(ArrayList<T>)
    public init(Array<T>)
}
```

**功能：** 表示用于进行状态管理的数组列表类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**父类型：**

- ObservedComplexAbstract
- CollectionEx\<T>

#### prop size

```cangjie
public prop size: Int64
```

**功能：** 获取状态管理数组列表的大小。

**类型：** Int64

**读写能力：** 只读

**起始版本：** 22

#### init(ArrayList\<T>)

```cangjie
public init(initValue: ArrayList<T>)
```

**功能：** 定义一个ObservedArrayList类型的数组列表。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|initValue|ArrayList\<T>|是|-|状态管理数组列表类型的初始化值。|

#### init(Array\<T>)

```cangjie
public init(initValue: Array<T>)
```

**功能：** 定义一个ObservedArrayList类型的数组列表。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|initValue|Array\<T>|是|-|状态管理数组列表类型的初始化值。|

#### func get()

```cangjie
public func get(): ArrayList<T>
```

**功能：** 获取状态管理的数组列表元素集合。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|ArrayList\<T>|获取的状态管理数组列表集合。|

#### func set(ArrayList\<T>)

```cangjie
public func set(newValue: ArrayList<T>): Unit
```

**功能：** 设置状态管理数组列表类型的新数组列表值。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|newValue|ArrayList\<T>|是|-|状态管理数组列表被设置的新数组列表值。|

#### func set(Array\<T>)

```cangjie
public func set(newValue: Array<T>): Unit
```

**功能：** 设置状态管理数组列表类型的新数组值。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|newValue|Array\<T>|是|-|状态管理数组列表被设置的新数组值。|

#### func set(ObservedComplexAbstract)

```cangjie
public func set(newValue: ObservedComplexAbstract): Unit
```

**功能：** 设置状态管理数组列表类型的新值。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|newValue|ObservedComplexAbstract|是|-|状态管理数组列表被设置的新值。|

#### operator func [](Int64)

```cangjie
public operator func [](index: Int64): T
```

**功能：** 通过索引获取数组列表中的元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|index|Int64|是|-|元素索引。|

**返回值：**

|类型|说明|
|:----|:----|
|T|指定索引位置的元素。|

#### operator func [](Int64, T)

```cangjie
public operator func [](index: Int64, value!: T): Unit
```

**功能：** 通过索引设置数组列表中的元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|index|Int64|是|-|元素索引。|
|value|T|否|-| **命名参数。** 要设置的元素值。|

#### func isEmpty()

```cangjie
public func isEmpty(): Bool
```

**功能：** 判断状态管理数组列表是否为空。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Bool|状态管理数组列表是否为空。|

#### func clone()

```cangjie
public func clone(): ObservedArrayList<T>
```

**功能：** 克隆状态管理数组列表。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|ObservedArrayList\<T>|克隆的状态管理数组列表。|

#### func clear()

```cangjie
public func clear(): Unit
```

**功能：** 清空状态管理数组列表。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

#### func append(T)

```cangjie
public func append(element: T): Unit
```

**功能：** 在状态管理数组列表末尾添加元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|element|T|是|-|要添加的元素。|

#### func appendAll(Collection\<T>)

```cangjie
public func appendAll(elements: Collection<T>): Unit
```

**功能：** 在状态管理数组列表末尾添加多个元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|elements|Collection\<T>|是|-|要添加的元素集合。|

#### func insert(Int64, T)

```cangjie
public func insert(index: Int64, element: T): Unit
```

**功能：** 在状态管理数组列表指定位置插入元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|index|Int64|是|-|插入位置的索引。|
|element|T|是|-|要插入的元素。|

#### func insertAll(Int64, Collection\<T>)

```cangjie
public func insertAll(index: Int64, elements: Collection<T>): Unit
```

**功能：** 在状态管理数组列表指定位置插入多个元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|index|Int64|是|-|插入位置的索引。|
|elements|Collection\<T>|是|-|要插入的元素集合。|

#### func prepend(T)

```cangjie
public func prepend(element: T): Unit
```

**功能：** 在状态管理数组列表开头添加元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|element|T|是|-|要添加的元素。|

#### func prependAll(Collection\<T>)

```cangjie
public func prependAll(elements: Collection<T>): Unit
```

**功能：** 在状态管理数组列表开头添加多个元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|elements|Collection\<T>|是|-|要添加的元素集合。|

#### func remove(Int64)

```cangjie
public func remove(index: Int64): T
```

**功能：** 删除状态管理数组列表指定位置的元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|index|Int64|是|-|要删除元素的索引。|

**返回值：**

|类型|说明|
|:----|:----|
|T|被删除的元素。|

#### func remove(Range\<Int64>)

```cangjie
public func remove(range: Range<Int64>): Unit
```

**功能：** 删除状态管理数组列表指定范围的元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|range|Range\<Int64>|是|-|要删除元素的范围。|

#### func removeIf((T) -> Bool)

```cangjie
public func removeIf(predicate: (T) -> Bool): Unit
```

**功能：** 根据条件删除状态管理数组列表中的元素。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|predicate|(T) -> Bool|是|-|删除条件。|

## 示例代码

状态更新时的注意事项：不允许在spawn表达式中对状态变量进行并发修改，会导致并发安全问题。建议当需要修改状态变量时，采用`concurrency`包提供的`launch`方法，将状态更新的步骤放回主线程中运行，以保证并发安全。如下实例演示如何在spawn表达式中更新变量状态：

<!-- run -->

```cangjie

package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var text: String = "begin"

    func build() {
        Column(space: 30) {
            Button(text).onClick({ evt =>
                changeText({ p: String =>
                    // 使用launch表达式在主线程中更新状态变量
                    launch {
                        text = p
                    }
                })
            })
        }.width(100.percent)
    }

    private func changeText(callback: (String) -> Unit): Unit {
        spawn {
            while (true) {
                callback("blink 0")
                sleep(Duration.millisecond * 100)
                callback("blink 1")
                sleep(Duration.millisecond * 100)
            }
        }
    }
}
```

![componentstatemanagement](figures/componentstatemanagement.gif)