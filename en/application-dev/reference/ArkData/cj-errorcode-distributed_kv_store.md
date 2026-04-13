# Distributed Key-Value Database Error Codes

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 15100001 Exceeded Maximum Subscription Limit

**Error Message**

Over max limits.

**Error Description**

The number of database subscriptions or open result sets has exceeded the maximum supported limit.

**Possible Causes**

1. When calling the database change subscription interface `on`, the number of database subscriptions has exceeded the maximum limit of 8.
2. When calling the result set acquisition interface `getResultSet`, the number of currently open result sets in the database has exceeded the maximum limit of 8.

**Resolution Steps**

1. If the number of database subscriptions has exceeded the limit when calling the `on` interface, cancel some subscriptions and try again.
2. If the number of open result sets has exceeded the limit when calling `getResultSet`, retry after close the database.

## 15100002 Changed Configuration When Opening Existing Database

**Error Message**

Open existed database with changed options.

**Error Description**

This error code indicates that the `options` configuration parameters have changed when calling the `getKVStore` interface to open an already created database.

**Possible Causes**

1. Attempting to create a new database using a `storeId` that already exists.
2. Attempting to modify the `options` parameter configuration of an already created database.

**Resolution Steps**

1. Before creating a new database, ensure the `storeId` does not duplicate an existing database name.
2. Currently, modifying the `options` parameters of an existing database is not supported. Delete the database and recreate it with new `options` parameters.

## 15100003 Database Corruption

**Error Message**

Database corrupted.

**Error Description**

This error code indicates that the database is corrupted when calling interfaces for operations such as adding, deleting, querying, or data synchronization.

**Possible Causes**

The database file is corrupted during operations such as adding, deleting, querying, or data synchronization.

**Resolution Steps**

1. If a backup exists, attempt to restore the database using the backup file.
2. If no backup is available, delete the database and recreate it.

## 15100004 Data Not Found

**Error Message**

Not found.

**Error Description**

This error code indicates that no relevant data was found when calling interfaces such as `deleteKVStore`, `sync`, or `get`.

**Possible Causes**

Relevant data was not found during database deletion, query, or synchronization operations. Possible reasons include:

1. The database does not exist or has already been deleted during a deletion operation.
2. The queried data does not exist or has been deleted during a query operation.
3. The database does not exist or has been deleted during a synchronization operation.

**Resolution Steps**

1. Before deleting a database, verify the database name or check for duplicate deletions.
2. Before querying data, ensure the query key is correct.
3. Before synchronizing data, confirm the relevant database has not been deleted.

## 15100005 Database or Result Set Already Closed

**Error Message**

Database or result set already closed.

**Error Description**

This error code indicates that the database or result set is in a closed state when calling related interfaces.

**Possible Causes**

The database or result set was manually closed before performing operations.

**Resolution Steps**

1. For database operations, reopen the database and retry the operation.
2. For result set operations, requery to obtain the result set and retry the operation.