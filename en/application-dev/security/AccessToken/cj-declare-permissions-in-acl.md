# Requesting Restricted Permissions  

Restricted permissions are typically not available for third-party applications to request. When an application requests permissions to access necessary resources, it may encounter situations where certain permission levels exceed the application's APL (Ability Privilege Level). In such cases, developers can resolve the level mismatch by using the ACL (Access Control List) method to gain access to restricted permissions.  

For example:  
- If an application needs to use a global floating window, it must request the `ohos.permission.SYSTEM_FLOAT_WINDOW` permission, which belongs to the `system_basic` level.  
- If an application requires screen capture functionality, it must request the `ohos.permission.CAPTURE_SCREEN` permission, which belongs to the `system_core` level.  
In these scenarios, a `normal`-level application must request permissions across levels.  

This section provides two methods for application debugging purposes. **Neither method should be used for commercial releases or app store submissions**. For commercial versions, developers must apply for release certificates and signing files through the respective app store.  

- **Method 1**: Use DevEco Studio to [request cross-level permissions via ACL](https://developer.huawei.com/consumer/en/doc/harmonyos-guides/ide-signing).  
- **Method 2**: Directly modify the HarmonyAppProvision configuration file.  

    1. Open the HarmonyAppProvision configuration file, located at:  
       `Sdk/openharmony/_{Version}_/toolchains/lib/UnsgnedReleasedProfileTemplate.json`.  

    2. Add the required restricted permissions:  
       - **Permissions without data payloads**: Modify the `"acls" > "allowed-acls"` field.  
       - **Permissions with data payloads**: Modify the `"app-services-capabilities"` field.  

        ```json
        {
          // ...
          "acls": {
            "allowed-acls": [
              "ohos.permission.WRITE_AUDIO",
              "ohos.permission.CAPTURE_SCREEN"
            ]
          },
          "app-services-capabilities": {
              "ohos.permission.ACCESS_DDK_DRIVERS": "..."
          }
        }
        ```  

    3. Re-sign the application.