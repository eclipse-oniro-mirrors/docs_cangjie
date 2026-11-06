# Interface Call Exception Error Codes

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 100001 Interface Call Exception Error Code

**Error Message**

When used as an error code of [Animator](./cj-apis-uicontext-animator.md), the error message is: "The specified page is not found or the object property list is not obtained.".

When used as an error code of [PromptAction](./cj-apis-uicontext-promptaction.md), the error message is: "Internal error.".

When used as an error code of [ComponentSnapshot](./cj-apis-uicontext-componentsnapshot.md), the error message is: "Invalid ID.".

**Error Description**

When used as an error code of [Animator](./cj-apis-uicontext-animator.md) and [PromptAction](./cj-apis-uicontext-promptaction.md), this error code is reported when an internal exception occurs that cannot be resolved by the developer, along with a description of the specific type of internal error.

When used as an error code of [ComponentSnapshot](./cj-apis-uicontext-componentsnapshot.md), this error code is triggered when the internal state is abnormal.

**Possible Causes**

When used as an error code of [Animator](./cj-apis-uicontext-animator.md), the possible causes are: failure to obtain the rendering engine, parameter parsing failure, etc.

When used as an error code of [PromptAction](./cj-apis-uicontext-promptaction.md), the possible causes are: failure to obtain the rendering engine, parameter parsing failure, unclear UI context, etc.

When used as an error code of [ComponentSnapshot](./cj-apis-uicontext-componentsnapshot.md), the possible causes are: failure to obtain the correct UI instance, null pointer exception, UI instance internal state validation exception, component not mounted on the tree so the node cannot be found, snapshot size exceeding the hardware limit (the limit varies by hardware platform), etc.

**Resolution Steps**

NA
