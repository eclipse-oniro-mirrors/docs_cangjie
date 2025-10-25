# Introduction to Connectivity Kit  

## Overview of Connectivity Kit Development  

Mobile terminal devices have become deeply integrated into people's daily lives. Common behaviors include connecting to Bluetooth headphones for music, using Wi-Fi for internet access, and employing NFC for tap-to-open doors, all of which are now routine activities for end users.  

In these diverse usage scenarios, Bluetooth provides fundamental capabilities such as music playback, calls, and file sharing, Wi-Fi offers basic wireless connectivity, and NFC enables proximity-based card swiping and reading functionalities.  

For developers, designing seamless communication experiences can make applications more aligned with the daily lives of end users.  

### Introduction to Bluetooth  

Bluetooth technology is a wireless communication standard that enables short-range data transmission. It can connect various devices such as smartphones, headphones, speakers, keyboards, mice, and printers. Its key features include low power consumption, cost-effectiveness, and ease of use. Currently in its fifth generation, Bluetooth supports higher data transfer rates and broader coverage.  

Below are some common Bluetooth-related modules:  

- **CONNECTION Module**  
  The Bluetooth connection module provides interfaces for device discovery, pairing, and retrieving local/peripheral information. To interact with peripherals, developers must first use this module's capabilities to establish successful pairing and connections before proceeding with data transmission.  

  For details, refer to the [ohos.bluetooth.connection API Reference](../../../en/application-dev/reference/ConnectivityKit/cj-apis-bluetooth-connection.md).  

- **BLE Module (Bluetooth Low Energy)**  
  BLE stands for Bluetooth Low Energy, a technology that enables communication with minimal power consumption. Compared to classic Bluetooth, BLE is more energy-efficient, making it ideal for long-running low-power devices like smartwatches, health monitors, and smart home gadgets.  

  For details, refer to the [ohos.bluetooth.ble API Reference](../../../en/application-dev/reference/ConnectivityKit/cj-apis-bluetooth-ble.md).  

- **A2DP Module (Advanced Audio Distribution Profile)**  
  A2DP is a Bluetooth protocol for wirelessly streaming high-quality audio, such as music or voice calls. It supports bidirectional communication and is commonly used in headphones, speakers, and car audio systems.  

For related development guidelines, see: [Bluetooth Development Guide](./bluetooth/cj-bluetooth-overview.md).  

### Introduction to WLAN  

Wireless Local Area Networks (WLAN) transmit and receive data via radio waves, infrared signals, or other technologies, enabling network communication without physical connections. WLAN is widely used in mobile office and public environments.  

The WLAN system provides users with:  
- **STA Mode (Station Mode)**  
  STA mode functions as a client in a network. Devices in this mode can connect to routers (e.g., home routers) for uplink data services.  

  For details, refer to the [ohos.wifi_manager API Reference](../../../en/application-dev/reference/ConnectivityKit/cj-apis-wifi_manager.md).  

- **P2P Mode (Wi-Fi Direct)**  
  P2P mode, or Wi-Fi Direct, establishes direct TCP/IP connections between two STAs without requiring an access point (AP). One STA acts as the Group Owner (GO), while the other functions as the Group Client (GC), connecting to the GO like a traditional AP.  

  For details, refer to the [ohos.wifi_manager API Reference](../../../en/application-dev/reference/ConnectivityKit/cj-apis-wifi_manager.md).  

- **AP Mode (Access Point Mode)**  
  AP mode provides downlink data services to client devices in a WLAN, serving as the central hub for wireless networking.  

  For details, refer to the [ohos.wifi_manager API Reference](../../../en/application-dev/reference/ConnectivityKit/cj-apis-wifi_manager.md).  

### Operational Mechanism  

As a fundamental communication service provided by the system, Connectivity capabilities require users to enable relevant switches or establish connections during application usage. Connections should be terminated proactively when tasks are completed.  

### Constraints and Limitations  

To utilize device capabilities, users must explicitly authorize and enable the corresponding switches. Otherwise, third-party applications will not receive system services.