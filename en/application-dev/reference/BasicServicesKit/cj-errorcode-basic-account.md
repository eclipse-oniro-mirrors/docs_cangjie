# Account Management Error Codes

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

The following error codes include system account, distributed account, and application account error codes.

## 12300001 System Service Exception

**Error Message**

The system service works abnormally.

**Possible Causes**

This error code indicates an abnormal system service operation. Possible causes include:

1. The account management service failed to start normally.
2. The IPC object for account management cannot be obtained.
3. Other services that account management depends on failed to start normally or their IPC objects cannot be obtained.
4. The service is not initialized.
5. Insufficient disk space.
6. File read/write exception.
7. Directory creation exception.
8. File creation/deletion exception.
9. Database read/write exception.

**Resolution Steps**

Please try again later or restart the device.

## 12300002 Invalid Parameter

**Error Message**

Invalid parameter.

**Possible Causes**

This error code indicates invalid input parameters. Possible causes include:

1. Username is empty.
2. System account username length exceeds 1024 characters.
3. Distributed account username length exceeds 256 characters.
4. System account ID is less than 0, less than 100, or greater than 1099.
5. Distributed account ID length exceeds 512 characters.
6. Unsupported event type provided for distributed account.
7. Domain name is empty.
8. Domain name length exceeds 128 characters.
9. Domain account is empty.
10. Domain account length exceeds 512 characters.
11. Constraint is empty.
12. Constraint length exceeds 128 characters.
13. Invalid authentication or query parameters provided.
14. System account avatar encoded string exceeds 4KB.
15. Distributed account avatar encoded string exceeds 2MB.
16. Non-JPG/PNG image provided.
17. Application account name length exceeds 512 characters.
18. Authentication type length exceeds 1024 characters.
19. Token length exceeds 1024 characters.
20. Key name length exceeds 1024 characters.
21. Custom data value length exceeds 1024 characters.
22. Invalid token.
23. Invalid context identifier.
24. Invalid credential identifier.

**Resolution Steps**

Please provide correct parameters.

## 12300003 Account Not Found

**Error Message**

The account does not exist.

**Possible Causes**

This error code indicates the target account does not exist. Possible causes include:

1. Querying/activating/deleting a non-existent account.
2. Querying/activating/deleting an already deleted account.
3. Setting constraints/username/avatar for a deleted account.
4. Updating a non-existent account.
5. Setting/revoking account information access authorization for a non-existent account.
6. Setting/deleting/querying password for a non-existent account.
7. Setting/deleting tokens for a non-existent account.
8. Setting additional information for a non-existent account.
9. Setting/deleting credentials for a non-existent account.
10. Setting custom data for a non-existent account.
11. Enabling distributed sync for a non-existent account.

**Resolution Steps**

Please verify the account existence.

## 12300004 Account Already Exists

**Error Message**

The account already exists.

**Possible Causes**

This error code indicates the account already exists. Possible causes include:

Creating an existing account.

**Resolution Steps**

Cancel the creation or retry with a different account name.

## 12300005 Multi-user Not Supported

**Error Message**

Multi-user is not supported.

**Possible Causes**

This error code indicates multi-user is not supported. Possible causes include:

Current device doesn't support multi-user mode, cannot create accounts.

**Resolution Steps**

Cannot create additional accounts. Please cancel the operation.

## 12300006 Unsupported Account Type

**Error Message**

The account type is not supported.

**Possible Causes**

This error code indicates an unsupported account type. Possible causes include:

Current device doesn't support creating the specified account type.

**Resolution Steps**

Please create other supported account types.

## 12300007 Account Limit Reached

**Error Message**

The number of accounts has reached the upper limit.

**Possible Causes**

This error code indicates the account limit has been reached. Possible causes include:

1000 system/application accounts already exist when attempting to create new ones.

**Resolution Steps**

Please delete other accounts before creating new ones.

## 12300008 Restricted Account

**Error Message**

The specified account is restricted.

**Possible Causes**

This error code indicates operation on a restricted account. Possible causes include:

1. Deleting system reserved users.
2. Querying constraint source type for system reserved users.
3. Creating accounts with IDs between 0-100.

**Resolution Steps**

Specified ID belongs to system reserved users and cannot be modified.

## 12300009 Account Already Activated

**Error Message**

The account has been activated.

**Possible Causes**

This error code indicates the account is already activated. Possible causes include:

Activating an already activated account.

**Resolution Steps**

The account is already active. No duplicate operation needed.

## 12300010 Account Service Busy

**Error Message**

The account service is busy.

