# Key Agreement (Cangjie)

Taking X25519 as the key agreement type and keys used exclusively within HUKS as an example, complete the key agreement. For specific scenarios and supported algorithm specifications, refer to [Supported Algorithms for Key Generation](./cj-huks-key-generation-overview.md#supported-algorithms).

## Development Steps

### Generate Keys

Device A and Device B each generate an asymmetric key pair. For details, refer to [Key Generation](./cj-huks-key-generation-overview.md) or [Key Import](./cj-huks-key-import-overview.md).

During key generation, the parameter `HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG` (optional) can be specified to indicate whether the agreed key derived from this key is managed by HUKS.

- When the TAG is set to `HUKS_STORAGE_ONLY_USED_IN_HUKS`, it means the agreed key derived from this key is managed by HUKS, ensuring the key's entire lifecycle remains within a secure environment.

- When the TAG is set to `HUKS_STORAGE_KEY_EXPORT_ALLOWED`, it means the agreed key derived from this key is returned to the caller for management, and the application is responsible for ensuring key security.

- If the TAG is not explicitly set, the agreed key derived from this key can either be managed by HUKS or returned to the caller. The application can later choose how to protect the key during the agreement process.

### Export Keys

Device A and Device B export the public key material of their asymmetric key pairs. For details, refer to [Key Export](./cj-huks-export-key.md).

### Key Agreement

Device A and Device B each derive a shared key based on their private key and the peer device's public key.

During key agreement, the parameter `HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG` (optional) can be specified to indicate whether the agreed key is managed by HUKS.

| Generation | Agreement | Specification |
| :-------- | :-------- | :-------- |
| `HUKS_STORAGE_ONLY_USED_IN_HUKS` | `HUKS_STORAGE_ONLY_USED_IN_HUKS` | Key managed by HUKS |
| `HUKS_STORAGE_KEY_EXPORT_ALLOWED` | `HUKS_STORAGE_KEY_EXPORT_ALLOWED` | Key returned to caller for management |
| TAG not specified | `HUKS_STORAGE_ONLY_USED_IN_HUKS` | Key managed by HUKS |
| TAG not specified | `HUKS_STORAGE_KEY_EXPORT_ALLOWED` | Key returned to caller for management |
| TAG not specified | TAG not specified | Key returned to caller for management |

The TAG value specified during agreement must not conflict with the TAG value specified during generation. The table lists only valid combinations.

### Delete Keys

When keys are no longer needed, Device A and Device B must delete them. For details, refer to [Key Deletion](./cj-huks-delete-key.md).

## Examples

Below are examples of key agreement using X25519 and DH keys.

- X25519 Asymmetric Key Agreement Example

    <!-- compile -->

    ```cangjie
    /*
     * The following demonstrates X25519 key operations
     */
    import kit.PerformanceAnalysisKit.Hilog
    import kit.BasicServicesKit.*
    import kit.CoreFileKit.*
    import kit.AbilityKit.*
    import kit.UniversalKeystoreKit.*

    func loggerInfo(str: String) {
        Hilog.info(0, "CangjieTest", str)
    }

    /*
     * Define key aliases and encapsulate key property parameter sets
     */
    let srcKeyAliasFirst = "AgreeX25519KeyFirstAlias"
    let srcKeyAliasSecond = "AgreeX25519KeySecondAlias"
    let agreeX25519InData = 'AgreeX25519TestIndata'
    var finishOutData: ?Array<UInt8> = None
    var handle: ?HuksHandleId = None
    var exportKey: ?Array<UInt8> = None
    var exportKeyFirst: ?Array<UInt8> = None
    var exportKeySecond: ?Array<UInt8> = None
    /* Assemble key generation parameter set */
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_X25519,
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE,
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_CURVE25519_KEY_SIZE_256,
        ),
        HuksParam(
            HuksTag.HuksTagDigest,
            HuksKeyDigest.HUKS_DIGEST_NONE,
        ),
        HuksParam(
            HuksTag.HuksTagPadding,
            HuksKeyPadding.HUKS_PADDING_NONE,
        ),
        HuksParam(
            HuksTag.HuksTagBlockMode,
            HuksCipherMode.HUKS_MODE_CBC,
        ),
        HuksParam(
            HuksTag.HuksTagDerivedAgreedKeyStorageFlag,
            HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
        )
    ]
    var huksOptions: HuksOptions = HuksOptions(
        properties: properties,
        inData: Bytes()
    )
    /* Assemble first agreement parameter set */
    let finishProperties1: Array<HuksParam> = [
        HuksParam(
            HuksTag.HuksTagDerivedAgreedKeyStorageFlag,
            HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
        ),
        HuksParam(
            HuksTag.HuksTagIsKeyAlias,
            HuksParamValue.BooleanValue(true)
        ),
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_AES,
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_AES_KEY_SIZE_256,
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksParamValue.Uint32Value(1 | 2),
        ),
        HuksParam(
            HuksTag.HuksTagDigest,
            HuksKeyDigest.HUKS_DIGEST_NONE,
        ),
        HuksParam(
            HuksTag.HuksTagPadding,
            HuksKeyPadding.HUKS_PADDING_NONE,
        ),
        HuksParam(
            HuksTag.HuksTagBlockMode,
            HuksCipherMode.HUKS_MODE_ECB,
        ),
        HuksParam(
            HuksTag.HuksTagKeyAlias,
            HuksParamValue.BytesValue((srcKeyAliasFirst + 'final').toArray())
        )
    ]
    let finishOptionsFirst: HuksOptions = HuksOptions(
        properties: finishProperties1,
        inData: StringToUint8Array(agreeX25519InData)
    )
    /* Assemble second agreement parameter set */
    let finishProperties2: Array<HuksParam> = [
        HuksParam(
            HuksTag.HuksTagDerivedAgreedKeyStorageFlag,
            HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
        ),
        HuksParam(
            HuksTag.HuksTagIsKeyAlias,
            HuksParamValue.BooleanValue(true)
        ),
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_AES,
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_AES_KEY_SIZE_256,
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksParamValue.Uint32Value(1 | 2),
        ),
        HuksParam(
            HuksTag.HuksTagDigest,
            HuksKeyDigest.HUKS_DIGEST_NONE,
        ),
        HuksParam(
            HuksTag.HuksTagPadding,
            HuksKeyPadding.HUKS_PADDING_NONE,
        ),
        HuksParam(
            HuksTag.HuksTagBlockMode,
            HuksCipherMode.HUKS_MODE_ECB,
        ),
        HuksParam(
            HuksTag.HuksTagKeyAlias,
            HuksParamValue.BytesValue((srcKeyAliasSecond + 'final').toArray())
        )
    ]
    let finishOptionsSecond: HuksOptions = HuksOptions(
        properties: finishProperties2,
        inData: StringToUint8Array(agreeX25519InData)
    )

    func StringToUint8Array(str: String) {
        return str.toArray()
    }

    class throwObject {
        var isThrow: Bool = false

        init(isThrow: Bool) {
            this.isThrow = isThrow
        }
    }

    /* Generate key */
    func generateKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: throwObject) {
        try {
            generateKeyItem(keyAlias, huksOptions)
        } catch (e: Exception) {
            throwObject.isThrow = true
            throw e
        }
    }

    /* Call generateKeyItem to generate key */
    func publicGenKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
        loggerInfo("enter generateKeyItem")
        let throwObject: throwObject = throwObject(false)
        try {
            generateKeyItem(keyAlias, huksOptions, throwObject)
        } catch (e: Exception) {
            loggerInfo("generateKeyItem input arg invalid, ${e}")
        }
    }

    /* Initialize key session interface and obtain a handle (required) and challenge value (optional) */
    func initSession(keyAlias: String, huksOptions: HuksOptions, throwObject: throwObject) {
        return try {
            initSession(keyAlias, huksOptions).handle
        } catch (e: Exception) {
            throwObject.isThrow = true
            throw e
        }
    }

    /* Call initSession to obtain handle */
    func publicInitFunc(keyAlias: String, huksOptions: HuksOptions) {
        loggerInfo("enter doInit")
        let throwObject: throwObject = throwObject(false)
        try {
            handle = initSession(keyAlias, huksOptions, throwObject)
        } catch (e: Exception) {
            loggerInfo("doInit input arg invalid, ${e}")
        }
    }

    /* Incrementally add key operation data and perform corresponding key operations, outputting processed data */
    func updateSession(handle: HuksHandleId, huksOptions: HuksOptions, throwObject: throwObject) {
        return try {
            updateSession(handle, huksOptions)
        } catch (e: Exception) {
            throwObject.isThrow = true
            throw e
        }
    }

    /* Call updateSession for agreement operation */
    func publicUpdateFunc(handle: HuksHandleId, huksOptions: HuksOptions) {
        loggerInfo("enter doUpdate")
        let throwObject: throwObject = throwObject(false)
        try {
            updateSession(handle, huksOptions, throwObject)
        } catch (e: Exception) {
            loggerInfo("doUpdate input arg invalid, ${e}")
        }
    }

    /* Terminate key session and perform corresponding key operations, outputting processed data */
    func finishSession(handle: HuksHandleId, huksOptions: HuksOptions, throwObject: throwObject) {
        return try {
            finishSession(handle, huksOptions)
        } catch (e: Exception) {
            throwObject.isThrow = true
            throw e
        }
    }

    /* Call finishSession to complete operation */
    func publicFinishFunc(handle: HuksHandleId, huksOptions: HuksOptions) {
        loggerInfo("enter doFinish")
        let throwObject: throwObject = throwObject(false)
        try {
            finishOutData = finishSession(handle, huksOptions, throwObject)
        } catch (e: Exception) {
            loggerInfo("doFinish input arg invalid, ${e}")
        }
    }

    /* Export key */
    func exportKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: throwObject) {
        return try {
            exportKeyItem(keyAlias, huksOptions)
        } catch (e: Exception) {
            throwObject.isThrow = true
            throw e
        }
    }

    /* Call exportKeyItem for public key export operation */
    func publicExportKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
        loggerInfo("enter export")
        let throwObject: throwObject = throwObject(false)
        try {
            exportKey = exportKeyItem(keyAlias, huksOptions, throwObject)
        } catch (e: Exception) {
            loggerInfo("exportKeyItem input arg invalid, ${e}")
        }
    }

    ```

- DH Key Agreement Example

    <!-- compile -->

    ```cangjie
    /*
     * The following demonstrates DH key operations
     */
    import kit.PerformanceAnalysisKit.Hilog
    import kit.BasicServicesKit.*
    import kit.CoreFileKit.*
    import kit.AbilityKit.*
    import kit.UniversalKeystoreKit.*
    import std.math.numeric.BigInt

    func loggerInfo(str: String) {
        Hilog.info(0, "CangjieTest", str)
    }

    func StringToUint8Array(str: String) {
        return str.toArray()
    }

    func Uint8ArrayToBigInt(arr: Array<UInt8>): BigInt {
        var i = 0
        let byteMax: BigInt = BigInt('100')
        var result: BigInt = BigInt('0')
        while (i < arr.size) {
            result = result * byteMax
            result = result + BigInt(arr[i])
            i += 1
        }
        return result
    }

    let dhAgree: Array<HuksParam> = [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_DH,
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE,
        )
    ]
    let dh2048Agree: Array<HuksParam> = [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_DH,
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE,
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_DH_KEY_SIZE_2048,
        )
    ]
    let dhGenOptions: HuksOptions = HuksOptions(
        properties: dh2048Agree,
        inData: Bytes()
    )
    let emptyOptions: HuksOptions = HuksOptions(properties: [], inData: Bytes())

    func HuksDhAgreeExportKey(
        keyAlias: String,
        peerPubKey: ?Array<UInt8>
    ): ?Array<UInt8> {
        let initHandle = initSession(keyAlias, dhGenOptions)
        let dhAgreeUpdateBobPubKey: HuksOptions = HuksOptions(
            properties: [
                HuksParam(
                    HuksTag.HuksTagAlgorithm,
                    HuksKeyAlg.HUKS_ALG_DH,
                ),
                HuksParam(
                    HuksTag.HuksTagPurpose,
                    HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE,
                ),
                HuksParam(
                    HuksTag.HuksTagDerivedAgreedKeyStorageFlag,
                    HuksKeyStorageType.HUKS_STORAGE_KEY_EXPORT_ALLOWED,
                )
            ],```swift
            inData: peerPubKey.getOrThrow()
        )
        updateSession(initHandle.handle, dhAgreeUpdateBobPubKey)
        return finishSession(initHandle.handle, emptyOptions)
    }

    func HuksDhAgreeExportTest(aliasA: String, aliasB: String, pubKeyA: ?Array<UInt8>, pubKeyB: ?Array<UInt8>) {
        let agreedKeyFromAlice = HuksDhAgreeExportKey(aliasA, pubKeyB).getOrThrow()
        loggerInfo("ok! agreedKeyFromAlice export is 0x${Uint8ArrayToBigInt(agreedKeyFromAlice).toString(radix: 16)}")

        let agreedKeyFromBob = HuksDhAgreeExportKey(aliasB, pubKeyA).getOrThrow()
        loggerInfo("ok! agreedKeyFromBob export is 0x${Uint8ArrayToBigInt(agreedKeyFromBob).toString(radix: 16)}")
    }

    func HuksDhAgreeInHuks(keyAlias: String, peerPubKey: ?Array<UInt8>, aliasAgreedKey: String): ?Array<UInt8> {
        let onlyUsedInHuks: Array<HuksParam> = [
            HuksParam(
                HuksTag.HuksTagKeyStorageFlag,
                HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
            ),
            HuksParam(
                HuksTag.HuksTagDerivedAgreedKeyStorageFlag,
                HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
            )
        ]
        let dhAgreeInit: HuksOptions = HuksOptions(
            properties: [
                HuksParam(
                    HuksTag.HuksTagKeyStorageFlag,
                    HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
                ),
                HuksParam(
                    HuksTag.HuksTagDerivedAgreedKeyStorageFlag,
                    HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
                ),
                HuksParam(HuksTag.HuksTagKeySize, HuksKeySize.HUKS_AES_KEY_SIZE_256),
                HuksParam(
                    HuksTag.HuksTagKeyStorageFlag,
                    HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
                ),
                HuksParam(
                    HuksTag.HuksTagDerivedAgreedKeyStorageFlag,
                    HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
                )
            ],
            inData: Bytes()
        )
        let dhAgreeFinishParams: Array<HuksParam> = [
            HuksParam(
                HuksTag.HuksTagKeyStorageFlag,
                HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
            ),
            HuksParam(
                HuksTag.HuksTagDerivedAgreedKeyStorageFlag,
                HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
            ),
            HuksParam(HuksTag.HuksTagIsKeyAlias, HuksParamValue.BooleanValue(true)),
            HuksParam(HuksTag.HuksTagAlgorithm, HuksKeyAlg.HUKS_ALG_AES),
            HuksParam(HuksTag.HuksTagKeySize, HuksKeySize.HUKS_AES_KEY_SIZE_256),
            HuksParam(
                HuksTag.HuksTagPurpose,
                HuksParamValue.Uint32Value(1 | 2)
            )
        ]

        let handle = initSession(keyAlias, dhAgreeInit)
        let dhAgreeUpdatePubKey: HuksOptions = HuksOptions(
            properties: [
                HuksParam(
                    HuksTag.HuksTagAlgorithm,
                    HuksKeyAlg.HUKS_ALG_DH,
                ),
                HuksParam(
                    HuksTag.HuksTagPurpose,
                    HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE,
                ),
                HuksParam(
                    HuksTag.HuksTagKeyStorageFlag,
                    HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
                ),
                HuksParam(
                    HuksTag.HuksTagDerivedAgreedKeyStorageFlag,
                    HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
                )
            ],
            inData: peerPubKey.getOrThrow()
        )
        updateSession(handle.handle, dhAgreeUpdatePubKey)
        let dhAgreeAliceFinnish: HuksOptions = HuksOptions(
            properties: [
                HuksParam(
                    HuksTag.HuksTagKeyStorageFlag,
                    HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
                ),
                HuksParam(
                    HuksTag.HuksTagDerivedAgreedKeyStorageFlag,
                    HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
                ),
                HuksParam(HuksTag.HuksTagIsKeyAlias, HuksParamValue.BooleanValue(true)),
                HuksParam(HuksTag.HuksTagAlgorithm, HuksKeyAlg.HUKS_ALG_AES),
                HuksParam(HuksTag.HuksTagKeySize, HuksKeySize.HUKS_AES_KEY_SIZE_256),
                HuksParam(
                    HuksTag.HuksTagPurpose,
                    HuksParamValue.Uint32Value(1 | 2)
                ),
                HuksParam(HuksTag.HuksTagKeyAlias, HuksParamValue.BytesValue(aliasAgreedKey.toArray()))
            ],
            inData: Bytes()
        )
        return finishSession(handle.handle, dhAgreeAliceFinnish)
    }

    func HuksDhAgreeInHuksTest(aliasA: String, aliasB: String, pubKeyA: ?Array<UInt8>, pubKeyB: ?Array<UInt8>,
        aliasAgreedKeyFromA: String, aliasAgreedKeyFromB: String) {
        let finishAliceResult = HuksDhAgreeInHuks(aliasA, pubKeyB, aliasAgreedKeyFromA).getOrThrow()
        loggerInfo("ok! finishAliceResult in huks is 0x${Uint8ArrayToBigInt(finishAliceResult).toString(radix: 16)}")
        let aliceAgreedExist = isKeyItemExist(aliasAgreedKeyFromA, emptyOptions)
        loggerInfo("ok! aliceAgreedExist in huks is ${aliceAgreedExist}")

        let finishBobResult = HuksDhAgreeInHuks(aliasB, pubKeyA, aliasAgreedKeyFromB).getOrThrow()
        loggerInfo("ok! finishBobResult in huks is 0x${Uint8ArrayToBigInt(finishBobResult).toString(radix: 16)}")
        let bobAgreedExist = isKeyItemExist(aliasAgreedKeyFromB, emptyOptions)
        loggerInfo("ok! bobAgreedExist in huks is ${bobAgreedExist}")

        deleteKeyItem(aliasAgreedKeyFromA, emptyOptions)
        deleteKeyItem(aliasAgreedKeyFromB, emptyOptions)
    }

    func huksDhAgreeTest() {
        let aliasAlice = 'alice'
        let aliasBob = 'bob'

        /* Generate two keys with aliases 'alice' and 'bob' using generateKeyItem */
        generateKeyItem(aliasAlice, dhGenOptions)
        generateKeyItem(aliasBob, dhGenOptions)

        /* Export public keys of asymmetric keys 'alice' and 'bob' */
        let pubKeyAlice = exportKeyItem(aliasAlice, emptyOptions)
        let pubKeyBob = exportKeyItem(aliasBob, emptyOptions)

        /* Start agreement, with the negotiated key returned to business management */
        HuksDhAgreeExportTest(aliasAlice, aliasBob, pubKeyAlice, pubKeyBob)

        /* Start agreement, with the negotiated key managed by HUKS */
        HuksDhAgreeInHuksTest(aliasAlice, aliasBob, pubKeyAlice, pubKeyBob, 'agreedKeyFromAlice', 'agreedKeyFromBob')

        deleteKeyItem(aliasAlice, emptyOptions)
        deleteKeyItem(aliasBob, emptyOptions)
    }
    ```