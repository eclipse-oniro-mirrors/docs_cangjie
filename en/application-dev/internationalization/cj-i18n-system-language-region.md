# System Language and Region

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## How It Works

You can add multiple languages in **Language & region** in **Settings**. The list formed by multiple languages is called a language list, and the first language in the list is called the system language. The system region is a specific region divided based on the region ID.

The system language and system region come from system settings, which are different from the application preferred language (`System.getAppPreferredLanguage()`). Their values may be inconsistent.

## How to Develop

For details about how to use the APIs, see the API document of [System](../reference/LocalizationKit/cj-apis-i18n.md#class-system).

1. Import the modules.

   <!-- compile -->

   ```cangjie
   import kit.LocalizationKit.*
   import kit.BasicServicesKit.*
   import kit.PerformanceAnalysisKit.Hilog
   import ohos.business_exception.*
   ```

2. Obtain the system language and system region.

   <!-- compile -->

   ```cangjie
   // index.cj

   let systemLanguage = System.getSystemLanguage() // If the system language is simplified Chinese, systemLanguage = 'zh-Hans'
   let systemRegion = System.getSystemRegion()     // If the system region is China, systemRegion = 'CN'
   Hilog.info(0, "test", "systemLanguage=${systemLanguage}, systemRegion=${systemRegion}")
   ```

3. Listen for system language or system region changes.

   When the system language or system region changes, the system publishes the common event `Support.COMMON_EVENT_LOCALE_CHANGED`. After subscribing to this common event, you can obtain the system language and system region again in the callback. For details about the subscription, see [Dynamic Subscription to Common Events](../basic-services/common-event/cj-common-event-subscription.md).

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
