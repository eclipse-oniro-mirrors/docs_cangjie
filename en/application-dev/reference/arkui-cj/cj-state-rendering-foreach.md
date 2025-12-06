# ForEach

The ForEach interface performs loop rendering based on array-type data.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class ForEach\<T>

```cangjie
public class ForEach<T> {
    public init(arr: CollectionEx<T>, itemGenerator!: ItemGeneratorFunc<T>,
        keyGenerator!: ?KeyGeneratorFunc<T> = None) {}
}
```

**Description:** Creates a loop rendering component. The ForEach interface performs loop rendering based on array-type data and must be used in conjunction with container components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(CollectionEx\<T>, ItemGeneratorFunc\<T>, ?KeyGeneratorFunc\<T>)

```cangjie
public init(arr: CollectionEx<T>, itemGenerator!: ItemGeneratorFunc<T>, keyGenerator!: ?KeyGeneratorFunc<T> = None)
```

**Description:** Defines the ForEach component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| arr | [CollectionEx](./cj-common-types.md#interface-collectionext)\<T> | Yes | - | Array collection for UI. |
| itemGenerator | [ItemGeneratorFunc](./cj-common-types.md#type-itemgeneratorfunc)\<T> | Yes | - | **Named parameter.** Item generator function. |
| keyGenerator | ?[KeyGeneratorFunc](./cj-common-types.md#type-keygeneratorfunc)\<T> | No | None | **Named parameter.** Key generator function. |

### func pop()

```cangjie
public func pop(): Unit
```

**Description:** Pops the ForEach component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22