# @Reusable Macro: Component Reusability

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Custom components decorated with @Reusable support component reuse. When a custom component is removed from the component tree, it is cached in the cache pool. When new components of the same type are needed, the system reuses cached objects instead of creating new ones. This avoids repeated creation and destruction of components and improves performance.

## Overview

Using @Reusable to decorate custom components indicates that these components are reusable.

When developing complex UIs, rendering efficiency is a key consideration. For example, during rapid scrolling through long lists, the frequent creation and destruction of numerous list items can cause interface stuttering. Component reuse is an important method for optimizing UI performance. By reusing previously created component objects that have been detached from the tree, the frequency of component creation and destruction is reduced, thereby lowering computational overhead and improving UI rendering efficiency.

> **Note:**
>
> - Custom components decorated with @Reusable (including view nodes, component instances, and state context), when removed from the component tree, will be placed into their parent custom component's cache pool. Subsequent component creation will prioritize reusing nodes from this cache pool, saving the time required for component re-creation.
> - @Reusable provides two lifecycle callbacks: [aboutToRecycle](../../reference/arkui-cj/cj-custom-component-lifecycle.md#func-abouttorecycle) and [aboutToReuse](../../reference/arkui-cj/cj-custom-component-lifecycle.md#func-abouttoreusereuseparams). aboutToRecycle is called to recycle a component, and aboutToReuse is called to reuse a component. You can implement the service logic related to component recycling and reuse in these two lifecycle callbacks.
> - When a @Reusable-decorated custom component has child components, the child components' aboutToRecycle and aboutToReuse will be called recursively during recycling and reuse (regardless of whether the child components are marked with @Reusable), continuing until all child components are traversed.
> - The component structure should remain unchanged before and after reuse. For scenarios where component structures differ, reuseId can be used to distinguish between reusable components with different structures.

## Constraints

### Only for Custom Components

@Reusable is only used for custom components decorated with [@Component](./cj-create-custom-components.md#component) and cannot be used together with [@Builder](./cj-macro-builder.md#builder-macro-custom-build-functions).

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_management.*
import ohos.arkui.state_macro_manage.*

// @Builder cannot be used with @Reusable
// @Reusable
@Builder
func MyBuilder() {
    Crash()
}

@Component
public class Crash {
    public func build() {
        Column() {
            Text("Crash")
                .fontSize(12)
                .lineHeight(8)
                .fontColor(Color.Blue)
        }
        .width(100.percent)
        .height(100.percent)
        .justifyContent(FlexAlign.Center)
    }
}

@Entry
@Component
public class EntryView {
    public func build(): Unit {
        Column() {
            MyBuilder()
        }
    }
}
```

### Component Structure Must Be Consistent

Custom components decorated with @Reusable should maintain the same component structure before and after reuse. Otherwise, child components may be created or destroyed during the reuse process, reducing reuse efficiency and performance, and potentially causing abnormal application behavior.

For child components created during reuse, the framework will call the aboutToReuse method followed by the aboutToAppear method after their creation. When aboutToReuse is called, since aboutToAppear has not yet been executed and internal child components have not been created, operations that depend on the execution result of aboutToAppear or the states of internal child components in aboutToReuse will cause unexpected behavior. After calling aboutToReuse, the framework will then call aboutToAppear to initialize the component.

For scenarios where component structures differ, you must differentiate them by setting different reuseId values. For details, see Multi-Item Type Usage Scenario.

### Nested Usage Not Recommended

Nesting @Reusable decorators is not recommended, as it increases memory usage, reduces reuse efficiency, and complicates maintenance. Nested usage creates additional cache pools with identical tree structures, leading to low reuse efficiency. In addition, it complicates lifecycle management and makes resource and variable sharing difficult.

## Usage Scenarios

### Dynamic Layout Updates

Repeatedly creating and removing views can trigger frequent layout calculations, which may affect frame rates. Component reuse avoids unnecessary view creation and layout recalculations, improving performance.

In the following example, the Child custom component is marked as reusable, and reuse is triggered by updating Child through Button clicks.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

public class Message {
    public var value: String
    public init(val: String) {
        value = val
    }
}

@Entry
@Component
public class EntryView {
    @State var switch: Bool = true
    public func build() {
        Column() {
            Button("Hello")
            .fontSize(30)
            .fontWeight(FontWeight.Bold)
            .onClick({evt =>
                switch = !switch
            })
            if (switch) {
                Child(message: Message("Child"))
            }
        }.height(100.percent).width(100.percent)
    }
}

@Reusable
@Component
class Child {
    @State
    var message: Message = Message("about to reuse")
    protected override func aboutToReuse(params: ReuseParams) {
        if (let Some(value) <- params.get<Message>("message")) {
            message = value
        }
    }
    func build() {
        Column() {
            Text(this.message.value)
        }.borderWidth(1).height(100)
    }
}
```

### List Scrolling with LazyForEach

When a user scrolls a list containing a large amount of data, frequent creation and destruction of list items can cause lag and performance issues. The reuse mechanism of the List component can reuse the existing list items to improve the scrolling smoothness.

The following example marks the CardView custom component as reusable. Scrolling the List up or down triggers reuse of CardView.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

class MyDataSource <: IDataSource<Int64> {
    public MyDataSource(let data_: ArrayList<Int64>) {}
    public var listenerOp: Option<DataChangeListener> = None
    public func totalCount(): Int64 {
        return data_.size
    }
    public func getData(index: Int64): Int64 {
        return data_[index]
    }

    public func pushData(val: Int64): Unit {
        data_.add(val)
    }

    public func registerDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = listener
    }

    public func unregisterDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = None
    }
}

