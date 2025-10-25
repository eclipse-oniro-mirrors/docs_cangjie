# ohos.raw_file_descriptor

本模块表示rawfile的描述符信息。

## 导入模块

```cangjie
import kit.LocalizationKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## class RawFileDescriptor

```cangjie
public class RawFileDescriptor {
    public let fd: Int32
    public let offset: Int64
    public let length: Int64
}
```

**功能：** 表示rawfile的描述符信息。

**系统能力：** SystemCapability.Global.ResourceManager

**起始版本：** 22

### let fd

```cangjie
public let fd: Int32
```

**功能：** rawfile所在hap的文件描述符。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.Global.ResourceManager

**起始版本：** 22

### let length

```cangjie
public let length: Int64
```

**功能：** rawfile的文件长度。

**类型：** Int64

**读写能力：** 只读

**系统能力：** SystemCapability.Global.ResourceManager

**起始版本：** 22

### let offset

```cangjie
public let offset: Int64
```

**功能：** rawfile的起始偏移量。

**类型：** Int64

**读写能力：** 只读

**系统能力：** SystemCapability.Global.ResourceManager

**起始版本：** 22
