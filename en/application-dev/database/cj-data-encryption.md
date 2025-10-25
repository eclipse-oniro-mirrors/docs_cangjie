# Database Encryption

## Scenario Description

To enhance database security, the database provides a secure and applicable encryption capability that effectively protects stored content. Through security methods like database encryption, it meets the confidentiality and integrity requirements of database storage, ensuring data is stored in ciphertext and operates in an encrypted state, thereby guaranteeing data security.

An encrypted database can only be accessed through interfaces; the database file cannot be opened by other means. The encryption property of a database is determined at creation and cannot be modified.

Both key-value databases and relational databases support encryption operations.

## Key-Value Database Encryption

For key-value databases, encryption is configured via the `encrypt` parameter in `options`, which defaults to `false` (no encryption). Setting `encrypt` to `true` enables encryption.

For specific interfaces and functionalities, refer to [Distributed Key-Value Database](../../../en/application-dev/reference/ArkData/cj-apis-distributed_kv_store.md).

1. Obtain the context.

    <!-- compile -->

    ```cangjie
    // main_ability.cj
    import kit.PerformanceAnalysisKit.Hilog
    import kit.AbilityKit.{UIAbility, AbilityStage, Want, LaunchParam, LaunchReason, UIAbilityContext}

    var globalAbilityContext: Option<UIAbilityContext> = Option<UIAbilityContext>.None

    class MainAbility <: UIAbility {
        public init() {
            super()
            registerSelf()
        }

        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            // Obtain the context
            globalAbilityContext = this.context

            match (launchParam.launchReason) {
                case LaunchReason.StartAbility => Hilog.info(0, "cangjie", "START_ABILITY")
                case _ => ()
            }
        } 
        // ...
    }
    ```

2. Configure key-value database encryption.

    <!-- compile -->

    ```cangjie
    // xxx.cj
    import kit.ArkData.{DistributedKVStore, KVManagerConfig}
    import ohos.business_exception.BusinessException
    import kit.AbilityKit.getStageContext
    import ohos.data.distributed_kv_store.Options as KVOptions
    import ohos.data.distributed_kv_store.SecurityLevel as KVSecurityLevel

    try {
        let context = globalAbilityContext.getOrThrow()
        let kvManagerConfig = KVManagerConfig(globalAbilityContext.getOrThrow(), "com.example.datamanagertest")
        // Create a KVManager instance
        let kvManager = DistributedKVStore.createKVManager(kvManagerConfig)
        Hilog.info(0, "cangjie", "Succeeded in creating KVManager.")

        let options = KVOptions(
            KVSecurityLevel.S3, // Set security level to S3
            createIfMissing: true,
            encrypt: true,
            backup: false,
            autoSync: false,
        )
        let kvStore = kvManager.getKVStore("storeId", options)
        Hilog.info(0, "cangjie", "getSingleKVStore success")
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    // Perform other database-related operations
    // ...
    ```

## Relational Database Encryption

For relational databases, encryption is configured via the `encrypt` property in `StoreConfig`, which defaults to `false` (no encryption). Setting `encrypt` to `true` enables encryption.

For specific interfaces and functionalities, refer to [Relational Database](../../../en/application-dev/reference/ArkData/cj-apis-relational_store.md).

1. Obtain the context.

    <!-- compile -->

    ```cangjie
    // main_ability.cj
    import kit.PerformanceAnalysisKit.Hilog
    import kit.AbilityKit.{UIAbility, AbilityStage, Want, LaunchParam, LaunchReason, UIAbilityContext}

    var globalAbilityContext: Option<UIAbilityContext> = Option<UIAbilityContext>.None

    class MainAbility <: UIAbility {
        public init() {
            super()
            registerSelf()
        }

        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            // Obtain the context
            globalAbilityContext = this.context

            match (launchParam.launchReason) {
                case LaunchReason.StartAbility => Hilog.info(0, "cangjie", "START_ABILITY")
                case _ => ()
            }
        } 
        // ...
    }
    ```

2. Configure relational database encryption.

    <!-- compile -->

    ```cangjie
    import kit.ArkData.{ getRdbStore, StoreConfig, RelationalStoreSecurityLevel }
    import ohos.business_exception.BusinessException

    try {
        // globalAbilityContext is obtained during Ability onCreate
        let context = globalAbilityContext.getOrThrow()
        let storeConfig = StoreConfig(
            RelationalStoreSecurityLevel.S3, // Database security level
            name: "RdbTest.db", // Database filename
            encrypt: true, // Enable database encryption
        )
        let rdbStore = getRdbStore(context, storeConfig)
        Hilog.info(0, "cangjie", "getRdbStore success")
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    // Perform other database-related operations
    // ...
    ```