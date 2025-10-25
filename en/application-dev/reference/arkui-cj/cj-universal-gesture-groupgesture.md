# Composite Gestures  

Gesture recognition composition refers to combining multiple gestures into composite gestures, supporting sequential recognition, parallel recognition, and exclusive recognition.  

## Importing the Module  

```cangjie  
import kit.UIkit.*  
```  

## Permission List  

None  

## func !=(GestureMode)  

```cangjie  
public operator func !=(other: GestureMode): Bool  
```  

**Function:** Determines whether two enumeration values are not equal.  

**Parameters:**  

| Parameter Name | Type | Required | Default Value | Description |  
|:---|:---|:---|:---|:---|  
| other | [GestureMode](#enum-gesturemode) | Yes | - | Another enumeration value to compare. |  

**Return Value:**  

| Type | Description |  
|:----|:----|  
| Bool | Returns `true` if the two enumeration values are not equal; otherwise, returns `false`. |  

## func ==(GestureMode)  

```cangjie  
public operator func ==(other: GestureMode): Bool  
```  

**Function:** Determines whether two enumeration values are equal.  

**Parameters:**  

| Parameter Name | Type | Required | Default Value | Description |  
|:---|:---|:---|:---|:---|  
| other | [GestureMode](#enum-gesturemode) | Yes | - | Another enumeration value to compare. |  

**Return Value:**  

| Type | Description |  
|:----|:----|  
| Bool | Returns `true` if the two enumeration values are equal; otherwise, returns `false`. |  

## Basic Type Definitions  

### enum GestureMode  

```cangjie  
public enum GestureMode <: Equatable<GestureMode> {  
    | Sequence  
    | Parallel  
    | Exclusive  
    | ...  
}  
```  

**Function:** Recognition modes for composite gestures.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since Version:** 21  

**Parent Type:**  

- Equatable\<GestureMode>  

#### Exclusive  

```cangjie  
Exclusive  
```  

**Function:** Exclusive recognition. Registered gestures are recognized simultaneously. If one gesture is successfully recognized, gesture recognition ends.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since Version:** 21  

#### Parallel  

```cangjie  
Parallel  
```  

**Function:** Parallel recognition. Registered gestures are recognized simultaneously until all gestures complete recognition. Gesture recognition does not interfere with each other.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since Version:** 21  

#### Sequence  

```cangjie  
Sequence  
```  

**Function:** Sequential recognition. Gestures are recognized in the order of registration until all gestures are successfully recognized. If one gesture fails recognition, all subsequent gestures fail. In a sequential gesture group, only the last gesture can respond to `onActionEnd`.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since Version:** 21