**Possible Causes**

This error code indicates the account service is busy. Possible causes include:

1. Submitting duplicate requests in short time (repeated activations/settings).
2. Application account authentication sessions exceed 256, unable to process new requests.

**Resolution Steps**

Please wait and retry later with reduced frequency.

## 12300011 Event Listener Already Registered

**Error Message**

The event listener has been registered.

**Possible Causes**

This error code indicates duplicate listener registration. Possible causes include:

Current application registering an already registered listener with the system.

**Resolution Steps**

Please unregister first or use a new listener for registration.

## 12300012 Event Listener Not Registered

**Error Message**

The event listener has not been registered.

**Possible Causes**

This error code indicates unregistering a non-existent listener. Possible causes include:

Unregistering a listener that was never registered.

**Resolution Steps**

Please use a registered listener for unregistration.

## 12300013 Network Exception

**Error Message**

Network exception.

**Possible Causes**

This error code indicates network issues. Possible causes include:

1. No network connection;
2. Network connectivity issues;
3. Application lacks network permissions;
4. Unknown network errors;

**Resolution Steps**

1. Connect to network;
2. Ensure stable network connection;
3. Verify application network permissions;
4. Retry the operation;

## 12300014 Domain Account Not Authenticated

**Error Message**

The domain account is not authenticated.

**Possible Causes**

Domain account is not logged in.

**Resolution Steps**

Please log in to the domain account first.

## 12300015 Short Name Already Exists

**Error Message**

The short name already exists.

**Possible Causes**

The short name used for account creation already exists.

**Resolution Steps**

Please use a different non-existent short name.

## 12300016 Account Login Limit Reached

**Error Message**

The number of logged in accounts reaches the upper limit.

**Possible Causes**

The maximum number of logged-in accounts has been reached.

**Resolution Steps**

Log out existing accounts before logging in new ones.

## 12300101 Incorrect Credential

**Error Message**

The credential is incorrect.

**Possible Causes**

This error code indicates invalid credentials. Possible causes include:

1. Wrong password input;
2. Biometric mismatch;
3. Expired token;

**Resolution Steps**

Please provide correct and valid credentials.

## 12300102 Credential Not Found

**Error Message**

The credential does not exist.

**Possible Causes**

This error code indicates missing credentials. Possible causes include:

1. Authenticating with unregistered credential type.
2. Querying unregistered credential type.
3. Deleting unregistered credential type.

**Resolution Steps**

Please verify the credential type existence.

## 12300103 Credential Inputter Already Exists

**Error Message**

The credential inputer already exists.

**Possible Causes**

This error code indicates duplicate credential inputer registration. Possible causes include:

PIN inputer already registered and cannot be re-registered before unregistration.

**Resolution Steps**

Credential inputer already exists. No duplicate operation needed.

## 12300104 Credential Inputter Not Found

**Error Message**

The credential inputer is not found.

**Possible Causes**

This error code indicates that the credential inputter does not exist. Possible causes include:

The credential inputter was not registered during authentication, credential addition, or modification.

**Resolution Steps**

Register the credential inputter.

## 12300105 Trust Level Not Supported

**Error Message**

The trust level is not supported.

**Possible Causes**

This error code indicates that an unsupported trust level was provided. Possible causes include:

An unsupported trust level was passed to the system.

**Resolution Steps**

Enter a valid trust level.

## 12300106 Authentication Type Not Supported

**Error Message**

The authentication type is not supported.

**Possible Causes**

This error code indicates that an unsupported authentication type was provided. Possible causes include:

An unsupported authentication type was passed to the system.

**Resolution Steps**

Provide an authentication type supported by the system.

## 12300107 Authentication Type Does Not Exist

**Error Message**

The authentication type does not exist.

**Possible Causes**

This error code indicates that the authentication type does not exist. Possible causes include:

The specified authentication type does not exist when querying/deleting a token.

**Resolution Steps**

Use an existing authentication type for querying/deletion.

## 12300108 Authentication Session Does Not Exist

**Error Message**

The authentication session does not exist.

**Possible Causes**

This error code indicates that the session does not exist. Possible causes include:

Querying a non-existent session callback.

**Resolution Steps**

Use a successfully opened session ID to query the session callback.

## 12300109 Authentication, Credential Enrollment, or Update Operation Canceled

**Error Message**

The authentication, enrollment, or update operation is canceled.

**Possible Causes**

This error code indicates that the authentication, credential enrollment, or update operation was canceled. Possible causes include:

1. The user canceled the authentication operation during the process.
2. The user canceled the enrollment operation during credential enrollment.
3. The user canceled the update operation during credential enrollment.

