# Popup Overview  

A popup is a modal window typically used to temporarily display information requiring user attention or pending operations while maintaining the current context. Users must complete relevant interactive tasks within the modal popup before exiting the modal mode. Popups can be independent of any component and their content is usually composed of various components such as text, lists, input fields, images, etc., to achieve layout. ArkUI currently provides two types of popup components: **fixed-style** and **custom**.  

* **Custom Popup:** Developers need to pass custom components to fill the popup based on usage scenarios to achieve customized popup content. This mainly includes the basic custom popup (CustomDialog) and the UI component-independent custom popup (openCustomDialog).  

* **Fixed-Style Popup:** Developers can use fixed-style popups to specify the text content and button operations to be displayed, achieving simple interactive effects. This mainly includes the alert dialog (AlertDialog), list selection popup (ActionSheet), dialog (showDialog), and action menu (showActionMenu).  

## Usage Scenarios  

| Name | Description |  
| :--- | :--- |  
| [UI Component-Independent Custom Popup (openCustomDialog)](cj-uicontext-custom-dialog.md) | Used when users need to dynamically update popup properties within a custom popup. |  
| [Basic Custom Popup (CustomDialog)](cj-common-components-custom-dialog.md) | Used when users need to customize the components and content within the popup. |  
| [Alert Dialog (AlertDialog)](cj-fixes-style-dialog.md#警告弹窗-alertdialog) | Fixed-style, typically used to display information or operations that users currently need or must pay attention to. For example, responding with a confirmation popup when a user performs a sensitive action. |  
| [List Selection Popup (ActionSheet)](cj-fixes-style-dialog.md#列表选择弹窗-actionsheet) | Fixed-style, used when users need to select from a list of options for attention or confirmation. |  
| [Dialog (showDialog)](cj-fixes-style-dialog.md#对话框-showdialog) | Fixed-style, called when users need to handle asynchronous return results after responding to the popup. |  
| [Action Menu (showActionMenu)](cj-fixes-style-dialog.md#操作菜单-showactionmenu) | Fixed-style, called when users need to handle asynchronous return results after responding to the action menu. |