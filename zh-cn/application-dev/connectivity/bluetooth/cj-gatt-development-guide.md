# 通用属性协议开发指导

## 简介

通用属性协议是GATT（Generic Attribute）的缩写，它是一种用于在蓝牙低功耗设备之间传输数据的协议，定义了一套通用的属性和服务框架。通过GATT协议，蓝牙设备可以向其他设备提供服务，也可以从其他设备获取服务。

## 场景介绍

主要场景有：

- 连接server端读取和写入信息。
- server端操作services和通知客户端信息。

## 接口说明

完整的仓颉 API 说明以及实例代码请参见：[GATT 接口](../../../../zh-cn/application-dev/reference/ConnectivityKit/cj-apis-bluetooth-ble.md)。

具体接口说明如下表。

| 接口名 | 功能描述 |
| ------------------------------------------ | ----------------------------------------------------------- |
| connect() | client端发起连接远端蓝牙低功耗设备。 |
| disconnect() | client端断开与远端蓝牙低功耗设备的连接。 |
| close() | 关闭客户端功能，注销client在协议栈的注册，调用该接口后GattClientDevice实例将不能再使用。|
| getDeviceName() | client获取远端蓝牙低功耗设备名。 |
| getServices() | client端获取蓝牙低功耗设备的所有服务，即服务发现 。 |
| readCharacteristicValue() | client端读取蓝牙低功耗设备特定服务的特征值。 |
| readDescriptorValue() | client端读取蓝牙低功耗设备特定的特征包含的描述符。 |
| writeCharacteristicValue() | client端向低功耗蓝牙设备写入特定的特征值。 |
| writeDescriptorValue() | client端向低功耗蓝牙设备特定的描述符写入二进制数据。 |
| getRssiValue() | client获取远端蓝牙低功耗设备的信号强度 (Received Signal Strength Indication, RSSI)，调用connect接口连接成功后才能使用。|
| setBLEMtuSize() | client协商远端蓝牙低功耗设备的最大传输单元（Maximum Transmission Unit, MTU），调用connect接口连接成功后才能使用。|
| setCharacteristicChangeNotification() | 向服务端发送设置通知此特征值请求。 |
| setCharacteristicChangeIndication() | 向服务端发送设置通知此特征值请求。 |
| on(`type`: BluetoothBleGattClientDeviceCallbackType) | 订阅蓝牙低功耗设备的特征值变化事件。需要先调用setNotifyCharacteristicChanged接口才能接收server端的通知。|
| off(`type`: BluetoothBleGattClientDeviceCallbackType) | 取消订阅蓝牙低功耗设备的特征值变化事件。  |
| on(`type`: BluetoothBleGattClientDeviceCallbackType) | client端订阅蓝牙低功耗设备的连接状态变化事件。 |
| off(`type`: BluetoothBleGattClientDeviceCallbackType) | 取消订阅蓝牙低功耗设备的连接状态变化事件。 |
| on(`type`: BluetoothBleGattClientDeviceCallbackType) | client端订阅MTU状态变化事件。 |
| off(`type`: BluetoothBleGattClientDeviceCallbackType) | client端取消订阅MTU状态变化事件。 |
| addService() | server端添加服务。 |
| removeService() | 删除已添加的服务。 |
| close() | 关闭服务端功能，去注销server在协议栈的注册，调用该接口后GattServer实例将不能再使用。 |
| notifyCharacteristicChanged() | server端特征值发生变化时，主动通知已连接的client设备。 |
| sendResponse() | server端回复client端的读写请求。 |
| on(`type`: BluetoothBleGattServerCallbackType) | server端订阅特征值读请求事件。 |
| off(`type`: BluetoothBleGattServerCallbackType) | server端取消订阅特征值读请求事件。 |
| on(`type`: BluetoothBleGattServerCallbackType) | server端订阅特征值写请求事件。 |
| off(`type`: BluetoothBleGattServerCallbackType) | server端取消订阅特征值写请求事件。 |
| on(`type`: BluetoothBleGattServerCallbackType) | server端订阅描述符读请求事件。 |
| off(`type`: BluetoothBleGattServerCallbackType) | server端取消订阅描述符读请求事件。 |
| on(`type`: BluetoothBleGattServerCallbackType) | server端订阅描述符写请求事件。 |
| off(`type`: BluetoothBleGattServerCallbackType) | server端取消订阅描述符写请求事件。 |
| on(`type`: BluetoothBleGattServerCallbackType) | server端订阅BLE连接状态变化事件。 |
| off(`type`: BluetoothBleGattServerCallbackType) | server端取消订阅BLE连接状态变化事件。 |
| on(`type`: BluetoothBleGattServerCallbackType) | server端订阅MTU状态变化事件。 |
| off(`type`: BluetoothBleGattServerCallbackType) | server端取消订阅MTU状态变化事件。 |

