# Open Permissions (User Authorization)

All permissions listed here are user-granted (user_grant) open permissions, available to all applications.

For this type of permission, applications must not only declare the permission in the installation package but also request user authorization dynamically during runtime by displaying a pop-up dialog. The application will only obtain the corresponding permission and successfully access the target operation object after the user manually grants authorization.

<!--Del-->
> **Note:**
>
> Permissions with a level of "normal" do not involve ACL enablement fields.
<!--DelEnd-->

## Authorization Method

The authorization method for the following permissions is [user_grant (user authorization)](./cj-app-permission-mgmt-overview.md#user_grant-user-authorization). For the application process, refer to [Declaring Permissions](./cj-declare-permissions.md) > [Requesting User Authorization](./cj-request-user-authorization.md).

## Permission List

### ohos.permission.ACCESS_BLUETOOTH

Allows applications to access Bluetooth and utilize Bluetooth capabilities, such as pairing and connecting to peripheral devices.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.MEDIA_LOCATION

Allows applications to access geographical location information embedded in user media files.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.APP_TRACKING_CONSENT

Allows applications to read open anonymous device identifiers.

<!--RP3--><!--RP3End-->

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.ACTIVITY_MOTION

Allows applications to read the user's motion status.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.CAMERA

Allows applications to use the camera.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.DISTRIBUTED_DATASYNC

Allows data exchange between different devices.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.LOCATION_IN_BACKGROUND

Allows applications to obtain device location information while running in the background.

Due to security and privacy requirements, applications cannot be granted background location permissions through pop-up dialogs. If an application requires background location permissions, it must guide users to manually grant the permission in the settings interface.

**Application Process:**

1. Declare the permission in the "module.json5" configuration file by [Declaring Permissions](./cj-declare-permissions.md).  

   Since foreground location permissions must be requested before applying for background location permissions, developers should configure both the background location permission `ohos.permission.LOCATION_IN_BACKGROUND` and the foreground location permission. There are two scenarios for foreground location permission requests:  
   - Request approximate foreground location permission: [ohos.permission.APPROXIMATELY_LOCATION](#ohospermissionapproximately_location).  
   - Request precise foreground location permission: [ohos.permission.APPROXIMATELY_LOCATION](#ohospermissionapproximately_location) and [ohos.permission.LOCATION](#ohospermissionlocation).  

2. The application must request the corresponding foreground location permission from the user via a pop-up dialog.  

3. After the user grants the foreground location permission via the pop-up dialog, the application should inform the user (through pop-ups, notifications, etc.) to navigate to the settings interface to grant the background location permission.  

4. The user must manually grant the permission by selecting "Always Allow" for the application's location access in the settings interface.  

   Settings Path:  
   <!--RP1-->
   - Path 1: Settings > Privacy > Permission Management > Location > *Specific Application*  
   - Path 2: Settings > Privacy > Permission Management > Applications > *Specific Application* > Location  
   <!--RP1End-->

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.LOCATION

Allows applications to obtain precise device location information.

**Prerequisite:** This permission must be requested together with the approximate location permission [ohos.permission.APPROXIMATELY_LOCATION](#ohospermissionapproximately_location).  

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.APPROXIMATELY_LOCATION

Allows applications to obtain approximate device location information.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.MICROPHONE

Allows applications to use the microphone.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.READ_CALENDAR

Allows applications to read calendar information.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.WRITE_CALENDAR

Allows applications to add, remove, or modify calendar events.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.READ_HEALTH_DATA

Allows applications to read user health data.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.ACCESS_NEARLINK

Allows applications to access NearLink and utilize NearLink capabilities, such as pairing and connecting to peripheral devices.

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Initial Version:** 12  

### ohos.permission.READ_WRITE_DOWNLOAD_DIRECTORY

Allows applications to access the Download directory and its subdirectories in the public directory.

<!--RP2--><!--RP2End-->

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Supported Devices:** 2in1 | Tablet  
**Initial Version:** 12  

### ohos.permission.READ_WRITE_DOCUMENTS_DIRECTORY

Allows applications to access the Documents directory and its subdirectories in the public directory.

<!--RP2--><!--RP2End-->

**Permission Level:** normal  
**Authorization Method:** user_grant  
**Supported Devices:** 2in1 | Tablet  
**Initial Version:** 12  

### ohos.permission.CUSTOM_SCREEN_CAPTURE

Allows applications to capture screen images.

After obtaining this permission, applications can perform operations such as screenshots.

**Permission Level:** system_basic  
**Authorization Method:** user_grant  
**Supported Devices:** 2in1 | Tablet  
**Initial Version:** 12