**Resolution Steps**

Retry or terminate the authentication operation.

## 12300110 Authentication Locked

**Error Message**

The authentication is locked.

**Possible Causes**

This error code indicates that authentication is locked. Possible causes include:

The number of authentication failures exceeded the limit.

**Resolution Steps**

Authentication failures have exceeded the limit. Retry after `freezingTime`.

## 12300111 Authentication Timeout

**Error Message**

The authentication timed out.

**Possible Causes**

This error code indicates that authentication timed out. Possible causes include:

1. For system accounts, authentication or enrollment exceeded three minutes.
2. The authentication service timed out due to network issues.

**Resolution Steps**

1. Retry if authentication or enrollment timed out.
2. Ensure the network environment is stable and retry.

## 12300112 Authentication Service Busy

**Error Message**

The authentication service is busy.

**Possible Causes**

This error code indicates that the authentication service is busy. Possible causes include:

1. For system accounts, the total number of authentications exceeded five.
2. For third-party app accounts, the authenticator service is busy (case-dependent).

**Resolution Steps**

The authentication service is busy. Retry later.

## 12300113 Account Authentication Service Not Found

**Error Message**

The account authentication service does not exist.

**Possible Causes**

This error code indicates that the authentication service does not exist. Possible causes include:

For app accounts:
1. The app associated with the account does not support the authenticator service during authentication.
2. The app associated with the account does not support the authenticator service during implicit account addition.
3. The app associated with the account does not support the authenticator service during credential verification.
4. The specified app does not support the authenticator service when setting app authentication attributes.
5. The specified app does not support the authenticator service when checking account labels.

**Resolution Steps**

Cancel the operation or authenticate using an app that supports the authentication service.

## 12300114 Account Authentication Service Abnormal

**Error Message**

The account authentication service works abnormally.

**Possible Causes**

This error code indicates that the account authentication service is abnormal. Possible causes include:

1. An unknown error occurred in the identity authentication service.
2. The app authenticator does not comply with specifications.

**Resolution Steps**

1. Retry or restart the system.
2. Develop the app authenticator according to specifications.

## 12300115 Maximum Number of User Authentication Credentials Reached

**Error Message**

The number of credentials reaches the upper limit.

**Possible Causes**

1. An unknown error occurred in the identity authentication service.
2. The user already has a credential of the corresponding type and cannot add another.

**Resolution Steps**

1. Retry or restart the system.
2. Modify or delete existing credentials.

## 12300116 Credential Complexity Verification Failed

**Error Message**

Credential complexity verification failed.

**Possible Causes**

The provided credential is too simple.

**Resolution Steps**

Enter a credential that meets the required complexity (e.g., specific characters).

## 12300117 PIN Expired

**Error Message**

PIN is expired.

**Possible Causes**

The user's authentication PIN has expired.

**Resolution Steps**

Reset the PIN.

## 12400001 Application Not Found

**Error Message**

The application does not exist.

**Possible Causes**

This error code indicates that the application does not exist. Possible causes include:

1. The target application does not exist when setting access permissions.
2. The target application does not exist when setting open authorization.

**Resolution Steps**

Cancel the operation or retry using an installed application package name.

## 12400002 Custom Data Not Found

**Error Message**

The custom data does not exist.

**Possible Causes**

This error code indicates that the custom data does not exist. Possible causes include:

The specified key does not exist when querying account custom data.

**Resolution Steps**

Query using an existing custom data key.

## 12400003 Maximum Number of Custom Data Records Reached

**Error Message**

The number of custom data records reaches the upper limit.

**Possible Causes**

This error code indicates that the maximum number of custom data records has been reached. Possible causes include:

The target account already has 512 custom data records when attempting to set custom data.

**Resolution Steps**

Cancel the operation or delete existing custom data before retrying.

## 12400004 Maximum Number of Tokens Reached

**Error Message**

The number of tokens reaches the upper limit.

**Possible Causes**

This error code indicates that the maximum number of tokens has been reached. Possible causes include:

The target account already has 1024 tokens when attempting to add a token.

**Resolution Steps**

Cancel the operation or delete existing tokens before retrying.

## 12400005 Maximum Authorization List Size Reached

**Error Message**

The size of the authorization list reaches the upper limit.

**Possible Causes**

This error code indicates that the authorization list has reached its maximum size. Possible causes include:

The authorization list size exceeds 1024 when setting access/open authorization.

**Resolution Steps**

Cancel the operation or revoke existing access/open authorizations before retrying.
```