# Full-Screen Modal Transition  

By using the `bindContentCover` property, a component can be bound to a full-screen modal page. Transition effects can be displayed during the insertion and deletion of the component by setting the `ModalTransition` parameter.  

> **Note:**  
>  
> - Does not support screen orientation switching.  
> - Does not support route navigation.  

## Import Module  

```cangjie  
import kit.ArkUI.*  
```  

## func bindContentCover(?Bool, ?CustomBuilder, ?ContentCoverOptions)  

```cangjie  
public func bindContentCover(isShow: ?Bool, builder: ?CustomBuilder, options!: ?ContentCoverOptions = None): T  
```  

**Function:**  
Binds a full-screen modal page to a component, which is displayed upon clicking. The content of the modal page is customizable, and the display method can be configured with no transition animation, vertical sliding transition, or transparent gradient transition.  

**System Capability:**  
SystemCapability.ArkUI.ArkUI.Full  

**Initial Version:**  
22  

**Parameters:**  

| Parameter | Type | Required | Default Value | Description |  
|:---|:---|:---|:---|:---|  
| isShow | ?Bool | Yes | - | Whether to display the full-screen modal page.<br/>Default value: false. |  
| builder | ?[CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | Configures the content of the full-screen modal page.<br>Default value: { => }. |  
| options | ?[ContentCoverOptions](./cj-common-types.md#class-contentcoveroptions) | No | None | **Named parameter.** Configures optional properties of the full-screen modal page.<br/>Default value: ContentCoverOptions(). |  

**Return Value:**  

| Type | Description |  
|:---|:---|  
| T | Returns the component instance itself that calls this interface. |