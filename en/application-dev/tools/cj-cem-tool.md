# CEM Tool  

The Common Event Manager (CEM) tool is designed to implement functionalities such as printing public event information and publishing public events. It provides developers with basic public event debugging and testing capabilities, including printing all public event subscribers, sent public events and their recipients, simulating public event publishing, and more.  

## Environment Requirements  

Before using this tool, developers need to obtain the [HDC tool](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-toolchain-hdc-guide.md) and execute the `hdc shell` command.  

## CEM Tool Command List  

| Command | Description |  
| ------- | ----------- |  
| `help`  | Help command, displays CEM-related help information. |  
| `publish` | Publish command, used to publish public events. |  
| `dump`  | Print command, used to print public event-related information. |  

## Help Command (`help`)  

```bash  
# Display CEM-related help information  
cem help  
```  

## Publish Command (`publish`)  

```bash  
# Publish a public event  
cem publish [<options>]  
```  

**Publish Command Parameter List:**  

| Parameter | Description |  
| --------- | ----------- |  
| `-e/--event` | Required parameter, specifies the event name to publish. |  
| `-o/--ordered` | Optional parameter, publishes an ordered event (default is unordered). |  
| `-c/--code` | Optional parameter, specifies the public event result code. |  
| `-d/--data` | Optional parameter, specifies the data carried by the public event. |  
| `-h/--help` | Help information. |  

**Examples:**  

```bash  
# Publish a public event named "testevent"  
cem publish --event "testevent"  
```  

```bash  
# Publish an ordered public event named "testevent" with a result code of 100 and data "this is data"  
cem publish -e "testevent" -o -c 100 -d "this is data"  
```  

## Print Command (`dump`)  

> **Note:**  
>  
> The current tool distinguishes between `eng` (engineering) and `user` versions. The `dump` command is only supported in the `eng` version. Using it in the `user` version will result in an error: `error: user version cannot use dump`.  

```bash  
# Print public event-related information  
cem dump [<options>]  
```  

**Print Command Parameter List:**  

| Parameter | Description |  
| --------- | ----------- |  
| `-a/--all` | Prints all sent public events and their details since boot. |  
| `-e/--event` | Queries detailed information about a specific event by name. |  
| `-h/--help` | Help information. |  

**Examples:**  

```bash  
# Print detailed information about the public event named "testevent"  
cem dump -e "testevent"  
```