# Implementing Data Persistence with Key-Value Databases

## Scenario Introduction

Key-value databases store data in key-value pairs. When the data to be stored does not involve complex relational models—such as storing product names with corresponding prices or employee IDs with today's attendance status—the low complexity of such data makes it more compatible across different database versions and device types. Therefore, key-value databases are recommended for persisting this type of data.

## Constraints and Limitations

- For device collaboration databases, each record must have a Key length ≤ 896 bytes and a Value length < 4 MB.
- For single-version databases, each record must have a Key length ≤ 1 KB and a Value length < 4 MB.
- Each application supports opening a maximum of 16 key-value distributed databases simultaneously.
- Blocking operations (e.g., modifying UI components) are not allowed in key-value database event callback methods.

## Interface Description

The following are key interfaces for key-value database persistence functionality, most of which are asynchronous. Asynchronous interfaces support both callback and Promise return types. The table below uses callback forms as examples. For more interfaces and usage details, refer to [Distributed Key-Value Database](../../../en/application-dev/reference/ArkData/cj-apis-distributed_kv_store.md).

| Interface Name | Description |
| -------- | -------- |
| createKVManager(config: KVManagerConfig): KVManager | Creates a KVManager instance for managing database objects. |
| getSingleKVStore(storeId: String, options: KVOptions): SingleKVStore | Creates and retrieves a single-version distributed key-value database with specified options and storeId. |
| getDeviceKVStore(storeId: String, options: KVOptions): DeviceKVStore | Creates and retrieves a multi-device collaboration database with specified options and storeId. |
| put(key: String, value: KVValueType): Unit | Adds a key-value pair of the specified type to the database. |
| get(key: String): KVValueType | Retrieves the value associated with the specified key. |
| delete(key: String): Unit | Deletes the data associated with the specified key from the database. |
| closeKVStore(appId: String, storeId: String): Unit | Closes the specified distributed key-value database using its storeId. |
| deleteKVStore(appId: String, storeId: String): Unit | Deletes the specified distributed key-value database using its storeId. |

## Development Steps

1. To use a key-value database, first obtain a KVManager instance to manage database objects. Example code:

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
            // Get context
            globalAbilityContext = this.context

            let kvManagerConfig = KVManagerConfig(globalAbilityContext.getOrThrow, "com.example.datamanagertest")
            try {
                // Create KVManager instance
                kvManager = DistributedKVStore.createKVManager(kvManagerConfig)
                // Proceed to create/retrieve database
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

2. Create and retrieve a key-value database. Example code:

    <!-- compile -->

    ```cangjie
    // xxx.cj
    import kit.ArkData.*
    import ohos.business_exception.BusinessException
    import ohos.data.distributed_kv_store.SingleKVStore

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

3. Use the put() method to insert data into the key-value database. Example code:

    <!-- compile -->

    ```cangjie
    // xxx.cj
    import ohos.data.distributed_kv_store.ValueType as KVValueType

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
    > If the Key already exists, put() will update its value; otherwise, it adds a new entry.

4. Use the get() method to retrieve the value of a specified key. Example code:

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

5. Use the delete() method to remove data associated with a specified key. Example code:

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

6. Close the specified distributed key-value database using its storeId. Example code:

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

7. Delete the specified distributed key-value database using its storeId. Example code:

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