# ohos.labels (通用接口标签)

标签说明。标签包括 atomicservice（是否支持原子服务）、crossplatform（是否支持跨平台）、deprecated（已弃用版本）、form（是否在表单中支持）、permission（所需权限）、since（API 级别）、stagemodelonly（是否仅支持 Stage 模型）、syscap（所需系统能力）等。

## 导入模块

```cangjie
import ohos.labels.*
```

## 使用说明

此包用于以注解形式为 API 添加标签标注，并对注解信息提供说明。不建议用户使用。

## interface PermissionValue

```cangjie
public interface PermissionValue {
    operator func &(rhs: PermissionValue): PermissionValue
    operator func |(rhs: PermissionValue): PermissionValue
}
```

**功能：** 用于处理权限之间的 “与 / 或” 关系。

**起始版本：** 22

### func &(PermissionValue)

```cangjie
operator func &(rhs: PermissionValue): PermissionValue
```

**功能：** 与另一个权限集进行 “与” 运算。返回 “与” 运算后的权限集。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值|描述|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|是|-|用于 “与” 运算的另一个权限集。|

**返回值：**

|类型| 描述    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| 运算结果。 |

### func |(PermissionValue)

```cangjie
operator func |(rhs: PermissionValue): PermissionValue
```

**功能：** 与另一个权限集进行 “或” 运算。返回 “或” 运算后的权限集。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值| 描述                     |
|:---|:---|:---|:---|:-----------------------|
|rhs|[PermissionValue](#interface-permissionvalue)|是|-| 与另一个权限集进行 “或” 运算后的权限集。 |

**返回值：**

|类型| 描述    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| 运算结果。 |

## interface LevelValue

```cangjie
public interface LevelValue {}
```

**功能：** 用于表示level标签的值。

**起始版本：** 22

## class APILevel

```cangjie
public class APILevel {
    public let since: String
    public let atomicservice: Bool
    public let crossplatform: Bool
    public let deprecated: ?String
    public let form: Bool
    public let permission: ?PermissionValue
    public let syscap: String
    public let throwexception: Bool
    public let workerthread: Bool
    public let systemapi: Bool
    public const init(since!: String, atomicservice!: Bool = false, crossplatform!: Bool = false,
        deprecated!: ?String = None, form!: Bool = false, permission!: ?PermissionValue = None,
        syscap!: String = "", throwexception!: Bool = false, workerthread!: Bool = false, systemapi!: Bool = false)
}
```

**功能：** 标签的定义。标签用于对 API 进行注解。标签包括 atomicservice（是否支持原子服务）、crossplatform（是否支持跨平台）、deprecated（已弃用版本）、form（是否在表单中支持）、permission（所需权限）、since（API 级别）、stagemodelonly（是否仅支持 Stage 模型）、syscap（所需系统能力）等。

**起始版本：** 22

### let atomicservice

```cangjie
public let atomicservice: Bool
```

**功能：** 当前 API 是否支持原子服务。

**类型：** Bool

**读写：** 只读

**起始版本：** 22

### let crossplatform

```cangjie
public let crossplatform: Bool
```

**功能：** 是否支持跨平台。

**类型：** Bool

**读写：** 只读

**起始版本：** 22

### let deprecated

```cangjie
public let deprecated: ?String
```

**功能：** 当前 API 的已弃用版本，默认值为 None，表示未弃用。

**类型：** String

**读写：** 只读

**起始版本：** 22

### let form

```cangjie
public let form: Bool
```

**功能：** 当前 API 在 forms 里是否支持。

**类型：** Bool

**读写：** 只读

**起始版本：** 22

### let permission

```cangjie
public let permission:?PermissionValue
```

**功能：** 使用当前API需要的权限。

**类型：** ?[PermissionValue](#interface-permissionvalue)

**读写：** 只读

**起始版本：** 22

### let since

```cangjie
public let since: String
```

**功能：** API 起始版本。

**类型：** String

**读写：** 只读

**起始版本：** 22

### let syscap

```cangjie
public let syscap: String
```

**功能：** 当前API需要的系统能力。

**类型：** String

**读写：** 只读

**起始版本：** 22

### let systemapi

```cangjie
public let systemapi: Bool
```

**功能：** 当前API是否仅供系统应用使用。

**类型：** Bool

**读写：** 只读

**起始版本：** 22

### let throwexception

```cangjie
public let throwexception: Bool
```

**功能：** 当前API是否抛出异常。

**类型：** Bool

**读写：** 只读

**起始版本：** 22

### let workerthread

```cangjie
public let workerthread: Bool
```

**功能：** 当前API是否建议并发执行。

**类型：** Bool

**读写：** 只读

**起始版本：** 22

### init(String, Bool, Bool, ?String, Bool, ?PermissionValue, String, Bool, Bool, Bool)

```cangjie
public const init(since!: String, atomicservice!: Bool = false, crossplatform!: Bool = false,
    deprecated!: ?String = None, form!: Bool = false, permission!: ?PermissionValue = None,
    syscap!: String = "", throwexception!: Bool = false, workerthread!: Bool = false, systemapi!: Bool = false)
```

**功能：** APILevel 构造函数。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值| 描述                 |
|:---|:---|:---|:---|:-------------------|
|since|[LevelValue](#interface-levelvalue)|是|-| API level。         |
|atomicservice|Bool|否|false| 命名参数 是否支持原子服务。     |
|crossplatform|Bool|否|false| 命名参数 是否支持跨平台。      |
|deprecated|[LevelValue](#interface-levelvalue)|否|0| 命名参数 弃用版本。         |
|form|Bool|否|false| 命名参数 是否支持forms。    |
|permission|?[PermissionValue](#interface-permissionvalue)|否|None| 命名参数 是否支持所需权限。      |
|stagemodelonly|Bool|否|true| 命名参数 是否只支持Stage模型。 |
|syscap|String|否|""| 命名参数 是否支持 系统能力。      |
|throwexception|Bool|否|""| 命名参数 是否支持 异常能力。      |
|workerthread|Bool|否|""| 命名参数 是否支持 异步接口力。      |
|systemapi|Bool|否|""| 命名参数 是否支持  系统api。      |

## class PermissionAnd

```cangjie
public class PermissionAnd <: PermissionValue {
    public let lhs: PermissionValue
    public let rhs: PermissionValue
    public const init(lhs: PermissionValue, rhs: PermissionValue)
}
```

**功能：** 表示多个权限的 “与” 运算。

**起始版本：** 22

**父类型：**

- [PermissionValue](#interface-permissionvalue)

### let lhs

```cangjie
public let lhs: PermissionValue
```

**功能：** 操作符左值。

**类型：** PermissionValue

**读写能力：** 只读

**起始版本：** 22

### let rhs

```cangjie
public let rhs: PermissionValue
```

**功能：** 操作符右值。

**类型：** PermissionValue

**读写能力：** 只读

**起始版本：** 22

### init(PermissionValue, PermissionValue)

```cangjie
public const init(lhs: PermissionValue, rhs: PermissionValue)
```

**功能：** 构造一个 PermissionAnd 权限集，表示两个权限集的 “与” 运算。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值| 描述                   |
|:---|:---|:---|:---|:---------------------|
|lhs|[PermissionValue](#interface-permissionvalue)|是|-| 用于构造 “与” 权限集的一个权限集。  |
|rhs|[PermissionValue](#interface-permissionvalue)|是|-| 用于构造 “与” 权限集的另一个权限集。 |

### func &(PermissionValue)

```cangjie
public const override operator func &(rhs: PermissionValue): PermissionValue
```

**功能：** 与另一个权限集进行 “与” 运算。返回 “与” 运算后的权限集。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值|描述|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|是|-|用于构造 “与” 权限集的另一个权限集。|

**返回值：**

|类型| 描述    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| 运算结果。 |

### func |(PermissionValue)

```cangjie
public const override operator func |(rhs: PermissionValue): PermissionValue
```

**功能：** 与另一个权限集进行 “或” 运算。返回 “或” 运算后的权限集。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值|描述|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|是|-|用于 “或” 运算的另一个权限集。|

**返回值：**

|类型| 描述    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| 运算结果。 |

## class PermissionOr

```cangjie
public class PermissionOr <: PermissionValue {
    public let lhs: PermissionValue
    public let rhs: PermissionValue
    public const init(lhs: PermissionValue, rhs: PermissionValue)
}
```

**功能：** 表示多个权限的逻辑 “或” 运算。

**起始版本：** 22

**父类型：**

- [PermissionValue](#interface-permissionvalue)

### let lhs

```cangjie
public let lhs: PermissionValue
```

**功能：** 操作符左值。

**类型：** PermissionValue

**读写能力：** 只读

**起始版本：** 22

### let rhs

```cangjie
public let rhs: PermissionValue
```

**功能：** 操作符右值。

**类型：** PermissionValue

**读写能力：** 只读

**起始版本：** 22

### init(PermissionValue, PermissionValue)

```cangjie
public const init(lhs: PermissionValue, rhs: PermissionValue)
```

**功能：** 构造一个 PermissionOr 权限集，表示两个权限集的逻辑 “或” 运算。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值| 描述   |
|:---|:---|:---|:---|:-----|
|lhs|[PermissionValue](#interface-permissionvalue)|是|-| 参数1。 |
|rhs|[PermissionValue](#interface-permissionvalue)|是|-| 参数2。 |

### func &(PermissionValue)

```cangjie
public const override operator func &(rhs: PermissionValue): PermissionValue
```

**功能：** 与另一个权限集执行逻辑 “与” 运算。返回 “与” 运算后的结果权限集。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值|描述|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|是|-|用于 “与” 运算的另一个权限集。|

**返回值：**

|类型|描述|
|:----|:----|
|[PermissionValue](#interface-permissionvalue)|与另一个权限集执行逻辑 “与” 运算后的权限集。|

### func |(PermissionValue)

```cangjie
public const override operator func |(rhs: PermissionValue): PermissionValue
```

**功能：** 与另一个权限集执行逻辑 “或” 运算。返回 “或” 运算后的结果权限集。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值| 描述                |
|:---|:---|:---|:---|:------------------|
|rhs|[PermissionValue](#interface-permissionvalue)|是|-| 用于 “或” 运算的另一个权限集。 |

**返回值：**

|类型| 描述    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| 运算结果。 |

## extend String

```cangjie
extend String <: PermissionValue {}
```

**功能：** 以下是一个扩展 PermissionValue 接口的实现，使用字符串表示单个权限。

**起始版本：** 22

**父类型：**

- [PermissionValue](#interface-permissionvalue)

### func &(PermissionValue)

```cangjie
public const operator func &(rhs: PermissionValue): PermissionValue
```

**功能：** 与另一个权限集执行逻辑 “与”（AND）运算。在 “与” 运算完成后，返回生成的权限集。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值|描述|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|是|-|用于 “与”（AND）运算的另一个权限集。|

**返回值：**

|类型|描述|
|:----|:----|
|[PermissionValue](#interface-permissionvalue)|与另一个权限集执行逻辑 “与”（AND）运算后的权限集。|

### func |(PermissionValue)

```cangjie
public const operator func |(rhs: PermissionValue): PermissionValue
```

**功能：** 与另一个权限集执行逻辑 “或”（OR）运算，在 “或” 运算完成后返回生成的权限集。

**起始版本：** 22

**参数：**

|参数|类型|必填|默认值|描述|
|:---|:---|:---|:---|:---|
|rhs|[PermissionValue](#interface-permissionvalue)|是|-|用于 “或”（OR）运算的另一个权限集。|

**返回值：**

|类型| 描述    |
|:----|:------|
|[PermissionValue](#interface-permissionvalue)| 运算结果。 |
