# Access Control Overview

By default, applications can only access limited system resources. However, in certain scenarios, applications may require extended functionalities that necessitate access to additional system data (including user personal data) and capabilities. The system must also provide explicit interfaces to share its data or functionalities externally.

The system employs access control mechanisms to prevent improper or malicious use of data or functionalities. Current access control mechanisms encompass multiple aspects, including application sandboxing, application permissions, system controls, and other solutions.

## Application Sandbox

Applications running on the system are deployed within protected sandboxes. Through the security isolation mechanisms of sandboxes, improper application behaviors (such as unauthorized data access between applications or device tampering) can be restricted. Each application is assigned a unique ID ([TokenID](./cj-app-permission-mgmt-overview.md#basic-concepts-in-permission-mechanism)), which the system uses to identify and restrict application access behaviors.

## Application Permissions

The system sets process domain and data domain labels based on an application's APL (Ability Privilege Level) and restricts the scope of data accessible to the application through access control mechanisms. This structurally mitigates the risk of data leakage.

Applications with different APL levels can request different permission levels. Various system resources (e.g., contacts) or system capabilities (e.g., accessing the camera or microphone) are protected by different application permissions. Through strict hierarchical permission protection, the system effectively resists malicious attacks, ensuring security and reliability.

For detailed information on application permission management, refer to [Application Permission Management Overview](./cj-app-permission-mgmt-overview.md).

## Secure Access Mechanism

OpenHarmony introduces a secure access mechanism that transforms how applications obtain private data, shifting user management from "permissions" to "data." This allows on-demand granting of system data. For example, when a user wants to change a social platform profile picture, the application can no longer gain access to the entire photo gallery. Instead, the user selects which photo to share, and the application receives only that specific photo. This controlled isolation between user privacy data and applications comprehensively safeguards user privacy.