@Entry
@Component
public class EntryView {
    let data: MyDataSource = MyDataSource(ArrayList<Int64>([]))
    protected override func aboutToAppear() {
        for (i in 0..1000) {
            data.pushData(i)
        }
    }

    public func build(): Unit {
        Column() {
            List() {
                LazyForEach(
                    data,
                    itemGenerator: {
                        item: Int64, idx: Int64 => ListItem() {
                            CardView(item: "${item}")
                        }
                    }
                )
            }
        }
    }
}

// Reusable component
@Reusable
@Component
class CardView {
    // Variables decorated with @State can be updated; variables not decorated with @State will not be updated.
    @State
    var item: String = ""

    protected override func aboutToReuse(params: ReuseParams) {
        if (let Some(value) <- params.get<String>("item")) {
            item = value
        }
    }

    func build() {
        Column() {
            Text(item).fontSize(30)
        }.borderWidth(1).height(100)
    }
}
```

### if Usage Scenario

The following example marks the OneMoment custom component as reusable. Scrolling the List up or down triggers reuse of OneMoment. reuseId can be used to assign a reuse group for reusable components. Components with the same reuseId are reused within the same reuse group. A single reusable component does not require reuseId. Using reuseId to identify reusable components avoids repeated deletion and re-creation logic in if statements, improving reuse efficiency and performance.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList
import kit.PerformanceAnalysisKit.Hilog
import kit.LocalizationKit.*

class MyDataSource <: IDataSource<FriendMoment> {
    public MyDataSource(let data_: ArrayList<FriendMoment>) {}
    public var listenerOp: Option<DataChangeListener> = None
    public func totalCount(): Int64 {
        return data_.size
    }
    public func getData(index: Int64): FriendMoment {
        return data_[index]
    }

    public func pushData(val: FriendMoment): Unit {
        data_.add(val)
    }

    public func registerDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = listener
    }

    public func unregisterDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = None
    }
}

public class FriendMoment {
    public var text: String = ""
    public var title: String = ""
    public var image: ?AppResource = None
    public init(text: String, title: String, image: ?AppResource) {
        this.text = text
        this.title = title
        this.image = image
    }

}

@Reusable
@Component
public class OneMoment {
    @State var moment: FriendMoment = FriendMoment("", "", @r(app.media.startIcon))
    protected override func aboutToReuse(params: ReuseParams) {
        if (let Some(value) <- params.get<FriendMoment>("moment")) {
            this.moment = value
            Hilog.info(0, "cangjie", "====aboutToReuse====OneMoment==reused==== ${value.text}")
        }
    }
    public func build() {
        Column() {
            Text(moment.text)
            if (moment.image.isSome()) {
                Flex(wrap: FlexWrap.Wrap) {
                    Image((moment.image) ?? @r(app.media.background)).height(50).width(50)
                    Image((moment.image) ?? @r(app.media.background)).height(50).width(50)
                    Image((moment.image) ?? @r(app.media.background)).height(50).width(50)
                    Image((moment.image) ?? @r(app.media.background)).height(50).width(50)
                }
            }
        }
    }
}

@Entry
@Component
public class EntryView {
    let data: MyDataSource = MyDataSource(ArrayList<FriendMoment>([]))
    protected override func aboutToAppear() {
        for (i in 0..20) {
            let title = "${i+1}test+if"
            data.pushData(FriendMoment("${i}", title, @r(app.media.startIcon)))
        }
        for (i in 0..50) {
            let title = "${i+1}test+if"
            data.pushData(FriendMoment("${i}", title, Option<AppResource>.None))
        }
    }

    public func build(): Unit {
        Column() {
            List() {
                LazyForEach(
                    data,
                    itemGenerator: {
                        item: FriendMoment, idx: Int64 => ListItem() {
                            OneMoment(moment: item)
                        }
                    }
                )
            }
        }
    }
}
```

