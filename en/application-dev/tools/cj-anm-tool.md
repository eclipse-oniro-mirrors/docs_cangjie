# anm Tool

Advanced Notification Manager (referred to as anm) is a tool designed to implement notification printing, configure notification parameters, and provide developers with fundamental notification debugging and testing capabilities. These include printing detailed information of published notifications, setting the number of cached notifications, and enabling notifications.

## Environment Requirements

Before using this tool, developers need to obtain the [hdc tool](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-toolchain-hdc-guide.md) and execute `hdc shell`.

Currently, this tool is only supported in eng versions. Using it in user versions will result in the error: `error: user version cannot use setting`.

## anm Tool Command List

| Command | Description |
| ------- | ----------- |
| help    | Help command, displays anm-related help information. |
| dump    | Print command, outputs notification-related information. |
| setting | Configuration command, sets notification parameters. |

## Help Command (help)

```bash
# Display anm-related help information
anm help
```

## Print Command (dump)

```bash
# Print notification-related information
anm dump [<options>]
```

**Print Command Parameter List:**

| Parameter | Description |
| --------- | ----------- |
| -A/--active      | Print all active notification information. |
| -R/--recent      | Print recent notification information. |
| -D/--distributed | Print distributed notification information from other devices. |
| -b/--bundle      | Optional parameter, specifies the Bundle name for printing. |
| -u/--user-id     | Optional parameter, specifies the user ID for printing. |
| -h/--help        | Help information. |

**Example:**

```bash
# Print active notification information
anm dump -A
```

## Configuration Command (setting)

```bash
# Set notification parameters
anm setting [<options>]
```

**Configuration Command Parameter List:**

| Parameter | Description |
| --------- | ----------- |
| -c/--recent-count        | Set the maximum number of recent notifications stored in memory. |
| -e/--enable-notification | Set the notification enable/disable switch. |
| -h/--help                | Help information. |

**Example:**

```bash
# Set the maximum number of recent notifications stored in memory to 100
anm setting -c 100
```