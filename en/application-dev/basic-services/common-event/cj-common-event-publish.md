# Public Event Publishing

## Scenario Description

When needing to publish a custom public event, you can use the [publish()](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md#static-func-publishstring) method to publish the event. Published public events can carry data for subscribers to parse and process further.

> **Note:**
>
> Sticky public events that have already been published can still be received by later subscribers. Other public events require subscription before reception. For subscription, refer to the [Public Event Subscription section](./cj-common-event-subscription.md).

## Interface Description

For detailed interfaces, please refer to the [API documentation](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md#static-func-publishstring).

| Interface Name                                               | Description                  |
| ------------------------------------------------------------ | ---------------------------- |
| publish(event:&nbsp;String): Unit | Publish a public event.      |
| publish(event:&nbsp;String,&nbsp;options:&nbsp;[CommonEventPublishData](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md#struct-commoneventpublishdata)): Unit | Publish a public event with specified information. |

## Publishing Public Events Without Data

Public events without data can only be published as unordered events.

1. Import the module.

   <!-- compile -->

   ```cangjie
   import kit.BasicServicesKit.*
   ```

2. Pass the event name to be published and the callback function to publish the event.

   <!-- compile -->

   ```cangjie
   // Publish a public event, where the event field should be replaced with the actual event name.
   let support1 = Support.COMMON_EVENT_SCREEN_ON
   CommonEventManager.publish(support1)
   ```

## Publishing Public Events With Data

Public events with data can be published as unordered events, ordered events, or sticky events. This can be configured via the `isOrdered` and `isSticky` fields in the [CommonEventPublishData](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-common_event_manager.md#struct-commoneventpublishdata) parameter.

1. Import the module.

   <!-- compile -->

   ```cangjie
   import kit.BasicServicesKit.*
   ```

2. Construct the public event information to be published.

   <!-- compile -->

   ```cangjie
   // Public event related information
    let pData = CommonEventPublishData("com.example.myapplication", "newbee", 123321)
   ```

3. Pass the event name to be published, the specified information to be published, and the callback function to publish the event.

   <!-- compile -->

   ```cangjie
   // Publish a public event, where the event field should be replaced with the actual event name
   let support1 = Support.COMMON_EVENT_SCREEN_ON
   CommonEventManager.publish(support1, pData)
   ```