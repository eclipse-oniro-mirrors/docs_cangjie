# AlphabetIndexer

A component that can interact with container components to quickly locate the display area of a container based on logical structure.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(Array\<String>, UInt32)

```cangjie
public init(arrayValue!: Array<String>, selected!: UInt32)
```

**Function:** Creates an AlphaIndexer component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| arrayValue | Array\<String> | Yes | - | **Named parameter.** String array where each string represents an index item. |
| selected | UInt32 | Yes | - | **Named parameter.** Initial selected index value. If it exceeds the index range, the default value 0 is used. |

## Universal Attributes/Events

Universal Attributes: All supported.

> **Note:**
>
> - When the [width](cj-text-input-imagespan.md#var-width) attribute is set to "auto", it indicates adaptive width, which changes with the maximum width of index items.
> - The [padding](./cj-universal-attribute-size.md#func-paddinglength) attribute defaults to 4.vp.
> - The maximum font scaling factor [maxFontScale](./cj-common-types.md#var-maxfontscale) and the minimum font scaling factor [minFontScale](./cj-common-types.md#var-minfontscale) are both 1 and do not adjust with system font size changes.

Universal Events: All supported.

## Component Attributes

### func alignStyle(IndexerAlign)

```cangjie
public func alignStyle(value: IndexerAlign): This
```

**Function:** Sets the alignment style of the alphabet indexer popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [IndexerAlign](#enum-indexeralign) | Yes | IndexerAlign.END | The alignment style of the alphabet indexer popup, supporting display on the left or right side of the popup. |

### func color(ResourceColor)

```cangjie
public func color(value: ResourceColor): This
```

**Function:** Sets the text color of unselected items.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Text color of unselected items.<br>Initial value: 0x99182431. |

### func font(Length, FontWeight, ResourceStr, FontStyle)

```cangjie
public func font(
    size!: Length = 10.vp,
    weight!: FontWeight = FontWeight.Normal,
    family!: ResourceStr = "HarmonyOS Sans",
    style!: FontStyle = FontStyle.Normal
): This
```

**Function:** Sets the text style of selected items.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 10.vp | **Named parameter.** Text size of selected items. |
| weight | [FontWeight](./cj-common-types.md#enum-fontweight) | No | FontWeight.Normal | **Named parameter.** Font weight of selected items. |
| family | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "HarmonyOS Sans" | **Named parameter.** Font family of selected items. |
| style | [FontStyle](./cj-common-types.md#enum-fontstyle) | No | FontStyle.Normal | **Named parameter.** Text style of selected items. |

### func itemSize(Length)

```cangjie
public func itemSize(size: Length): This
```

**Function:** Sets the size of the index item area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Size of the index item area. The index item area is square, i.e., the side length of the square.<br>Percentage values are not supported.<br>Initial value: 16.vp.<br>Unit: vp. |

### func popupBackground(ResourceColor)

```cangjie
public func popupBackground(value: ResourceColor): This
```

**Function:** Sets the background color of the popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Background color of the popup.<br>Initial value: 0x66808080. |

### func popupColor(ResourceColor)

```cangjie
public func popupColor(value: ResourceColor): This
```

**Function:** Sets the text color of primary index items in the popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Text color of primary index items in the popup.<br>Initial value: 0xFF007DFF. |

### func popupFont(Length, FontWeight, ResourceStr, FontStyle)

```cangjie
public func popupFont(
    size!: Length = 24.vp,
    weight!: FontWeight = FontWeight.Normal,
    family!: ResourceStr = "HarmonyOS Sans",
    style!: FontStyle = FontStyle.Normal
): This
```

**Function:** Sets the font style of the popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 24.vp | **Named parameter.** Text size of selected items. |
| weight | [FontWeight](./cj-common-types.md#enum-fontweight) | No | FontWeight.Normal | **Named parameter.** Font weight of selected items. |
| family | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "HarmonyOS Sans" | **Named parameter.** Font family of selected items. |
| style | [FontStyle](./cj-common-types.md#enum-fontstyle) | No | FontStyle.Normal | **Named parameter.** Text style of selected items. |

### func popupPosition(Length, Length)

```cangjie
public func popupPosition(x!: Length = 60.vp, y!: Length = 48.vp): This
```

**Function:** Sets the position of the popup relative to the midpoint of the top border of the indexer bar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 60.vp | **Named parameter.** Horizontal position of the popup relative to the midpoint of the top border of the indexer bar. |
| y | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 48.vp | **Named parameter.** Vertical position of the popup relative to the midpoint of the top border of the indexer bar. |

### func selected(Int32)

```cangjie
public func selected(index: Int32): This
```

**Function:** Sets the selected index value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int32 | Yes | - | Selected index value.<br/>Initial value: 0. |

### func selectedBackgroundColor(ResourceColor)

```cangjie
public func selectedBackgroundColor(value: ResourceColor): This
```

**Function:** Sets the background color of selected items.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Background color of selected items.<br>Initial value: 0x1A007DFF. |

### func selectedColor(ResourceColor)

```cangjie
public func selectedColor(value: ResourceColor): This
```

**Function:** Sets the text color of selected items.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Text color of selected items.<br>Initial value: 0xFF007DFF. |

### func selectedFont(Length, FontWeight, ResourceStr, FontStyle)

```cangjie
public func selectedFont(
    size!: Length = 10.vp,
    weight!: FontWeight = FontWeight.Normal,
    family!: ResourceStr = "HarmonyOS Sans",
    style!: FontStyle = FontStyle.Normal
): This
```

**Function:** Sets the text style of selected items.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 10.vp | **Named parameter.** Text size of selected items. |
| weight | [FontWeight](./cj-common-types.md#enum-fontweight) | No | FontWeight.Normal | **Named parameter.** Font weight of selected items. |
| family | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "HarmonyOS Sans" | **Named parameter.** Font family of selected items. |
| style | [FontStyle](./cj-common-types.md#enum-fontstyle) | No | FontStyle.Normal | **Named parameter.** Text style of selected items. |

### func usingPopup(Bool)

```cangjie
public func usingPopup(value: Bool): This
```

**Function:** Sets whether to use the popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to use the popup.<br/>Initial value: false. |

## Component Events

### func onPopupSelect(OnAlphabetIndexerPopupSelectCallback)

```cangjie
public func onPopupSelect(callback: OnAlphabetIndexerPopupSelectCallback): This
```

**Function:** Triggered when a string in the alphabet indexer popup list is selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | [OnAlphabetIndexerPopupSelectCallback](./cj-common-types.md#class-onalphabetindexerpopupselectcallback) | Yes | - | Callback function triggered when a string in the alphabet indexer popup list is selected. |

### func onRequestPopupData(OnAlphabetIndexerRequestPopupDataCallback)

```cangjie
public func onRequestPopupData(callback: OnAlphabetIndexerRequestPopupDataCallback): This
```

**Function:** Triggered when an alphabet index is selected, requesting the content to be displayed in the popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | [OnAlphabetIndexerRequestPopupDataCallback](./cj-common-types.md#class-onalphabetindexerrequestpopupdatacallback) | Yes | - | Callback function triggered when the current index is selected.<br>Return value: String array corresponding to the index, displayed vertically in the popup. The string list displays up to 5 items; additional items can be scrolled. |

### func onSelect(OnAlphabetIndexerSelectCallback)

```cangjie
public func onSelect(callback: OnAlphabetIndexerSelectCallback): This
```

**Function:** Triggered when the index bar is selected, returning the current selected index.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | [OnAlphabetIndexerSelectCallback](./cj-common-types.md#class-onalphabetindexerselectcallback) | Yes | - | Callback function triggered when the index bar is selected. |

## Basic Type Definitions

### enum IndexerAlign

```cangjie
public enum IndexerAlign <: Equatable<IndexerAlign> {
    | Left
    | Right
    | ...
}
```

**Function:** Alignment style of the indexer.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<IndexerAlign>

#### Left

```cangjie
Left
```

**Function:** Left alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Right

```cangjie
Right
```

**Function:** Right alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func getValue()

```cangjie
public func getValue(): Int32
```

**Function:** Gets the parameter value, returning whether the unlock result corresponds to the integer value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | The value represented by the current enumeration. |## Example Code

### Example 1 (Setting Prompt Popup Display Text Content)

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var arrayA: Array<String> = ["An"]
    var arrayB: Array<String> = ["Bu", "Bai", "Bao", "Bi", "Bing"]
    var arrayC: Array<String> = ["Cao", "Cheng", "Chen", "Cui"]
    var arrayJ: Array<String> = ["Jia", "Jia"]
    var arrayNull: Array<String> = []
    let value: Array<String> = ["#", "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q","R", "S", "T", "U", "V", "W", "X", "Y", "Z"]
    @State var indexerHeight: Length = 75.percent;
    func build() {
        Stack(alignContent: Alignment.Start) {
            Row() {
                List(space: 20, initialIndex: 0) {
                    ForEach(
                        this.arrayA,
                        {
                            item: String, idx: Int64 => ListItem() {
                                Text(item)
                                    .width(80.percent)
                                    .height(5.percent)
                                    .fontSize(30)
                                    .textAlign(TextAlign.Center)
                            }
                        }
                    )
                    ForEach(
                        this.arrayB,
                        {
                            item: String, idx: Int64 => ListItem() {
                                Text(item)
                                    .width(80.percent)
                                    .height(5.percent)
                                    .fontSize(30)
                                    .textAlign(TextAlign.Center)
                            }
                        }
                    )
                    ForEach(
                        this.arrayC,
                        {
                            item: String, idx: Int64 => ListItem() {
                                Text(item)
                                    .width(80.percent)
                                    .height(5.percent)
                                    .fontSize(30)
                                    .textAlign(TextAlign.Center)
                            }
                        }
                    )
                    ForEach(
                        this.arrayJ,
                        {
                            item: String, idx: Int64 => ListItem() {
                                Text(item)
                                    .width(80.percent)
                                    .height(5.percent)
                                    .fontSize(30)
                                    .textAlign(TextAlign.Center)
                            }
                        }
                    )
                }
                    .width(50.percent)
                    .height(100.percent)
                Column() {
                    Column() {
                        AlphabetIndexer(arrayValue: value, selected: 0)
                            .height(this.indexerHeight) // Index bar height
                            .selectedColor(0xFFFFFF) // Selected item text color
                            .popupColor(0xFFFAF0) // Popup text color
                            .selectedBackgroundColor(0xCCCCCC) // Selected item background color
                            .popupBackground(0xD2B48C) // Popup background color
                            .usingPopup(true) // Whether to display popup
                            .selectedFont(size: 16.vp, weight: FontWeight.Bolder) // Selected item font style
                            .popupFont(size: 30.vp, weight: FontWeight.Bolder) // Popup content font style
                            .itemSize(28) // Size of each item
                            .alignStyle(IndexerAlign.Right) // Popup appears on the left side of the index bar
                            .popupBackground(0xCCCCCC) // Set the first index item's popup background color
                            .selectedColor(0x00FF00)
                            .onSelect({index: Int64 => Hilog.info(0, "AppLogCj", this.value[index] + " Selected!");})
                            .onRequestPopupData(
                                {
                                    index: Int64 => if (this.value[index] == "A") {
                                        return this.arrayA.toArray()
                                    } else if (this.value[index] == "B") {
                                        return this.arrayB.toArray()
                                    } else if (this.value[index] == "C") {
                                        return this.arrayC.toArray()
                                    } else if (this.value[index] == "J") {
                                        return this.arrayJ.toArray()
                                    } else {
                                        return Array<String>()
                                    }
                                })
                            .onPopupSelect({
                                index: Int64 => Hilog.info(0, "AppLogCj", "onPopupSelected:${index}");
                            })
                    }
                        .height(80.percent)
                        .justifyContent(FlexAlign.Center)
                }
                    .width(50.percent)
                    .justifyContent(FlexAlign.Center)
            }
                .width(100.percent)
                .height(100.percent)
        }
    }
}
```

![alphabet_indexer1](figures/alphabet_indexer1.gif)