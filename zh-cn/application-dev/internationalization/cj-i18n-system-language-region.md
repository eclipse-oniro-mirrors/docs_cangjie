# 系统语言与区域

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

## 实现原理

在设置的“语言和地区”中可以添加多种语言，多种语言形成的列表称为语言列表，列表中的第一个语言称为系统语言。系统地区是依据地区ID划分的特定地区。

系统语言和系统地区来源于系统设置，与应用偏好语言（`System.getAppPreferredLanguage()`）是两个不同的来源，取值可能不一致。

## 开发步骤

接口具体使用方法和说明请参考[System](../reference/LocalizationKit/cj-apis-i18n.md#class-system)的API接口文档。

1. 导入模块。

   <!-- compile -->

   ```cangjie
   import kit.LocalizationKit.*
   import kit.BasicServicesKit.*
   import kit.PerformanceAnalysisKit.Hilog
   import ohos.business_exception.*
   ```

2. 获取系统语言和系统地区。

   <!-- compile -->

   ```cangjie
   // index.cj

   let systemLanguage = System.getSystemLanguage() // 如果系统语言为简体中文，systemLanguage = 'zh-Hans'
   let systemRegion = System.getSystemRegion()     // 如果系统地区为中国，systemRegion = 'CN'
   Hilog.info(0, "test", "systemLanguage=${systemLanguage}, systemRegion=${systemRegion}")
   ```

3. 监听系统语言或系统地区变化。

   系统语言和系统地区发生变化时，系统会发布公共事件`Support.COMMON_EVENT_LOCALE_CHANGED`。订阅该公共事件后，可以在回调中重新获取系统语言和系统地区。订阅方法请参见[动态订阅公共事件](../basic-services/common-event/cj-common-event-subscription.md)。

   <!-- compile -->

   ```cangjie
   let events = [Support.COMMON_EVENT_LOCALE_CHANGED]
   let subscribeInfo = CommonEventSubscribeInfo(events)
   let subscriber = CommonEventManager.createSubscriber(subscribeInfo)
   let callback = {
       a: ?BusinessException, b: ?CommonEventData =>
           let systemLanguage = System.getSystemLanguage()
           let systemRegion = System.getSystemRegion()
           Hilog.info(0, "test", "systemLanguage=${systemLanguage}, systemRegion=${systemRegion}")
   }
   CommonEventManager.subscribe(subscriber, callback)
   ```
