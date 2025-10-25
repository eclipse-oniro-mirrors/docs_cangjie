# Stepper  

A step navigator component that displays current progress when completing a task requires multiple steps.  

## Import Module  

```cangjie  
import kit.ArkUI.*  
```  

## Subcomponents  

Can only contain [StepperItem](./cj-navigation-switching-stepperitem.md) subcomponents.  

## Creating the Component  

### init(UInt32, () -> Unit)  

```cangjie  
public init(index!: UInt32 = 0, child!: () -> Unit = {=>})  
```  

**Function:** Constructs a step navigator component.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parameters:**  

| Parameter | Type      | Required | Default | Description |  
|:----------|:----------|:---------|:--------|:------------|  
| index     | UInt32    | No       | 0       | The index value of the currently displayed StepperItem in the step navigator.<br/>Initial value: 0. |  
| child     | () -> Unit | No       | { => }  | The subcomponents of the step navigator. |  

## Universal Attributes/Events  

Universal Attributes: All supported.  

Universal Events: All supported.  

## Component Events  

### func onChange((UInt32, UInt32) -> Unit)  

```cangjie  
public func onChange(callback: (UInt32, UInt32) -> Unit): This  
```  

**Function:** Triggered when clicking the prevLabel of the current StepperItem to switch steps; or when clicking the nextLabel of the current StepperItem and the current page is not the last StepperItem in the step navigator, and the ItemState property is Normal.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parameters:**  

| Parameter | Type               | Required | Default | Description |  
|:----------|:-------------------|:---------|:--------|:------------|  
| callback  | (UInt32, UInt32) -> Unit | Yes      | -       | Callback function triggered when switching step pages.<br/>First parameter: Index value of the step page before switching.<br/>Second parameter: Index value of the step page (previous or next) after switching. |  

### func onFinish(() -> Unit)  

```cangjie  
public func onFinish(callback: () -> Unit): This  
```  

**Function:** Triggered when the nextLabel of the last StepperItem in the step navigator is clicked and the ItemState property is Normal.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parameters:**  

| Parameter | Type       | Required | Default | Description |  
|:----------|:-----------|:---------|:--------|:------------|  
| callback  | () -> Unit | Yes      | -       | Callback function triggered when the last step of the step navigator is completed. |  

### func onNext((UInt32, UInt32) -> Unit)  

```cangjie  
public func onNext(callback: (UInt32, UInt32) -> Unit): This  
```  

**Function:** Triggered when clicking the nextLabel of a StepperItem to switch to the next step, and the current page is not the last StepperItem in the step navigator, and the ItemState property is Normal.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parameters:**  

| Parameter | Type               | Required | Default | Description |  
|:----------|:-------------------|:---------|:--------|:------------|  
| callback  | (UInt32, UInt32) -> Unit | Yes      | -       | Callback function triggered when switching to the next step page.<br/>First parameter: Index value of the current step page.<br/>Second parameter: Index value of the next step page. |  

### func onPrevious((UInt32, UInt32) -> Unit)  

```cangjie  
public func onPrevious(callback: (UInt32, UInt32) -> Unit): This  
```  

**Function:** Triggered when clicking the prevLabel of a StepperItem to switch to the previous step.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parameters:**  

| Parameter | Type               | Required | Default | Description |  
|:----------|:-------------------|:---------|:--------|:------------|  
| callback  | (UInt32, UInt32) -> Unit | Yes      | -       | Callback function triggered when switching to the previous step page.<br/>First parameter: Index value of the current step page.<br/>Second parameter: Index value of the previous step page. |  

### func onSkip(() -> Unit)  

```cangjie  
public func onSkip(callback: () -> Unit): This  
```  

**Function:** Triggered when the nextLabel is clicked while the currently displayed StepperItem's state is ItemState.Skip.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parameters:**  

| Parameter | Type       | Required | Default | Description |  
|:----------|:-----------|:---------|:--------|:------------|  
| callback  | () -> Unit | Yes      | -       | Callback function triggered when clicking to switch to the next step page. |  

## Example Code  

This example demonstrates how to use the step navigator component.  

<!-- run -->  

```cangjie  
package ohos_app_cangjie_entry  
import kit.ArkUI.*  
import ohos.arkui.state_macro_manage.*  
import kit.PerformanceAnalysisKit.Hilog  

@Entry  
@Component  
class EntryView {  
    @State var currentIndex: UInt32  = 0  
    @State var firstState: ItemState = ItemState.Normal  
    @State var secondState: ItemState = ItemState.Normal  
    @State var thirdState: ItemState = ItemState.Normal  

    func build() {  
        Column() {  
            Stepper(index:currentIndex) {  
                StepperItem() {  
                    Column() {  
                      Text("Page One").fontSize(35).fontColor(0x182431)  
                      Button("change status")  
                        .backgroundColor(0x007dFF)  
                        .onClick({ evt =>  
                            if(this.firstState.toString() == ItemState.Skip) {  
                                this.firstState = ItemState.Normal  
                            } else {  
                                this.firstState = ItemState.Skip  
                            }  
                        })  
                    }  
                }  
                .nextLabel("Next Page")  
                .status(status:this.firstState)  
                StepperItem() {  
                    Column() {  
                      Text("Page Two").fontSize(35).fontColor(0x182431)  
                      Button("change status")  
                        .backgroundColor(0x007dFF)  
                        .onClick({ evt =>  
                            if(this.secondState.toString() == ItemState.Disabled) {  
                                this.secondState = ItemState.Normal  
                            } else {  
                                this.secondState = ItemState.Disabled  
                            }  
                        })  
                    }  
                }  
                .nextLabel("Next Page")  
                .prevLabel("Previous Page")  
                .status(status:this.secondState)  
                StepperItem() {  
                    Column() {  
                      Text("Page Three").fontSize(35).fontColor(0x182431)  
                      Button("change status")  
                        .backgroundColor(0x007dFF)  
                        .onClick({ evt =>  
                            if(this.thirdState.toString() == ItemState.Waiting) {  
                                this.thirdState = ItemState.Normal  
                            } else {  
                                this.thirdState = ItemState.Waiting  
                            }  
                        })  
                    }  
                }  
                .nextLabel("Next Page")  
                .prevLabel("Previous Page")  
                .status(status:this.thirdState)  
                StepperItem() {  
                    Column() {  
                        Text("Page Four").fontSize(35).fontColor(0x182431)  
                    }  
                }  
            }  
            .backgroundColor(0xF1F3F5)  
            .onFinish({=>  
                Hilog.info(0, "AppLogCj", "onFinish")  
            })  
            .onSkip({=>  
                Hilog.info(0, "AppLogCj", "onSkip")  
            })  
            .onChange({prevIndex: UInt32, index: UInt32 =>  
                if(index != 0){  
                    currentIndex = index  
                }  
            })  
        }  
        .width(100.percent)  
        .padding(top: 5)  
    }  
}  
```  

![stepper](./figures/stepper.gif)