## 主要场景开发步骤

### 连接server端读取和写入信息

1. import需要的ble模块。
2. 创建gattClient实例对象。
3. 连接gattServer。
4. 读取gattServer的特征值和描述符。
5. 向gattServer写入特征值和描述符。
6. 断开连接，销毁gattClient实例。
7. 示例代码:

    <!-- compile -->

    ```cangjie
    import kit.ConnectivityKit.*
    import ohos.base.{BusinessException,Callback1Argument}

    const TAG: String = 'GattClientManager'

    class GattClientManager {
        var device: ?String = None
        var gattClient: ?GattClientDevice = None
        let connectState: ProfileConnectionState = ProfileConnectionState.StateDisconnected
        let myServiceUuid: String = '00001810-0000-1000-8000-00805F9B34FB'
        let myCharacteristicUuid: String = '00001820-0000-1000-8000-00805F9B34FB'
        let myFirstDescriptorUuid: String = '00002902-0000-1000-8000-00805F9B34FB' // 2902一般用于notification或者indication
        let mySecondDescriptorUuid: String = '00002903-0000-1000-8000-00805F9B34FB'
        var found: Bool = false

        // 构造BLEDescriptor
        private func initDescriptor(des: String, value: Array<Byte>): BLEDescriptor {
            let descriptor: BLEDescriptor = BLEDescriptor(
                this.myServiceUuid,
                this.myCharacteristicUuid,
                des,
                value
            )
            return descriptor
        }

        // 构造BLECharacteristic
        private func initCharacteristic(): BLECharacteristic {
            let descValue: Array<UInt8> = [11, 12]
            let descriptors: Array<BLEDescriptor> = [initDescriptor(this.myFirstDescriptorUuid, [0, 0]), initDescriptor(this.mySecondDescriptorUuid, descValue)]
            let charValue: Array<UInt8> = [1, 2]
            let characteristic: BLECharacteristic = BLECharacteristic(
                this.myServiceUuid,
                this.myCharacteristicUuid,
                charValue,
                descriptors,
                GattProperties()
            )
            return characteristic
        }

        private func logCharacteristic(char: BLECharacteristic) {
            var message = 'logCharacteristic uuid:' + char.characteristicUuid + '\n'
            let value = char.characteristicValue
            message += 'logCharacteristic value: '
            for (i in 0..value.size) {
                message += value[i].toString() + ' '
            }
            AppLog.info(message)
        }

        private func logDescriptor(des: BLEDescriptor) {
            var message = 'logDescriptor uuid:' + des.descriptorUuid + '\n'
            let value = des.descriptorValue
            message += 'logDescriptor value: '
            for (i in 0..value.size) {
                message += value[i].toString() + ' '
            }
            AppLog.info(message)
        }

        private func checkService(services: Array<GattService>): Bool {
            for (i in 0..services.size) {
                if (services[i].serviceUuid != this.myServiceUuid) {
                    continue
                }
                for (j in 0..services[i].characteristics.size) {
                    if (services[i].characteristics[j].characteristicUuid != this.myCharacteristicUuid) {
                        continue
                    }
                    for (k in 0..services[i].characteristics[j].descriptors.size) {
                        if (services[i].characteristics[j].descriptors[k].descriptorUuid == this.myFirstDescriptorUuid) {
                            AppLog.info('find expected service from server')
                            return true
                        }
                    }
                }
            }
            AppLog.error('no expected service from server')
            return false
        }

        // 1. 订阅连接状态变化事件
        public func onGattClientStateChange() {
            if (this.gattClient.isNone()) {
                AppLog.error('no gattClient')
                return
            }
            try {
                this.gattClient?.on(BluetoothBleGattClientDeviceCallbackType.BLE_CONNECTION_STATE_CHANGE, ChangeStateCb())
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 2. client端主动连接时调用
        public func startConnect(peerDevice: String) { // 对端设备一般通过ble scan获取到
            if (this.connectState != ProfileConnectionState.StateDisconnected) {
                AppLog.error('startConnect failed')
                return
            }
            AppLog.info('startConnect ' + peerDevice)
            this.device = peerDevice
            // 2.1 使用device构造gattClient，后续的交互都需要使用该实例
            this.gattClient = createGattClientDevice(peerDevice)
            try {
                this.onGattClientStateChange() // 2.2 订阅连接状态
                this.gattClient?.connect() // 2.3 发起连接
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 3. client端连接成功后，需要进行服务发现
        public func discoverServices() {
            if (this.gattClient.isNone()) {
                AppLog.info('no gattClient')
                return
            }
            AppLog.info('discoverServices')
            try {
                let result = this.gattClient?.getServices()
                this.found = this.checkService(result.getOrThrow()) // 要确保server端的服务内容有业务所需要的服务
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 4. 在确保拿到了server端的服务结果后，读取server端特定服务的特征值时调用
        public func readCharacteristicValue() {
            if (this.gattClient.isNone() || this.connectState != ProfileConnectionState.STATE_CONNECTED) {
                AppLog.error('no gattClient or not connected')
                return
            }
            if (!this.found) { // 要确保server端有对应的characteristic
                AppLog.error('no characteristic from server')
                return
            }

            let characteristic = this.initCharacteristic()
            AppLog.info('readCharacteristicValue')
            try {
                this.gattClient?.readCharacteristicValue(characteristic) {
                        e, outData => this.logCharacteristic(outData.getOrThrow())
                    }
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 5. 在确保拿到了server端的服务结果后，写入server端特定服务的特征值时调用
        public func writeCharacteristicValue() {
            if (this.gattClient.isNone() || this.connectState != ProfileConnectionState.STATE_CONNECTED) {
                AppLog.error('no gattClient or not connected')
                return
            }
            if (!this.found) { // 要确保server端有对应的characteristic
                AppLog.error('no characteristic from server')
                return
            }

            let characteristic = this.initCharacteristic()
            AppLog.info('writeCharacteristicValue')
            try {
                this.gattClient?.writeCharacteristicValue(characteristic, GattWriteType.WRITE) {
                        err =>
                        if (let Some(e) <- err) {
                            AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
                            return
                        }
                        AppLog.info('writeCharacteristicValue success')
                    }
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 6. 在确保拿到了server端的服务结果后，读取server端特定服务的描述符时调用
        public func readDescriptorValue() {
            if (this.gattClient.isNone() || this.connectState != ProfileConnectionState.STATE_CONNECTED) {
                AppLog.error('no gattClient or not connected')
                return
            }
            if (!this.found) { // 要确保server端有对应的descriptor
                AppLog.error('no descriptor from server')
                return
            }

            let descBuffer = Array<Byte>()
            let descriptor = this.initDescriptor(this.mySecondDescriptorUuid, descBuffer)
            AppLog.info('readDescriptorValue')
            try {
                this.gattClient?.readDescriptorValue(descriptor) {
                    e, outData => this.logDescriptor(outData.getOrThrow())
                }
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 7. 在确保拿到了server端的服务结果后，写入server端特定服务的描述符时调用
        public func writeDescriptorValue() {
            if (this.gattClient.isNone() || this.connectState != ProfileConnectionState.STATE_CONNECTED) {
                AppLog.error('no gattClient or not connected')
                return
            }
            if (!this.found) { // 要确保server端有对应的descriptor
                AppLog.error('no descriptor from server')
                return
            }

            let descBuffer: Array<UInt8> = [11, 12]
            let descriptor = this.initDescriptor(this.mySecondDescriptorUuid, descBuffer)
            AppLog.info('writeDescriptorValue')
            try {
                this.gattClient?.writeDescriptorValue(descriptor) {
                        err =>
                        if (let Some(e) <- err) {
                            AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
                            return
                        }
                        AppLog.info('writeDescriptorValue success')
                    }
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 8.client端主动断开时调用
        public func stopConnect() {
            if (this.gattClient.isNone() || this.connectState != ProfileConnectionState.STATE_CONNECTED) {
                AppLog.error('no gattClient or not connected')
                return
            }

            AppLog.info('stopConnect ' + this.device.getOrThrow())
            try {
                this.gattClient?.disconnect() // 8.1 断开连接
                this.gattClient?.off(BluetoothBleGattClientDeviceCallbackType.BLE_CONNECTION_STATE_CHANGE)
                this.gattClient?.close() // 8.2 如果不再使用此gattClient，则需要close
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }
    }

    class ChangeStateCb <: Callback1Argument<BLEConnectionChangeState> {
        public func invoke(stateInfo: BLEConnectionChangeState) {
            let state = match (stateInfo.state) {
                case STATE_DISCONNECTED => 'DISCONNECTED'

                case STATE_CONNECTING => 'CONNECTING'

                case STATE_CONNECTED => 'CONNECTED'

                case STATE_DISCONNECTING => 'DISCONNECTING'

                case _ => 'undefined'
            }
            AppLog.info('onGattClientStateChange: device=' + stateInfo.deviceId + ', state=' + state)
        }
    }

    let gattClientManager = GattClientManager()
    ```

