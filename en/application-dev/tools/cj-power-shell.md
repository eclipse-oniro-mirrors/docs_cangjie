# Power-Shell Tool

Power-Shell is a tool that implements functions such as device power state transitions, providing developers with basic device power state debugging capabilities, including screen off, wake-up, power mode settings, etc.

## Environment Requirements

<!--RP1-->
Before using this tool, developers need to obtain the [hdc tool](../tools/cj-hdc.md) and execute `hdc shell`.
<!--RP1End-->

## Power-Shell Command List

| Command | Description |
| -------- | -------- |
| help | Help command, displays supported command information for power-shell. |
| setmode | Power mode setting command, used to configure the current device's power mode. |
| wakeup | Screen wake command, used to wake the system and turn on the screen. |
| suspend | Screen off command, used to suspend the system and turn off the screen. |
| timeout | Auto screen-off command, used to override or restore the auto screen-off time set in system settings. |

## Help Command

```bash
# Display help information
power-shell help
```

## Set Power Mode Command

```bash
power-shell setmode
```

**Power Mode Command List:**

| Command     | Description       |
| -------- | ------- |
| power-shell setmode -h | Displays supported command information for setmode. |
| power-shell setmode 600 | Normal mode. |
| power-shell setmode 601 | Power-saving mode. |
| power-shell setmode 602 | Performance mode. |
| power-shell setmode 603 | Ultra power-saving mode. |

Examples:

```bash
# Set device power state to normal mode
power-shell setmode 600
# Set device power state to power-saving mode
power-shell setmode 601
# Set device power state to performance mode
power-shell setmode 602
# Set device power state to ultra power-saving mode
power-shell setmode 603
```

## Screen Wake Command

```bash
power-shell wakeup
```

**Screen Wake Command List:**

| Command  | Description   |
| ---------- | -------- |
| power-shell wakeup | Turns on the screen. |

Example:

```bash
# Shell command to turn on the screen
power-shell wakeup
```

## Screen Off Command

```bash
power-shell suspend
```

**Screen Off Command List:**

| Command    | Description    |
| ---------- | --------- |
| power-shell suspend  | Turns off the screen. |

Example:

```bash
# Shell command to turn off the screen
power-shell suspend
```

## Auto Screen-Off Command

```bash
power-shell timeout
```

**Auto Screen-Off Command Parameters:**

| Parameter       | Description   |
| ---------- | ----------- |
| -o \<time> | Required parameter, sets auto screen-off time. [time] is in milliseconds. |
| -r | Required parameter, restores the auto screen-off time set in current system settings. |

Examples:

```bash
# Auto screen-off time in system settings is 30 seconds
# Shell command to set auto screen-off time to 15000 milliseconds
power-shell timeout -o 15000
# Restore system auto screen-off settings (now 30 seconds)
power-shell timeout -r
```