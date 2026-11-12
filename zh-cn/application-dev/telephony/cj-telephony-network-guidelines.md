# 获取蜂窝网络信息

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

## 场景介绍

应用可以查询注册网络的国家码、网络注册状态、自动或手动选网模式、主卡卡槽、无线接入技术，以及设备是否支持NR。本文介绍一次性查询；查询结果不会在设备状态变化时自动更新。

## 基本概念

| 名称 | 说明 |
| :--- | :--- |
| 卡槽ID | 从0开始的卡槽编号。例如0表示卡槽1，1表示卡槽2。可用卡槽取决于设备配置，不应假定所有设备都有两个卡槽。 |
| 主卡卡槽 | 系统配置的主卡所在卡槽，可通过getPrimarySlotId查询。不带卡槽参数的getNetworkState固定查询卡槽0。 |
| NetworkState | 网络状态，包括运营商名称、网络注册状态、接入技术、是否漫游等信息。 |
| NetworkSelectionMode | 选网模式，包括未知、自动选网和手动选网。查询接口不会切换选网模式。 |
| NetworkRadioTech | 无线接入技术信息。csRadioTech表示CS（电路交换）域技术，psRadioTech表示PS（分组交换）域技术。 |
| NR | New Radio，5G无线接入技术。设备支持NR与设备当前已连接5G网络是不同的信息。 |

## 约束与限制

- 本文接口从26.1.0版本开始支持，设备需具备SystemCapability.Telephony.CoreService系统能力。
- 调用getNetworkState和getRadioTechSync需要ohos.permission.GET_NETWORK_INFO权限。
- 未注册网络时，国家码可能为空；卡槽无效时国家码也为空。getRadioTechSync在卡槽无效或查询失败时返回的CS、PS技术均为RadioTechnologyUnknown，不能将Unknown当成某个特定错误。
- 当前getNetworkState返回的nsaState为NsaStateNotSupport，isCaActive为false，不能依靠这两个属性判断实际的NSA组网或载波聚合状态。
- 修改返回对象的属性只修改当前对象，不会改变设备网络配置。查询结果与SIM卡、网络覆盖及设备能力有关。

## 接口说明

完整接口、参数和错误码见[ohos.telephony.radio](../reference/TelephonyKit/cj-apis-telephony-radio.md)。

| 接口名 | 描述 |
| :--- | :--- |
| getISOCountryCodeForNetworkSync(Int32) | 同步获取指定卡槽注册网络的ISO国家码。 |
| getNetworkSelectionMode(Int32, AsyncCallback\<NetworkSelectionMode>) | 异步获取指定卡槽的选网模式。 |
| getNetworkState(Int32, AsyncCallback\<NetworkState>) | 异步获取指定卡槽的网络状态。 |
| getNetworkState(AsyncCallback\<NetworkState>) | 异步获取卡槽0的网络状态。 |
| getPrimarySlotId(AsyncCallback\<Int32>) | 异步获取主卡卡槽ID。 |
| getRadioTechSync(Int32) | 同步获取指定卡槽的CS、PS域无线接入技术。 |
| isNRSupported() | 查询设备是否支持NR。 |

## 开发步骤

1. 在模块的module.json5中声明GET_NETWORK_INFO权限。该权限为系统授权，声明方法见[声明权限](../security/AccessToken/cj-declare-permissions.md)。以下内容放入module节点；已有requestPermissions时，将权限项合并到原数组。

   ```json
   "requestPermissions": [
     {
       "name": "ohos.permission.GET_NETWORK_INFO"
     }
   ]
   ```

2. 导入TelephonyKit以及回调、异常和日志类型。根据业务需要选择设备上可用的卡槽ID；以下示例使用卡槽0。
3. 同步查询可直接读取返回值。异步查询在回调中处理结果：error为Some时读取错误码；error为None且data为Some时使用返回数据。不要在接口调用后立即读取尚未到达的异步结果。
4. 将以下函数添加到仓颉工程，在业务代码中调用需要的函数。queryNetworkState查询指定卡槽，queryDefaultNetworkState查询卡槽0。如需查询主卡，应在getPrimarySlotId成功回调中调用getNetworkState(value, callback)。

