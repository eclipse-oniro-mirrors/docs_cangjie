# Relational Database Error Codes

> **Note:**
>
> This document only introduces error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 14800000 Internal Error

**Error Message**

Inner error.

**Error Description**

Internal error.

**Possible Causes**

Check the error log first for detailed error information. Main causes include:

1. SQL execution exception.
2. Internal state exception.
3. Incorrect interface usage.
4. System errors such as null pointer, insufficient memory, abnormal restart of data service, I/O error, IPC exception, JS engine exception, etc.

**Resolution Steps**

1. Developers should verify the correctness of SQL statements and predicates.
2. Developers should check if objects are being used after being closed.
3. Developers should ensure interfaces are used correctly as per documentation.
4. Try retrying. If the issue persists, prompt users to restart the application, upgrade the application, or update the device version.

## 14800010 Invalid Database Path

**Error Message**

Invalid database path.

**Error Description**

The database path is invalid.

**Possible Causes**

Invalid database path.

**Resolution Steps**

Check the provided database path.

## 14800011 Database File Corrupted

**Error Message**

Database corrupted.

**Error Description**

This error code indicates that the database is corrupted when calling interfaces for operations like insert, delete, query, or data synchronization.

**Possible Causes**

The database file is corrupted during operations such as insert, delete, query, or data synchronization.

**Resolution Steps**

1. If a backup exists, attempt to restore the database using the backup file.
2. If no backup exists, try deleting and recreating the database.

## 14800012 Result Set Empty or Invalid Position

**Error Message**

Row out of bounds.

**Error Description**

The result set is empty or the specified position is invalid.

**Possible Causes**

The result set is empty or the specified row number exceeds the valid range [0, m - 1], where m = resultsetV9.rowCount.

**Resolution Steps**

Check if the current result set is empty or if the specified position is valid.

## 14800013 Column Value Null or Incompatible Column Type

**Error Message**

Column out of bounds.

**Error Description**

The column value is null or the column type is incompatible with the current interface call.

**Possible Causes**

1. The result set is empty.
2. The current row number exceeds the range [0, m - 1], where m = resultsetV9.rowCount.
3. The current column number exceeds the range [0, n - 1], where n = resultsetV9.columnCount.
4. The current column data type is not supported by the interface.

**Resolution Steps**

1. Check if the result set is empty.
2. Verify if the current row or column number is out of bounds.
3. Ensure the current column data type is supported.

## 14800014 Database or Result Set Closed

**Error Message**

Already closed.

**Error Description**

The database or result set is closed.

**Possible Causes**

Objects with close interfaces like RdbStore or ResultSet have either been closed or failed to open successfully.

**Resolution Steps**

Reopen the RdbStore or requery to obtain a new ResultSet.

## 14800015 Database Not Responding

**Error Message**

The database does not respond.

**Error Description**

The database is not responding.

**Possible Causes**

Read, write, attach, or detach operations are in progress, preventing the current operation from executing within the specified time (default 2s).

**Resolution Steps**

Retry the operation.

## 14800016 Database Alias Already in Use

**Error Message**

The database is already attached.

**Error Description**

The alias of the attached database is already in use.

**Possible Causes**

The alias of the attached database is already in use.

**Resolution Steps**

Either skip attaching the database or modify the alias of the attached database.

## 14800017 Critical Configuration Changed

**Error Message**

Config changed.

**Error Description**

Critical database configurations have been changed.

**Possible Causes**

Changes in critical configurations such as area, isEncrypt, or securityLevel.

**Resolution Steps**

Either maintain the original configuration or export data using the original configuration, delete the old database, create a new one with the new configuration, and import the data.

## 14800018 No Data Matches the Condition

**Error Message**

No data meets the condition.

**Error Description**

The SQL statement is incorrect, and no data matching the condition was found.

**Possible Causes**

The SQL statement does not correctly query the result set.

**Resolution Steps**

Write a correct query statement or add data to the database before querying.

## 14800019 SQL Must Be a Query Statement

**Error Message**

The SQL must be a query statement.

**Error Description**

The SQL must be a query statement.

**Possible Causes**

The SQL statement does not comply with the specifications, causing the query to fail.

**Resolution Steps**

When the SQL statement fails due to non-compliance, rewrite it to meet the specifications.

## 14800021 SQLite: Generic Error

**Error Message**

