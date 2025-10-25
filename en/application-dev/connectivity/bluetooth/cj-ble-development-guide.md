# Broadcasting and Scanning Development Guide

## Introduction

Broadcasting and scanning primarily provide methods for Bluetooth devices to start/stop broadcasting and scanning. Through broadcasting and scanning, peer Bluetooth devices can be discovered to achieve low-power communication.

## Scenarios

Main scenarios include:

- Starting/Stopping broadcasting
- Starting/Stopping scanning

## API Description

For complete Cangjie API documentation and sample code, refer to: [BLE APIs](../../../../en/application-dev/reference/ConnectivityKit/cj-apis-bluetooth-ble.md).

Detailed API descriptions are shown in the following table.

| API Name | Description |
| ---------------------------------- | -----------------------------------------------|
| startBLEScan() | Initiates BLE scanning process. |
| stopBLEScan() | Stops BLE scanning process. |
| startAdvertising() | Starts BLE broadcasting. |
| disableAdvertising() | Temporarily stops BLE broadcasting. |
| enableAdvertising() | Temporarily resumes BLE broadcasting. |
| stopAdvertising() | Stops BLE broadcasting. |
| on(`type`: BluetoothBleCallbackType) | Subscribes to BLE broadcast state changes. |
| off(`type`: BluetoothBleCallbackType) | Unsubscribes from BLE broadcast state changes. |
| on(`type`: BluetoothBleCallbackType) | Subscribes to BLE device discovery events. |
| off(`type`: BluetoothBleCallbackType) | Unsubscribes from BLE device discovery events. |

## Key Scenario Development Steps

### Starting/Stopping Broadcasting

1. Import required BLE modules.
2. Enable device Bluetooth.
3. Requires SystemCapability.Communication.Bluetooth.Core capability.
4. Start broadcasting for peer devices to scan.
5. Stop broadcasting.
6. Sample code:

    <!-- compile -->

    ```cangjie
    import kit.ConnectivityKit.*
    import ohos.callback_invoke.*
    import ohos.business_exception.*

    let TAG: String = 'BleAdvertisingManager'

    class BleAdvertisingManager {
        private var advHandle: UInt32 = 0xFF // default invalid value

        // 1 Subscribe to broadcast state changes
        public func onAdvertisingStateChange() {
            try {
                on(BluetoothBleCallbackType.ADVERTISING_STATE_CHANGE, StateChangeInfoCb())
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 2 Start initial broadcast
        public func startAdvertising() {
            // 2.1 Configure broadcast parameters
            let setting: AdvertiseSetting = AdvertiseSetting(160, 0, true)
            // 2.2 Construct broadcast data
            let manufactureValueBuffer: Array<UInt8> = [1, 2, 3, 4]
            let serviceValueBuffer: Array<UInt8> = [5, 6, 7, 8]
            let manufactureDataUnit: ManufactureData = ManufactureData(4567, manufactureValueBuffer)
            let serviceDataUnit: ServiceData = ServiceData("00001888-0000-1000-8000-00805f9b34fb", serviceValueBuffer)
            let advData: AdvertiseData = AdvertiseData(["00001888-0000-1000-8000-00805f9b34fb"], [manufactureDataUnit],
                [serviceDataUnit], includeDeviceName: false // Optional parameter indicating whether to include device name. Note: Broadcast packet length cannot exceed 31 bytes when including device name.
                )
            let advResponse: AdvertiseData = AdvertiseData(["00001888-0000-1000-8000-00805f9b34fb"], [manufactureDataUnit],
                [serviceDataUnit])
            // 2.3 Construct complete broadcast parameters AdvertisingParams
            let advertisingParams: AdvertisingParams = AdvertisingParams(
                setting,
                advData,
                advResponse,
                duration: 0 // Optional parameter. If >0, broadcasting will temporarily stop after specified duration and can be restarted
            )

            // 2.4 Start initial broadcast and obtain broadcast ID
            try {
                this.onAdvertisingStateChange()
                this.advHandle = startAdvertising(advertisingParams)
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 4 Temporarily stop broadcasting (broadcast resources remain)
        public func disableAdvertising() {
            // 4.1 Construct temporary stop parameters
            let advertisingDisableParams: AdvertisingDisableParams = AdvertisingDisableParams(this.advHandle) // Use broadcast ID obtained during initial broadcast

            // 4.2 Temporarily stop
            try {
                disableAdvertising(advertisingDisableParams)
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 5 Resume broadcasting
        public func enableAdvertising(enableDuration: UInt16) {
            // 5.1 Construct resume parameters
            let advertisingEnableParams: AdvertisingEnableParams = AdvertisingEnableParams(
                this.advHandle, // Use broadcast ID obtained during initial broadcast
                duration: enableDuration
            )
            // 5.2 Resume broadcasting
            try {
                enableAdvertising(advertisingEnableParams)
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 6 Completely stop broadcasting and release resources
        public func stopAdvertising() {
            try {
                stopAdvertising(this.advHandle)
                off(BluetoothBleCallbackType.ADVERTISING_STATE_CHANGE)
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }
    }

    class StateChangeInfoCb <: Callback1Argument<AdvertisingStateChangeInfo> {
        public func invoke(err: ?BusinessException, info: AdvertisingStateChangeInfo): Unit {
            AppLog.info("advertisingId: ${info.advertisingId}, AdvertisingState: ${info.state}")
        }
    }

    let bleAdvertisingManager = BleAdvertisingManager()
    ```

