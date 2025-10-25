# Motion Path Animation (motionPath)

Sets the motion path for component displacement animation.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class MotionPathOptions

```cangjie
public class MotionPathOptions {
    public var path: String
    public var from: Float64 = 0.0
    public var to: Float64 = 1.0
    public var rotatable: Bool = false
    public init(
        path!: String,
        from!: Float64 = 0.0,
        to!: Float64 = 1.0,
        rotatable!: Bool = false
    )
}
```

**Function:** Configures animation path options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var from

```cangjie
public var from: Float64 = 0.0
```

**Function:** Sets the starting position of the animation path.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var path

```cangjie
public var path: String
```

**Function:** Sets the animation path.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var rotatable

```cangjie
public var rotatable: Bool = false
```

**Function:** Sets whether the animation path is rotatable.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var to

```cangjie
public var to: Float64 = 1.0
```

**Function:** Sets the ending position of the animation path.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(String, Float64, Float64, Bool)

```cangjie
public init(
    path!: String,
    from!: Float64 = 0.0,
    to!: Float64 = 1.0,
    rotatable!: Bool = false
)
```

**Function:** Constructs a MotionPathOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Sets the animation path. |
| from | Float64 | No | 0.0 | Sets the starting position of the animation path. |
| to | Float64 | No | 1.0 | Sets the ending position of the animation path. |
| rotatable | Bool | No | false | Sets whether the animation path is rotatable. |