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

- **LTR**: Left-to-right sequence.
- **RTL**: Right-to-left sequence.

## Usage Constraints

ArkUI has default mirroring adaptation for the following capabilities:

|**Category**|**Name**|
|:---|:---|
| Basic Components | [Swiper](../../../en/application-dev/reference/arkui-cj/cj-scroll-swipe-swiper.md), [Tabs](../../../en/application-dev/reference/arkui-cj/cj-navigation-switching-tabs.md), [List](../../../en/application-dev/reference/arkui-cj/cj-scroll-swipe-list.md), [Progress](../../../en/application-dev/reference/arkui-cj/cj-information-display-progress.md), [CalendarPickerDialog](../../../en/application-dev/arkui-cj/cj-fixes-style-dialog.md#日历选择器弹窗), [TextPicker](../../../en/application-dev/reference/arkui-cj/cj-button-picker-textpicker.md), [DatePicker](../../../en/application-dev/reference/arkui-cj/cj-button-picker-datepicker.md), [Grid](../../../en/application-dev/reference/arkui-cj/cj-scroll-swipe-grid.md), [Scroll](../../../en/application-dev/reference/arkui-cj/cj-scroll-swipe-scroll.md), [ScrollBar](../../../en/application-dev/reference/arkui-cj/cj-scroll-swipe-scrollbar.md), [AlphabetIndexer](../../../en/application-dev/reference/arkui-cj/cj-information-display-alphabetindexer.md), [Stepper](../../../en/application-dev/reference/arkui-cj/cj-navigation-switching-stepper.md), [SideBarContainer](../../../en/application-dev/reference/arkui-cj/cj-grid-layout-sidebar.md), [Navigation](../../../en/application-dev/reference/arkui-cj/cj-navigation-switching-navigation.md), [Rating](../../../en/application-dev/reference/arkui-cj/cj-button-picker-rating.md), [Slider](../../../en/application-dev/reference/arkui-cj/cj-button-picker-slider.md), [Toggle](../../../en/application-dev/reference/arkui-cj/cj-button-picker-toggle.md), [Badge](../../../en/application-dev/reference/arkui-cj/cj-information-display-badge.md), [bindMenu](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-menu.md#funcbindMenu), [bindContextMenu](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-menu.md#funcbindContextMenu), [TextInput](../../../en/application-dev/reference/arkui-cj/cj-text-input-textinput.md), [TextArea](../../../en/application-dev/reference/arkui-cj/cj-text-input-textarea.md), [Search](../../../en/application-dev/reference/arkui-cj/cj-text-input-search.md), [Stack](../../../en/application-dev/reference/arkui-cj/cj-row-column-stack-stack.md), [GridRow](../../../en/application-dev/reference/arkui-cj/cj-grid-layout-gridrow.md), [Text](../../../en/application-dev/reference/arkui-cj/cj-text-input-text.md), [Select](../../../en/application-dev/reference/arkui-cj/cj-button-picker-select.md), [Row](../../../en/application-dev/reference/arkui-cj/cj-row-column-stack-row.md), [Column](../../../en/application-dev/reference/arkui-cj/cj-row-column-stack-column.md), [Flex](../../../en/application-dev/reference/arkui-cj/cj-row-column-stack-flex.md), [RelativeContainer](../../../en/application-dev/reference/arkui-cj/cj-row-column-stack-relativecontainer.md), [ListItemGroup](../../../en/application-dev/reference/arkui-cj/cj-scroll-swipe-listgroup.md) |
| Advanced Components | [Popup](./cj-popup-and-menu-components-popup.md), [Dialog](./cj-dialog-base-overview.md) |
| Universal Attributes | [position](../../../en/application-dev/reference/arkui-cj/cj-common-types.md#Position), [markAnchor](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-location.md#funcmarkAnchor), [offset](../../../en/application-dev/arkui-cj/cj-layout-development-grid-layout.md#offset), [alignRules](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-location.md#funcalignRules), [borderWidth](../../../en/application-dev/reference/arkui-cj/cj-information-display-progress.md#varborderWidth), [borderColor](../../../en/application-dev/reference/arkui-cj/cj-information-display-progress.md#varborderColor), [padding](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-size.md#fun-cpadding), [margin](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-size.md#func-marginlength) |
| Interfaces | [promptAction.showDialog](./cj-fixes-style-dialog.md#对话框-showdialog)|

However, the following three scenarios require additional adaptation:

1. **UI Layout and Border Settings**: For direction-related universal attributes, if mirroring capability support is needed, use generalized directional indicators (start/end parameter types) instead of absolute directional indicators (left/right, x/y) to represent adaptive mirroring capability.

2. **Canvas Component**: Only limited support for text drawing mirroring capability.

3. **XComponent Component**: Does not support component mirroring capability.