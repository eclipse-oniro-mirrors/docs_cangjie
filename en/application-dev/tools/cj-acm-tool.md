# acm Tool

Account Manager (referred to as acm) is a tool that enables account creation, deletion, querying, and other functionalities. It provides developers with basic capabilities to manage local accounts, such as creating and deleting accounts.

> **Note:**
>
> Before using this tool, developers need to obtain the [hdc tool](../tools/cj-hdc.md) and execute `hdc shell`.

**acm Tool Command List**

| Command | Description |
| :-------- | :-------- |
| help | Help command, displays supported command information for acm. |
| create | Create command, used to create an account. Note: Requires root privileges to use this command. |
| delete | Delete command, used to delete an account. Note: Requires root privileges to use this command. |
| dump | Query command, used to retrieve account-related information. Note: Requires root privileges to use this command. |
| switch | Switch command, used to switch between accounts. Note: Requires root privileges to use this command. |
| deactivate | Deactivate command, used to deactivate an account. Note: Requires root privileges to use this command. |
| set | Set constraints command, used to configure account constraints. Note: Requires root privileges to use this command. |

## help

**Usage:**

```bash
acm help
```

**Display Information**

Shows help information related to acm.

## create

**Usage:**

```bash
# Display help command
acm create -h
# Create an account with a specified name and type
acm create -n <accountName> -t <accountType> [-s <shortName>] [-l <disallowed-install-hap-list>]
```

**Display Information**

When account creation is successful, displays "create the local account successfully."; if creation fails, displays the corresponding failure message.

**Create Command Parameter List**

| Parameter | Description |
| :--------| :-------------------------- |
| -h | Optional parameter. Displays supported command information for create. |
| -n | Required parameter. Specifies the name of the new account. |
| -t | Required parameter. Specifies the account type for the new account. Account types include admin (administrator account), normal (standard account), guest (guest account), and private (private account). |
| -s | Optional parameter. Specifies the short name for the new account. |
| -l | Optional parameter. Specifies the preset application blacklist for the new account. |

## delete

**Usage:**

```bash
# Display help command
acm delete -h
# Delete an account with a specified ID
acm delete -i <accountId>
```

**Display Information**

When account deletion is successful, displays "delete the local account successfully."; if deletion fails, displays the corresponding failure message.

**Delete Command Parameter List**

| Parameter | Description |
| :-----| :-------------------------- |
| -h | Optional parameter. Displays supported command information for delete. |
| -i | Required parameter. Specifies the ID of the account to be deleted. |

## dump

**Usage:**

```bash
# Display help command
acm dump -h
# Query information for all accounts
acm dump -a
# Query information for an account with a specified ID
acm dump -i <accountId>
```

**Display Information**

When the query is successful, displays the corresponding account information; if the query fails, displays the corresponding failure message.

**Query Command Parameter List**

| Parameter | Description |
| :------| :-------------------------- |
| -h | Optional parameter. Displays supported command information for dump. |
| -a | Required parameter. Indicates querying information for all accounts. |
| -i | Required parameter. Specifies the account ID to query information for the corresponding account. |

## switch

**Usage:**

```bash
# Display help command
acm switch -h
# Switch to an account with a specified ID
acm switch -i <accountId>
```

**Display Information**

When account switching is successful, displays "switch the local account successfully."; if switching fails, displays the corresponding failure message.

**Switch Command Parameter List**

| Parameter | Description |
| :----------| :-------------------------- |
| -h | Optional parameter. Displays supported command information for switch. |
| -i | Required parameter. Specifies the ID of the account to switch to. |

## deactivate

**Usage:**

```bash
# Display help command
acm deactivate -h
# Deactivate all accounts
acm deactivate -a
# Deactivate an account with a specified ID
acm deactivate -i <accountId>
```

**Display Information**

When account deactivation is successful, displays "deactivate the local account successfully."; if deactivation fails, displays the corresponding failure message.

**Deactivate Command Parameter List**

| Parameter | Description |
| :--------- | :-------------------------- |
| -h | Optional parameter. Displays supported command information for deactivate. |
| -a | Required parameter. Indicates deactivating all accounts. |
| -i | Required parameter. Specifies the account ID to deactivate the corresponding account. |

## set

**Usage:**

```bash
# Display help command
acm set -h
# Set constraints for an account with a specified ID
acm set -i <accountId> -c <constraints> [-e]
```

**Display Information**

When constraint setting is successful, displays "set constraints for the local account successfully."; if setting fails, displays the corresponding failure message.

**Set Constraints Command Parameter List**

| Parameter | Description |
| :----------| :-------------------------- |
| -h | Optional parameter. Displays supported command information for set. |
| -i | Required parameter. Specifies the account ID. |
| -c | Required parameter. Specifies the constraint set to be configured, with each constraint in the set separated by ';'. |
| -e | Optional parameter. Including this option adds constraints; excluding it removes constraints. |