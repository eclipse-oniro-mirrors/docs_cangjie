# Menu Control (Menu)

Menu is an interface for contextual menus, commonly used for right-click pop-ups, click-triggered pop-ups, etc. For specific usage, please refer to [Menu Control](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-menu.md).

When using [bindContextMenu](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-menu.md#func-bindcontextmenu---unit-responsetype) with a preview image set, the menu will appear with an overlay layer, making it modal.

When using [bindMenu](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-menu.md#func-bindmenu---unit) or bindContextMenu without setting a preview image, the menu will appear without an overlay layer, making it non-modal.

## Lifecycle

| Name | Type | Description |
|:---|:---|:---|
| aboutToAppear | () -> Unit | Callback triggered before the menu display animation. |
| onAppear | () -> Unit | Callback triggered when the menu pops up. |
| aboutToDisappear | () -> Unit | Callback triggered before the menu exit animation. |
| onDisappear | () -> Unit | Callback triggered when the menu disappears. |

## Creating Default-Style Menus

Menus need to be implemented by calling the bindMenu interface. bindMenu responds to click events on bound components. After binding to a component, the menu will pop up when the corresponding component is clicked.

```cangjie
Button("click for Menu").bindMenu(
    Action(
        value: 'Menu1',
        action: {
            => AppLog.info('handle Menu1 select')
        }
    )
)
```

![menu](figures/menu1.png)

### Creating Custom-Style Menus

When the default style doesn't meet development requirements, you can use [@Builder](./paradigm/cj-macro-builder.md) to customize menu content and implement custom menus through the bindMenu interface.

#### Developing Menu Content with @Builder

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*

class Tmp {
    var iconStr2: AppResource = @r(app.media.startIcon)

    public func set(val: AppResource) {
        this.iconStr2 = val
    }
}

@Entry
@Component
class EntryView {
    @State var select: Bool = true
    private var iconStr: AppResource = @r(app.media.startIcon)
    private var iconStr2: AppResource = @r(app.media.startIcon)

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
            MenuItem(startIcon: @r(app.media.startIcon), content: @r(app.string.module_desc),
                endIcon: @r(app.string.module_desc), labelInfo: @r(app.string.module_desc))
            MenuItem(startIcon: @r(app.media.startIcon), content: @r(app.string.module_desc),
                endIcon: @r(app.string.module_desc), labelInfo: @r(app.string.module_desc)).enabled(false)
            MenuItem(
                startIcon: this.iconStr,
                content: @r(app.string.module_desc),
                endIcon: @r(app.media.startIcon),
                labelInfo: @r(app.string.module_desc),
                // When the builder parameter is configured, it indicates a submenu bound to the menu item. Hovering over this menu item will display the submenu.
                builder: {=> bind(this.SubMenu, this)()}
            )
            MenuItemGroup(header: "Subtitle", footer: "") {
                =>
                MenuItem(startIcon: "", content: "Menu Option", endIcon: "", labelInfo: "")
                    .selectIcon(true)
                    .selected(this.select)
                    .onChange(
                        {
                            selected =>
                            let Str: Tmp = Tmp()
                            Str.set(@r(app.media.startIcon))
                        }
                    )
                MenuItem(
                    startIcon: @r(app.media.startIcon),
                    content: @r(app.string.module_desc),
                    endIcon: @r(app.media.startIcon),
                    labelInfo: @r(app.string.module_desc),
                    builder: {=> bind(this.SubMenu, this)()}
                )
            }

            MenuItem(
                startIcon: this.iconStr2,
                content: @r(app.string.module_desc),
                endIcon: @r(app.media.startIcon),
                labelInfo: @r(app.string.module_desc)
            )
        }
    }

    func build() {
        // ...
    }
}
```

### Binding Components with bindMenu Property

```cangjie
Button('click for Menu')
    .bindMenu(builder: this.MyMenu)
```

![menu](figures/menu2.png)

## Creating Right-Click or Long-Press Menus

Customize menus through the bindContextMenu interface and set the trigger method for menu display, which can be right-click or long-press. Menus triggered by bindContextMenu appear in an independent sub-window and can display outside the application window.

- Developing menu content with @Builder follows the same approach as described above.
- Determine the menu trigger method and bind components using the bindContextMenu property. The example shows right-click menu triggering.

```cangjie
Button('click for Menu')
    .bindContextMenu(
        builder: this.MyMenu,
        responseType: ResponseType.RightClick
    )
```