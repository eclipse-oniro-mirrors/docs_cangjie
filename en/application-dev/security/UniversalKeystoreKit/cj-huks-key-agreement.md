# Key Agreement (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Taking X25519 as the negotiated key type and keys used exclusively within HUKS as an example, complete key agreement. For specific scenarios and supported algorithm specifications, refer to [Supported Algorithms for Key Generation](./cj-huks-key-generation-overview.md#supported-algorithms).

## Development Steps

### Generate Keys

Device A and Device B each generate an asymmetric key pair. For details, refer to [Key Generation](./cj-huks-key-generation-overview.md) or [Key Import](./cj-huks-key-import-overview.md).

During key generation, the parameter HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG (optional) can be specified to indicate whether keys derived from this key agreement will be managed by HUKS.

- When TAG is set to HUKS_STORAGE_ONLY_USED_IN_HUKS, it means keys derived from this key agreement will be managed by HUKS, ensuring the entire lifecycle of the negotiated key remains within a secure environment.

- When TAG is set to HUKS_STORAGE_KEY_EXPORT_ALLOWED, it means keys derived from this key agreement will be returned to the caller for management, with the business responsible for ensuring key security.

- If the business does not specify a TAG value, it means keys derived from this key agreement can either be managed by HUKS or returned to the caller. The business can later choose how to protect the keys during subsequent agreements.

### Export Keys

Device A and B export the public key material of their asymmetric key pairs. For details, refer to [Key Export](./cj-huks-export-key.md).

### Key Agreement

Device A and B each derive a shared key based on their private key and the peer device's public key.

During key agreement, the parameter HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG (optional) can be specified to indicate whether the negotiated key will be managed by HUKS.

| Generation | Agreement | Specification |
| :-------- | :-------- | :-------- |
| HUKS_STORAGE_ONLY_USED_IN_HUKS | HUKS_STORAGE_ONLY_USED_IN_HUKS | Key managed by HUKS |
| HUKS_STORAGE_KEY_EXPORT_ALLOWED | HUKS_STORAGE_KEY_EXPORT_ALLOWED | Key returned to caller for management |
| TAG value not specified | HUKS_STORAGE_ONLY_USED_IN_HUKS | Key managed by HUKS |
| TAG value not specified | HUKS_STORAGE_KEY_EXPORT_ALLOWED | Key returned to caller for management |
| TAG value not specified | TAG value not specified | Key returned to caller for management |

The TAG value specified during agreement must not conflict with the TAG value specified during generation. The table only lists valid specification methods.

### Delete Keys

When keys are no longer needed, Device A and B must delete them. For details, refer to [Key Deletion](./cj-huks-delete-key.md).

## Examples

Below are examples of agreement using X25519 and DH keys respectively.

