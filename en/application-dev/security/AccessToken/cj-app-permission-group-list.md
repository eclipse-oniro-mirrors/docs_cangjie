# Application Permission Group List

## Usage Instructions

- Before applying for target permissions, developers are advised to first read the [Application Permission Management Overview - Permission Groups and Sub-permissions](./cj-app-permission-mgmt-overview.md#permission-groups-and-sub-permissions) to understand related concepts, then reasonably apply for corresponding permission groups.
- When an application requests permissions, permissions within the same permission group will be requested together in a single pop-up window. After user authorization is granted, all permissions within the group will be authorized simultaneously. Exceptions include location, contacts, call logs, phone, messaging, and calendar permission groups.

  Examples using location information and camera permission groups:

    - When an application only requests the permission `ohos.permission.APPROXIMATELY_LOCATION` (belonging to the location information permission group), the user will receive a single pop-up requesting location information, containing the application for that single permission.
    - When an application requests both `ohos.permission.APPROXIMATELY_LOCATION` and `ohos.permission.LOCATION` (both belonging to the location information permission group), the user will receive a single pop-up requesting location information, containing the application for both permissions.
    - When an application requests both `ohos.permission.APPROXIMATELY_LOCATION` (belonging to the location information permission group) and `ohos.permission.CAMERA` (belonging to the camera permission group), the user will receive two separate pop-ups: one requesting location information and another requesting camera access.

- The permission groups currently supported by the system are listed below. For details on each sub-permission, please refer to the [Application Permission List](./cj-permissions-for-all-user.md).

## Location<!--Del--> Information<!--DelEnd-->

- [ohos.permission.LOCATION_IN_BACKGROUND](./cj-permissions-for-all-user.md#ohospermissionlocation_in_background)
- [ohos.permission.LOCATION](./cj-permissions-for-all-user.md#ohospermissionlocation)
- [ohos.permission.APPROXIMATELY_LOCATION](./cj-permissions-for-all-user.md#ohospermissionapproximately_location)

## Camera

- [ohos.permission.CAMERA](./cj-permissions-for-all-user.md#ohospermissioncamera)

## Microphone

- [ohos.permission.MICROPHONE](./cj-permissions-for-all-user.md#ohospermissionmicrophone)

## Contacts

- [ohos.permission.READ_CONTACTS](./cj-restricted-permissions.md#ohospermissionread_contacts)
- [ohos.permission.WRITE_CONTACTS](./cj-restricted-permissions.md#ohospermissionwrite_contacts)

## Calendar

- [ohos.permission.READ_CALENDAR](./cj-permissions-for-all-user.md#ohospermissionread_calendar)
- [ohos.permission.WRITE_CALENDAR](./cj-permissions-for-all-user.md#ohospermissionwrite_calendar)<!--Del-->
- [ohos.permission.READ_WHOLE_CALENDAR](./cj-permissions-for-system-apps-user.md#ohospermissionread_whole_calendar)
- [ohos.permission.WRITE_WHOLE_CALENDAR](./cj-permissions-for-system-apps-user.md#ohospermissionwrite_whole_calendar)<!--DelEnd-->

<!--RP1-->
## Fitness Activity

- [ohos.permission.ACTIVITY_MOTION](./cj-permissions-for-all-user.md#ohospermissionactivity_motion)

## Body Sensors

- [ohos.permission.READ_HEALTH_DATA](./cj-permissions-for-all-user.md#ohospermissionread_health_data)

<!--RP1End-->

## Photos and Videos

- [ohos.permission.WRITE_IMAGEVIDEO](./cj-restricted-permissions.md#ohospermissionwrite_imagevideo)
- [ohos.permission.READ_IMAGEVIDEO](./cj-restricted-permissions.md#ohospermissionread_imagevideo)
- [ohos.permission.MEDIA_LOCATION](./cj-permissions-for-all-user.md#ohospermissionmedia_location)

## Music and Audio

- [ohos.permission.WRITE_AUDIO](./cj-restricted-permissions.md#ohospermissionwrite_audio)
- [ohos.permission.READ_AUDIO](./cj-restricted-permissions.md#ohospermissionread_audio)

<!--RP2-->
## Advertising Tracking

- [ohos.permission.APP_TRACKING_CONSENT](./cj-permissions-for-all-user.md#ohospermissionapp_tracking_consent)

<!--RP2End-->

<!--Del-->
## Installed Applications List

- [ohos.permission.GET_INSTALLED_BUNDLE_LIST](./cj-permissions-for-system-apps-user.md#ohospermissionget_installed_bundle_list)

<!--DelEnd-->

<!--RP3-->
## Multi-Device Collaboration

- [ohos.permission.DISTRIBUTED_DATASYNC](./cj-permissions-for-all-user.md#ohospermissiondistributed_datasync)

## Bluetooth

- [ohos.permission.ACCESS_BLUETOOTH](./cj-permissions-for-all-user.md#ohospermissionaccess_bluetooth)

## NearLink

- [ohos.permission.ACCESS_NEARLINK](./cj-permissions-for-all-user.md#ohospermissionaccess_nearlink)

<!--RP3End-->

<!--Del-->
## Phone

- [ohos.permission.ANSWER_CALL](./cj-permissions-for-system-apps-user.md#ohospermissionanswer_call)
- [ohos.permission.MANAGE_VOICEMAIL](./cj-permissions-for-system-apps-user.md#ohospermissionmanage_voicemail)

## Call Logs

- [ohos.permission.READ_CALL_LOG](./cj-permissions-for-system-apps-user.md#ohospermissionread_call_log)
- [ohos.permission.WRITE_CALL_LOG](./cj-permissions-for-system-apps-user.md#ohospermissionwrite_call_log)

## Messaging

- [ohos.permission.READ_CELL_MESSAGES](./cj-permissions-for-system-apps-user.md#ohospermissionread_cell_messages)
- [ohos.permission.READ_MESSAGES](./cj-permissions-for-system-apps-user.md#ohospermissionread_messages)
- [ohos.permission.RECEIVE_MMS](./cj-permissions-for-system-apps-user.md#ohospermissionreceive_mms)
- [ohos.permission.RECEIVE_SMS](./cj-permissions-for-system-apps-user.md#ohospermissionreceive_sms)
- [ohos.permission.RECEIVE_WAP_MESSAGES](./cj-permissions-for-system-apps-user.md#ohospermissionreceive_wap_messages)
- [ohos.permission.SEND_MESSAGES](./cj-permissions-for-system-apps-user.md#ohospermissionsend_messages)

<!--DelEnd-->

## Clipboard

- [ohos.permission.READ_PASTEBOARD](./cj-restricted-permissions.md#ohospermissionread_pasteboard)

## Screenshot

- [ohos.permission.CUSTOM_SCREEN_CAPTURE](./cj-permissions-for-all-user.md#ohospermissioncustom_screen_capture)

## Folders

> **Note:**
>
> Only available for 2-in-1 devices.

- [ohos.permission.READ_WRITE_DOWNLOAD_DIRECTORY](./cj-permissions-for-all-user.md#ohospermissionread_write_download_directory)
- [ohos.permission.READ_WRITE_DESKTOP_DIRECTORY](./cj-restricted-permissions.md#ohospermissionread_write_desktop_directory)
- [ohos.permission.READ_WRITE_DOCUMENTS_DIRECTORY](./cj-permissions-for-all-user.md#ohospermissionread_write_documents_directory)

## Folders

> **Note:**
>
> Only available for 2-in-1 devices.

- [ohos.permission.READ_WRITE_DOWNLOAD_DIRECTORY](./cj-permissions-for-all-user.md#ohospermissionread_write_download_directory)
- [ohos.permission.READ_WRITE_DOCUMENTS_DIRECTORY](./cj-permissions-for-all-user.md#ohospermissionread_write_documents_directory)

## Files

- Reading media library audio files:

  Apply for restricted permissions [ohos.permission.READ_AUDIO](./cj-restricted-permissions.md#ohospermissionread_audio) or [ohos.permission.WRITE_AUDIO](./cj-restricted-permissions.md#ohospermissionwrite_audio) to read/write audio files in the media library.