SQLite: Generic error.

**Error Description**

SQLite: Generic error.

**Possible Causes**

Errors during SQL execution, such as:

1. Inserting or updating a non-existent table.
2. Inserting or updating a non-existent column.
3. Calling an undefined function. Refer to SQLITE_ERROR for related scenarios.

**Resolution Steps**

Analyze the erroneous SQL statement to identify the issue.

## 14800022 SQLite: Callback Request Aborted

**Error Message**

SQLite: Callback routine requested an abort.

**Error Description**

SQLite: Callback request aborted.

**Possible Causes**

1. Typically occurs when using SQLite's custom function mechanism, where the callback is aborted.
2. Refer to SQLITE_ABORT for related scenarios.

**Resolution Steps**

Check the implementation of SQLite's callback functions to ensure correctness.

## 14800023 SQLite: Access Permission Denied

**Error Message**

SQLite: Access permission denied.

**Error Description**

SQLite access permission denied.

**Possible Causes**

1. Operating system-level permission issues, where SQLite attempts to access or modify a file without sufficient permissions.
2. Refer to SQLITE_PERM for related scenarios.

**Resolution Steps**

1. Ensure the file is not read-only; if it is, remove the read-only attribute.
2. Check file and folder permissions to ensure the current user has sufficient read/write permissions.
3. Verify the file system is not read-only; if it is, change it to writable.
4. Ensure no other processes are locking the database file; if so, close the process occupying the file.
5. When handling permission issues, ensure sufficient permissions to modify relevant files or folders.

## 14800024 SQLite: Database File Locked

**Error Message**

SQLite: The database file is locked.

**Error Description**

SQLite database file is locked.

**Possible Causes**

1. Two processes of the same application (e.g., UIability and datashareability) open the same database for insert, delete, or update operations, or processes within the same group from different applications open the same database for such operations.
2. Refer to SQLITE_BUSY for related scenarios.

**Resolution Steps**

1. Avoid concurrent database operations by processes.
2. Wait and retry after some time.

## 14800025 SQLite: Table Locked

**Error Message**

SQLite: A table in the database is locked.

**Error Description**

SQLite: A table in the database is locked.

**Possible Causes**

1. Attempting to write to an SQLite database while the file is locked by another process, possibly due to an ongoing transaction or other lock mechanisms.
2. Refer to SQLITE_LOCKED for related scenarios.

**Resolution Steps**

1. Ensure no other processes or threads are writing to the database file.
2. If using transactions, ensure no write operations are performed between starting and committing the transaction.
3. Check for other lock mechanisms (e.g., file locks) that may prevent writing.
4. If database connection objects are not properly closed, ensure they are closed after operations.
5. In multi-threaded environments, ensure database operations are locked to prevent race conditions.

## 14800026 SQLite: Out of Memory

**Error Message**

SQLite: The database is out of memory.

**Error Description**

SQLite: Out of memory.

**Possible Causes**

Insufficient database memory, possibly due to excessive data volume or inadequate memory allocation.

**Resolution Steps**

Reduce data volume or increase memory allocation.

## 14800027 SQLite: Attempt to Write Readonly Database

**Error Message**

SQLite: Attempt to write a readonly database.

**Error Description**

SQLite: Attempt to write a readonly database.

**Possible Causes**

1. Attempting to write to an SQLite database opened in read-only mode, possibly due to file permissions, read-only file system, or the database being marked as read-only.
2. Refer to SQLITE_READONLY for related scenarios.

**Resolution Steps**

1. Ensure sufficient permissions to write to the database file.
2. If the file system is read-only, change it to writable.
3. Confirm that the database was not opened with read-only parameters.

## 14800028 SQLite: Disk I/O Error

**Error Message**

SQLite: Some kind of disk I/O error occurred.

**Error Description**

SQLite encountered a disk I/O error.

**Possible Causes**

Possible reasons include but are not limited to:

1. File does not exist.
2. File is read-only.
3. Insufficient disk space.
4. File corruption.
5. Refer to SQLITE_IOERR for related scenarios.

**Resolution Steps**

1. Check if the file path is correct and the file exists.
2. Ensure the file is not set to read-only.
3. Verify disk space and free up unnecessary files if needed.
4. Check file permissions to ensure the application has sufficient read/write permissions.

## 14800029 SQLite: Database Full

**Error Message**

SQLite: The database is full.

