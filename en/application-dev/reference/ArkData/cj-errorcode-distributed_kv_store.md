# Distributed Key-Value Database Error Codes

> **Note:**
>
> This document only introduces error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 15100001 Exceeded Maximum Subscription Limit

**Error Message**

Over max limits.

**Error Description**

The number of database subscriptions or open result sets has exceeded the maximum supported limit.

**Possible Causes**

1. When calling the database change subscription interface `on`, the number of database subscriptions has exceeded the maximum limit of 8.
2. When calling the result set acquisition interface `getResultSet`, the number of currently open result sets has exceeded the maximum limit of 8.

**Resolution Steps**

1. If the number of database subscriptions exceeds the limit when calling the `on` interface, cancel some subscriptions and retry.
2. If the number of open result sets exceeds the limit when calling `getResultSet`, close some result sets and retry.

## 15100002 Parameter Configuration Changed When Opening Existing Database

**Error Message**

Open existed database with changed options.

**Error Description**

This error indicates that when calling `getKVStore` to open an existing database, the `options` configuration parameters have changed.

**Possible Causes**

1. Attempting to create a new database using a storeId that already exists.
2. Attempting to modify the `options` parameter configuration of an existing database.

**Resolution Steps**

1. Before creating a new database, ensure the storeId doesn't duplicate any existing database names.
2. Currently, modifying `options` for existing databases is not supported. Delete the database and recreate it with new parameters.

## 15100003 Database Corruption

**Error Message**

Database corrupted.

**Error Description**

This error indicates database corruption when calling CRUD or data synchronization interfaces.

**Possible Causes**

Database files were corrupted during CRUD operations or data synchronization.

**Resolution Steps**

1. If a database backup exists, attempt restoration using the backup file.
2. If no backup exists, delete and recreate the database.

## 15100004 Data Not Found

**Error Message**

Not found.

**Error Description**

This error indicates missing data when calling `deleteKVStore`, `sync`, or `get` interfaces.

**Possible Causes**

1. During database deletion: the database doesn't exist or was already deleted.
2. During data queries: the target data doesn't exist or was deleted.
3. During data synchronization: the database doesn't exist or was deleted.

**Resolution Steps**

1. Verify database name and deletion status before deletion operations.
2. Verify query keywords before data queries.
3. Verify database existence before synchronization operations.

## 15100005 Database or Result Set Already Closed

**Error Message**

Database or result set already closed.

**Error Description**

This error occurs when operating on a closed database or result set.

**Possible Causes**

Manual closure of database/result set prior to operations.

**Resolution Steps**

1. For database operations: reopen the database before retrying.
2. For result set operations: requery to obtain a new result set before retrying.