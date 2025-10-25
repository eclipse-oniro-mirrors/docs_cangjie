# Application Event Logging Error Codes

> **Note:**
>
> The following only introduces error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 11100001 Logging Function Disabled

**Error Message**

Function is disabled.

**Error Description**

When calling the write interface for application event logging, the system will ignore related events because the logging function is not enabled.

**Possible Causes**

The application event logging function has been disabled.

**Solution**

Call the configuration interface to enable the logging function.

   ```cangjie
   import ohos.hiappevent.*

   var config : ConfigOption = ConfigOption("100M", disable: false)
   HiAppEvent.configure(config)
   ```

## 11101001 Invalid Event Domain Name

**Error Message**

Invalid event domain.

**Error Description**

When calling the write interface for application event logging, the system will ignore related events because an invalid event domain name was passed.

**Possible Causes**

The passed event domain name does not comply with the following rules:
- The event domain name only contains digits, lowercase letters, and underscore characters.
- The event domain name starts with a lowercase letter and does not end with an underscore.
- The event domain name is not empty and its length does not exceed 16 characters.

**Solution**

Pass a valid event domain name.

## 11101002 Invalid Event Name

**Error Message**

Invalid event name.

**Error Description**

When calling the write interface for application event logging, the system will ignore related events because an invalid event name was passed.

**Possible Causes**

The passed event name does not comply with the following rules:
- The event name only contains $ characters, digits, letters, and underscore characters.
- The first character of the event name must be a letter or $ character, middle characters must be digits, letters, or underscores, and the last character must be a digit or letter.
- The event name is not empty and its length does not exceed 48 characters.

**Solution**

Pass a valid event name.

## 11101003 Invalid Number of Event Parameters

**Error Message**

Invalid number of event parameters.

**Error Description**

When calling the write interface for application event logging, additional event parameters will be discarded because an invalid number of event parameters was passed.

**Possible Causes**

The number of passed event parameters exceeds 32.

**Solution**

Pass a valid number of event parameters.

## 11101004 Invalid String Length of Event Parameter

**Error Message**

Invalid string length of the event parameter.

**Error Description**

When calling the write interface for application event logging, the system will ignore related event parameters because an excessively long string was passed as the event parameter value.

**Possible Causes**

The string length in the passed event parameter value exceeds 8*1024 characters.

**Solution**

Pass an event parameter value with a valid string length.

## 11101005 Invalid Event Parameter Name

**Error Message**

Invalid event parameter name.

**Error Description**

When calling the write interface for application event logging, the system will ignore related event parameters because an invalid event parameter name was passed.

**Possible Causes**

The passed event parameter name does not comply with the following rules:
- The event parameter name only contains $ characters, digits, letters, and underscore characters.
- The first character of the event parameter name must be a letter or $ character, middle characters must be digits, letters, or underscores, and the last character must be a digit or letter.
- The event parameter name is not empty and its length does not exceed 16 characters.

**Solution**

Pass a valid event parameter name.

## 11101006 Invalid Array Length of Event Parameter

**Error Message**

Invalid array length of the event parameter.

**Error Description**

When calling the write interface for application event logging, additional array elements will be discarded because an excessively long array was passed as the event parameter value.

**Possible Causes**

The array length in the passed event parameter value exceeds 100.

**Solution**

Pass an event parameter value with a valid array length.

## 11101007 Invalid Number of Custom Event Parameters

**Error Message**

The number of parameter keys exceeds the limit.

**Error Description**

When calling the setEventParam interface to set custom event parameters, the system will ignore this call because an invalid number of event parameters was passed.

**Possible Causes**

The number of passed custom event parameters exceeds 64.

**Solution**

Pass a valid number of custom event parameters.

## 11102001 Invalid Watcher Name

**Error Message**

Invalid watcher name.

**Error Description**

When calling the addWatcher interface for event subscription, the system will ignore this subscription because an invalid watcher name was passed.

**Possible Causes**

The passed watcher name does not comply with the following rules:
- The watcher name only contains digits, lowercase letters, and underscore characters.
- The watcher name starts with a lowercase letter and does not end with an underscore.
- The watcher name is not empty and its length does not exceed 32 characters.

**Solution**

Pass a valid watcher name.

## 11102002 Invalid Filtering Event Domain

**Error Message**

Invalid filtering event domain.

**Error Description**

When calling the addWatcher interface for event subscription, the system will ignore this subscription because an invalid filtering event domain was passed.

**Possible Causes**

The passed filtering event domain name does not comply with the following rules:
- The event domain name only contains digits, lowercase letters, and underscore characters.
- The event domain name starts with a lowercase letter and does not end with an underscore.
- The event domain name is not empty and its length does not exceed 32 characters.

**Solution**

Pass a valid filtering event domain name.

## 11102003 Invalid Row Value

**Error Message**

Invalid row value.

**Error Description**

When calling the addWatcher interface for event subscription, the system will ignore this subscription because an invalid event count value was passed in the callback trigger condition.

**Possible Causes**

The row value in the passed callback trigger condition is negative.

**Solution**

Pass a natural number as the row value.

## 11102004 Invalid Size Value

**Error Message**

Invalid size value.

**Error Description**

When calling the addWatcher interface for event subscription, the system will ignore this subscription because an invalid event size value was passed in the callback trigger condition.

**Possible Causes**

The size value in the passed callback trigger condition is negative.

**Solution**

Pass a natural number as the size value.

## 11102005 Invalid Timeout Value

**Error Message**

Invalid timeout value.

**Error Description**

When calling the addWatcher interface for event subscription, the system will ignore this subscription because an invalid timeout value was passed in the callback trigger condition.

**Possible Causes**

The timeout value in the passed callback trigger condition is negative.

**Solution**

Pass a natural number as the timeout value.

## 11103001 Invalid Maximum Storage Quota Value

**Error Message**

Invalid max storage quota value.

**Error Description**

When calling the configure interface for logging configuration, the system will ignore this configuration because an invalid maximum storage quota value was passed.

**Possible Causes**

The passed maximum storage quota value string does not comply with the following rules:
- The quota value string only consists of digits and size unit characters (unit characters support [b|k|kb|m|mb|g|gb|t|tb], case-insensitive).
- The quota value string must start with a digit, followed by an optional unit character (default unit is byte), or end with a unit character.

**Solution**

Pass a valid maximum storage quota value string.

## 11104001 Invalid Event Package Size Value

**Error Message**

Invalid size value.

**Error Description**

When calling the setSize interface to set the threshold for the size of each retrieved event package, the system will ignore this setting because an invalid event package size value was passed.

**Possible Causes**

The passed event package size value is negative.

**Solution**

Pass a natural number as the event package size.