### List Scrolling - ForEach Usage Scenario

When the ForEach rendering control syntax is used to create reusable custom components, the full-expansion behavior of ForEach prevents component reuse. In the example: Clicking update successfully refreshes data, but ListItemView cannot be reused during list scrolling; clicking clear and then update allows ListItemView to be reused, as this triggers re-creation of multiple destroyed custom components within a single frame.

 <!-- run -->

 ```cangjie
 package ohos_app_cangjie_entry

 import kit.ArkUI.*
 import ohos.arkui.state_macro_manage.*
 import kit.PerformanceAnalysisKit.Hilog

 @Entry
 @Component
 public class EntryView {
    @State var arrlist: ObservedArrayList<Int64> = ObservedArrayList<Int64>([])
    @State var switch: Bool = true

    func build() {
        Column() {
            Button("clear").onClick({e=>
                if (arrlist.size < 50) { return }
                for (i in 0..50) {
                    this.arrlist.remove(0)
                }
            })
            Button("update").onClick({e=>
                for (i in 0..50) {
                    this.arrlist.append(i)
                }
            })
            List(space: 10) {
                ForEach(this.arrlist, itemGenerator: {item: Int64, idx: Int64 =>
                    ListItem() {
                        ListItemView(num: item)
                    }
                }, keyGenerator: {item: Int64, idx: Int64 => "${item}"})
            }.cachedCount(0)
        }.height(100.percent).width(100.percent)
    }
 }

 @Reusable
 @Component
 class ListItemView {
    @State
    var num: Int64 = 0
    protected override func aboutToAppear() {
        // Click update, first entry, scroll up and down, cannot be reused due to ForEach folding and expansion properties.
        Hilog.info(0, "TEST", "=== Child created ===")
    }
    protected override func aboutToReuse(params: ReuseParams) {
        // Click clear, then update again, reuse successful.
        // Matches the scenario of repeatedly creating multiple destroyed custom components within one frame.
        if (let Some(value) <- params.get<Int64>("num")) {
            num = value
        }
    }
    func build() {
        Column() {
            Text("Child ${num}")
        }
    }
 }
 ```

 ### Grid Usage Scenario

 In the following example, the @Reusable macro is used to decorate the custom component ReusableChildComponent in GridItem, indicating that the component can be reused.

