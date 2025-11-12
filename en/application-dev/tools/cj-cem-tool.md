# CEM Tool

The Common Event Manager (abbreviated as CEM) is a tool designed to implement functionalities such as printing public event information and publishing public events. It provides developers with fundamental public event debugging and testing capabilities, including printing all public event subscribers, sent public events and their recipients, simulating public event publishing, and more.

## Environment Requirements

Before using this tool, developers need to obtain the [HDC tool](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-toolchain-hdc-guide.md) and execute the `hdc shell` command.

## CEM Tool Command List

| Command | Description |
| ---- | --- |
| help | Help command, used to display CEM-related help information. |
| publish | Publish command, used to publish public events. |
| dump | Print command, used to print public event-related information. |

## Help Command (help)

```bash
# Display CEM-related help information
cem help
```

## Publish Command (publish)

```bash
# Publish a public event
cem publish [<options>]
```

**Publish Command Parameter List:**

| Parameter | Description  |
| ------------ | ------- |
| -e/--event   | Required parameter, specifies the name of the event to be published.  |
| -o/--ordered | Optional parameter, publishes an ordered event (default is unordered).  |
| -c/--code   | Optional parameter, specifies the result code of the public event.  |
| -d/--data   | Optional parameter, specifies the data carried by the public event. |
| -h/--help   | Help information.     |

**Examples:**

```bash
# Publish a public event named "testevent"
cem publish --event "testevent"
```

```bash
# Publish an ordered public event named "testevent" with a result code of 100 and carrying the data "this is data"
cem publish -e "testevent" -o -c 100 -d "this is data"
```

## Print Command (dump)

> **Note:**
>
> The current tool distinguishes between `eng` and `user` versions. The `dump` command is only supported in `eng` versions. Using it in `user` versions will result in the error: `error: user version cannot use dump`.

```bash
# Print public event-related information
cem dump [<options>]
```

**Print Command Parameter List:**

| Parameter   | Description   |
| ---- | ------ |
| -a/--all   | Prints all sent public events and their detailed information since system boot. |
| -e/--event | Queries detailed information for a specific event name.  |
| -h/--help  | Help information.  |

**Examples:**

```bash
# Print detailed information for the public event named "testevent"
cem dump -e "testevent"
```