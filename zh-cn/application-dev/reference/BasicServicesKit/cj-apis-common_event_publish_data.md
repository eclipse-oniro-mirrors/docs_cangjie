# ohos.common_event_publish_data

本模块描述公共事件内容和属性。

## 导入模块

```cangjie
import kit.BasicServicesKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## class CommonEventPublishData

```cangjie
public class CommonEventPublishData {
    public var bundleName: String
    public var data: String
    public var code: Int32
    public var subscriberPermissions: Array<String>
    public var isOrdered: Bool
    public var isSticky: Bool
    public var parameters: HashMap<String, ValueType>
    public init(
        bundleName!: String = "",
        data!: String = "",
        code!: Int32 = 0,
        subscriberPermissions!: Array<String> = Array<String>(),
        isOrdered!: Bool = false,
        isSticky!: Bool = false,
        parameters!: HashMap<String, ValueType> = HashMap<String, ValueType>()
    )
}
```

**功能：** 包含公共事件内容和属性。

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### var bundleName

```cangjie
public var bundleName: String
```

**功能：** 表示订阅者包名称，只有包名为bundleName的订阅者才能收到该公共事件。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### var code

```cangjie
public var code: Int32
```

**功能：** 表示公共事件的结果代码。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### var data

```cangjie
public var data: String
```

**功能：** 表示公共事件的自定义结果数据。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### var isOrdered

```cangjie
public var isOrdered: Bool
```

**功能：** 表示是否是有序事件。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### var isSticky

```cangjie
public var isSticky: Bool
```

**功能：** 表示是否是粘性事件。仅系统应用或系统服务允许发送粘性事件。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### var parameters

```cangjie
public var parameters: HashMap<String, ValueType>
```

**功能：** 表示公共事件的附加信息。

**类型：** HashMap\<String, ValueType>

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### var subscriberPermissions

```cangjie
public var subscriberPermissions: Array<String>
```

**功能：** 表示订阅者的权限。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### init(String, String, Int32, Array\<String>, Bool, Bool, HashMap\<String,ValueType>)

```cangjie
public init(
    bundleName!: String = "",
    data!: String = "",
    code!: Int32 = 0,
    subscriberPermissions!: Array<String> = Array<String>(),
    isOrdered!: Bool = false,
    isSticky!: Bool = false,
    parameters!: HashMap<String, ValueType> = HashMap<String, ValueType>()
)
```

**功能：** 构造CommonEventPublishData对象。

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|bundleName|String|否|""|表示订阅者包名称，只有包名为bundleName的订阅者才能收到该公共事件。|
|data|String|否|""|表示公共事件的自定义结果数据。|
|code|Int32|否|0|表示公共事件的结果代码。|
|subscriberPermissions|Array\<String>|否|Array\<String>()| **命名参数。** 表示订阅者的权限。|
|isOrdered|Bool|否|false| **命名参数。** 表示是否是有序事件。|
|isSticky|Bool|否|false| **命名参数。** 表示是否是粘性事件。仅系统应用或系统服务允许发送粘性事件。|
|parameters|HashMap\<String, ValueType>|否|HashMap<String, ValueType>()| **命名参数。** 表示公共事件的附加信息|
