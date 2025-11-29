# Database Backup and Recovery

## Scenario Introduction

When an application is performing a critical operation that cannot be interrupted, such as writing transactions involving multiple related tables, each table write is performed individually, but the transactional relationships between tables must not be split.

If issues arise during the operation, developers can use the recovery function to restore the database to its previous state and re-execute the database operations.

In scenarios where the database is tampered with, deleted, or the device loses power, the database may become unavailable due to data loss, corruption, or dirty data. The database's backup and recovery capabilities can restore it to a usable state.

Both key-value databases and relational databases support backup and recovery operations. Additionally, key-value databases support deleting database backups to free up local storage space.

## Key-Value Database Backup, Recovery, and Deletion

For key-value databases, backups are implemented via the `backup` interface, recovery via the `restore` interface, and backup deletion via the `deletebackup` interface. For specific interfaces and functionalities, refer to [Distributed Key-Value Database](../reference/ArkData/cj-apis-distributed_kv_store.md).

1. Create a database.

    a. Obtain the context.

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
                case LaunchReason.StartAbility => Hilog.info(0, "cangjie", "StartAbility")
                case _ => ()
            }
        } 
        // ...
    }
    ```

    b. Create a kvStore.

    <!-- compile -->

    ```cangjie
    // xxx.cj
    import kit.ArkData.*
    import ohos.business_exception.BusinessException
    import ohos.data.distributed_kv_store.KVManager
    import ohos.data.distributed_kv_store.SingleKVStore
    import ohos.data.relational_store.*

    var kvManager: Option<KVManager> = Option<KVManager>.None
    var kvStore: Option<SingleKVStore> = Option<SingleKVStore>.None

    try {
        // 1. Create kvManager
        let kvManagerConfig = KVManagerConfig(globalAbilityContext.getOrThrow(), "com.example.datamanagertest")
        kvManager = DistributedKVStore.createKVManager(kvManagerConfig)
        // 2. Configure database parameters
        let options = KVOptions(
            KVSecurityLevel.S3,
            createIfMissing: true,
            encrypt: true,
            backup: false,
            autoSync: false,
        )
        // 3. Create kvStore
        kvStore = kvManager.getOrThrow().getKVStore("storeId", options)
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
   ```

2. Insert data using the `put()` method.

    <!-- compile -->

    ```cangjie
    import ohos.data.distributed_kv_store.*

    const KEY_TEST_STRING_ELEMENT: String = "key_test_string"
    const VALUE_TEST_STRING_ELEMENT: String = "value_test_string"

    try {
        kvStore.getOrThrow().put(KEY_TEST_STRING_ELEMENT, KVValueType.StringValue(VALUE_TEST_STRING_ELEMENT))
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```

3. Backup data using the `backup()` method.

    <!-- compile -->

    ```cangjie
    try {
        kvStore.getOrThrow().backup("BK001")
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```

4. Delete data using the `delete()` method (simulating accidental deletion or tampering scenarios).

    <!-- compile -->

    ```cangjie
    try {
        kvStore.getOrThrow().delete(KEY_TEST_STRING_ELEMENT)
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```

5. Recover data using the `restore()` method.

    <!-- compile -->

    ```cangjie
    try {
        kvStore.getOrThrow().restore("BK001")
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```

## Relational Database Backup

During database operations or storage processes, unexpected database exceptions may occur due to various reasons. The relational database's backup capability can be used as needed to ensure reliable and efficient data recovery when the database becomes abnormal, maintaining normal business operations.

Relational databases support two backup methods: manual backup and automatic backup (available only to system applications).

### Manual Backup

Manual backup is implemented by calling the [`backup`](../reference/ArkData/cj-apis-relational_store.md#func-backupstring) interface. Example:

<!-- compile -->

```cangjie
import kit.ArkData.*
import ohos.business_exception.BusinessException
import ohos.data.relational_store.*

var rdbStore_: Option<RdbStore> = Option<RdbStore>.None
let storeConfig_ = StoreConfig(
    RelationalStoreSecurityLevel.S3, // Database security level
    name: "RdbTest.db", // Database filename
    encrypt: false, // Optional parameter, specifies whether the database is encrypted (default: false)
)

try {
    let store = getRdbStore(globalAbilityContext.getOrThrow(), storeConfig_)
    store.executeSql("CREATE TABLE EMPLOYEE(ID int NOT NULL, NAME varchar(255) NOT NULL, AGE int, SALARY float NOT NULL, CODES Bit NOT NULL, PRIMARY KEY (Id))")
    /**
     * "Backup.db" is the backup database filename, which is backed up in the same path as RdbStore by default.
     * An absolute path can also be specified: "/data/storage/el2/database/Backup.db". The file path must exist; directories are not created automatically.
     */
    store.backup("Backup.db")
    rdbStore_ = store
} catch (e: BusinessException) {
    Hilog.error(0, "ErrorCode: ${e.code}", e.message)
}
```

## Relational Database Data Recovery

In cases where the database becomes abnormal, after rebuilding the database, pre-backed-up data can be used for recovery.

### Recovering Manually Backed-Up Data

Relational databases support manual backup via the `backup` interface and manual recovery via the `restore` interface.

The recovery process and key code snippets are as follows. For complete example code, implement it in conjunction with the context of relational database backup and rebuilding.

1. Throw database exception error codes.

    <!-- compile -->

    ```cangjie
    import ohos.data.relational_store.RdbPredicates
    import ohos.data.relational_store.RdbStore

    try {
        let predicates = RdbPredicates("EMPLOYEE")
        let columns = ["ID", "NAME", "AGE", "SALARY", "CODES"]
        let resultSet = rdbStore_.getOrThrow().query(predicates, columns: columns)
        /*
         * Business logic for insert, delete, and update operations
         * ...
         */
        // Throw an exception
        if (resultSet.rowCount == -1) {
            resultSet.isColumnNull(0)
        }
        // Other interfaces like resultSet.goToFirstRow(), resultSet.count, etc., may also throw exceptions
        while (resultSet.goToNextRow()) {
            Hilog.info(0, "info", "${resultSet.getRow().size}")
        }
        resultSet.close()
    } catch (e: BusinessException) {
        if (e.code == 14800011) {
            // Proceed with the steps below, i.e., close all result sets before performing data recovery
        }
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```

2. Close all open result sets.

    <!-- compile -->

    ```cangjie
    import ohos.data.relational_store.ResultSet
    try {
        // All open result sets
        var resultSets: Array<ResultSet> = Array<ResultSet>()
        // Add result sets to resultSets
        // ...
        // Close all open result sets using resultSet.close()
        for (i in (0..resultSets.size)) {
            resultSets[i].close()
        }
    } catch (e: BusinessException) {
        if (e.code != 14800014) {
            Hilog.error(0, "ErrorCode: ${e.code}", e.message)
        }
    }
   ```

3. Call the `restore` interface to recover data.

    <!-- compile -->

    ```cangjie
    import kit.CoreFileKit.FileIo
    try {
        /**
         * "Backup.db" is the backup database filename, which is searched for in the same path as the current store by default.
         * If an absolute path was specified during backup, e.g., "/data/storage/el2/database/Backup.db", the absolute path must be provided.
         */
        let backup = '/data/storage/el2/database/Backup.db' + '/entry/rdb/Backup.db'
        if (!FileIo.access(backup)) {
            Hilog.info(0, "info", "no backup file")
        }
        // Call the restore interface to recover data
        rdbStore_.getOrThrow().restore("Backup.db")
        Hilog.info(0, "info","Succeeded in backup data.")
    } catch (e: BusinessException) {
        Hilog.error(0, "ErrorCode: ${e.code}", e.message)
    }
    ```