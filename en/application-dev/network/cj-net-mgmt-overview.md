# Introduction to Network Kit

Network Kit (Network Service) primarily provides the following functionalities:

- [HTTP Data Request](./cj-http-request.md): Initiates a data request via HTTP.
- [Network Connection Management](./cj-net-connection-manager.md): Network connection management offers fundamental capabilities for managing networks, including priority management for multiple network connections (WiFi, cellular, Ethernet, etc.), network quality assessment, subscription to default or specified network connection status changes, querying network connection information, DNS resolution, and more.

## Constraints and Limitations

When using the network management module's related functionalities, corresponding permissions must be requested.

Before applying for permissions, ensure compliance with the [Basic Principles of Permission Usage](../security/AccessToken/cj-app-permission-mgmt-overview.md#basic-principles-of-permission-usage). Then, refer to [Access Control - Declaring Permissions](../security/AccessToken/cj-declare-permissions.md) to declare the corresponding permissions.

| Permission Name                     | Description                                   |
| ------------------------------------ | -------------------------------------------- |
| ohos.permission.GET_NETWORK_INFO     | Retrieves network connection information.    |
| ohos.permission.INTERNET             | Allows the program to open network sockets and establish network connections. |