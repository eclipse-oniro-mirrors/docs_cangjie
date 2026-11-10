# Bluetooth Service Development Overview

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Overview

Bluetooth technology is a wireless communication technology that enables data transmission over short distances. It was proposed by Ericsson in 1994 and operates in the 2.4 GHz ISM band, allowing communication within a range of approximately 10 meters. It can be used to connect various devices such as mobile phones, headphones, speakers, keyboards, mice, printers, etc. Key features include low power consumption, low cost, and ease of use. Currently, it has evolved to the fifth generation, supporting higher data transfer rates and broader coverage.

## Implementation Principle

The implementation principle of Bluetooth is based on a short-range communication protocol using radio technology. It employs 2.4 GHz radio waves for communication and utilizes Frequency Hopping Spread Spectrum (FHSS) to avoid interference with other wireless devices. During communication, Bluetooth devices send and receive data packets and use different Bluetooth protocols to control the communication process and data transmission.

## Module Introduction

- **a2dp Module (Advanced Audio Distribution Profile)**: A2DP stands for Advanced Audio Distribution Profile. It is a Bluetooth protocol that enables wireless transmission of high-quality audio streams, such as music or voice calls, while supporting bidirectional communication. It is commonly used in devices like headphones, speakers, and car audio systems. For details, refer to the [@ohos.bluetooth.a2dp API Reference](../../reference/ConnectivityKit/cj-apis-bluetooth-a2dp.md).

- **ble Module (Bluetooth Low Energy)**: BLE stands for Bluetooth Low Energy. It is a Bluetooth technology capable of communication under low power consumption. Compared to traditional Bluetooth, BLE consumes significantly less power, making it suitable for low-power devices that require long-term operation, such as smartwatches, health monitoring devices, and smart home products. For details, refer to the [@ohos.bluetooth.ble API Reference](../../reference/ConnectivityKit/cj-apis-bluetooth-ble.md).

- **gatt Module (Generic Attribute)**: GATT refers to Generic Attribute in Bluetooth technology. It is a protocol used for data transmission between Bluetooth Low Energy devices. The GATT protocol defines a set of generic attributes and service frameworks to describe communication between Bluetooth devices. Bluetooth devices can provide services to other devices or obtain services from them. For details, refer to the [@ohos.bluetooth.ble API Reference](../../reference/ConnectivityKit/cj-apis-bluetooth-ble.md).

- **socket Module (Bluetooth Socket)**: The socket module provides Bluetooth socket capabilities for establishing point-to-point connections and transmitting data between two Bluetooth devices. It supports RFCOMM (Serial Port Profile, SPP) and L2CAP link types. For details, refer to the [@ohos.bluetooth.socket API Reference](../../reference/ConnectivityKit/cj-apis-bluetooth-socket.md). For the development guide, see [SPP Connection and Data Transmission](cj-spp-development-guide.md).