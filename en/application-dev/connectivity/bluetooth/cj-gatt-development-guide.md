# Generic Attribute Protocol (GATT) Development Guide

## Introduction

The Generic Attribute Protocol (GATT) is an abbreviation for Generic Attribute, which is a protocol used for data transmission between Bluetooth Low Energy (BLE) devices. It defines a universal framework of attributes and services. Through the GATT protocol, Bluetooth devices can provide services to other devices or obtain services from other devices.

## Scenarios

Main scenarios include:

- Connecting to the server to read and write information.
- Server operations on services and notifying client information.

## Interface Description

For complete Cangjie API documentation and sample code, please refer to: [GATT Interface](../../../../en/application-dev/reference/ConnectivityKit/cj-apis-bluetooth-ble.md).

Detailed interface descriptions are shown in the following table.

| Interface Name | Function Description |
| ------------------------------------------ | ----------------------------------------------------------- |
| connect() | Client initiates connection to remote BLE device. |
| disconnect() | Client disconnects from remote BLE device. |
| close() | Closes client functionality, deregisters client from protocol stack. The GattClientDevice instance becomes unusable after calling this interface. |
| getDeviceName() | Client retrieves the name of remote BLE device. |
| getServices() | Client discovers all services of BLE device (service discovery). |
| readCharacteristicValue() | Client reads characteristic value of specific service from BLE device. |
| readDescriptorValue() | Client reads descriptor contained in specific characteristic of BLE device. |
| writeCharacteristicValue() | Client writes specific characteristic value to BLE device. |
| writeDescriptorValue() | Client writes binary data to specific descriptor of BLE device. |
| getRssiValue() | Client retrieves signal strength (RSSI) of remote BLE device. Must be called after successful connection via connect(). |
| setBLEMtuSize() | Client negotiates Maximum Transmission Unit (MTU) with remote BLE device. Must be called after successful connection via connect(). |
| setCharacteristicChangeNotification() | Sends request to server to enable notifications for characteristic value changes. |
| setCharacteristicChangeIndication() | Sends request to server to enable indications for characteristic value changes. |
| on(`type`: BluetoothBleGattClientDeviceCallbackType, Callback1Argument<BLECharacteristic>) | Subscribes to characteristic value change events of BLE device. Requires calling setNotifyCharacteristicChanged first to receive notifications from server. |
| off(`type`: BluetoothBleGattClientDeviceCallbackType, ?CallbackObject = None) | Unsubscribes from characteristic value change events of BLE device. |
| on(`type`: BluetoothBleGattClientDeviceCallbackType, Callback1Argument<BLEConnectionChangeStage>) | Client subscribes to connection state change events of BLE device. |
| off(`type`: BluetoothBleGattClientDeviceCallbackType, ?CallbackObject = None) | Unsubscribes from connection state change events of BLE device. |
| on(`type`: BluetoothBleGattClientDeviceCallbackType, Callback1Argument<Int32>) | Client subscribes to MTU state change events. |
| off(`type`: BluetoothBleGattClientDeviceCallbackType, ?CallbackObject = None) | Client unsubscribes from MTU state change events. |
| addService() | Server adds service. |
| removeService() | Removes added service. |
| close() | Closes server functionality, deregisters server from protocol stack. The GattServer instance becomes unusable after calling this interface. |
| notifyCharacteristicChanged() | Server actively notifies connected clients when characteristic value changes. |
| sendResponse() | Server responds to client's read/write requests. |
| on(`type`: BluetoothBleGattServerCallbackType, Callback1Argument<CharacteristicReadRequest>) | Server subscribes to characteristic read request events. |
| off(`type`: BluetoothBleGattServerCallbackType, ?CallbackObject = None) | Server unsubscribes from characteristic read request events. |
| on(`type`: BluetoothBleGattServerCallbackType, Callback1Argument<CharacteristicWriteRequest>) | Server subscribes to characteristic write request events. |
| off(`type`: BluetoothBleGattServerCallbackType, ?CallbackObject = None) | Server unsubscribes from characteristic write request events. |
| on(`type`: BluetoothBleGattServerCallbackType, Callback1Argument<DescriptorReadRequest>) | Server subscribes to descriptor read request events. |
| off(`type`: BluetoothBleGattServerCallbackType, ?CallbackObject = None) | Server unsubscribes from descriptor read request events. |
| on(`type`: BluetoothBleGattServerCallbackType, Callback1Argument<DescriptorWriteRequest>) | Server subscribes to descriptor write request events. |
| off(`type`: BluetoothBleGattServerCallbackType, ?CallbackObject = None) | Server unsubscribes from descriptor write request events. |
| on(`type`: BluetoothBleGattServerCallbackType, callback1Argument<BLEConnectionChangeState>) | Server subscribes to BLE connection state change events. |
| off(`type`: BluetoothBleGattServerCallbackType, ?CallbackObject = None) | Server unsubscribes from BLE connection state change events. |
| on(`type`: BluetoothBleGattServerCallbackType, Callback1Argument<Int32>) | Server subscribes to MTU state change events. |
| off(`type`: BluetoothBleGattServerCallbackType, ?CallbackObject = None) | Server unsubscribes from MTU state change events. |

