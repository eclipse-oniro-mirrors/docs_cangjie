# Menu

A menu displayed in a vertical list format.

> **Note:**
>
> The Menu component must be used in conjunction with the [bindMenu](cj-universal-attribute-menu.md#func-bindmenuarraymenuelement) or [bindContextMenu](cj-universal-attribute-menu.md#func-bindcontextmenucustombuilder-responsetype-contextmenuoptions) methods and cannot be used as a standalone component.

## Import Module

```cangjie
import ohos.arkui.component.menu
```

## Child Components

Includes [MenuItem](cj-menu-menuitem.md) and [MenuItemGroup](cj-menu-menuitemgroup.md) child components.

## Creating the Component

### init(() -> Unit)

```cangjie
public init(child!: () -> Unit = {=>})
```

**Function:** Creates a menu with child components.

> **Note:**
>
> Menu and menu item width calculation rules:<br/>During layout, it is expected that each menu item has the same width. If a child component sets a width, it follows the [size calculation rules](./cj-universal-attribute-size.md#func-constraintsizelength-length-length-length).<br/>When width is not set: The menu component will set a default width of 2 grid units for child components MenuItem and MenuItemGroup. If the content area of a menu item is wider than 2 grid units, it will adaptively expand.<br/>When width is set: The menu component will set a fixed width for child components MenuItem and MenuItemGroup after subtracting padding.<br/>When setting the [width](./cj-universal-attribute-size.md#func-widthlength) of the Menu border, the minimum supported width is 64vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| child | () -> Unit | No | {=>} | Declares the child components within the container. |

## Universal Attributes/Events

Universal Attributes: All supported.

Universal Events: All supported.

## Component Attributes

### func font(?Length, ?FontWeight, ?ResourceStr, ?FontStyle)

```cangjie
public func font(
    size!: ?Length = None,
    weight!: ?FontWeight = None,
    family!: ?ResourceStr = None,
    style!: ?FontStyle = None
): This
```

**Function:** Sets the text size for all text within the Menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the text size. When Length is Int64 or Float64, the unit is fp. Percentage settings are not supported. Default: 16.vp. |
| weight | ?[FontWeight](./cj-common-types.md#enum-fontweight) | No | None | **Named parameter.** Sets the font weight of the text. Default: FontWeight.Normal. |
| family | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Sets the font list for the text. Multiple fonts can be specified, separated by commas, with priority in order. Example: 'Arial, HarmonyOS Sans'. Currently supports 'HarmonyOS Sans' font and [registered custom fonts](./cj-apis-uicontext-font.md). Default: "HarmonyOS Sans". |
| style | ?[FontStyle](./cj-common-types.md#enum-fontstyle) | No | None | **Named parameter.** Sets the font style of the text. Default: FontStyle.Normal. |

### func fontColor(?ResourceColor)

```cangjie
public func fontColor(value: ?ResourceColor): This
```

**Function:** Uniformly sets the color for all text within the Menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | The color for all text within the Menu. Default: 0x99000000. |

### func radius(?BorderRadiuses)

```cangjie
public func radius(value: ?BorderRadiuses): This
```

**Function:** Sets the border radius of the Menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[BorderRadiuses](./cj-common-types.md#class-borderradiuses) | Yes | - | The border radius of the Menu. |

### func radius(?Length)

```cangjie
public func radius(value: ?Length): This
```

**Function:** Sets the border radius of the Menu.

> **Note:**
>
> If the sum of the two horizontal border radii exceeds the menu width, or the sum of the two vertical border radii exceeds the menu height, the menu will use the default border radius values for all four corners.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | The border radius of the Menu. |

## Example Code

This example demonstrates a multi-level menu by configuring the `builder` parameter in MenuItem.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.i18n.*
import ohos.resource_manager.*
import ohos.resource.*

@Entry
@Component
class EntryView {
    @State
    var select: Bool = true
    let iconStr: AppResource = @r(app.media.startIcon)
    var iconStr2: AppResource = @r(app.media.right)

    @Builder
    func SubMenu() {
        Menu() {
            MenuItem(startIcon: "", content: "Copy", endIcon: "", labelInfo: "Ctrl+C")
            MenuItem(startIcon: "", content: "Paste", endIcon: "", labelInfo: "Ctrl+V")
        }
    }

    @Builder
    func MyMenu() {
        Menu() {
            MenuItem(startIcon: @r(app.media.startIcon), content: @r(app.string.contentName),
                endIcon: @r(app.media.blank), labelInfo: @r(app.string.emptyName))
            MenuItem(startIcon: @r(app.media.startIcon), content: @r(app.string.contentName),
                endIcon: @r(app.media.blank), labelInfo: @r(app.string.emptyName)).enabled(false)
            MenuItem(
                startIcon: this.iconStr,
                content: @r(app.string.contentName),
                endIcon: this.iconStr,
                labelInfo: @r(app.string.emptyName),
                builder: {=> bind(this.SubMenu, this)()}
            )
            MenuItemGroup(header: "Subtitle", footer: "") {
                =>
                MenuItem(
                    startIcon: this.iconStr,
                    content: @r(app.string.contentName),
                    endIcon: @r(app.string.emptyName),
                    labelInfo: @r(app.string.emptyName),
                    builder: {=> bind(this.SubMenu, this)()}
                    )
                MenuItem(
                    startIcon: @r(app.media.startIcon),
                    content: @r(app.string.contentName),
                    endIcon: @r(app.media.right),
                    labelInfo: @r(app.string.emptyName),
                    builder: {=> bind(this.SubMenu, this)()}
                )
                MenuItem(
                startIcon: "",
                content: "Menu Option",
                endIcon: "",
                labelInfo: "",
                ).selectIcon(true).selected(
                    select).onChange({
                    selected => iconStr2 = @r(app.media.foreground)
                })
            }

        }
    }

    func build() {
        Row() {
            Column() {
                Text("click to show menu")
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
            }.bindMenu(builder: this.MyMenu).width(50.percent)
        }.height(100.percent)
    }
}
```

![menu](./figures/menu.gif)