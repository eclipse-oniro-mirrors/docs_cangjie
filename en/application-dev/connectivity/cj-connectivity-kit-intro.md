# Introduction to Connectivity Kit

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Overview of Connectivity Kit Development

Mobile terminal devices have become deeply integrated into people's daily lives. Common behaviors for end users now include connecting Bluetooth headphones for music, using WiFi for internet access, and employing NFC for touch-to-open door functions.

In these diverse usage scenarios, Bluetooth provides fundamental capabilities based on wireless connections (such as music/calls/file sharing), WiFi offers basic wireless connectivity, and NFC enables proximity-based card reading and swiping functions.

For developers, designing experience services for basic communication can make application usage more aligned with each end user's daily life.

### Introduction to Bluetooth

Bluetooth technology is a wireless communication standard that enables short-range data transmission. It can connect various devices including smartphones, headphones, speakers, keyboards, mice, and printers. Its characteristics include low power consumption, low cost, and ease of use. Currently in its fifth generation, it supports higher data transfer rates and broader coverage.

Below are introductions to several common Bluetooth-related modules:

- **BLE Module (Bluetooth Low Energy)**

  BLE stands for Bluetooth Low Energy. It's a Bluetooth technology that enables communication with minimal power consumption. Compared to traditional Bluetooth, BLE consumes significantly less power, making it ideal for low-power devices requiring long-term operation, such as smartwatches, health monitoring devices, and smart home products.

  For details, see [ohos.bluetooth.ble API Reference](../reference/ConnectivityKit/cj-apis-bluetooth-ble.md).

- **A2DP Module (Advanced Audio Distribution Profile)**

  A2DP stands for Advanced Audio Distribution Profile. It's a Bluetooth protocol that enables wireless transmission of high-quality audio streams (such as music or voice calls) while supporting bidirectional communication. This makes it suitable for headphones, speakers, car audio systems, and similar devices.

  For details, see [ohos.bluetooth.a2dp API Reference](../reference/ConnectivityKit/cj-apis-bluetooth-a2dp.md).

- **socket Module (Bluetooth Socket)**

  The socket module provides Bluetooth socket capabilities and supports RFCOMM (corresponding to the Serial Port Profile, SPP) and L2CAP link types. It is used to establish point-to-point connections and transmit data between two Bluetooth devices. The communicating parties are classified by role into a server and a client.

  For details, see [ohos.bluetooth.socket API Reference](../reference/ConnectivityKit/cj-apis-bluetooth-socket.md).

Related development guide: [Bluetooth Development Guide](./bluetooth/cj-bluetooth-overview.md).

### Introduction to WLAN

Wireless Local Area Networks (WLAN) transmit and receive data via radio waves, infrared signals, or other technologies, enabling network communication between nodes without physical connections. Commonly used in office and public environments with mobile terminals.

The WLAN system provides users with:
- WLAN network access (STA mode)
- Peer-to-peer data transmission (P2P mode)
- Hotspot sharing (AP mode)

These functions allow applications to interconnect with other devices via WLAN.

- **STA Mode**
  STA (Station) mode refers to client mode in a network. When a device has this capability, it can connect to another routed network (such as a home router), typically used for providing network uplink services.

  For details, see [ohos.wifiManager API Reference](../reference/ConnectivityKit/cj-apis-wifi_manager.md).

- **P2P Mode**
  P2P mode, also known as Wi-Fi Direct, is a peer-to-peer connection technology that establishes TCP/IP links directly between two STAs without requiring an Access Point (AP). One STA acts as a traditional AP, called Group Owner (GO), while the other connects to it as a Group Client (GC).

  For details, see [ohos.wifiManager API Reference](../reference/ConnectivityKit/cj-apis-wifi_manager.md).

- **AP Mode**
  AP mode provides downlink data services for client devices in a WLAN. It serves as the central device in a wireless local area network.

  For details, see [ohos.wifiManager API Reference](../reference/ConnectivityKit/cj-apis-wifi_manager.md).

### Introduction to NFC

NFC stands for Near Field Communication. The NFC service provides functions including NFC switch control, NFC tag read/write, and NFC card emulation.

### Operation Mechanism

As a fundamental communication service provided by the system to applications, Connectivity capabilities require corresponding switch activation/connection handling during application usage scenarios, with active connection termination upon service completion.

### Constraints and Limitations

Using device-related capabilities requires users to actively authorize and enable the corresponding switches. Otherwise, the system will not provide services to third-party applications.