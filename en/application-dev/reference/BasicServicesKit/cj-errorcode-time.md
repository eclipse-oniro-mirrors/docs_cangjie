# Time and Timezone Service Error Codes

## -1 Time and Timezone Service Exception

**Error Message**

  The parameter check failed or permission denied or system error.

**Error Description**

Parameter validation failed, permission verification failed, or time and timezone service exception.

**Possible Causes**

This error code represents a generic error code. The specific exception can be determined based on the error message. Possible causes include:

1. Parameter validation failed due to invalid input parameters.
2. Permission verification failed due to unconfigured permissions. The application lacks ohos.permission.SET_TIME for setting time or ohos.permission.SET_TIME_ZONE for setting timezone.
3. System runtime exception. Common kernel errors such as memory allocation or multi-threading processing failures.

**Resolution Steps**

1. For parameter validation failure: Verify that all parameters are passed according to requirements.
2. For permission verification failure: Configure ohos.permission.SET_TIME for time setting or ohos.permission.SET_TIME_ZONE for timezone setting in the application.
3. For system runtime exception: Check whether sufficient memory is available.