- X25519 Asymmetric Key Agreement Example

    <!-- compile -->

    ```cangjie
    /*
     * The following demonstrates operations using X25519 keys
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
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_X25519),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksParamValue.Uint32Value(HuksKeySize.HUKS_CURVE25519_KEY_SIZE_256),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksParamValue.Uint32Value(HuksKeyDigest.HUKS_DIGEST_NONE),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PADDING,
            HuksParamValue.Uint32Value(HuksKeyPadding.HUKS_PADDING_NONE),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_BLOCK_MODE,
            HuksParamValue.Uint32Value(HuksCipherMode.HUKS_MODE_CBC),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
            HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
        )
    ]
    var huksOptions: HuksOptions = HuksOptions(
        properties: properties,
        inData: Bytes()
    )
    /* Assemble first agreement parameter set */
    let finishProperties1: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
            HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_IS_KEY_ALIAS,
            HuksParamValue.BooleanValue(true)
        ),
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_AES),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksParamValue.Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_256),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksParamValue.Uint32Value(HuksKeyDigest.HUKS_DIGEST_NONE),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PADDING,
            HuksParamValue.Uint32Value(HuksKeyPadding.HUKS_PADDING_NONE),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_BLOCK_MODE,
            HuksParamValue.Uint32Value(HuksCipherMode.HUKS_MODE_ECB),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_ALIAS,
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
            HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
            HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_IS_KEY_ALIAS,
            HuksParamValue.BooleanValue(true)
        ),
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_AES),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksParamValue.Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_256),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksParamValue.Uint32Value(HuksKeyDigest.HUKS_DIGEST_NONE),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PADDING,
            HuksParamValue.Uint32Value(HuksKeyPadding.HUKS_PADDING_NONE),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_BLOCK_MODE,
            HuksParamValue.Uint32Value(HuksCipherMode.HUKS_MODE_ECB),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_ALIAS,
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

    class ThrowObject {
        var isThrow: Bool = false

        init(isThrow: Bool) {
            this.isThrow = isThrow
        }
    }

    /* Generate key */
    func generateKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
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
        let throwObject: ThrowObject = ThrowObject(false)
        try {
            generateKeyItem(keyAlias, huksOptions, throwObject)
        } catch (e: Exception) {
            loggerInfo("generateKeyItem input arg invalid, ${e}")
        }
    }

    /* Initialize key session interface and obtain a handle (required) and challenge value (optional) */
    func initSession(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
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
        let throwObject: ThrowObject = ThrowObject(false)
        try {
            handle = initSession(keyAlias, huksOptions, throwObject)
        } catch (e: Exception) {
            loggerInfo("doInit input arg invalid, ${e}")
        }
    }

    /* Incrementally add key operation data and perform corresponding key operations, outputting processed data */
    func updateSession(handle: HuksHandleId, huksOptions: HuksOptions, throwObject: ThrowObject) {
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
        let throwObject: ThrowObject = ThrowObject(false)
        try {
            updateSession(handle, huksOptions, throwObject)
        } catch (e: Exception) {
            loggerInfo("doUpdate input arg invalid, ${e}")
        }
    }

    /* Terminate key session and perform corresponding key operations, outputting processed data */
    func finishSession(handle: HuksHandleId, huksOptions: HuksOptions, throwObject: ThrowObject) {
        return try {
            finishSession(handle, huksOptions)
        } catch (e: Exception) {
            throwObject.isThrow = true
            throw e
        }
    }

    /* Call finishSession to terminate operation */
    func publicFinishFunc(handle: HuksHandleId, huksOptions: HuksOptions) {
        loggerInfo("enter doFinish")
        let throwObject: ThrowObject = ThrowObject(false)
        try {
            finishOutData = finishSession(handle, huksOptions, throwObject)
        } catch (e: Exception) {
            loggerInfo("doFinish input arg invalid, ${e}")
        }
    }

    /* Export key */
    func exportKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
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
        let throwObject: ThrowObject = ThrowObject(false)
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
     * The following demonstrates operations using DH keys
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
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_DH),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE),
        )
    ]
    let dh2048Agree: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_DH),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE),
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksParamValue.Uint32Value(HuksKeySize.HUKS_DH_KEY_SIZE_2048),
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
                    HuksTag.HUKS_TAG_ALGORITHM,
                    HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_DH),
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_PURPOSE,
                    HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE),
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
                    HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_KEY_EXPORT_ALLOWED),
                )
            ],
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
                HuksTag.HUKS_TAG_KEY_STORAGE_FLAG,
                HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
            ),
            HuksParam(
                HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
                HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
            )
        ]
        let dhAgreeInit: HuksOptions = HuksOptions(
            properties: [
                HuksParam(
                    HuksTag.HUKS_TAG_KEY_STORAGE_FLAG,
                    HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
                    HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_KEY_SIZE, 
                    HuksParamValue.Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_256)
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_KEY_STORAGE_FLAG,
                    HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
                    HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
                )
            ],
            inData: Bytes()
        )
        let dhAgreeFinishParams: Array<HuksParam> = [
            HuksParam(
                HuksTag.HUKS_TAG_KEY_STORAGE_FLAG,
                HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
            ),
            HuksParam(
                HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
                HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
            ),
            HuksParam(HuksTag.HUKS_TAG_IS_KEY_ALIAS, HuksParamValue.BooleanValue(true)),
            HuksParam(HuksTag.HUKS_TAG_ALGORITHM, HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_AES)),
            HuksParam(
                HuksTag.HUKS_TAG_KEY_SIZE, 
                HuksParamValue.Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_256)
            ),
            HuksParam(
                HuksTag.HUKS_TAG_PURPOSE,
                HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT)
            )
        ]

        let handle = initSession(keyAlias, dhAgreeInit)
        let dhAgreeUpdatePubKey: HuksOptions = HuksOptions(
            properties: [
                HuksParam(
                    HuksTag.HUKS_TAG_ALGORITHM,
                    HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_DH),
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_PURPOSE,
                    HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE),
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_KEY_STORAGE_FLAG,
                    HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
                    HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
                )
            ],
            inData: peerPubKey.getOrThrow()
        )
        updateSession(handle.handle, dhAgreeUpdatePubKey)
        let dhAgreeAliceFinnish: HuksOptions = HuksOptions(
            properties: [
                HuksParam(
                    HuksTag.HUKS_TAG_KEY_STORAGE_FLAG,
                    HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
                    HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
                ),
                HuksParam(HuksTag.HUKS_TAG_IS_KEY_ALIAS, HuksParamValue.BooleanValue(true)),
                HuksParam(
                    HuksTag.HUKS_TAG_ALGORITHM, 
                    HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_AES)
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_KEY_SIZE, 
                    HuksParamValue.Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_256)
                ),
                HuksParam(
                    HuksTag.HUKS_TAG_PURPOSE,
                    HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT)
                ),
                HuksParam(HuksTag.HUKS_TAG_KEY_ALIAS, HuksParamValue.BytesValue(aliasAgreedKey.toArray()))
            ],
            inData: Bytes()
        )
        return finishSession(handle.handle, dhAgreeAliceFinnish)
    }

    func HuksDhAgreeInHuksTest(aliasA: String, aliasB: String, pubKeyA: ?Array<UInt8>, pubKeyB: ?Array<UInt8>,
        aliasAgreedKeyFromA: String, aliasAgreedKeyFromB: String) {
        let finishAliceResult = HuksDhAgreeInHuks(aliasA, pubKeyB, aliasAgreedKeyFromA).getOrThrow()
        loggerInfo("ok! finishAliceResult in huks is 0x${Uint8ArrayToBigInt(finishAliceResult).toString(radix: 16)}")
        let aliceAgreedExist = hasKeyItem(aliasAgreedKeyFromA, emptyOptions)
        loggerInfo("ok! aliceAgreedExist in huks is ${aliceAgreedExist}")

        let finishBobResult = HuksDhAgreeInHuks(aliasB, pubKeyA, aliasAgreedKeyFromB).getOrThrow()
        loggerInfo("ok! finishBobResult in huks is 0x${Uint8ArrayToBigInt(finishBobResult).toString(radix: 16)}")
        let bobAgreedExist = hasKeyItem(aliasAgreedKeyFromB, emptyOptions)
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

        /* Start agreement, the negotiated key is returned to the business for management */
        HuksDhAgreeExportTest(aliasAlice, aliasBob, pubKeyAlice, pubKeyBob)

        /* Start agreement, the negotiated key is managed by HUKS */
        HuksDhAgreeInHuksTest(aliasAlice, aliasBob, pubKeyAlice, pubKeyBob, 'agreedKeyFromAlice', 'agreedKeyFromBob')

        deleteKeyItem(aliasAlice, emptyOptions)
        deleteKeyItem(aliasBob, emptyOptions)
    }
    ```