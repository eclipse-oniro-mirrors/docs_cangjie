# Overview of Application Permission Control

## Introduction

The system provides a universal permission access mechanism that allows applications to access system resources (e.g., contacts) and system capabilities (e.g., camera, microphone) while protecting system data (including user personal data) and functionalities from improper or malicious use.

The objects protected by application permissions can be categorized into data and functionalities:

- **Data** includes personal data (e.g., photos, contacts, calendar, location) and device data (e.g., device identifiers, camera, microphone).
- **Functionalities** include device capabilities (e.g., accessing camera/microphone, making phone calls, network connectivity) and application features (e.g., displaying floating windows, creating shortcuts).

## Basic Principles of Permission Usage

Reasonable usage scenarios facilitate proper permission requests and utilization. When developing applications, permission requests must adhere to the following principles:

- All permissions required by an application (including third-party libraries it references) must be explicitly declared in the application's configuration file in strict accordance with the development guidelines. Refer to [Declaring Permissions](./cj-declare-permissions.md).
- Permission requests must follow the principle of minimalism. Applications must not request unnecessary or deprecated permissions. Excessive permission requests may raise user concerns about application security and degrade user experience, potentially affecting installation and retention rates.
- When requesting sensitive permissions (typically those closely related to user privacy, such as location, camera, microphone, calendar, fitness data, biometric sensors, media files, photos/videos), applications must provide justification for permission usage. Refer to [Requesting User Authorization](./cj-request-user-authorization.md).
- Sensitive permissions must be requested dynamically before executing corresponding business functionalities to comply with privacy minimization requirements.
- If a user denies a permission request, unrelated application functionalities should remain fully operational.

## Authorization Methods

Permissions are categorized into two types based on authorization methods: `system_grant` (system authorization) and `user_grant` (user authorization).

### system_grant (System Authorization)

`system_grant` refers to permissions where the system automatically grants access during installation. These permissions allow applications to access non-sensitive data or perform operations with controlled impact on the system or other applications.

For `system_grant` permissions, the system automatically grants them when the application is installed.

### user_grant (User Authorization)

`user_grant` refers to permissions that require explicit user approval during runtime. These permissions involve access to sensitive user/device data or operations that may significantly impact the system or other applications.

For these permissions, applications must:
1. Declare them in the installation package
2. Request user authorization via runtime dialogs
3. Only gain access after explicit user consent

For example, in the [Application Permission List](./cj-permissions-for-all.md), microphone and camera permissions are `user_grant` types with detailed usage justifications. Applications must display requested `user_grant` permissions in their app store listings.

## Permission Groups and Sub-permissions

To minimize permission dialog frequency and optimize user experience, the system groups logically related `user_grant` permissions into permission groups. When an application requests permissions, all sub-permissions within the same group are presented in a single dialog.

Note: Permission group assignments may change over time. Current supported groups are documented in the [Application Permission Group List](./cj-app-permission-group-list.md).

## Key Concepts in Permission Mechanism

- **TokenID**

  The system uses TokenID (Token identity) as the unique identifier for applications. The Permission Management Service manages Access Token (AT) information through TokenID, including:
  - Application identity (APP ID)
  - Sub-user ID
  - Application clone index
  - Application APL level
  - Permission grant status

  During resource access, the system uses TokenID to verify permission grants and control application behavior.

  Note: The system supports multi-user and application cloning features. The same application under different users or clones will have distinct ATs with different TokenIDs.

- **APL Levels (Ability Privilege Level)**

  To prevent permission abuse, the system configures different permission availability based on APL levels, which define application permission request priorities.

### Application APL Levels

Applications are classified into three ascending levels:

| APL Level | Description |
|-----------|-------------|
| normal | Default level for most applications |
| system_basic | Applications providing fundamental system services |
| system_core | Applications providing core OS capabilities (Note: Cannot be configured by developers) |

### Permission APL Levels

Permissions are classified into three ascending levels with different availability:

| APL Level | Description | Availability |
|-----------|-------------|--------------|
| normal | Allows access to general system resources beyond default rules (e.g., Wi-Fi configuration, camera access). These pose low risk to privacy and other applications. | Available to normal+ APL applications |
| system_basic | Allows access to basic OS services (e.g., system settings, authentication). These pose higher risks. | Available to system_basic+ APL applications (some permissions may be [restricted](./cj-declare-permissions-in-acl.md) for normal apps) |
| system_core | Involves access to core OS resources. Compromise could render the OS inoperable. | Exclusively for system_core applications |

- **Access Control List (ACL)**

  While permission APL levels generally match application APL levels, the ACL mechanism provides a special channel for lower-APL applications to request higher-level permissions when necessary.

  System permissions include an "ACL enabled" flag. When TRUE, applications can use ACL to request cross-level permissions. See [Restricted Permissions](./cj-declare-permissions-in-acl.md) for details.

  Example scenario: A normal-APL application needing a system_basic permission can request it via ACL if the permission's ACL flag is enabled.