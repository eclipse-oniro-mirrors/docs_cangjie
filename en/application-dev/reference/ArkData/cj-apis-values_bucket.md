# ohos.data.values_bucket

A ValuesBucket is a collection of data that developers insert into a database, transmitted in the form of key-value pairs.

## Import Module

```cangjie
import kit.ArkData.*
```

## enum ValueType

```cangjie
public enum ValueType {
    | Integer(Int64)
    | Double(Float64)
    | StringValue(String)
    | Boolean(Bool)
}
```

**Description:** This type is used to represent the data field types allowed in the database.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

### Boolean(Bool)

```cangjie
Boolean(Bool)
```

**Description:** Indicates the field type is boolean.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

### Double(Float64)

```cangjie
Double(Float64)
```

**Description:** Indicates the field type is floating-point number.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

### Integer(Int64)

```cangjie
Integer(Int64)
```

**Description:** Indicates the field type is integer.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

### StringValue(String)

```cangjie
StringValue(String)
```

**Description:** Indicates the field type is string.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21