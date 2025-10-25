# Overview of UIAbility Component  

## Overview  

[UIAbility](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) is a UI-included application component primarily designed for user interaction.  

Design philosophy of UIAbility:  

1. Supports cross-device migration and multi-device collaboration at the application component level.  
2. Supports multiple devices and window forms.  

Principles and recommendations for UIAbility division:  

The UIAbility component is the basic unit of system scheduling, providing a window for the application to render its interface. An application may contain one or more UIAbility components. For example, in a payment application, the entry function and payment/receipt function can be configured as separate UIAbility components.  

Each UIAbility component instance will display a corresponding task in the recent tasks list.  

For developers, the choice between a single or multiple UIAbility components depends on specific scenarios. The recommendations are as follows:  

- If developers want to see a single task in the task view, it is recommended to adopt the "one UIAbility + multiple pages" approach to avoid unnecessary resource loading.  
- If developers want to see multiple tasks in the task view or need to open multiple windows simultaneously, it is recommended to use multiple UIAbility components to implement different functionalities.  

  For example, in an instant messaging application, the message list and audio/video call functionalities can be developed using different UIAbility components. This not only facilitates task window switching but also enables split-screen display of two task windows on a single screen.  

> **Note:**  
>  
> The task view is used for quickly viewing and managing all running tasks or applications on the current device.  

## Declaration Configuration  

For an application to properly use UIAbility, it is necessary to declare the UIAbility's name, entry point, label, and other relevant information in the [abilities tag](../cj-start/basic-knowledge/module-configuration-file.md#abilities标签) of the [module.json5 configuration file](../cj-start/basic-knowledge/module-configuration-file.md).  

```json  
{  
  "module": {  
    // ...  
    "abilities": [  
      {  
        "name": "EntryAbility", // Name of the UIAbility component  
        "srcEntry": "ohos_app_cangjie_entry.MainAbility", // Code path of the UIAbility component  
        "description": "$string:EntryAbility_desc", // Description of the UIAbility component  
        "icon": "$media:startIcon", // Icon of the UIAbility component  
        "label": "$string:EntryAbility_label", // Label of the UIAbility component  
        "startWindowIcon": "$media:startIcon", // Resource index for the start page icon of the UIAbility component  
        "startWindowBackground": "$color:start_window_background", // Resource index for the start page background color of the UIAbility component  
        // ...  
      }  
    ]  
  }  
}  
```  

Additionally, registration must be completed.  

<!-- compile -->  

```cangjie  
import kit.AbilityKit.UIAbility  

let ENTRYABILITY_REGISTER_RESULT = UIAbility.registerCreator("EntryAbility", {=> MainAbility()})  
```