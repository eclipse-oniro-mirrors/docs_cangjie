# WLAN开发指导

## 简介

WLAN（Wireless Local Area Network）是一种无线局域网络技术，允许设备通过无线方式连接到网络。通过WLAN，设备可以访问互联网、共享资源以及与其他设备通信。

## 场景介绍

主要场景有：

- 扫描并获取周围的WLAN热点信息。
- 连接到指定的WLAN热点。
- 监听WLAN状态变化事件。
- 使用P2P功能发现和连接设备。

## 接口说明

完整的仓颉 API 说明以及实例代码请参见：[WLAN 接口](../../../../zh-cn/application-dev/reference/ConnectivityKit/cj-apis-wifi_manager.md)。

具体接口说明如下表。

| 接口名 | 功能描述 |
| ------------------------------------------ | ----------------------------------------------------------- |
| getScanInfoList() | 获取扫描结果，返回周围的WLAN热点信息列表。 |
| isWifiActive() | 查询WLAN是否已使能。 |
| on(WifiCallbackType, Callback1Argument\<Int32>) | 注册WLAN状态改变事件。 |
| off(eventType: WifiCallbackType, callback!: ?CallbackObject = None): Unit | 取消注册WLAN状态改变事件。 |
| p2pCancelConnect() | 在P2P连接过程中，取消P2P连接。 |
| p2pConnect(config: WifiP2PConfig) | 执行P2P连接。 |
| startDiscoverDevices() | 开始发现P2P设备。 |
| stopDiscoverDevices() | 停止发现P2P设备。 |

## 主要场景开发步骤

### 扫描并获取WLAN热点信息

1. import需要的WLAN模块。
2. 检查WLAN是否已启用。
3. 获取扫描结果。
4. 处理扫描到的热点信息。
5. 示例代码:

    <!-- compile -->

    ```cangjie
    import kit.ConnectivityKit.*
    import ohos.base.BusinessException

    const TAG: String = 'WifiScanManager'

    class WifiScanManager {
        // 检查WLAN是否已启用
        public func checkWifiState(): Bool {
            try {
                let isActive = isWifiActive()
                AppLog.info("WiFi is " + (isActive ? "active" : "inactive"))
                return isActive
            } catch (e: BusinessException) {
                AppLog.error("Failed to check WiFi state. errCode: ${e.code}, errMessage: ${e.message}")
                return false
            }
        }

        // 获取扫描结果
        public func getWifiScanResults() {
            // 首先检查WLAN是否已启用
            if (!checkWifiState()) {
                AppLog.error("WiFi is not active, cannot scan")
                return
            }

            try {
                // 获取扫描结果
                let scanResults = getScanInfoList()
                AppLog.info("Found ${scanResults.size} WiFi networks")
                
                // 处理扫描结果
                for (i in 0..scanResults.size) {
                    let info = scanResults[i]
                    AppLog.info("Network ${i}: SSID=${info.ssid}, BSSID=${info.bssid}, RSSI=${info.rssi}, Frequency=${info.frequency}")
                }
            } catch (e: BusinessException) {
                AppLog.error("Failed to get scan info. errCode: ${e.code}, errMessage: ${e.message}")
            }
        }
    }

    let wifiScanManager = WifiScanManager()
    ```

### 监听WLAN状态变化事件

1. import需要的WLAN模块。
2. 定义回调函数处理WLAN状态变化。
3. 注册WLAN状态变化事件监听器。
4. 在适当时候取消注册监听器。
5. 示例代码:

    <!-- compile -->

    ```cangjie
    import kit.ConnectivityKit.*
    import ohos.base.{BusinessException, Callback1Argument}

    const TAG: String = 'WifiStateListener'

    class WifiStateListener {
        // 注册WLAN状态变化事件
        public func registerWifiStateListener() {
            try {
                on(WifiCallbackType.WifiScanStateChange, WifiStateChangeCallback())
                AppLog.info("Registered WiFi state change listener")
            } catch (e: BusinessException) {
                AppLog.error("Failed to register WiFi state listener. errCode: ${e.code}, errMessage: ${e.message}")
            }
        }

        // 取消注册WLAN状态变化事件
        public func unregisterWifiStateListener() {
            try {
                off(WifiCallbackType.WifiScanStateChange)
                AppLog.info("Unregistered WiFi state change listener")
            } catch (e: BusinessException) {
                AppLog.error("Failed to unregister WiFi state listener. errCode: ${e.code}, errMessage: ${e.message}")
            }
        }
    }

    // WLAN状态变化回调实现
    class WifiStateChangeCallback <: Callback1Argument<Int32> {
        public func invoke(state: Int32) {
            let stateStr = match (state) {
                case 0 => "disabled"
                case 1 => "enabled"
                case 2 => "enabling"
                case 3 => "disabling"
                case _ => "unknown"
            }
            AppLog.info("WiFi state changed to: ${stateStr} (${state})")
        }
    }

    let wifiStateListener = WifiStateListener()
    ```

### 使用P2P功能发现和连接设备

1. import需要的WLAN模块。
2. 开始发现P2P设备。
3. 处理发现的设备。
4. 连接到指定设备。
5. 停止发现设备。
6. 示例代码:

    <!-- compile -->

    ```cangjie
    import kit.ConnectivityKit.*
    import ohos.base.BusinessException

    const TAG: String = 'WifiP2PManager'

    class WifiP2PManager {
        // 开始发现设备
        public func startDeviceDiscovery() {
            try {
                startDiscoverDevices()
                AppLog.info("Started P2P device discovery")
            } catch (e: BusinessException) {
                AppLog.error("Failed to start device discovery. errCode: ${e.code}, errMessage: ${e.message}")
            }
        }

        // 停止发现设备
        public func stopDeviceDiscovery() {
            try {
                stopDiscoverDevices()
                AppLog.info("Stopped P2P device discovery")
            } catch (e: BusinessException) {
                AppLog.error("Failed to stop device discovery. errCode: ${e.code}, errMessage: ${e.message}")
            }
        }

        // 连接到P2P设备
        public func connectToDevice(deviceAddress: String) {
            try {
                // 创建P2P配置
                let config = WifiP2PConfig(
                    deviceAddress=deviceAddress,
                    netId=-1, // 临时组
                    passphrase="12345678", // 连接密码
                    groupName="P2P_Group",
                    goBand=GroupOwnerBand.GoBandAuto,
                    deviceAddressType=DeviceAddressType.RandomDeviceAddress
                )
                
                // 执行连接
                p2pConnect(config)
                AppLog.info("Connecting to P2P device: ${deviceAddress}")
            } catch (e: BusinessException) {
                AppLog.error("Failed to connect to P2P device. errCode: ${e.code}, errMessage: ${e.message}")
            }
        }

        // 取消P2P连接
        public func cancelP2PConnection() {
            try {
                p2pCancelConnect()
                AppLog.info("Cancelled P2P connection")
            } catch (e: BusinessException) {
                AppLog.error("Failed to cancel P2P connection. errCode: ${e.code}, errMessage: ${e.message}")
            }
        }
    }

    let wifiP2PManager = WifiP2PManager()
    ```

7. 错误码请参见[WLAN服务子系统错误码](../../../../zh-cn/application-dev/reference/ConnectivityKit/cj-errorcode-wifi-manager.md)。

## 相关信息

- 权限列表：
  - ohos.permission.GET_WIFI_INFO
  - ohos.permission.SET_WIFI_INFO）

- 系统能力：
  - SystemCapability.Communication.WiFi.STA（基础WLAN功能）
  - SystemCapability.Communication.WiFi.P2P（P2P功能）