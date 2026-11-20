# Pasteboard Error Codes

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

> **Note:**
>
> The following describes only error codes specific to this module. For general error codes, see [Universal Error Codes](../cj-errorcode-universal.md).

## 12900001 Index Out of Range

**Error Message**

The index is out of range.

**Error Description**

The specified index is outside the valid range when a pasteboard data record is accessed.

**Possible Causes**

The index is less than 0 or greater than or equal to the number of records in the PasteData object.

**Resolution**

Use an index that is greater than or equal to 0 and less than the number of records in the PasteData object. Check the record count before the operation.

## 12900005 Internal Data Processing Timeout

**Error Message**

Excessive processing time for internal data.

**Error Description**

The pasteboard service times out while processing internal data.

**Possible Causes**

The data volume is too large, the system is overloaded, or the pasteboard service is abnormal.

**Resolution**

Reduce the data volume per operation and try again later. If the problem persists, check the pasteboard service status.

## 27787277 Another Copy or Paste Operation in Progress

**Error Message**

Another copy or paste operation is in progress.

**Error Description**

A copy or paste operation is already in progress, and a new operation cannot be started at the same time.

**Possible Causes**

A new operation is started before the previous copy or paste operation is complete.

**Resolution**

Wait until the previous operation is complete and try again. Perform copy and paste operations in sequence.

## 27787278 Copying Prohibited

**Error Message**

Replication is prohibited.

**Error Description**

The current pasteboard content or application state does not allow copying.

**Possible Causes**

The content has copy restrictions, or the current application does not meet the copying conditions.

**Resolution**

Check the copy restrictions of the content and the current application state, and try again in a scenario where copying is allowed.