**Error Description**

SQLite database is full.

**Possible Causes**

The database is full, possibly due to excessive data volume or insufficient disk space.

**Resolution Steps**

Reduce data volume or increase disk space.## 14800030 SQLite: Unable to Open Database File

**Error Message**

SQLite: Unable to open the database file.

**Error Description**

SQLite: Unable to open the database file.

**Possible Causes**

1. The file does not exist, and creating a new database failed.
2. The file exists, but the database file is corrupted.
3. File permission issues prevent SQLite from reading/writing the file.
4. Insufficient disk space.
5. Refer to error scenarios related to SQLITE_CANTOPEN.

**Resolution Steps**

1. Verify the database file path is correct. Check file permissions to ensure the application has sufficient read/write access.
2. Confirm there is sufficient disk space.

## 14800031 SQLite: TEXT or BLOB Exceeds Size Limit

**Error Message**

SQLite: TEXT or BLOB exceeds size limit.

**Error Description**

SQLite: TEXT or BLOB exceeds size limit.

**Possible Causes**

1. The query result set exceeds SQLite's processing size limit.
2. Refer to error scenarios related to SQLITE_TOOBIG.

**Resolution Steps**

Break down large queries into smaller ones, processing data in batches.

## 14800032 SQLite: Abort Due to Constraint Violation

**Error Message**

SQLite: Abort due to constraint violation.

**Error Description**

SQLite: Abort due to constraint violation.

**Possible Causes**

1. A database write operation violated integrity constraints.
2. Refer to error scenarios related to SQLITE_CONSTRAINT.

**Resolution Steps**

Check if the inserted/updated data violates any constraints.

## 14800033 SQLite: Data Type Mismatch

**Error Message**

SQLite: Data type mismatch.

**Error Description**

SQLite: Data type mismatch.

**Possible Causes**

1. Data types in an SQL statement conflict with stored database types.
2. Refer to error scenarios related to SQLITE_MISMATCH.

**Resolution Steps**

Verify column data types in the SQL statement. Ensure inserted/updated/queried data matches column types.

## 14800034 SQLite: Incorrect Library Usage

**Error Message**

SQLite: Library used incorrectly.

**Error Description**

SQLite: Incorrect library usage.

**Possible Causes**

1. Indicates improper database operations or context. Common scenarios:
    - Initiating new operations before completing current ones.
    - Operating on closed database connections.
    - Using released or invalid database objects.
2. Refer to error scenarios related to SQLITE_MISUSE.

**Resolution Steps**

1. Ensure proper synchronization between database operations (e.g., using locks).
2. Verify connections are open before use and closed after operations.
3. Ensure all database objects are properly released after use.

## 14800047 WAL File Size Exceeds Default Limit

**Error Message**

The WAL file size exceeds the default limit.

**Error Description**

WAL file size exceeds the default limit (200MB).

**Possible Causes**

Continuous insert/update/delete operations during open read transactions or unclosed result sets cause WAL file expansion.

**Resolution Steps**

Check for unclosed result sets or transactions. Close all result sets and transactions.

## 14800050 Failed to Obtain Subscription Service

**Error Message**

Failed to obtain subscription service.

**Error Description**

Failed to obtain subscription service.

**Possible Causes**

The current platform doesn't support subscription services.

**Resolution Steps**

Deploy subscription services on the current platform.

## 14801001 Context Not in Stage Model

**Error Message**

Only supported in stage mode.

**Error Description**

This operation only supports Stage model.

**Possible Causes**

Current context is not in Stage model.

**Resolution Steps**

Switch context to Stage model.

## 14801002 Invalid dataGroupId in storeConfig

**Error Message**

The data group id is not valid.

**Error Description**

Invalid dataGroupId parameter used.

**Possible Causes**

The dataGroupId wasn't properly obtained from the app market.

**Resolution Steps**

Apply for dataGroupId from the app market and pass it correctly.

## 14800051 Distributed Table Type Mismatch

**Error Message**

The type of the distributed table does not match.

**Error Description**

Inconsistent distributed table types set for the same database table.

**Possible Causes**

Conflicting distributed table types assigned to the same table. See [DistributedType](../ArkData/cj-apis-relational_store.md#enum-distributedtype).

**Resolution Steps**

Maintain consistent distributed table types. Tables configured for device-device sync cannot be reused for device-cloud sync.