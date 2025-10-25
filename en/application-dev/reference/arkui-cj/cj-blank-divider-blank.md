# Blank

The Blank component is a space-filling component that automatically occupies the remaining space along the main axis of its container. It only takes effect when the parent component is a [Row](./cj-row-column-stack-row.md), [Column](./cj-row-column-stack-column.md), or [Flex](./cj-row-column-stack-flex.md).

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(Length)

```cangjie
public init(min!: Length = 0.vp)
```

**Function:** Creates a Blank component.

> **Notes:**
>
> - Blank automatically stretches or compresses along the main axis of its parent container ([Row](./cj-row-column-stack-row.md), [Column](./cj-row-column-stack-column.md), [Flex](./cj-row-column-stack-flex.md)) when no size is specified. It does not stretch or compress if a size is set or if the container adapts to the size of its child nodes.
> - The constraint relationship between the main axis size (size) and min for Blank is max(min, size).
> - When a size is set for the cross axis of the parent container, Blank does not fill the cross axis. If no size is set for the cross axis, the default alignSelf value is ItemAlign.Stretch, which fills the container's cross axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| min | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** The minimum size of the Blank component along the main axis of the container. The default unit is vp if no pixel unit is specified. Percentage values are not supported. Negative values use the default value. If the minimum value exceeds the available container space, the minimum value is used as the component size, causing it to overflow the container. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func color(ResourceColor)

```cangjie
public func color(value: ResourceColor): This
```

**Function:** Sets the fill color of the Blank component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | The fill color of the Blank component.<br/>Initial value: Color.TRANSPARENT |

## Example Code

### Example 1 (Filling Remaining Space)

Demonstrates the Blank component filling the remaining space in both portrait and landscape orientations.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Column() {
            Row() {
                Text("Bluetooth").fontSize(18)
                Blank()
                Toggle(ToggleType.Switch).margin(top: 14, bottom: 14, left: 6, right: 6)
            }.width(100.percent).backgroundColor(0xFFFFFF).borderRadius(15).padding( left: 12 )
        }.backgroundColor(0xEFEFEF).padding(20)
    }
}
```

![blank1](./figures/blank1.gif)

### Example 2 (Filling Fixed Width)

Demonstrates the effect of the min parameter when the parent component of the Blank component does not have a specified width.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Column(space: 20) {
            Row() {
                Text("Bluetooth").fontSize(18)
                Blank().color(0xFFFF00)
                Toggle(ToggleType.Switch).margin(top: 14, bottom: 14, left: 6, right: 6)
            }.backgroundColor(0xFFFFFF).borderRadius(15).padding(left: 12)

            Row() {
                Text("Bluetooth").fontSize(18)
                Blank(min: 160.vp).color(0xFFFF00)
                Toggle(ToggleType.Switch).margin(top: 14, bottom: 14, left: 6, right: 6)
            }.backgroundColor(0xFFFFFF).borderRadius(15).padding(left: 12)
        }.backgroundColor(0xEFEFEF).padding(20).width(100.percent)
    }
}
```

![blank2](./figures/blank2.png)