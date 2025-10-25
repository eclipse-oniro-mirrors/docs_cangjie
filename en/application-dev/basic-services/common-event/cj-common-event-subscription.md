# Dynamic Subscription to Public Events

## Scenario Description

Dynamic subscription refers to subscribing to a public event while an application is running. During runtime, if a subscribed event is published, the application that subscribed to this event will receive the event along with its transmitted parameters.

For example, if an application wishes to receive low battery level events during its operation and reduce its power consumption accordingly, it can dynamically subscribe to the low battery event. Upon receiving this event, the application can shut down non-essential tasks to lower power consumption.

Subscribing to certain system public events requires [requesting permissions](../../security/AccessToken/cj-determine-application-mode.md) first.

> **Note:**
>
> The lifecycle of the subscriber object must be managed by the integrating party. It should be actively destroyed and released when no longer in use to prevent memory leaks.

## Interface Description

For detailed interfaces, refer to the [API Documentation](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md).

| Interface Name | Description |
| -------- | -------- |
| createSubscriber(subscribeInfo:&nbsp;[CommonEventSubscribeInfo](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md#class-commoneventsubscribeinfo)): [CommonEventSubscriber](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md#class-commoneventsubscriber)| Creates a subscriber object. |
| subscribe(subscriber:&nbsp;[CommonEventSubscriber](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md#class-commoneventsubscriber),&nbsp;callback: ([CommonEventData](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md#struct-commoneventdata)) -> Unit): Unit | Subscribes to a public event. |

## Development Steps

1. Import the module.

   <!-- compile -->

   ```cangjie
   import kit.BasicServicesKit.*
   ```

2. Create subscriber information. For detailed data types and parameters of subscriber information, refer to the [CommonEventSubscribeInfo](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md#class-commoneventsubscribeinfo) documentation.

   <!-- compile -->

   ```cangjie
   // Used to store the successfully created subscriber object for subsequent subscription and unsubscription actions
   let subscriber: CommonEventSubscriber
   // Subscriber information, where the event field should be replaced with the actual event name
   let support1 = Support.COMMON_EVENT_SCREEN_ON
   let events = [support1]
   let subscribeInfo = CommonEventSubscribeInfo(events)
   ```

3. Create a subscriber and store the returned subscriber object `subscriber` for performing subsequent operations such as subscription, unsubscription, and receiving event callbacks.

   <!-- compile -->

   ```cangjie
   // Create subscriber callback
   subscriber = CommonEventManager.createSubscriber(subscribeInfo)
   ```

4. Create a subscription callback function, which will be triggered when an event is received. The callback function returns `data`, which contains the public event name, data carried by the publisher, and other information. For detailed parameters and data types of public event data, refer to the [CommonEventData](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md#struct-commoneventdata) documentation.

   <!-- compile -->

   ```cangjie
      // Public event subscription callback
   func callback(c: CommonEventData): Unit {
         AppLog.info("=======================================")
         AppLog.info("event of p is = ${c.event}")
         AppLog.info("p of p is = ${c .parameters .size}")
         AppLog.info("callback execute success!")
   }
   CommonEventManager.subscribe(subscriber, callback)
   ```