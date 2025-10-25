# Refresh

可以进行页面下拉操作并显示刷新动效的容器组件。

## 导入模块

```cangjie
import kit.ArkUI.*
```

## 子组件

支持单个子组件。

## 创建组件

### init(?RefreshOptions, () -> Unit)

```cangjie
public init(value: ?RefreshOptions, child: () -> Unit)
```

**功能：** 创建refresh组件。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|value|?RefreshOptions|是|-|设置组件刷新时的参数。|
|child|() -> Unit|是|-|声明容器子组件。|

## 通用属性/通用事件

通用属性：全部支持。

通用事件：全部支持。



## 组件事件

### func onStateChange(?(RefreshStatus) -> Unit)

```cangjie
public func onStateChange(callback: ?(RefreshStatus) -> Unit): This
```

**功能：** 设置刷新状态变更时，触发回调。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|?(RefreshStatus)-> Unit|是|-|刷新状态。<br>初始值：{res: RefreshStatus =>}。|

### func onRefreshing(?() -> Unit)

```cangjie
public func onRefreshing(callback: ?() -> Unit): This
```

**功能：** 进入刷新状态时触发回调。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|?()->Unit|是|-|进入刷新状态时触发回调。<br>初始值：{=>}。|

## 基础类型定义

### class RefreshOptions

```cangjie
public class RefreshOptions {
    public var refreshing: ?Bool
    public var changeEvent: ?(Bool) -> Unit
    public init(refreshing!: ?Bool)
    public init(refreshing!: ?Bindable<Bool>)
}
```

**功能：** 用于设置Refresh组件参数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**父类型：**

无

#### var refreshing

```cangjie
public var refreshing: ?Bool
```

**功能：** 当前组件是否正在刷新。

**类型：** ?Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

#### var changeEvent

```cangjie
public var changeEvent: ?(Bool) -> Unit
```

**功能：** 配合 @Binder 宏使用，用于refreshing属性的双向绑定。

**类型：** ?(Bool) -> Unit

**读写能力：** 可读写

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

#### init(?Bool)

```cangjie
public init(refreshing!: ?Bool)
```

**功能：** 创建一个 RefreshOptions 对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|refreshing|?Bool|是|-| **命名参数。** 标识刷新组件当前是否正在刷新。|

#### init(?Bindable\<Bool>)

```cangjie
public init(refreshing!: ?Bindable<Bool>)
```

**功能：** 根据刷新状态创建一个 RefreshOptions 对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|refreshing|?[Bindable](./cj-common-types.md#class-bindable)\<Bool>|否|-| **命名参数。** 标识刷新组件当前是否正在刷新。|


## 示例代码

### 示例1（默认刷新样式）

刷新区域使用默认刷新样式。

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.*
import std.time.*
import std.sync.*

class MyDataSource <: IDataSource<Int64> {
    public MyDataSource(let data_: ArrayList<Int64>) {}
    public var listenerOp: Option<DataChangeListener> = None
    public func getData(index: Int64): Int64 {
        return data_[index]
    }

    public func registerDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = listener
    }

    public func unregisterDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = None
    }
    
    public func refresh(): Unit {
        data_.clear()
        let now = Date.now()
        for (_, index) in data_.indices() {
            data_.insertAt(0, now + index)
        }
        match (listenerOp) {
            case Some(listener) => listener.onDataReloaded()
            case None => ()
        }
    }
}

@Entry
@Component
class EntryView {
    @State @Bind var refreshing: Bool = false
    let data_ = ArrayList<Int64>()
    let dataSrc: MyDataSource
    
    public init() {
        for (index in 0..10) {
            data_.pushBack(Date.now() + index)
        }
        dataSrc = MyDataSource(data_)
    }
    
    func build() {
        Column() {
            Refresh(value: RefreshOptions(refreshing: $refreshing), {
                Scroll() {
                    LazyForEach(this.dataSrc, itemGeneratorFunc: {item: Int64, _: Int64 =>
                        Column() {
                            Text("${Date(item).toLocaleString()}")
                                .fontSize(20)
                                .width(100.percent)
                                .height(50)
                                .textAlign(TextAlign.Center)
                        }
                        .backgroundColor(0xFFFFFF)
                        .margin(5)
                        .borderRadius(5)
                    })
                }
                .edgeEffect(EdgeEffect.Spring)
            })
            .onRefreshing({=>
                TaskRunner.delay({=>
                    this.dataSrc.refresh()
                    this.refreshing = false
                }, 2000)
            })
        }
        .padding(10)
        .backgroundColor(0xDCDCDC)
    }
}
```

![refresh_ex1](figures/refresh_ex1.gif)
