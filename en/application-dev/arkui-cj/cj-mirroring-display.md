# Using Mirroring Capability

## Overview

To accommodate different users' reading habits, ArkUI provides mirroring capability. Under specific circumstances, it mirrors the display content along the X-axis, transforming left-to-right display into right-to-left display.

|**Before Mirroring**|**After Mirroring**|
|:---|:---|
| ![mirroring-capability](./figures/mirroring_capability1.png) | ![mirroring-capability](./figures/mirroring_capability2.png) |

The mirroring capability takes effect when a component meets any of the following conditions:

1. The component's `direction` property is set to `Direction.Rtl`.

2. The component's `direction` property is set to `Direction.Auto`, and the current system language (e.g., Uyghur) follows a right-to-left reading habit.

## Basic Concepts

- LTR: Left-to-right sequence.
- RTL: Right-to-left sequence.

## Usage Constraints

ArkUI has default mirroring adaptation for the following capabilities:

|**Category**|**Name**|
|:---|:---|
| Basic Components | [Swiper](../reference/arkui-cj/cj-scroll-swipe-swiper.md), [Tabs](../reference/arkui-cj/cj-navigation-switching-tabs.md), [List](../reference/arkui-cj/cj-scroll-swipe-list.md), [Progress](../reference/arkui-cj/cj-information-display-progress.md), [TextPicker](../reference/arkui-cj/cj-button-picker-textpicker.md), [DatePicker](../reference/arkui-cj/cj-button-picker-datepicker.md), [Grid](../reference/arkui-cj/cj-scroll-swipe-grid.md), [Scroll](../reference/arkui-cj/cj-scroll-swipe-scroll.md), [ScrollBar](../reference/arkui-cj/cj-scroll-swipe-scrollbar.md), [AlphabetIndexer](../reference/arkui-cj/cj-information-display-alphabetindexer.md), [Stepper](../reference/arkui-cj/cj-navigation-switching-stepper.md), [SideBarContainer](../reference/arkui-cj/cj-grid-layout-sidebar.md), [Navigation](../reference/arkui-cj/cj-navigation-switching-navigation.md), [Rating](../reference/arkui-cj/cj-button-picker-rating.md), [Slider](../reference/arkui-cj/cj-button-picker-slider.md), [Toggle](../reference/arkui-cj/cj-button-picker-toggle.md), [Badge](../reference/arkui-cj/cj-information-display-badge.md), [bindMenu](../reference/arkui-cj/cj-universal-attribute-menu.md#funcbindMenu), [bindContextMenu](../reference/arkui-cj/cj-universal-attribute-menu.md#funcbindContextMenu), [TextInput](../reference/arkui-cj/cj-text-input-textinput.md), [TextArea](../reference/arkui-cj/cj-text-input-textarea.md), [Search](../reference/arkui-cj/cj-text-input-search.md), [Stack](../reference/arkui-cj/cj-row-column-stack-stack.md), [GridRow](../reference/arkui-cj/cj-grid-layout-gridrow.md), [Text](../reference/arkui-cj/cj-text-input-text.md), [Select](../reference/arkui-cj/cj-button-picker-select.md), [Row](../reference/arkui-cj/cj-row-column-stack-row.md), [Column](../reference/arkui-cj/cj-row-column-stack-column.md), [Flex](../reference/arkui-cj/cj-row-column-stack-flex.md), [RelativeContainer](../reference/arkui-cj/cj-row-column-stack-relativecontainer.md), [ListItemGroup](../reference/arkui-cj/cj-scroll-swipe-listgroup.md) |
| Advanced Components | [Popup](./cj-popup-and-menu-components-popup.md), [Dialog](./cj-dialog-base-overview.md) |
| Universal Attributes | [position](../reference/arkui-cj/cj-common-types.md#Position), [markAnchor](../reference/arkui-cj/cj-universal-attribute-location.md#funcmarkAnchor), [offset](../arkui-cj/cj-layout-development-grid-layout.md#offset), [alignRules](../reference/arkui-cj/cj-universal-attribute-location.md#funcalignRules), [borderWidth](../reference/arkui-cj/cj-universal-attribute-border.md#func-borderwidthedgewidths), [borderColor](../reference/arkui-cj/cj-universal-attribute-border.md#func-bordercolorresourcecolor), [padding](../reference/arkui-cj/cj-universal-attribute-size.md#func-paddinglength), [margin](../reference/arkui-cj/cj-universal-attribute-size.md#func-marginlength) |
| Interfaces | [promptAction.showDialog](./cj-fixes-style-dialog.md#dialog-showdialog)|

However, the following three scenarios still require adaptation:

1. Interface layout and border settings: For direction-related universal attributes, if mirroring capability support is needed, use generalized directional indicators (start/end parameter types) to replace absolute directional indicators (left/right, x/y, etc.) to represent adaptive mirroring capability.

2. The Canvas component has limited support for text rendering mirroring capability.