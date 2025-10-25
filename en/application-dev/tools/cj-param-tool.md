# param Tool

param is a system parameter operation tool provided for developers, which only supports standard systems.

## Environment Requirements

- Obtain the <!--Del-->[<!--DelEnd-->hdc tool<!--Del-->](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-toolchain-hdc-guide.md)<!--DelEnd--> and execute `hdc shell`.
- Ensure the device is properly connected.

## param Command List

| Option | Description |
| ----------------- | ------------------------------------------ |
| -h | Get the commands supported by param. |
| ls [-r] [name] | Display system parameter information matching the specified name. With "-r", it retrieves information based on parameter permissions; without "-r", it directly fetches parameter information. |
| get [name] | Get the value of the specified system parameter by name; if no name is specified, returns all system parameters. |
| set name value | Set the value of the specified system parameter by name to the given value. |
| wait name [value] [timeout] | Synchronously wait for the specified system parameter to match the given value. The value supports fuzzy matching, e.g., "\*" matches any value, "val\*" matches values starting with "val". Timeout specifies the wait duration (in seconds), defaulting to 30s if not set. |
| save | Save persist parameters to the workspace. |

## Get Commands Supported by param

- To get the commands supported by param, use the following format:

  ```bash
  param -h
  ```

## Get System Parameter Information

- Display system parameter information matching the specified name with the following command:

  ```bash
  param ls [-r] [name]
  ```

  **Examples:**

  ![ls-integrity](./figures/param-ls-integrity.png)
  ![ls-part](./figures/param-ls-part.png)
  ![ls](./figures/param-ls.png)

## Get System Parameter Values

- Get the value of the specified system parameter with the following command:

  ```bash
  param get [name]
  ```

  **Example:**

  ![get](./figures/param-get.png)

## Set System Parameter Values

- Set the value of the specified system parameter with the following command:

  ```bash
  param set name value
  ```

  **Example:**

  ![set](./figures/param-set.png)

## Wait for System Parameter Value Match

- Synchronously wait for the specified system parameter to match the given value with the following command:

  ```bash
  param wait name [value] [timeout]
  ```

  **Example:**

  ![wait](./figures/param-wait.png)

## Save Persist Parameters

- Save persist parameters to the workspace with the following command:

  ```bash
  param save
  ```

  **Example:**

  ![save](./figures/param-save.png)