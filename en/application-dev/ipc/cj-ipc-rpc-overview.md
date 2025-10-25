# Introduction to IPC Kit

## Basic Concepts

IPC: Inter-Process Communication within a device  
RPC: Remote Procedure Call between devices  

IPC/RPC is used to achieve cross-process communication. The difference lies in that the former uses the Binder driver for intra-device cross-process communication, while the latter employs the soft bus driver for cross-device cross-process communication. The need for cross-process communication arises because each process has its own independent resources and memory space, preventing other processes from arbitrarily accessing different processes' memory and resources. IPC/RPC is designed to overcome this limitation.

> **Note:**  
>
> The Stage model cannot directly use the IPC and RPC described in this document. Below are typical usage scenarios for IPC and RPC:
>
> - A typical IPC scenario involves background services, where an application's background service provides cross-process service invocation capabilities through the IPC mechanism.
> - A typical RPC scenario involves multi-device collaboration, where the RPC mechanism enables remote interface invocation and data transfer capabilities.

## Implementation Principles

> **Note:**  
>
> Client: The end requesting services, referred to as the client.  
>
> Server: The end providing services, referred to as the server.  
>
> In the IPC Kit, Proxy often represents the service requester (client), while Stub represents the service provider (server). Subsequent documentation will not elaborate further on Proxy and Stub.

IPC and RPC typically adopt the client-server (Client-Server) model. During usage, the requesting client process can obtain a proxy (Proxy) for the server process and use this proxy to read and write data, thereby achieving inter-process data communication. More specifically, the client first establishes a proxy object for the server. This proxy object possesses the same functionality as the server. To access a specific method on the server, the client simply invokes the corresponding method on the proxy object, which then forwards the request to the server. The server processes the received request and returns the result to the proxy object via the driver. Finally, the proxy object relays the result back to the client.

Typically, the Stub registers system capabilities (System Ability) with the System Ability Manager (SAMgr), which manages these SAs and provides relevant interfaces to clients. To communicate with a specific SA, the client must first obtain the SA's Proxy object from SAMgr and then use this Proxy object to interact with the SA. Throughout the communication process, IPC relies on the Binder driver, while RPC relies on the soft bus driver.

## Constraints and Limitations

- For cross-process communication on a single device, the maximum data transfer size is approximately 1MB. For larger data volumes, use [Anonymous Shared Memory](../../../en/application-dev/reference/IPCKit/cj-apis-rpc.md#class-ashmem).

- Death notifications for anonymous Stub objects (those not registered with SAMgr) are not supported in RPC.

- Cross-device Proxy objects cannot be passed back to the device where the Stub object they point to resides. In other words, a Proxy object pointing to a remote Stub cannot undergo secondary cross-process transmission within the local device.