7. For error codes, refer to [Bluetooth Service Subsystem Error Codes](../../../../en/application-dev/reference/ConnectivityKit/cj-errorcode-bluetooth_manager.md).

### Starting/Stopping Scanning

1. Import required BLE modules.
2. Enable device Bluetooth.
3. Requires SystemCapability.Communication.Bluetooth.Core capability.
4. Peer device starts broadcasting.
5. Local device starts scanning and obtains results.
6. Stop scanning.
7. Sample code:

    <!-- compile -->

    ```cangjie
    import kit.ConnectivityKit.*
    import ohos.callback_invoke.*
    import ohos.business_exception.*
    import std.collection.{HashMap, ArrayList}
    import std.math.numeric.BigInt

    const BLE_ADV_TYPE_FLAG = 0x01
    const BLE_ADV_TYPE_16_BIT_SERVICE_UUIDS_INCOMPLETE = 0x02
    const BLE_ADV_TYPE_16_BIT_SERVICE_UUIDS_COMPLETE = 0x03
    const BLE_ADV_TYPE_32_BIT_SERVICE_UUIDS_INCOMPLETE = 0x04
    const BLE_ADV_TYPE_32_BIT_SERVICE_UUIDS_COMPLETE = 0x05
    const BLE_ADV_TYPE_128_BIT_SERVICE_UUIDS_INCOMPLETE = 0x06
    const BLE_ADV_TYPE_128_BIT_SERVICE_UUIDS_COMPLETE = 0x07
    const BLE_ADV_TYPE_LOCAL_NAME_SHORT = 0x08
    const BLE_ADV_TYPE_LOCAL_NAME_COMPLETE = 0x09
    const BLE_ADV_TYPE_TX_POWER_LEVEL = 0x0A
    const BLE_ADV_TYPE_16_BIT_SERVICE_SOLICITATION_UUIDS = 0x14
    const BLE_ADV_TYPE_128_BIT_SERVICE_SOLICITATION_UUIDS = 0x15
    const BLE_ADV_TYPE_32_BIT_SERVICE_SOLICITATION_UUIDS = 0x1F
    const BLE_ADV_TYPE_16_BIT_SERVICE_DATA = 0x16
    const BLE_ADV_TYPE_32_BIT_SERVICE_DATA = 0x20
    const BLE_ADV_TYPE_128_BIT_SERVICE_DATA = 0x21
    const BLE_ADV_TYPE_MANUFACTURER_SPECIFIC_DATA = 0xFF
    const BLUETOOTH_UUID_16_BIT_LENGTH: UInt8 = 2
    const BLUETOOTH_UUID_32_BIT_LENGTH: UInt8 = 4
    const BLUETOOTH_UUID_128_BIT_LENGTH: UInt8 = 16
    const BLUETOOTH_MANUFACTURE_ID_LENGTH: UInt8 = 2

    class BleScanManager {
        // 1 Subscribe to scan results
        public func onScanResult() {
            on(BluetoothBleCallbackType.BLE_DEVICE_FIND, ScanResultCb())
        }

        // 2 Start scanning
        public func startScan() {
            // 2.1 Construct scan filter to match expected broadcast packets
            let manufactureId: UInt16 = 4567
            let manufactureData: Array<UInt8> = [1, 2, 3, 4]
            let manufactureDataMask: Array<UInt8> = [0xFF, 0xFF, 0xFF, 0xFF]
            var scanFilter: ScanFilter = ScanFilter() // Define filter based on actual requirements
            scanFilter.manufactureId = manufactureId
            scanFilter.manufactureData = manufactureData
            scanFilter.manufactureDataMask = manufactureDataMask

            // 2.2 Construct scan parameters
            let scanOptions: ScanOptions = ScanOptions(
                interval: 0,
                dutyMode: ScanDuty.ScanModeLowPower,
                matchMode: MatchMode.MatchModeAggressive,
                phyType: PhyType.PhyLe1M
            )
            try {
                this.onScanResult() // Subscribe to scan results
                startBLEScan([scanFilter], options: scanOptions)
                AppLog.info('startBleScan success')
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }

        // 3 Stop scanning
        public func stopScan() {
            try {
                off(BluetoothBleCallbackType.BLE_DEVICE_FIND) // Unsubscribe from scan results
                stopBLEScan()
                AppLog.info('stopBleScan success')
            } catch (e: BusinessException) {
                AppLog.error('errCode: ${e.code}, errMessage: ' + e.message)
            }
        }
    }

    private func parseScanResult(data: Array<UInt8>) {
        if (data.size == 0) {
            AppLog.warn('nothing, adv data length is 0')
            return
        }
        AppLog.info('data: ' + String.fromUtf8(data))

        var advFlags: UInt8 = 0
        var txPowerLevel: UInt8 = 0
        var localName: String = ""
        var serviceUuids: ArrayList<String> = ArrayList<String>()
        var serviceSolicitationUuids: ArrayList<String> = ArrayList<String>()
        var serviceDatas: HashMap<String, Array<UInt8>> = HashMap()
        var manufactureSpecificDatas: HashMap<UInt16, Array<UInt8>> = HashMap()

        var curPos = 0
        while (curPos < data.size) {
            let length = data[curPos]
            curPos++
            if (length == 0) {
                break
            }
            let dataLength = length - 1
            let dataType = data[curPos]
            curPos++
            match (dataType) {
                case BLE_ADV_TYPE_FLAG => advFlags = data[curPos]
                case BLE_ADV_TYPE_LOCAL_NAME_SHORT => localName = data[curPos..curPos + Int64(dataLength)].toString()
                case BLE_ADV_TYPE_LOCAL_NAME_COMPLETE => localName = data[curPos..curPos + Int64(dataLength)].toString()
                case BLE_ADV_TYPE_TX_POWER_LEVEL => txPowerLevel = data[curPos]
                case BLE_ADV_TYPE_16_BIT_SERVICE_UUIDS_INCOMPLETE => parseServiceUuid(BLUETOOTH_UUID_16_BIT_LENGTH, curPos,
                    dataLength, data, serviceUuids)
                case BLE_ADV_TYPE_16_BIT_SERVICE_UUIDS_COMPLETE => parseServiceUuid(BLUETOOTH_UUID_16_BIT_LENGTH, curPos,
                    dataLength, data, serviceUuids)
                case BLE_ADV_TYPE_32_BIT_SERVICE_UUIDS_INCOMPLETE => parseServiceUuid(BLUETOOTH_UUID_32_BIT_LENGTH, curPos,
                    dataLength, data, serviceUuids)
                case BLE_ADV_TYPE_32_BIT_SERVICE_UUIDS_COMPLETE => parseServiceUuid(BLUETOOTH_UUID_32_BIT_LENGTH, curPos,
                    dataLength, data, serviceUuids)
                case BLE_ADV_TYPE_128_BIT_SERVICE_UUIDS_INCOMPLETE => parseServiceUuid(BLUETOOTH_UUID_128_BIT_LENGTH, curPos,
                    dataLength, data, serviceUuids)
                case BLE_ADV_TYPE_128_BIT_SERVICE_UUIDS_COMPLETE => parseServiceUuid(BLUETOOTH_UUID_128_BIT_LENGTH, curPos,
                    dataLength, data, serviceUuids)
                case BLE_ADV_TYPE_16_BIT_SERVICE_SOLICITATION_UUIDS => parseServiceSolicitationUuid(
                    BLUETOOTH_UUID_16_BIT_LENGTH, curPos, dataLength, data, serviceSolicitationUuids)
                case BLE_ADV_TYPE_32_BIT_SERVICE_SOLICITATION_UUIDS => parseServiceSolicitationUuid(
                    BLUETOOTH_UUID_32_BIT_LENGTH, curPos, dataLength, data, serviceSolicitationUuids)
                case BLE_ADV_TYPE_128_BIT_SERVICE_SOLICITATION_UUIDS => parseServiceSolicitationUuid(
                    BLUETOOTH_UUID_128_BIT_LENGTH, curPos, dataLength, data, serviceSolicitationUuids)
                case BLE_ADV_TYPE_16_BIT_SERVICE_DATA => parseServiceData(BLUETOOTH_UUID_16_BIT_LENGTH, curPos, dataLength,
                    data, serviceDatas)
                case BLE_ADV_TYPE_32_BIT_SERVICE_DATA => parseServiceData(BLUETOOTH_UUID_32_BIT_LENGTH, curPos, dataLength,
                    data, serviceDatas)
                case BLE_ADV_TYPE_128_BIT_SERVICE_DATA => parseServiceData(BLUETOOTH_UUID_128_BIT_LENGTH, curPos, dataLength,
                    data, serviceDatas)
                case BLE_ADV_TYPE_MANUFACTURER_SPECIFIC_DATA => parseManufactureData(curPos, dataLength, data,
                    manufactureSpecificDatas)
                case _ => ()
            }
            curPos += Int64(dataLength)
        }
    }

    private func parseServiceUuid(uuidLength: UInt8, curPos: Int64, dataLength: UInt8, data: Array<UInt8>,
        serviceUuids: ArrayList<String>) {
        var dataLength_ = dataLength
        var curPos_ = curPos
        while (dataLength > 0) {
            let tmpData: Array<UInt8> = data.slice(curPos, Int64(uuidLength))
            serviceUuids.add(getUuidFromArray(Int64(uuidLength), tmpData))
            dataLength_ -= uuidLength
            curPos_ += Int64(uuidLength)
        }
    }

    private func parseServiceSolicitationUuid(uuidLength: UInt8, curPos: Int64, dataLength: UInt8, data: Array<UInt8>,
        serviceSolicitationUuids: ArrayList<String>) {
        var dataLength_ = dataLength
        var curPos_ = curPos
        while (dataLength > 0) {
            let tmpData: Array<UInt8> = data.slice(curPos, Int64(uuidLength))
            serviceSolicitationUuids.add(getUuidFromArray(Int64(uuidLength), tmpData))
            dataLength_ -= uuidLength
            curPos_ += Int64(uuidLength)
        }
    }

    private func getUuidFromArray(uuidLength: Int64, uuidData: Array<UInt8>): String {
        var uuid = ""
        var temp: String = ""
        for (i in uuidLength - 1..-1 : -1) {
            temp = temp + BigInt
                .parse(uuidData[i].toString())
                .toString(radix: 16)
                .padStart(2, padding: "0")
        }
        match (uuidLength) {
            case BLUETOOTH_UUID_16_BIT_LENGTH => uuid = "0000${temp}-0000-1000-8000-00805F9B34FB"
            case BLUETOOTH_UUID_32_BIT_LENGTH => uuid = "${temp}-0000-1000-8000-00805F9B34FB"
            case BLUETOOTH_UUID_128_BIT_LENGTH => uuid = "${temp[0..8]}-${temp[8..12]}-${temp[12..16]}-${temp[16..20]}-${temp[20..32]}"
            case _ => ()
        }
        return uuid
    }

    private func parseServiceData(uuidLength: UInt8, curPos: Int64, dataLength: UInt8, data: Array<UInt8>,
        serviceDatas: HashMap<String, Array<UInt8>>) {
        let tmpUuid: Array<UInt8> = data.slice(curPos, Int64(uuidLength))
        let tmpValue: Array<UInt8> = data.slice(curPos + Int64(uuidLength), Int64(dataLength - uuidLength))
        serviceDatas[tmpUuid.toString()] = tmpValue
    }

    private func parseManufactureData(curPos: Int64, dataLength: UInt8, data: Array<UInt8>,
        manufactureSpecificDatas: HashMap<UInt16, Array<UInt8>>) {
        let manufactureId: UInt16 = UInt16(data[curPos + 1]) << 8 + UInt16(data[curPos])
        let tmpValue: Array<UInt8> = data.slice(curPos + Int64(BLUETOOTH_MANUFACTURE_ID_LENGTH),
            Int64(dataLength - BLUETOOTH_MANUFACTURE_ID_LENGTH))
        manufactureSpecificDatas[manufactureId] = tmpValue
    }

    class ScanResultCb <: Callback1Argument<Array<ScanResult>> {
        public func invoke(err: ?BusinessException, data: Array<ScanResult>): Unit {
            if (data.size > 0) {
                AppLog.info('BLE scan result = ' + data[0].deviceId)
                parseScanResult(data[0].data)
            }
        }
    }

    let bleScanManager = BleScanManager()
    ```

8. For error codes, please refer to [Bluetooth Service Subsystem Error Codes](../../../../en/application-dev/reference/ConnectivityKit/cj-errorcode-bluetooth_manager.md).
