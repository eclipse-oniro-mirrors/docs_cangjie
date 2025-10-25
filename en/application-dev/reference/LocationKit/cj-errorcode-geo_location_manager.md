# Location Service Error Codes

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 3301000 Location Service Unavailable

**Error Message**

The location service is unavailable.

**Error Description**

The location service is unavailable, and interfaces related to the location service cannot be invoked.

**Possible Causes**

1. Abnormal startup of the location service, resulting in communication failure between the application and the location service subsystem, making the location service unavailable.

2. GNSS chip initialization failure, causing GNSS positioning to malfunction.

3. Abnormal network location service, causing network positioning to malfunction.

**Resolution**

Stop invoking this interface.

## 3301100 Location Function Failure Due to Switch Being Off

**Error Message**

The location switch is off.

**Error Description**

The location function fails because the location switch is not turned on.

**Possible Causes**

The location switch is not turned on, making basic functions such as continuous positioning and single-time positioning unavailable.

**Resolution**

Prompt the user to turn on the location switch.

## 3301200 Positioning Failed, No Location Result Obtained

**Error Message**

Failed to obtain the geographical location.

**Error Description**

Positioning failed, and no location result was obtained.

**Possible Causes**

1. Weak GNSS signal, causing positioning timeout.

2. Abnormal network positioning, causing positioning timeout.

3. The positioning result does not meet the accuracy requirement (maxAccuracy) specified in the positioning request parameters, causing positioning timeout.

4. No cached location in the system, causing failure to obtain the last known location.

5. Incorrect system time setting, causing failure to obtain the location.

**Resolution**

1. Move to an open area and initiate positioning again.

2. Check whether the device can connect to the network, whether a SIM card is inserted, and whether the WiFi switch is turned on.

3. Check whether the maxAccuracy field in the positioning request is reasonable.

4. If there is no cached location in the system, use the getCurrentLocation interface to obtain real-time location information.

5. Enable automatic time setting on the "Date & Time" page.

## 3301300 Reverse Geocoding Query Failed

**Error Message**

Reverse geocoding query failed.

**Error Description**

The reverse geocoding query failed.

**Possible Causes**

- Slow data network, causing the client-side request to fail or the cloud-side result not to be returned to the client.

- The X86 emulator does not support reverse geocoding, causing the query to fail when debugging on the X86 emulator.

**Resolution**

- For network issues, try retrying the reverse geocoding query.

- For X86 emulator issues, verify on a real device.

## 3301400 Geocoding Query Failed

**Error Message**

Geocoding query failed.

**Error Description**

The geocoding query failed.

**Possible Causes**

1. Incorrect request parameters, or no results found based on the parameters.  
2. Slow data network, causing the client-side request to fail or the cloud-side result not to be returned to the client.

**Resolution**

Check the request parameters or network status and retry.

## 3301500 Area Information (Including Country Code) Query Failed

**Error Message**

Failed to query the area information.

**Error Description**

The area information (including country code) query failed.

**Possible Causes**

No correct area information was queried.

**Resolution**

Stop invoking the area code query interface.

## 3301600 Geofence Operation Failed

**Error Message**

Failed to operate the geofence.

**Error Description**

Geofence operations failed, including adding, deleting, pausing, and resuming.

**Possible Causes**

1. The GNSS chip does not support geofencing.  
2. Underlying business logic abnormalities caused geofence operations to fail.

**Resolution**

Stop invoking the geofence operation interface.

## 3301601 Adding Geofence Failed Due to Exceeding Maximum Limit

**Error Message**

The number of geofences exceeds the maximum.

**Error Description**

Adding a geofence failed because the number of geofences exceeded the maximum limit.

**Possible Causes**

1. The number of existing geofences in the system exceeds the maximum limit.

**Resolution**

Delete excess geofences before adding new ones.

## 3301602 Deleting Geofence Failed Due to Incorrect ID

**Error Message**

Failed to delete a geofence due to an incorrect ID.

**Error Description**

Deleting a geofence failed because the geofence ID was incorrect.

**Possible Causes**

1. The geofence ID passed when invoking the delete geofence interface was incorrect.

**Resolution**

Pass the correct geofence ID when invoking the delete geofence interface.

## 3301700 No Response to Request

**Error Message**

No response to the request.

**Error Description**

Some asynchronous requests require user confirmation via button clicks or responses from the GNSS chip and network server. No response was received in these scenarios, causing the operation to fail.

**Possible Causes**

1. The user did not click the confirmation button.  
2. The GNSS chip did not respond.  
3. The network server did not respond.

**Resolution**

Stop invoking the related interface.

## 3301800 Failed to Start WiFi or Bluetooth Scanning

**Error Message**

Failed to start WiFi or Bluetooth scanning.

**Error Description**

When subscribing to WiFi or Bluetooth scan information, the system may first initiate scanning. If scanning fails to start, an error code is returned to the app.

**Possible Causes**

1. Internal errors in the WiFi or Bluetooth service caused scanning to fail.  
2. In low-battery scenarios, power restrictions prevent scanning from being initiated.  
3. The WiFi or Bluetooth switch is not turned on.

**Resolution**

Turn the WiFi or Bluetooth switch off and on again.