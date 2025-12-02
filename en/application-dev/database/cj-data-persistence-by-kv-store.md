# Implementing Data Persistence with Key-Value Databases

## Scenario Description

Key-value databases store data in key-value pairs. When the data to be stored does not have a complex relational model—such as storing product names and their corresponding prices, or employee IDs and their attendance status for the day—a key-value database is recommended for persistence due to its low complexity, which ensures better compatibility across different database versions and device types.

## Constraints and Limitations

- For device collaboration databases, each record must have a Key length ≤ 896 bytes and a Value length < 4 MB.
- For single-version databases, each record must have a Key length ≤ 1 KB and a Value length < 4 MB.
- Each application can open a maximum of 16 key-value distributed databases simultaneously.
- Blocking operations, such as modifying UI components, are not allowed in key-value database event callback methods.

## Interface Description

The following are the key interfaces for key-value database persistence functionality. Most are asynchronous interfaces, which support both callback and Promise return types. The table below uses the callback form as an example. For more interfaces and usage details, refer to [Distributed Key-Value Database](../reference/ArkData/cj-apis-distributed_kv_store.md).

| Interface Name | Description |
| -------- | -------- |
| createKVManager(config: KVManagerConfig): KVManager | Creates a KVManager instance for managing database objects. |
| getSingleKVStore(storeId: String, options: KVOptions): SingleKVStore | Creates and retrieves a single-version distributed key-value database with the specified `options` and `storeId`. |
| getDeviceKVStore(storeId: String, options: KVOptions): DeviceKVStore | Creates and retrieves a multi-device collaboration database with the specified `options` and `storeId`. |
| put(key: String, value: KVValueType): Unit | Adds a key-value pair of the specified type to the database. |
| get(key: String): KVValueType | Retrieves the value associated with the specified key. |
| delete(key: String): Unit | Deletes the data associated with the specified key from the database. |
| closeKVStore(appId: String, storeId: String): Unit | Closes the specified distributed key-value database using the `storeId`. |
| deleteKVStore(appId: String, storeId: String): Unit | Deletes the specified distributed key-value database using the `storeId`. |

## Development Steps

1. To use a key-value database, first obtain a `KVManager` instance to manage database objects. Example code:

    <!-- compile -->

    ```cangjie
    // main_ability.cj
    import kit.ArkData.{ DistributedKVStore, KVManagerConfig }
    import kit.PerformanceAnalysisKit.Hilog
    import kit.AbilityKit.{UIAbility, AbilityStage, Want, LaunchParam, LaunchReason, UIAbilityContext}
    import ohos.business_exception.BusinessException
    import ohos.data.distributed_kv_store.KVManager

    var kvManager: Option<KVManager> = Option<KVManager>.None
    var globalAbilityContext: Option<UIAbilityContext> = Option<UIAbilityContext>.None

    class MainAbility <: UIAbility {
        public init() {
            super()
            registerSelf()
        }

        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            // Get the context
            globalAbilityContext = this.context

            let kvManagerConfig = KVManagerConfig(globalAbilityContext.getOrThrow(), "com.example.datamanagertest")
            try {
                // Create a KVManager instance
                kvManager = DistributedKVStore.createKVManager(kvManagerConfig)
                // Proceed to create and retrieve the database
                // ...
            } catch (e: BusinessException) {
                Hilog.error(0, "ErrorCode: ${e.code}", e.message)
            }
            match (launchParam.launchReason) {
                case LaunchReason.START_ABILITY => Hilog.info(0, "cangjie", "START_ABILITY")
                case _ => ()
            }
        }
        // ...
    }
    ```

2. Create and retrieve the key-value database. Example code:

    To create and retrieve the key-value database, the following packages need to be imported:

    <!-- compile -->

    ```cangjie
    // xxx.cj
    import kit.ArkData.*
    import ohos.business_exception.BusinessException
    import ohos.data.distributed_kv_store.SingleKVStore
    ```

    The core code for create and retrieve the key-value database is:

    <!-- compile -->

    ```cangjie
    var kvStore: Option<SingleKVStore> = Option<SingleKVStore>.None

    try {
        let options = KVOptions(
            KVSecurityLevel.S1,
            createIfMissing: true,
            encrypt: false,
            backup: false,
            autoSync: false
        )
        kvStore = kvManager.getOrThrow().getKVStore("storeId", options)
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```

3. Use the `put()` method to insert data into the key-value database. Example code:

    To insert data, the following packages need to be imported:

    <!-- compile -->

    ```cangjie
    // xxx.cj
    import ohos.data.distributed_kv_store.KVValueType
    ```

    The core code for insert data is:

    <!-- compile -->

    ```cangjie
    const KEY_TEST_STRING_ELEMENT: String = "key_test_string"
    const VALUE_TEST_STRING_ELEMENT: String = "value_test_string"

    try {
        kvStore.getOrThrow().put(KEY_TEST_STRING_ELEMENT, KVValueType.StringValue(VALUE_TEST_STRING_ELEMENT))
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```

    > **Note:**
    >
    > If the Key already exists, `put()` will update its value; otherwise, it will add a new entry.

4. Use the `get()` method to retrieve the value associated with a specified key. Example code:

    <!-- compile -->

    ```cangjie
    // xxx.cj
    try {
        let singleKVStore = kvStore.getOrThrow()
        singleKVStore.put(KEY_TEST_STRING_ELEMENT, KVValueType.StringValue(VALUE_TEST_STRING_ELEMENT))
        Hilog.info(0, "cangjie", "Succeeded in putting data.")
        let value = singleKVStore.get(KEY_TEST_STRING_ELEMENT)
        match (value) {
            case StringValue(v) => Hilog.info(0, "cangjie", "The obtained value is a String")
            case _ => Hilog.info(0, "cangjie", "The obtained value is not a string.")
        }
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
   ```

5. Use the `delete()` method to remove data associated with a specified key. Example code:

    <!-- compile -->

    ```cangjie
    // xxx.cj
    try {
        let singleKVStore = kvStore.getOrThrow()
        singleKVStore.put(KEY_TEST_STRING_ELEMENT, KVValueType.StringValue(VALUE_TEST_STRING_ELEMENT))
        singleKVStore.delete(KEY_TEST_STRING_ELEMENT)
        Hilog.info(0, "cangjie", "delete data success.")
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```

6. Close the specified distributed key-value database using its `storeId`. Example code:

    <!-- compile -->

    ```cangjie
    // xxx.cj
    try {
        kvManager.getOrThrow().closeKVStore("com.example.datamanagertest", "storeId")
        Hilog.info(0, "cangjie", "closeKVStore success.")
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```

7. Delete the specified distributed key-value database using its `storeId`. Example code:

    <!-- compile -->

    ```cangjie
    // xxx.cj
    try {
        kvManager.getOrThrow().deleteKVStore("com.example.datamanagertest", "storeId")
        Hilog.info(0, "cangjie", "deleteKVStore success.")
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```