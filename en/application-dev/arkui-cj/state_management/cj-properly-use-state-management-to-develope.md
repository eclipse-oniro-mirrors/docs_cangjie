# Development Guide for Proper Usage of State Management

Due to unfamiliarity with current state management features, many developers encounter issues such as UI not refreshing or poor refresh performance when using state management for development. This document analyzes five typical scenarios from two perspectives, providing corresponding positive and negative examples to help developers learn how to properly utilize state management in development.

## Proper Usage of Properties

## Merging Simple Property Arrays into Object Arrays

During development, we often need to set the same property for multiple components, such as the content of Text components or style information like width and height. Storing these properties in an array and using them with ForEach is a simple and convenient approach.

### Splitting Complex Large Objects into Collections of Smaller Objects

In development, we sometimes define a large object containing numerous style-related properties and pass this object between parent and child components, binding its properties to the components.

### Using @Observed Decorated or State Variable Declared Class Objects to Bind Components

During development, there are scenarios like "resetting data," where a newly created object is assigned to an existing state variable to refresh the data. If the type of the newly created object is not carefully considered, it may result in the UI not refreshing.

## Proper Usage of ForEach/LazyForEach

### Minimizing UI Refresh via LazyForEach's Rebuild Mechanism

### Using ObservedArrayList in ForEach

In development, object arrays are often used with ForEach, but improper implementation can lead to UI not refreshing.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList
import kit.PerformanceAnalysisKit.Hilog

@Observed
class TextStyles{
    @Publish
    var fontSize: Int64
}

@Entry
@Component
class EntryView {
    @State
    var styleList: ArrayList<TextStyles> = ArrayList<TextStyles>([])

    public override func aboutToAppear(){
        for(i in 1..=35){
            this.styleList.add(TextStyles(fontSize: i))
        }
    }

    func build() {
        Column {
            Text("Font Size List")
                .fontSize(50)
                .onClick {
                    evt =>
                        for(i in 0..this.styleList.size){
                            this.styleList[i].fontSize++
                        }
                        Hilog.info(0, "AppLogCj", "change font size")
                    }
            List() {
                ForEach(this.styleList, {
                        item: TextStyles, _: Int64 =>
                        ListItem(){
                            Text("Hello World")
                                .fontSize(item.fontSize)
                        }
                })
            }
        }
    }
}
```

![developguide51](./figures/developguide51.gif)

Since the items generated in ForEach are constants, clicking to change the item content does not trigger a UI refresh, even though the logs show the item values have changed ("change font size" is printed). Therefore, ObservedArrayList must be used in conjunction with the @Publish decorator on custom class properties to achieve observable capabilities.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList
import kit.PerformanceAnalysisKit.Hilog

@Observed
class TextStyles{
    @Publish var fontSize: Int64
}

@Entry
@Component
class EntryView {
    @State
    var styleList: ObservedArrayList<TextStyles> = ObservedArrayList<TextStyles>([])

    public override func aboutToAppear(){
        for(i in 1..= 35) {
            this.styleList.append(TextStyles(fontSize: i))
        }
    }

    func build() {
        Column {
            Text("Font Size List")
                .fontSize(50)
                .onClick{
                    evt =>
                    for(i in 0..this.styleList.size){
                        this.styleList[i].fontSize++
                    }
                    Hilog.info(0,"AppLog: info","change font size")
                }
            List(){
                ForEach(this.styleList ,{
                        item: TextStyles, _:Int64 =>
                        ListItem(){
                            Text("Hello World")
                                .fontSize(item.fontSize)
                        }
                })
            }
        }
    }
}
```

![developguide52](./figures/developguide52.gif)

Using the @Publish decorator on custom class properties gives the Text component's textStyles variable observable capabilities. When values in styleList are modified, the system observes that the fontSize value of each textStyles item in styleList has changed, thereby triggering a UI refresh.

This is a practical approach to refreshing using state management in development.