## 示例代码

```cangjie
import kit.TelephonyKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

func queryCountryCode(): Unit {
    let code = getISOCountryCodeForNetworkSync(0)
    if (code.isEmpty()) {
        Hilog.info(0, "TelephonyExample", "No network country code is available", [])
    } else {
        Hilog.info(0, "TelephonyExample", "ISO country code: ${code}", [])
    }
}

func querySelectionMode(): Unit {
    let callback: AsyncCallback<NetworkSelectionMode> = { error: ?BusinessException, data: ?NetworkSelectionMode =>
        if (let Some(e) <- error) {
            Hilog.error(0, "TelephonyExample", "Query failed. Code: ${e.code}, message: ${e.message}", [])
        } else if (let Some(value) <- data) {
            Hilog.info(0, "TelephonyExample", "Selection mode: ${value.toString()}", [])
        }
    }
    try {
        getNetworkSelectionMode(0, callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "TelephonyExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}

func queryNetworkState(): Unit {
    let callback: AsyncCallback<NetworkState> = { error: ?BusinessException, data: ?NetworkState =>
        if (let Some(e) <- error) {
            Hilog.error(0, "TelephonyExample", "Query failed. Code: ${e.code}, message: ${e.message}", [])
        } else if (let Some(value) <- data) {
            Hilog.info(0, "TelephonyExample",
                "Registration: ${value.regState.toString()}, operator: ${value.longOperatorName}", [])
        }
    }
    try {
        getNetworkState(0, callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "TelephonyExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}

func queryDefaultNetworkState(): Unit {
    let callback: AsyncCallback<NetworkState> = { error: ?BusinessException, data: ?NetworkState =>
        if (let Some(e) <- error) {
            Hilog.error(0, "TelephonyExample", "Query failed. Code: ${e.code}, message: ${e.message}", [])
        } else if (let Some(value) <- data) {
            Hilog.info(0, "TelephonyExample",
                "Registration: ${value.regState.toString()}, roaming: ${value.isRoaming}", [])
        }
    }
    try {
        getNetworkState(callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "TelephonyExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}

func queryPrimarySlot(): Unit {
    let callback: AsyncCallback<Int32> = { error: ?BusinessException, data: ?Int32 =>
        if (let Some(e) <- error) {
            Hilog.error(0, "TelephonyExample", "Query failed. Code: ${e.code}, message: ${e.message}", [])
        } else if (let Some(value) <- data) {
            Hilog.info(0, "TelephonyExample", "Primary slot ID: ${value}", [])
        }
    }
    try {
        getPrimarySlotId(callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "TelephonyExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}

func queryRadioTechnology(): Unit {
    try {
        let technology = getRadioTechSync(0)
        if (technology.psRadioTech == RadioTechnology.RadioTechnologyUnknown &&
            technology.csRadioTech == RadioTechnology.RadioTechnologyUnknown) {
            Hilog.info(0, "TelephonyExample", "Radio technology is unknown or unavailable", [])
        } else {
            Hilog.info(0, "TelephonyExample",
                "PS: ${technology.psRadioTech.toString()}, CS: ${technology.csRadioTech.toString()}", [])
        }
    } catch (e: BusinessException) {
        Hilog.error(0, "TelephonyExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}

func queryNrCapability(): Unit {
    let supported = isNRSupported()
    Hilog.info(0, "TelephonyExample", "NR supported: ${supported}", [])
}
```

示例通过Hilog输出结果。异步查询错误通过回调返回；外围的try/catch不能代替回调内的错误处理。各个查询独立执行，返回时间和顺序不固定。