The aboutToReuse API is triggered when the component is obtained from the reuse cache and added to the component tree during grid scrolling. This allows you to update the component's state variables to display correct content.

Note that there is no need to update state variables that automatically synchronize values (such as variables decorated with [\@Link](../state_management/cj-macro-link.md), [\@StorageLink](../state_management/cj-appstorage.md#storagelink), or [\@Consume](../state_management/cj-macro-provide-and-consume.md)) in aboutToReuse, as this may trigger unnecessary component re-renders.

 <!-- run -->

 ```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

class MyDataSource <: IDataSource<Int64> {
    public MyDataSource(let data_: ArrayList<Int64>) {}
    public var listenerOp: Option<DataChangeListener> = None
    public func totalCount(): Int64 {
        return data_.size
    }
    public func getData(index: Int64): Int64 {
        return data_[index]
    }

    public func pushData(val: Int64): Unit {
        data_.add(val)
    }

    public func registerDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = listener
    }

    public func unregisterDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = None
    }
}

@Entry
@Component
public class EntryView {
    let data: MyDataSource = MyDataSource(ArrayList<Int64>([]))
    protected override func aboutToAppear() {
        for (i in 0..100) {
            data.pushData(i)
        }
    }

    public func build(): Unit {
        Column() {
            Grid() {
                LazyForEach(data, itemGenerator: {item: Int64, idx: Int64 =>
                    GridItem() {
                        ReusableChildComponent(item: item)
                    }
                })
            }
            .cachedCount(2)
            .columnsTemplate("1fr 1fr 1fr")
            .columnsGap(10)
            .rowsGap(10)
            .margin(10)
            .height(500)
            .backgroundColor(0xFAEEE0)
        }
    }
}


@Reusable
@Component
class ReusableChildComponent {
    @State
    var item: Int64 = 0

    // aboutToReuse is called before adding from reuse cache to the component tree, where you can update component state variables to display correct content.
    protected override func aboutToReuse(params: ReuseParams) {
        if (let Some(value) <- params.get<Int64>("item")) {
            item = value
        }
    }
    public func build() {
        Column() {
           Text("Grid child ${item}")
        }.padding(20)
    }
}
 ```

 ### Swiper Usage Scenario

 For Swiper scrolling scenarios where child components are frequently created and destroyed, you can encapsulate the child components into a custom component and decorate it with @Reusable to implement component reuse.

 <!-- run -->

 ```cangjie
 package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

class MyDataSource <: IDataSource<Int64> {
    public MyDataSource(let data_: ArrayList<Int64>) {}
    public var listenerOp: Option<DataChangeListener> = None
    public func totalCount(): Int64 {
        return data_.size
    }
    public func getData(index: Int64): Int64 {
        return data_[index]
    }

    public func pushData(val: Int64): Unit {
        data_.add(val)
    }

    public func registerDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = listener
    }

    public func unregisterDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = None
    }
}

@Entry
@Component
public class EntryView {
    let data: MyDataSource = MyDataSource(ArrayList<Int64>([]))
    protected override func aboutToAppear() {
        for (i in 0..100) {
            data.pushData(i)
        }
    }

    public func build(): Unit {
        Column() {
            Swiper() {
                LazyForEach(data, itemGenerator: {item: Int64, idx: Int64 =>
                    SwiperItem(item: item)
                }, keyGenerator: {item: Int64, idx: Int64 => "${item}"})
            }
        }
    }
}


@Reusable
@Component
class SwiperItem {
    @State
    var item: Int64 = 0

    protected override func aboutToReuse(params: ReuseParams) {
        if (let Some(value) <- params.get<Int64>("item")) {
            item = value
        }
    }
    public func build() {
        Column() {
           Text("Swiper Content ${item}")
        }.padding(20).height(100).width(100.percent)
    }
}
 ```

 ### List Scrolling - ListItemGroup Usage Scenario

 For list scrolling scenarios where the ListItemGroup component is used, you can encapsulate child components in ListItem that need to be destroyed and re-created into a custom component and decorate it with @Reusable to implement component reuse.

 ```cangjie
 package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

class DataSrc1 <: IDataSource<String> {
    public DataSrc1() {}
    public var data: ArrayList<String> = ArrayList<String>()
    public var listenerOp: Option<DataChangeListener> = None

    public func totalCount(): Int64 {
        return data.size
    }

    public func getData(index: Int64): String {
        return data[index]
    }

    public func registerDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = listener
    }

    public func unregisterDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = None
    }

    public func pushData(val: String): Unit {
        data.add(val)
    }
}

class DataSrc2 <: IDataSource<DataSrc1> {
    public DataSrc2() {}
    public var data: ArrayList<DataSrc1> = ArrayList<DataSrc1>()
    public var listenerOp: Option<DataChangeListener> = None

    public func totalCount(): Int64 {
        return data.size
    }

    public func getData(index: Int64): DataSrc1 {
        return data[index]
    }

    public func registerDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = listener
    }

    public func unregisterDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = None
    }

    public func pushData(val: DataSrc1): Unit {
        data.add(val)
    }
}

@Entry
@Component
class EntryView {
    let data: DataSrc2 = DataSrc2()

    protected override func aboutToAppear() {
        for (i in 0..10000) {
            let data1 = DataSrc1()
            for (j in 0..12) {
                data1.pushData("Test item data: ${i} - ${j}")
            }
            data.pushData(data1)
        }
    }
      @Builder
      func itemHead(text: String) {
        Text(text)
          .fontSize(20)
          .backgroundColor(0xAABBCC)
          .width(100.percent)
          .padding(10)
      }
    public func build() {
        Stack() {
            List() {
                LazyForEach(
                    data,
                    itemGenerator: { item: DataSrc1, index: Int64 =>
                        ListItemGroup(header: {=> bind(itemHead, this)("${index}")}) {
                            LazyForEach(
                                item,
                                itemGenerator: { item2: String, index2: Int64 =>
                                    ListItem() {
                                        Inner(str: item2)
                                    }
                                }
                            )
                        }
                        .width(100.percent)
                        .height(60)
                    }
                )
            }
        }
        .width(100.percent)
        .height(100.percent)
    }
}

@Reusable
@Component
class Inner {
    @State var str: String = ""

    protected override func aboutToReuse(params: ReuseParams) {
        if (let Some(value) <- params.get<String>("str")) {
            str = value
        }
    }

    func build() {
        Text(str)
    }
}
 ```

### Multi-Item Type Usage Scenario

**Standard**

The layout of reusable components is the same. For implementation examples, see the list scrolling sections in this document.

**Composite**

Reusable components have multiple differences but usually share common child components. After converting three reusable components into Builder functions in a combination manner, the internal shared child components will be uniformly placed under the parent component EntryView. When reusing these child components, the cache pool is shared at the parent component level, reducing resource consumption during component creation.

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList
import kit.PerformanceAnalysisKit.Hilog
import kit.LocalizationKit.*

class MyDataSource <: IDataSource<String> {
    public MyDataSource() {}
    private var dataArray: ArrayList<String> = ArrayList<String>()
    private var listenerOp: Option<DataChangeListener> = None

    public func totalCount(): Int64 {
        return dataArray.size
    }

    public func getData(index: Int64): String {
        return dataArray[index]
    }

    public func pushData(data: String): Unit {
        dataArray.add(data)
    }

    public func registerDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = listener
    }

    public func unregisterDataChangeListener(listener: DataChangeListener): Unit {
        listenerOp = None
    }
}

@Entry
@Component
class EntryView {
    let data: MyDataSource = MyDataSource()

    protected override func aboutToAppear() {
        for (i in 0..1000) {
            data.pushData("${i}")
        }
    }

    @Builder
    func itemBuilderOne(item: String) {
        Column() {
            ChildComponentA(item: item)
            ChildComponentB(item: item)
            ChildComponentC(item: item)
        }
    }

    @Builder
    func itemBuilderTwo(item: String) {
        Column() {
            ChildComponentA(item: item)
            ChildComponentC(item: item)
            ChildComponentD(item: item)
        }
    }

    @Builder
    func itemBuilderThree(item: String) {
        Column() {
            ChildComponentA(item: item)
            ChildComponentB(item: item)
            ChildComponentD(item: item)
        }
    }

    public func build() {
        List(space: 40) {
            LazyForEach(
                data,
                itemGenerator: { item: String, index: Int64 =>
                    ListItem() {
                        if (index % 3 == 0) {
                            itemBuilderOne(item)
                        } else if (index % 5 == 0) {
                            itemBuilderTwo(item)
                        } else {
                            itemBuilderThree(item)
                        }
                    }
                    .backgroundColor(0xFFCCCCCC)
                    .width(100.percent)
                    .onAppear({ =>
                        Hilog.info(0, "Sample_ReusableComponent", "ListItem ${index} onAppear")
                    })
                }
            )
        }
        .width(100.percent)
        .height(100.percent)
        .cachedCount(0)
    }
}

@Reusable
@Component
class ChildComponentA {
    @State var item: String = ""

    protected override func aboutToReuse(params: ReuseParams) {
        Hilog.info(0, "Sample_ReusableComponent", "ChildComponentA Reuse")
        if (let Some(value) <- params.get<String>("item")) {
            item = value
        }
    }

    protected override func aboutToRecycle() {
        Hilog.info(0, "Sample_ReusableComponent", "ChildComponentA Recycle")
    }

    func build() {
        Column() {
            Text("Item ${item} Child Component A")
                .fontSize(20)
                .margin(left: 10)
                .fontColor(Color.Blue)
            Grid() {
                ForEach([1,2,3,4,5,6,7,8,9], itemGenerator: { item: Int64, index: Int64 =>
                    GridItem() {
                        // Please add app.media.startIcon image in src/main/resources/base/media path, otherwise runtime will report error due to missing resource.
                        Image(@r(app.media.startIcon))
                            .height(20)
                    }
                })
            }
            .columnsTemplate("1fr 1fr 1fr 1fr 1fr")
            .rowsTemplate("1fr 1fr 1fr 1fr")
            .columnsGap(10)
            .width(90.percent)
            .height(160)
        }
        .margin(left: 10, right: 10)
        .backgroundColor(0xFAEEE0)
    }
}

@Reusable
@Component
class ChildComponentB {
    @State var item: String = ""

    protected override func aboutToReuse(params: ReuseParams) {
        if (let Some(value) <- params.get<String>("item")) {
            item = value
        }
    }

    func build() {
        Row() {
            Text("Item ${item} Child Component B")
                .fontSize(20)
                .margin(left: 10)
                .fontColor(Color.Red)
        }
        .margin(left: 10, right: 10)
    }
}

@Reusable
@Component
class ChildComponentC {
    @State var item: String = ""

    protected override func aboutToReuse(params: ReuseParams) {
        if (let Some(value) <- params.get<String>("item")) {
            item = value
        }
    }

    func build() {
        Row() {
            Text("Item ${item} Child Component C")
                .fontSize(20)
                .margin(left: 10)
                .fontColor(Color.Green)
        }
        .margin(left: 10, right: 10)
    }
}

@Reusable
@Component
class ChildComponentD {
    @State var item: String = ""

    protected override func aboutToReuse(params: ReuseParams) {
        if (let Some(value) <- params.get<String>("item")) {
            item = value
        }
    }

    func build() {
        Row() {
            Text("Item ${item} Child Component D")
                .fontSize(20)
                .margin(left: 10)
                .fontColor(Color.Green)
        }
        .margin(left: 10, right: 10)
    }
}
```
