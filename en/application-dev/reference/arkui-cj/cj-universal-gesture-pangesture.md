# PanGesture  

A swipe gesture event that triggers when the minimum swipe distance reaches the set threshold.  

## Import Module  

```cangjie  
import kit.ArkUI.*  
```  

## func !=(PanDirection)  

```cangjie  
public operator func !=(other: PanDirection): Bool  
```  

**Description:** Determines whether two enumeration values are not equal.  

**Parameters:**  

| Parameter | Type | Required | Default | Description |  
|:---|:---|:---|:---|:---|  
| other | [PanDirection](#enum-pandirection) | Yes | - | Another enumeration value. |  

**Return Value:**  

| Type | Description |  
|:----|:----|  
| Bool | Returns `true` if the two enumeration values are not equal; otherwise, returns `false`. |  

## func ==(PanDirection)  

```cangjie  
public operator func ==(other: PanDirection): Bool  
```  

**Description:** Determines whether two enumeration values are equal.  

**Parameters:**  

| Parameter | Type | Required | Default | Description |  
|:---|:---|:---|:---|:---|  
| other | [PanDirection](#enum-pandirection) | Yes | - | Another enumeration value. |  

**Return Value:**  

| Type | Description |  
|:----|:----|  
| Bool | Returns `true` if the two enumeration values are equal; otherwise, returns `false`. |  

## func &(PanDirection)  

```cangjie  
public operator func &(right: PanDirection): PanDirection  
```  

**Description:** Performs a logical AND (`&`) operation on `PanDirection`.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parameters:**  

| Parameter | Type | Required | Default | Description |  
|:---|:---|:---|:---|:---|  
| right | [PanDirection](#enum-pandirection) | Yes | - | Swipe direction |  

**Return Value:**  

| Type | Description |  
|:----|:----|  
| [PanDirection](#enum-pandirection) | Swipe direction |  

## func |(PanDirection)  

```cangjie  
public operator func |(right: PanDirection): PanDirection  
```  

**Description:** Performs a logical OR (`|`) operation on `PanDirection`.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parameters:**  

| Parameter | Type | Required | Default | Description |  
|:---|:---|:---|:---|:---|  
| right | [PanDirection](#enum-pandirection) | Yes | - | Swipe direction |  

**Return Value:**  

| Type | Description |  
|:----|:----|  
| [PanDirection](#enum-pandirection) | Swipe direction |  

## Basic Type Definitions  

### enum PanDirection  

```cangjie  
public enum PanDirection <: Equatable<PanDirection> {  
    | None  
    | Left  
    | Right  
    | Horizontal  
    | Up  
    | Down  
    | Vertical  
    | All  
    | Computed(UInt32)  
    | ...  
}  
```  

**Description:** Direction of the drag gesture.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parent Type:**  

- Equatable\<PanDirection>  

#### All  

```cangjie  
All  
```  

**Description:** All directions.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

#### Computed(UInt32)  

```cangjie  
Computed(UInt32)  
```  

**Description:** Supports logical AND (`&`) and logical OR (`|`) operations.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

#### Down  

```cangjie  
Down  
```  

**Description:** Drag downward.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

#### Horizontal  

```cangjie  
Horizontal  
```  

**Description:** Horizontal direction.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

#### Left  

```cangjie  
Left  
```  

**Description:** Drag leftward.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

#### None  

```cangjie  
None  
```  

**Description:** All directions.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

#### Right  

```cangjie  
Right  
```  

**Description:** Drag rightward.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

#### Up  

```cangjie  
Up  
```  

**Description:** Drag upward.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

#### Vertical  

```cangjie  
Vertical  
```  

**Description:** Vertical direction.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

#### func &(PanDirection)  

```cangjie  
public operator func &(right: PanDirection): PanDirection  
```  

**Description:** Performs a logical AND (`&`) operation on `PanDirection`.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parameters:**  

| Parameter | Type | Required | Default | Description |  
|:---|:---|:---|:---|:---|  
| right | [PanDirection](#enum-pandirection) | Yes | - | Swipe direction |  

**Return Value:**  

| Type | Description |  
|:----|:----|  
| [PanDirection](#enum-pandirection) | Swipe direction |  

#### func |(PanDirection)  

```cangjie  
public operator func |(right: PanDirection): PanDirection  
```  

**Description:** Performs a logical OR (`|`) operation on `PanDirection`.  

**System Capability:** SystemCapability.ArkUI.ArkUI.Full  

**Since:** 21  

**Parameters:**  

| Parameter | Type | Required | Default | Description |  
|:---|:---|:---|:---|:---|  
| right | [PanDirection](#enum-pandirection) | Yes | - | Swipe direction |  

**Return Value:**  

| Type | Description |  
|:----|:----|  
| [PanDirection](#enum-pandirection) | Swipe direction |