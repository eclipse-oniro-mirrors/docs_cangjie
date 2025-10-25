# Requesting Restricted Permissions  

Restricted permissions are typically not available for third-party applications to request. When an application needs to request permissions to access essential resources but encounters permissions with a higher level than its own APL (Application Privilege Level), developers can resolve this level mismatch by using the ACL (Access Control List) method to gain access to restricted permissions.  

For example:  
- If an application requires a global floating window, it must request the `ohos.permission.SYSTEM_FLOAT_WINDOW` permission, which belongs to the `system_basic` level.  
- If an application needs to capture screen images, it must request the `ohos.permission.CAPTURE_SCREEN` permission, which belongs to the `system_core` level.  
In such cases, a `normal`-level application must request these permissions across privilege levels.  

This section provides two methods for application debugging purposes. **Neither method is suitable for commercial release on app markets.** To develop a commercial version of the application, apply for the necessary release certificates and signature files through the respective app market.  

### Method 1: Using DevEco Studio  
- Complete the [Cross-Level Permission Request via ACL](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing) process in DevEco Studio.  

### Method 2: Directly Modifying the HarmonyAppProvision Configuration File  
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