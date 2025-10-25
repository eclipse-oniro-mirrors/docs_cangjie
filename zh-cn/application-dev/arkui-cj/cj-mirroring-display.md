# 使用镜像能力

## 概述

为满足不同用户的阅读习惯，ArkUI提供了镜像能力。在特定情况下将显示内容在X轴上进行镜像反转，由从左向右显示变成从右向左显示。

|**镜像前**|**镜像后**|
|:---|:---|
| ![mirroring-capability](./figures/mirroring_capability1.png) | ![mirroring-capability](./figures/mirroring_capability2.png) |

当组件满足以下任意条件时，镜像能力生效：

1. 组件的direction属性设置为Direction.Rtl。

2. 组件的direction属性设置为Direction.Auto，且当前的系统语言（如维吾尔语）的阅读习惯是从右向左。

## 基本概念

- LTR：顺序为从左向右。
- RTL：顺序为从右向左。

## 使用约束

ArkUI 如下能力已默认适配镜像：

|**类别**|**名称**|
|:---|:---|
| 基础组件 | [Swiper](../../../zh-cn/application-dev/reference/arkui-cj/cj-scroll-swipe-swiper.md)、[Tabs](../../../zh-cn/application-dev/reference/arkui-cj/cj-navigation-switching-tabs.md)、[List](../../../zh-cn/application-dev/reference/arkui-cj/cj-scroll-swipe-list.md)、[Progress](../../../zh-cn/application-dev/reference/arkui-cj/cj-information-display-progress.md)、[CalendarPickerDialog](../../../zh-cn/application-dev/arkui-cj/cj-fixes-style-dialog.md#日历选择器弹窗)、[TextPicker](../../../zh-cn/application-dev/reference/arkui-cj/cj-button-picker-textpicker.md)、[DatePicker](../../../zh-cn/application-dev/reference/arkui-cj/cj-button-picker-datepicker.md)、[Grid](../../../zh-cn/application-dev/reference/arkui-cj/cj-scroll-swipe-grid.md)、[Scroll](../../../zh-cn/application-dev/reference/arkui-cj/cj-scroll-swipe-scroll.md)、[ScrollBar](../../../zh-cn/application-dev/reference/arkui-cj/cj-scroll-swipe-scrollbar.md)、[AlphabetIndexer](../../../zh-cn/application-dev/reference/arkui-cj/cj-information-display-alphabetindexer.md)、[Stepper](../../../zh-cn/application-dev/reference/arkui-cj/cj-navigation-switching-stepper.md)、[SideBarContainer](../../../zh-cn/application-dev/reference/arkui-cj/cj-grid-layout-sidebar.md)、[Navigation](../../../zh-cn/application-dev/reference/arkui-cj/cj-navigation-switching-navigation.md)、[Rating](../../../zh-cn/application-dev/reference/arkui-cj/cj-button-picker-rating.md)、[Slider](../../../zh-cn/application-dev/reference/arkui-cj/cj-button-picker-slider.md)、[Toggle](../../../zh-cn/application-dev/reference/arkui-cj/cj-button-picker-toggle.md)、[Badge](../../../zh-cn/application-dev/reference/arkui-cj/cj-information-display-badge.md)、[bindMenu](../../../zh-cn/application-dev/reference/arkui-cj/cj-universal-attribute-menu.md#funcbindMenu)、[bindContextMenu](../../../zh-cn/application-dev/reference/arkui-cj/cj-universal-attribute-menu.md#funcbindContextMenu)、[TextInput](../../../zh-cn/application-dev/reference/arkui-cj/cj-text-input-textinput.md)、[TextArea](../../../zh-cn/application-dev/reference/arkui-cj/cj-text-input-textarea.md)、[Search](../../../zh-cn/application-dev/reference/arkui-cj/cj-text-input-search.md)、[Stack](../../../zh-cn/application-dev/reference/arkui-cj/cj-row-column-stack-stack.md)、[GridRow](../../../zh-cn/application-dev/reference/arkui-cj/cj-grid-layout-gridrow.md)、[Text](../../../zh-cn/application-dev/reference/arkui-cj/cj-text-input-text.md)、[Select](../../../zh-cn/application-dev/reference/arkui-cj/cj-button-picker-select.md)、[Row](../../../zh-cn/application-dev/reference/arkui-cj/cj-row-column-stack-row.md)、[Column](../../../zh-cn/application-dev/reference/arkui-cj/cj-row-column-stack-column.md)、[Flex](../../../zh-cn/application-dev/reference/arkui-cj/cj-row-column-stack-flex.md)、[RelativeContainer](../../../zh-cn/application-dev/reference/arkui-cj/cj-row-column-stack-relativecontainer.md)、[ListItemGroup](../../../zh-cn/application-dev/reference/arkui-cj/cj-scroll-swipe-listgroup.md) |
| 高级组件 | [Popup](./cj-popup-and-menu-components-popup.md)、[Dialog](./cj-dialog-base-overview.md) |
| 通用属性 | [position](../../../zh-cn/application-dev/reference/arkui-cj/cj-common-types.md#Position)、[markAnchor](../../../zh-cn/application-dev/reference/arkui-cj/cj-universal-attribute-location.md#funcmarkAnchor)、[offset](../../../zh-cn/application-dev/arkui-cj/cj-layout-development-grid-layout.md#offset)、[alignRules](../../../zh-cn/application-dev/reference/arkui-cj/cj-universal-attribute-location.md#funcalignRules)、[borderWidth](../../../zh-cn/application-dev/reference/arkui-cj/cj-information-display-progress.md#varborderWidth)、[borderColor](../../../zh-cn/application-dev/reference/arkui-cj/cj-information-display-progress.md#varborderColor)、[padding](../../../zh-cn/application-dev/reference/arkui-cj/cj-universal-attribute-size.md#fun-cpadding)、[margin](../../../zh-cn/application-dev/reference/arkui-cj/cj-universal-attribute-size.md#func-marginlength) |
| 接口 | [promptAction.showDialog](./cj-fixes-style-dialog.md#对话框-showdialog)|

但如下三种场景还需要进行适配：

1. 界面布局、边框设置：关于方向类的通用属性，如果需要支持镜像能力，使用泛化的方向指示词 start/end入参类型替换 left/right、x/y等绝对方向指示词的入参类型，来表示自适应镜像能力。

2. Canvas组件只有限支持文本绘制的镜像能力。

3. XComponent组件不支持组件镜像能力。
