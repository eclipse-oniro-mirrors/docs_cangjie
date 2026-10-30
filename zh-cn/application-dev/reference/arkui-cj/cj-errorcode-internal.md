# 接口调用异常错误码

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](../cj-errorcode-universal.md)。

## 100001 接口调用异常错误码

**错误信息**

作为[Animator](./cj-apis-uicontext-animator.md)的错误码时，错误信息为："The specified page is not found or the object property list is not obtained."。

作为[PromptAction](./cj-apis-uicontext-promptaction.md)的错误码时，错误信息为："Internal error."。

作为[ComponentSnapshot](./cj-apis-uicontext-componentsnapshot.md)的错误码时，错误信息为："The builder is not a valid build function."。

**错误描述**

作为[Animator](./cj-apis-uicontext-animator.md)和[PromptAction](./cj-apis-uicontext-promptaction.md)的错误码时，出现了由系统内部产生的异常错误，开发者无法通过修改自身代码解决，系统会报此错误码，并描述具体是哪种内部错误。

作为[ComponentSnapshot](./cj-apis-uicontext-componentsnapshot.md)的错误码时，该错误码在内部状态出现异常时被触发。

**可能原因**

作为[Animator](./cj-apis-uicontext-animator.md)的错误码时，可能原因为：未成功获取渲染引擎、解析参数失败等。

作为[PromptAction](./cj-apis-uicontext-promptaction.md)的错误码时，可能原因为：未成功获取渲染引擎、解析参数失败、UI上下文不明确等。

作为[ComponentSnapshot](./cj-apis-uicontext-componentsnapshot.md)的错误码时，可能原因为：无法获取正确的UI实例、空指针异常、UI实例内部状态校验异常、组件未上树无法查询到节点、截图尺寸超过硬件限制（不同硬件平台的限制值有所不同）等。

**处理步骤**

NA
