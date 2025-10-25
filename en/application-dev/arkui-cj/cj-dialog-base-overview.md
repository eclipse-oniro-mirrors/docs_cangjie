# Popup Overview  

A popup is a modal window typically used to temporarily display information requiring user attention or pending operations while maintaining the current context. Users must complete relevant interactive tasks within the modal popup before exiting the modal mode. Popups can be independent of any component and are usually composed of multiple components such as text, lists, input fields, images, etc., to achieve layout. ArkUI currently provides two types of popup components: **fixed-style** and **custom**.  

* **Custom Popup:** Developers need to pass custom components to populate the popup based on usage scenarios, achieving customized popup content. This mainly includes basic custom popups (CustomDialog) and custom popups independent of UI components (openCustomDialog).  

* **Fixed-Style Popup:** Developers can use fixed-style popups to specify the text content and button operations to be displayed, completing simple interactive effects. This mainly includes alert dialogs (AlertDialog), list selection popups (ActionSheet), picker popups (PickerDialog), dialogs (showDialog), and action menus (showActionMenu).  

## Usage Scenarios  

| Name | Description |  
| :--- | :--- |  
| [Custom Popup Independent of UI Components (openCustomDialog)](cj-uicontext-custom-dialog.md) | Used when users need to dynamically update popup attributes within a custom popup. |  
| [Basic Custom Popup (CustomDialog)](cj-common-components-custom-dialog.md) | Used when users need to customize the components and content within the popup. |  
| [Alert Dialog (AlertDialog)](cj-fixes-style-dialog.md#警告弹窗-alertdialog) | Fixed style, typically used to display information or operations that users currently need or must pay attention to. For example, responding with a confirmation popup when users perform a sensitive action. |  
| [List Selection Popup (ActionSheet)](cj-fixes-style-dialog.md#列表选择弹窗-actionsheet) | Fixed style, used when users need to select from a list of options for attention or confirmation. |  
| [Picker Popup (PickerDialog)](cj-fixes-style-dialog.md#选择器弹窗-pickerdialog) | Fixed style, used when users need to select dates, times, or text within the popup. |  
| [Dialog (showDialog)](cj-fixes-style-dialog.md#对话框-showdialog) | Fixed style, called when users need to handle asynchronous return results after the popup response. |  
| [Action Menu (showActionMenu)](cj-fixes-style-dialog.md#操作菜单-showactionmenu) | Fixed style, called when users need to handle asynchronous return results after the action menu response. |