## Development Steps for Main Scenarios

### Connecting to Server to Read and Write Information

1. Import required BLE modules.
2. Create gattClient instance object.
3. Connect to gattServer.
4. Read characteristic values and descriptors from gattServer.
5. Write characteristic values and descriptors to gattServer.
6. Disconnect and destroy gattClient instance.
7. Sample code:

    <!-- compile -->

    ```cangjie
    import kit.ConnectivityKit.*
    import ohos.base.{BusinessException,Callback1Argument}

    const TAG: String = 'GattClientManager'

    class GattClientManager {
        var device: ?String = None
        var gattClient: ?GattClientDevice = None
        let connectState: ProfileConnectionState = ProfileConnectionState.STATE_DISCONNECTED
        let myServiceUuid: String = '00001810-0000-1000-8000-00805F9B34FB'
        let myCharacteristicUuid: String = '00001820-0000-1000-8000-00805F9B34FB'
        let myFirstDescriptorUuid: String = '00002902-0000-1000-8000-00805F9B34FB' // 2902 is typically used for notification or indication
        let mySecondDescriptorUuid: String = '00002903-0000-1000-8000-00805F9B34FB'
        var found: Bool = false

        // Construct BLEDescriptor
        private func initDescriptor(des: String, value: Array<Byte>): BLEDescriptor {
            let descriptor: BLEDescriptor = BLEDescriptor(
                this.myServiceUuid,
                this.myCharacteristicUuid,
                des,
                value
            )
            return descriptor
        }

        // Construct BLECharacteristic
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

        // 1. Subscribe to connection state change events
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

        // 2. Called when client actively connects
        public func startConnect(peerDevice: String) { // Peer device is typically obtained through BLE scan
            if (this.connectState != ProfileConnectionState.STATE_DISCONNECTED) {
                AppLog.error('startConnect failed')
                return
            }
            AppLog.info('startConnect ' + peerDevice)
            this.device = peerDevice
            // 2.1 Create gattClient using device, all subsequent interactions require this instance
            this.gattClient = createGattClientDevice(peerDevice)
            try {
                this.onGattClientStateChange() // 2.2 Subscribe to connection state
                this.gattClient?.connect() // 2.3 Initiate connection
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 3. After successful connection, client needs to perform service discovery
        public func discoverServices() {
            if (this.gattClient.isNone()) {
                AppLog.info('no gattClient')
                return
            }
            AppLog.info('discoverServices')
            try {
                let result = this.gattClient?.getServices()
                this.found = this.checkService(result.getOrThrow()) // Ensure server has required services
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 4. Called to read characteristic value from server after confirming service availability
        public func readCharacteristicValue() {
            if (this.gattClient.isNone() || this.connectState != ProfileConnectionState.STATE_CONNECTED) {
                AppLog.error('no gattClient or not connected')
                return
            }
            if (!this.found) { // Ensure server has corresponding characteristic
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

        // 5. Called to write characteristic value to server after confirming service availability
        public func writeCharacteristicValue() {
            if (this.gattClient.isNone() || this.connectState != ProfileConnectionState.STATE_CONNECTED) {
                AppLog.error('no gattClient or not connected')
                return
            }
            if (!this.found) { // Ensure server has corresponding characteristic
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

        // 6. Called to read descriptor from server after confirming service availability
        public func readDescriptorValue() {
            if (this.gattClient.isNone() || this.connectState != ProfileConnectionState.STATE_CONNECTED) {
                AppLog.error('no gattClient or not connected')
                return
            }
            if (!this.found) { // Ensure server has corresponding descriptor
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

        // 7. Called to write descriptor to server after confirming service availability
        public func writeDescriptorValue() {
            if (this.gattClient.isNone() || this.connectState != ProfileConnectionState.STATE_CONNECTED) {
                AppLog.error('no gattClient or not connected')
                return
            }
            if (!this.found) { // Ensure server has corresponding descriptor
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
        // 8. Called when the client actively disconnects
        public func stopConnect() {
            if (this.gattClient.isNone() || this.connectState != ProfileConnectionState.STATE_CONNECTED) {
                AppLog.error('no gattClient or not connected')
                return
            }

            AppLog.info('stopConnect ' + this.device.getOrThrow())
            try {
                this.gattClient?.disconnect() // 8.1 Disconnect
                this.gattClient?.off(BluetoothBleGattClientDeviceCallbackType.BLE_CONNECTION_STATE_CHANGE)
                this.gattClient?.close() // 8.2 Close the gattClient if no longer in use
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

8. For error codes, please refer to [Bluetooth Service Subsystem Error Codes](../../../../en/application-dev/reference/ConnectivityKit/cj-errorcode-bluetooth_manager.md).

### Server-Side Operations on Services and Notifying Clients

1. Import required BLE modules.
2. Create a gattServer instance object.
3. Add service information.
4. Notify the gattClient when writing characteristic values to the gattServer.
5. Remove service information.
6. Deregister the gattServer instance.
7. Example code:

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
        let myFirstDescriptorUuid: String = '00002902-0000-1000-8000-00805F9B34FB' // 2902 is typically used for notification or indication
        let mySecondDescriptorUuid: String = '00002903-0000-1000-8000-00805F9B34FB'

        // Construct BLEDescriptor
        private func initDescriptor(des: String, value: Array<Byte>): BLEDescriptor {
            let descriptor: BLEDescriptor = BLEDescriptor(
                this.myServiceUuid,
                this.myCharacteristicUuid,
                des,
                value
            )
            return descriptor
        }

        // Construct BLECharacteristic
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

        // 1. Subscribe to connection state change events
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

        // 2. Called when the server registers a service
        public func registerServer(peerDevice: String) { // Peer device is typically obtained via BLE scan
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
                this.gattServer = createGattServer() // 2.1 Create gattServer instance for subsequent interactions
                this.onGattServerStateChange() // 2.2 Subscribe to connection state
                this.gattServer?.addService(gattService)
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 3. Called when subscribing to read characteristic value requests from gattClient
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

        // 4. Called when subscribing to write characteristic value requests from gattClient
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

        // 5. Called when subscribing to read descriptor requests from gattClient
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

        // 6. Called when subscribing to write descriptor requests from gattClient
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

        // 7. Called when the server removes a service and no longer uses it
        public func unRegisterServer() {
            if (this.gattServer.isNone()) {
                AppLog.error('no gattServer')
                return
            }

            AppLog.info('unRegisterServer ' + this.myServiceUuid)
            try {
                this.gattServer?.removeService(this.myServiceUuid) // 7.1 Remove service
                this.gattServer?.off(BluetoothBleGattServerCallbackType.CONNECTION_STATE_CHANGE)
                this.gattServer?.close() // 7.3 Close the gattServer if no longer in use
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
                0, // 0 indicates success
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
                0, // 0 indicates success
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
                0, // 0 indicates success
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
                0, // 0 indicates success
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

8. For error codes, please refer to [Bluetooth Service Subsystem Error Codes](../../../../en/application-dev/reference/ConnectivityKit/cj-errorcode-bluetooth_manager.md).
