# ohos.arkui.component.recycle

Component recycling interface, exclusively for UI framework usage.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class __Recycle__

```cangjie
public class __Recycle__ <: ContainerBase {
    public init()
    public init(child: () -> Unit)
}
```

**Description:** Component pending recycling, used by UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [ContainerBase](./cj-ui-framework.md#class-containerbase)

### init()

```cangjie
public init()
```

**Description:** Initializes a component pending recycling, used by UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(() -> Unit)

```cangjie
public init(child: () -> Unit)
```

**Description:** Initializes a component pending recycling from child components, used by UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|child|()->Unit|Yes|-|Child component pending recycling.|

### func pop()

```cangjie
public override func pop()
```

**Description:** Recycles this component, used by UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21