8. 错误码请参见[蓝牙服务子系统错误码](../../../../zh-cn/application-dev/reference/ConnectivityKit/cj-errorcode-bluetooth_manager.md)。

### server端操作services和通知客户端信息

1. import需要的ble模块。
2. 创建gattServer实例对象。
3. 添加services信息。
4. 当向gattServer写入特征值通知gattClient。
5. 移除services信息。
6. 注销gattServer实例。
7. 示例代码:

    <!-- compile -->

    ```cangjie
    import kit.ConnectivityKit.*
    import ohos.base.{BusinessException,Callback1Argument}
    import std.collection.ArrayList

    const TAG: String = 'GattServerManager'

    class GattServerManager {
        public var gattServer: ?GattServer = None
        let connectState: ProfileConnectionState = ProfileConnectionState.STATE_DISCONNECTED
        let myServiceUuid: String = '00001810-0000-1000-8000-00805F9B34FB'
        let myCharacteristicUuid: String = '00001820-0000-1000-8000-00805F9B34FB'
        let myFirstDescriptorUuid: String = '00002902-0000-1000-8000-00805F9B34FB' // 2902一般用于notification或者indication
        let mySecondDescriptorUuid: String = '00002903-0000-1000-8000-00805F9B34FB'

        // 构造BLEDescriptor
        private func initDescriptor(des: String, value: Array<Byte>): BLEDescriptor {
            let descriptor: BLEDescriptor = BLEDescriptor(
                this.myServiceUuid,
                this.myCharacteristicUuid,
                des,
                value
            )
            return descriptor
        }

        // 构造BLECharacteristic
        private func initCharacteristic(): BLECharacteristic {
            let descValue: Array<UInt8> = [31, 32]
            let descriptors: Array<BLEDescriptor> = [initDescriptor(this.myFirstDescriptorUuid, [0, 0]),
                initDescriptor(this.mySecondDescriptorUuid, descValue)]
            let charValue: Array<UInt8> = [21, 22]
            let characteristic: BLECharacteristic = BLECharacteristic(
                this.myServiceUuid,
                this.myCharacteristicUuid,
                charValue,
                descriptors,
                GattProperties()
            )
            return characteristic
        }

        // 1. 订阅连接状态变化事件
        public func onGattServerStateChange() {
            if (this.gattServer.isNone()) {
                AppLog.error('no gattServer')
                return
            }
            try {
                this.gattServer?.on(BluetoothBleGattServerCallbackType.CONNECTION_STATE_CHANGE, ChangeStateCb())
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 2. server端注册服务时调用
        public func registerServer(peerDevice: String) { // 对端设备一般通过ble scan获取到
            let characteristics: ArrayList<BLECharacteristic> = ArrayList<BLECharacteristic>()
            let characteristic = this.initCharacteristic()
            characteristics.add(characteristic)
            let gattService: GattService = GattService(
                this.myServiceUuid,
                true,
                characteristics.toArray(),
                Array<GattService>()
            )
            AppLog.info('registerServer ' + this.myServiceUuid)
            try {
                this.gattServer = createGattServer() // 2.1 构造gattServer，后续的交互都需要使用该实例
                this.onGattServerStateChange() // 2.2 订阅连接状态
                this.gattServer?.addService(gattService)
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 3. 订阅来自gattClient的读取特征值请求时调用
        public func onCharacteristicRead() {
            if (this.gattServer.isNone()) {
                AppLog.info('no gattServer')
                return
            }
            AppLog.info('onCharacteristicRead')
            try {
                this.gattServer?.on(BluetoothBleGattServerCallbackType.CHARACTERISTIC_READ, ReadRequestCb())
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 4. 订阅来自gattClient的写入特征值请求时调用
        public func onCharacteristicWrite() {
            if (this.gattServer.isNone()) {
                AppLog.error('no gattServer')
                return
            }

            AppLog.info('onCharacteristicWrite')
            try {
                this.gattServer?.on(BluetoothBleGattServerCallbackType.CHARACTERISTIC_WRITE, WriteRequestCb())
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 5. 订阅来自gattClient的读取描述符请求时调用
        public func onDescriptorRead() {
            if (this.gattServer.isNone()) {
                AppLog.error('no gattServer')
                return
            }

            AppLog.info('onDescriptorRead')
            try {
                this.gattServer?.on(BluetoothBleGattServerCallbackType.DESCRIPTOR_READ, DescriptorReadRequestCb())
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 6. 订阅来自gattClient的写入描述符请求时调用
        public func onDescriptorWrite() {
            if (this.gattServer.isNone()) {
                AppLog.error('no gattServer')
                return
            }

            AppLog.info('onDescriptorWrite')
            try {
                this.gattServer?.on(BluetoothBleGattServerCallbackType.DESCRIPTOR_WRITE, DescriptorWriteRequestCb())
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 7. server端删除服务，不再使用时调用
        public func unRegisterServer() {
            if (this.gattServer.isNone()) {
                AppLog.error('no gattServer')
                return
            }

            AppLog.info('unRegisterServer ' + this.myServiceUuid)
            try {
                this.gattServer?.removeService(this.myServiceUuid) // 7.1 删除服务
                this.gattServer?.off(BluetoothBleGattServerCallbackType.CONNECTION_STATE_CHANGE)
                this.gattServer?.close() // 7.3 如果不再使用此gattServer，则需要close
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }
    }

    class ChangeStateCb <: Callback1Argument<BLEConnectionChangeState> {
        public func invoke(stateInfo: BLEConnectionChangeState) {
            let state = match (stateInfo.state) {
                case STATE_DISCONNECTED => 'DISCONNECTED'
                case STATE_CONNECTING => 'CONNECTING'
                case STATE_CONNECTED => 'CONNECTED'
                case STATE_DISCONNECTING => 'DISCONNECTING'
                case _ => 'undefined'
            }
            AppLog.info('onGattClientStateChange: device=' + stateInfo.deviceId + ', state=' + state)
        }
    }

    let gattServerManager = GattServerManager()

    class ReadRequestCb <: Callback1Argument<CharacteristicReadRequest> {
        public func invoke(charReq: CharacteristicReadRequest): Unit {
            let deviceId: String = charReq.deviceId
            let transId: Int32 = charReq.transId
            let offset: Int32 = charReq.offset
            AppLog.info('receive characteristicRead')
            let rspBuffer: Array<UInt8> = [21, 22]
            let serverResponse: ServerResponse = ServerResponse(
                deviceId,
                transId,
                0, // 0表示成功
                offset,
                rspBuffer
            )

            try {
                gattServerManager.gattServer?.sendResponse(serverResponse)
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }
    }

    class WriteRequestCb <: Callback1Argument<CharacteristicWriteRequest> {
        public func invoke(charReq: CharacteristicWriteRequest): Unit {
            let deviceId: String = charReq.deviceId
            let transId: Int32 = charReq.transId
            let offset: Int32 = charReq.offset
            AppLog.info('receive characteristicWrite: needRsp=${charReq.needRsp}')
            if (!charReq.needRsp) {
                return
            }
            let rspBuffer: Array<UInt8> = [0]
            let serverResponse: ServerResponse = ServerResponse(
                deviceId,
                transId,
                0, // 0表示成功
                offset,
                rspBuffer
            )

            try {
                gattServerManager.gattServer?.sendResponse(serverResponse)
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }
    }

    class DescriptorReadRequestCb <: Callback1Argument<DescriptorReadRequest> {
        public func invoke(desReq: DescriptorReadRequest): Unit {
            let deviceId: String = desReq.deviceId
            let transId: Int32 = desReq.transId
            let offset: Int32 = desReq.offset
            AppLog.info('receive descriptorRead')
            let rspBuffer: Array<UInt8> = [31, 32]
            let serverResponse: ServerResponse = ServerResponse(
                deviceId,
                transId,
                0, // 0表示成功
                offset,
                rspBuffer
            )

            try {
                gattServerManager.gattServer?.sendResponse(serverResponse)
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }
    }

    class DescriptorWriteRequestCb <: Callback1Argument<DescriptorWriteRequest> {
        public func invoke(desReq: DescriptorWriteRequest): Unit {
            let deviceId: String = desReq.deviceId
            let transId: Int32 = desReq.transId
            let offset: Int32 = desReq.offset
            AppLog.info('receive descriptorWrite: needRsp=${desReq.needRsp}')
            if (!desReq.needRsp) {
                return
            }
            let rspBuffer: Array<UInt8> = [0]
            let serverResponse: ServerResponse = ServerResponse(
                deviceId,
                transId,
                0, // 0表示成功
                offset,
                rspBuffer
            )

            try {
                gattServerManager.gattServer?.sendResponse(serverResponse)
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }
    }
    ```

8. 错误码请参见[蓝牙服务子系统错误码](../../../../zh-cn/application-dev/reference/ConnectivityKit/cj-errorcode-bluetooth_manager.md)。
