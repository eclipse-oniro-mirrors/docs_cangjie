# Overview of Bluetooth Service Development

## Overview

Bluetooth technology is a wireless communication technology that enables data transmission over short distances. It was proposed by Ericsson in 1994 and operates in the 2.4 GHz ISM band, allowing communication within a range of approximately 10 meters. It can be used to connect various devices such as handheld communication devices, headphones, speakers, keyboards, mice, printers, and more. Its key characteristics include low power consumption, low cost, and ease of use. Currently, it has evolved to the fifth generation, supporting higher data transfer rates and broader coverage.

## Implementation Principle

The implementation principle of Bluetooth is based on a short-range communication protocol using radio technology. It employs 2.4GHz radio waves for communication and utilizes Frequency Hopping Spread Spectrum (FHSS) to avoid interference with other wireless devices. During communication, Bluetooth devices send and receive data packets and use different Bluetooth protocols to control the communication process and data transmission.

## Module Introduction

- **BLE Module (Bluetooth Low Energy)**: BLE stands for Bluetooth Low Energy. It is a Bluetooth technology that enables communication under low power conditions. Compared to traditional Bluetooth, BLE consumes significantly less power, making it suitable for low-power devices that require long-term operation, such as smartwatches, health monitoring devices, and smart home appliances. For details, refer to the [@ohos.bluetooth.ble API Reference](../../../../en/application-dev/reference/ConnectivityKit/cj-apis-bluetooth-ble.md).

- **GATT Module (Generic Attribute)**: GATT refers to the Generic Attribute in Bluetooth technology. It is a protocol used for data transmission between Bluetooth Low Energy devices. The GATT protocol defines a universal framework of attributes and services to describe communication between Bluetooth devices. Bluetooth devices can provide services to other devices or obtain services from them. For details, refer to the [@ohos.bluetooth.ble API Reference](../../../../en/application-dev/reference/ConnectivityKit/cj-apis-bluetooth-ble.md).