# Development Preparation

The main workflow for camera application development includes preparation, device input, session management, preview, photo capture, and video recording.

## Requesting Permissions

When developing a camera application, it is necessary to first request camera-related permissions to ensure the app has access to the camera hardware and other functionalities. The required permissions are listed in the table below. Before requesting permissions, ensure compliance with the [Basic Principles of Permission Usage](../../security/AccessToken/cj-app-permission-mgmt-overview.md#权限使用的基本原则).

- To use the camera for capturing photos, the **ohos.permission.CAMERA** permission must be requested.
- When audio recording via microphone is required simultaneously, the **ohos.permission.MICROPHONE** permission must be requested.
- If the captured photos/videos need to display geographical location information, the **ohos.permission.MEDIA_LOCATION** permission must be requested to access location data in user media files.

All the above permissions require user authorization via pop-up dialogs. For specific request and verification methods, refer to [Requesting User Authorization](../../security/AccessToken/cj-request-user-authorization.md#向用户申请授权).

> **Note:**
>
> Only when an application needs to clone, back up, or synchronize image or video files from public user directories, it may request the ohos.permission.READ_IMAGEVIDEO and ohos.permission.WRITE_IMAGEVIDEO permissions for reading and writing audio files. For the request method, refer to [Requesting Restricted Permissions](../../security/AccessToken/cj-declare-permissions-in-acl.md#申请使用受限权限).

## Development Guide

| Development Workflow | Cangjie Development Guide |
| -------------------- | ------------------------- |
| Device Input         | [Device Input](./cj-camera-device-input.md) |
| Session Management   | [Session Management](./cj-camera-session-management.md) |
| Metadata             | [Metadata] |