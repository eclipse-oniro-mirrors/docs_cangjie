# Access Control Based on Device Classification and Data Classification

## Basic Concepts

Distributed data management implements classified and hierarchical protection for data, providing an access control mechanism based on data security labels and device security levels.

The higher the data security label and device security level, the stricter the encryption measures and access control measures, resulting in higher data security.

### Data Security Labels

According to the data classification and hierarchical specification requirements, data can be divided into four security levels: S1, S2, S3, and S4.

| Risk Level | Risk Criteria | Definition | Examples |
| ---------- | ------------- | ---------- | -------- |
| Critical | S4 | Special data types defined by industry laws and regulations, involving the most private information of individuals. Leakage, tampering, destruction, or deletion may cause significant adverse impacts on individuals or organizations. | Political views, religious and philosophical beliefs, trade union membership, genetic data, biometric information, health and sexual life status, sexual orientation, or device authentication credentials, personal credit card and other financial information. |
| High | S3 | Leakage, tampering, destruction, or deletion of data may cause severe adverse impacts on individuals or organizations. | Real-time precise location information, movement trajectories, etc. |
| Medium | S2 | Leakage, tampering, destruction, or deletion of data may cause serious adverse impacts on individuals or organizations. | Detailed communication addresses, names, nicknames, etc. |
| Low | S1 | Leakage, tampering, destruction, or deletion of data may cause limited adverse impacts on individuals or organizations. | Gender, nationality, user application records, etc. |

### Device Security Levels

<!--RP1-->
Based on device security capabilities (e.g., whether it has TEE, secure storage chips, etc.), device security levels are divided into five levels: SL1, SL2, SL3, SL4, and SL5. For example, development boards like rk3568 and hi3516 are low-security SL1 devices, while tablets are high-security SL4 devices.

During device networking, you can use the `hidumper -s 3511` command to view the device's security level. If no result is returned, you can start the corresponding process with `service_control start dslm_service` and then use the `hidumper` command to query. For example, the security level query for an rk3568 device is as follows:
<!--RP1End-->
<!--Del-->
![zh-cn_image_0000001542496993](./figures/zh-cn_image_0000001542496993.png)
<!--DelEnd-->

## Cross-Device Synchronization Access Control Mechanism

During cross-device data synchronization, data management performs access control based on data security labels and device security levels. The rule is: Data can be synchronized from the local device to the peer device only when the local device's data security label is not higher than the peer device's security level; otherwise, synchronization is prohibited. The specific access control matrix is as follows:

| Device Security Level | Synchronizable Data Security Labels |
| --------------------- | ----------------------------------- |
| SL1                   | S1                                  |
| SL2                   | S1~S2                               |
| SL3                   | S1~S3                               |
| SL4                   | S1~S4                               |
| SL5                   | S1~S4                               |

<!--RP2-->
For example, for development board devices like rk3568 and hi3516 with a security level of SL1, if a database with a data security label of S1 is created, the data in this database can be synchronized among these devices. If the database label is S2-S4, synchronization among these devices is not allowed.
<!--RP2End-->

## Scenario Introduction

The access control mechanism of the distributed database ensures security capabilities during data storage and synchronization. When creating a database, the security label of the database should be set reasonably based on the data classification and hierarchical specification to ensure consistency between the database content and the data label.

## Implementing Data Classification with Key-Value Databases

Key-value databases set the security level of the database through the `securityLevel` parameter. Here is an example of creating a database with a security level of S1.

For specific interfaces and functions, refer to [Distributed Key-Value Database](../reference/ArkData/cj-apis-distributed_kv_store.md).

> **Note:**
>
> In single-device usage scenarios, the KV database supports modifying the `securityLevel` parameter to upgrade the security level. The following points should be noted for database security level upgrades:
>
> * This operation is not supported for databases that require cross-device synchronization. Databases with different security levels cannot synchronize data. For databases requiring cross-device synchronization, it is recommended to create a new database with a higher security level.
> * This operation requires closing the current database first, modifying the `securityLevel` parameter to reset the database's security level, and then reopening the database.
> * This operation only supports upgrades, not downgrades. For example, upgrading from S2 to S3 is supported, but downgrading from S3 to S2 is not.

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

2. Create a key-value database with a security level of S1.

    <!-- compile -->

    ```cangjie
    // xxx.cj
    import kit.ArkData.{DistributedKVStore, KVManagerConfig}
    import ohos.business_exception.BusinessException
    import ohos.data.distributed_kv_store.*

    try {
        let context = globalAbilityContext.getOrThrow()
        let kvManagerConfig = KVManagerConfig(globalAbilityContext.getOrThrow(), "com.example.datamanagertest")
        // Create a KVManager instance
        let kvManager = DistributedKVStore.createKVManager(kvManagerConfig)
        Hilog.info(0, "cangjie", "Succeeded in creating KVManager.")

        let options = KVOptions(
            KVSecurityLevel.S1, // Set the security level to S1
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

## Implementing Data Classification with Relational Databases

Relational databases set the security level of the database through the `securityLevel` parameter. Here is an example of creating a database with a security level of S1.

For specific interfaces and functions, refer to [Relational Database](../reference/ArkData/cj-apis-relational_store.md).

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

2. Create a relational database with a security level of S1.

    <!-- compile -->

    ```cangjie
    // xxx.cj
    import kit.ArkData.{StoreConfig, getRdbStore}
    import ohos.business_exception.BusinessException
    import ohos.data.relational_store.*

    try {
        let context = globalAbilityContext.getOrThrow()
        let storeConfig = StoreConfig(
            RelationalStoreSecurityLevel.S1, // Set the security level to S1
            name: "RdbTest.db",
        )
        let rdbStore = getRdbStore(context, storeConfig)
        Hilog.info(0, "cangjie", "getRdbStore success")
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    // Perform other database-related operations
    // ...
    ```