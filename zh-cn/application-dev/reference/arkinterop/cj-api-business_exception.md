# ohos.business_exception (通用异常信息)

本模块定义了接口调用过程中出现的常见异常信息。

## class BusinessException

```cangjie
public open class BusinessException <: Exception {
    public let code: Int32
    public init(code: Int32, msg: String)
}
```

**功能：** 业务异常类，继承自Exception类。

**系统能力：** SystemCapability.Base

**起始版本：** 22

**父类型：**

- Exception

### let code

```cangjie
public let code: Int32
```

**功能：** 错误码。

**类型：** Int32

**读写能力：** 只读

**起始版本：** 22

### init(Int32, String)

```cangjie
public init(code: Int32, msg: String)
```

**功能：** 创建BusinessException类的实例。

**系统能力：** SystemCapability.Base

**起始版本：** 22

**参数：**

| 参数 | 类型 | 必填 | 说明    |
|:---|:---|:---|:------|
| code | Int32 | 是 | 错误码。 |
| msg | String | 是 | 错误信息。|

### func toString()

```cangjie
public open func toString(): String
```

**功能：** 获取错误信息字符串。

**系统能力：** SystemCapability.Base

**起始版本：** 22

**返回值：**

| 类型 | 说明    |
|:----|:------|
| String | 错误信息。|

## class BusinessError

```cangjie
public class BusinessError<T> <: BusinessException  {
    public var data: T
    public init (data: T, code: Int32, msg: String)
}
```

**功能：** 业务错误类，继承自BusinessException。

**系统能力：** SystemCapability.Base

**起始版本：** 22

**父类型：**

- BusinessException

### let data

```cangjie
public var data: T
```

**功能：** 定义错误的额外信息。

**类型：** T

**读写能力：** 读写

**起始版本：** 22

### init(T, Int32, String)

```cangjie
public init(data: T, code: Int32, msg: String)
```

**功能：** 创建一个BusinessError类的实例。

**系统能力：** SystemCapability.Base

**起始版本：** 22

**参数：**

| 参数 | 类型 | 必填 | 说明    |
|:---|:---|:---|:------|
 | data | T | 是 | 额外信息  |
| code | Int32 | 是 | 错误码。 |
| msg | String | 是 | 错误信息。|

### getClassName()

```cangjie
protected override func getClassName(): String
```

**功能：** 获取异常类型名称。

**系统能力：** SystemCapability.Base

**起始版本：** 22

**返回值：**

| 类型     | 说明    |
|:-------|:------|
| String | 类型名称。 |

## type AsyncCallback

```cangjie
public type AsyncCallback<T>=(Option<AsyncError>, Option<T>) -> Unit
```

**功能：** 定义了异步回调类型。

**系统能力：** SystemCapability.Base

**起始版本：** 22
