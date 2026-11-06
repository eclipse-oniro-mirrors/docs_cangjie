# Key Derivation (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Taking HKDF256 key as an example, complete key derivation. For specific scenario descriptions and supported algorithm specifications, please refer to [Supported Algorithms for Key Generation](./cj-huks-key-generation-overview.md#supported-algorithms).

## Development Steps

### Generate Key

1. Specify a key alias.

2. Initialize the key property set. You can optionally specify the parameter `HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG` to indicate whether keys derived from this key are managed by HUKS.

    - When the TAG is set to `HUKS_STORAGE_ONLY_USED_IN_HUKS`, it means that keys derived from this key are managed by HUKS, ensuring the derived keys remain within the secure environment throughout their lifecycle.

    - When the TAG is set to `HUKS_STORAGE_KEY_EXPORT_ALLOWED`, it means that keys derived from this key are returned to the caller for management, and the application is responsible for ensuring key security.

    - If the application does not specify a value for TAG, it means that keys derived from this key can either be managed by HUKS or returned to the caller. The application can later choose how to protect the derived keys.

3. Call [generateKeyItem](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-generatekeyitemstring-huksoptions) to generate the key. For details, see [Key Generation](./cj-huks-key-generation-overview.md).

Additionally, developers can refer to [Key Import](./cj-huks-key-import-overview.md) to import existing keys.

### Key Derivation

1. Obtain the key alias and specify the corresponding attribute parameters in `HuksOptions`.

    You can optionally specify the parameter `HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG` to indicate whether the derived key is managed by HUKS.

    | Generation | Derivation | Specification |
    | :-------- | :-------- | :-------- |
    | HUKS_STORAGE_ONLY_USED_IN_HUKS | HUKS_STORAGE_ONLY_USED_IN_HUKS | Key managed by HUKS |
    | HUKS_STORAGE_KEY_EXPORT_ALLOWED | HUKS_STORAGE_KEY_EXPORT_ALLOWED | Key returned to caller for management |
    | TAG value not specified | HUKS_STORAGE_ONLY_USED_IN_HUKS | Key managed by HUKS |
    | TAG value not specified | HUKS_STORAGE_KEY_EXPORT_ALLOWED | Key returned to caller for management |
    | TAG value not specified | TAG value not specified | Key returned to caller for management |

    The TAG value specified during derivation must not conflict with the TAG value specified during generation. The table only lists valid specification methods.

2. Call [initSession](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-initsessionstring-huksoptions) to initialize the key session and obtain the session handle.

3. Call [updateSession](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-updatesessionhukshandleid-huksoptions-bytes) to update the key session.

4. Call [finishSession](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-finishsessionhukshandleid-huksoptions-bytes) to end the key session and complete the derivation.

### Delete Key

When a key is no longer needed, call [deleteKeyItem](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-deletekeyitemstring-huksoptions) to delete it. For details, see [Key Deletion](./cj-huks-delete-key.md).

## Development Examples

### HKDF

<!-- compile -->

```cangjie
/*
 * The following demonstrates the operation and usage of HKDF keys
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
 * Determine the key alias and encapsulate the key attribute parameter set
 */
let srcKeyAlias = "hkdf_Key"
let deriveHkdfInData = "deriveHkdfTestIndata"
var handle: ?HuksHandleId = None
var finishOutData: ?Array<UInt8> = None
let HuksKeyDeriveKeySize: UInt32 = 32
/* Integrate key generation parameter set */
let properties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_AES),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_DERIVE),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksParamValue.Uint32Value(HuksKeyDigest.HUKS_DIGEST_SHA256),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_SIZE,
        HuksParamValue.Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_128),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
        HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
    )
]
let huksOptions: HuksOptions = HuksOptions(
    properties: properties,
    inData: Bytes()
)
/* Integrate init key parameter set */
let initProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_HKDF),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_DERIVE),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksParamValue.Uint32Value(HuksKeyDigest.HUKS_DIGEST_SHA256),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DERIVE_KEY_SIZE,
        HuksParamValue.Uint32Value(HuksKeyDeriveKeySize),
    )
]
var initOptions: HuksOptions = HuksOptions(
    properties: initProperties,
    inData: Bytes()
)
/* Integrate finish key parameter set */
let finishProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
        HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_IS_KEY_ALIAS,
        HuksParamValue.BooleanValue(true),
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
        HuksTag.HUKS_TAG_KEY_ALIAS,
        HuksParamValue.BytesValue(srcKeyAlias.toArray()),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PADDING,
        HuksParamValue.Uint32Value(HuksKeyPadding.HUKS_PADDING_NONE),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_BLOCK_MODE,
        HuksParamValue.Uint32Value(HuksCipherMode.HUKS_MODE_ECB),
    )
]
let finishOptions: HuksOptions = HuksOptions(
    properties: finishProperties,
    inData: Bytes()
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

func generateKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
    try {
        generateKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicGenKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter generateKeyItem")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        generateKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("generateKeyItem input arg invalid, ${e}")
    }
}

func initSession(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
    return try {
        initSession(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicInitFunc(keyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter doInit")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        handle = initSession(keyAlias, huksOptions, throwObject).handle
    } catch (e: Exception) {
        loggerInfo("doInit input arg invalid, ${e}")
    }
}

func updateSession(handle: HuksHandleId, huksOptions: HuksOptions, throwObject: ThrowObject) {
    return try {
        updateSession(handle, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicUpdateFunc(handle: HuksHandleId, huksOptions: HuksOptions) {
    loggerInfo("enter doUpdate")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        updateSession(handle, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("doUpdate input arg invalid, ${e}")
    }
}

func finishSession(handle: HuksHandleId, huksOptions: HuksOptions, throwObject: ThrowObject) {
    return try {
        finishSession(handle, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicFinishFunc(handle: HuksHandleId, huksOptions: HuksOptions) {
    loggerInfo("enter doFinish")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        finishSession(handle, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("doFinish input arg invalid, ${e}")
    }
}

func deleteKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
    try {
        deleteKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicDeleteKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter deleteKeyItem")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        deleteKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("deleteKeyItem input arg invalid, ${e}")
    }
}

func testDerive() {
    /* Generate key */
    publicGenKeyFunc(srcKeyAlias, huksOptions)
    /* Perform derivation operation */
    publicInitFunc(srcKeyAlias, initOptions)
    initOptions.inData = StringToUint8Array(deriveHkdfInData)
    publicUpdateFunc(handle.getOrThrow(), initOptions)
    publicFinishFunc(handle.getOrThrow(), finishOptions)
    publicDeleteKeyFunc(srcKeyAlias, huksOptions)
}
```

### PBKDF2

<!-- compile -->

```cangjie
/*
 * The following demonstrates the operation and usage of PBKDF2 keys
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
 * Determine the key alias and encapsulate the key attribute parameter set
 */
let srcKeyAlias = "pbkdf2_Key"
let salt = "mySalt"
let iterationCount: UInt32 = 10000
let derivedKeySize: UInt32 = 32
var handle: ?HuksHandleId = None
var finishOutData: ?Array<UInt8> = None

/* Integrate key generation parameter set */
let properties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_AES),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_DERIVE),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksParamValue.Uint32Value(HuksKeyDigest.HUKS_DIGEST_SHA256),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_SIZE,
        HuksParamValue.Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_128),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
        HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
    )
]
let huksOptions: HuksOptions = HuksOptions(
    properties: properties,
    inData: Bytes()
)

/* Integrate init key parameter set */
let initProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_PBKDF2),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_DERIVE),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksParamValue.Uint32Value(HuksKeyDigest.HUKS_DIGEST_SHA256),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DERIVE_KEY_SIZE,
        HuksParamValue.Uint32Value(derivedKeySize),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_ITERATION,
        HuksParamValue.Uint32Value(iterationCount),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_SALT,
        HuksParamValue.BytesValue(salt.toArray()),
    )
]
let initOptions: HuksOptions = HuksOptions(
    properties: initProperties,
    inData: Bytes()
)

/* Integrate finish key parameter set */
let finishProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
        HuksParamValue.Uint32Value(HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_IS_KEY_ALIAS,
        HuksParamValue.BooleanValue(true),
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
        HuksTag.HUKS_TAG_KEY_ALIAS,
        HuksParamValue.BytesValue(srcKeyAlias.toArray()),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PADDING,
        HuksParamValue.Uint32Value(HuksKeyPadding.HUKS_PADDING_NONE),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_BLOCK_MODE,
        HuksParamValue.Uint32Value(HuksCipherMode.HUKS_MODE_ECB),
    )
]
let finishOptions: HuksOptions = HuksOptions(
    properties: finishProperties,
    inData: Bytes()
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

func generateKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
    try {
        generateKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicGenKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter generateKeyItem")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        generateKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("generateKeyItem input arg invalid, ${e}")
    }
}

func initSession(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
    return try {
        initSession(keyAlias, huksOptions).handle
    } catch (e: Exception) {
        throwObject.isThrow = true
        loggerInfo("initSession failed")
        throw e
    }
}

func publicInitFunc(keyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter doInit")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        handle = initSession(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("doInit input arg invalid, ${e}")
    }
}

func updateSession(handle: HuksHandleId, huksOptions: HuksOptions, throwObject: ThrowObject) {
    return try {
        updateSession(handle, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicUpdateFunc(handle: HuksHandleId, huksOptions: HuksOptions) {
    loggerInfo("enter doUpdate")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        updateSession(handle, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("doUpdate input arg invalid, ${e}")
    }
}

func finishSession(handle: HuksHandleId, huksOptions: HuksOptions, throwObject: ThrowObject) {
    return try {
        finishSession(handle, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicFinishFunc(handle: HuksHandleId, huksOptions: HuksOptions) {
    loggerInfo("enter doFinish")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        finishOutData = finishSession(handle, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("doFinish input arg invalid, ${e}")
    }
}

func deleteKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
    try {
        deleteKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicDeleteKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter deleteKeyItem")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        deleteKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("deleteKeyItem input arg invalid, ${e}")
    }
}

func testDerive() {
    /* Generate key */
    publicGenKeyFunc(srcKeyAlias, huksOptions)
    /* Perform derivation operation */
    publicInitFunc(srcKeyAlias, initOptions)
    publicUpdateFunc(handle.getOrThrow(), initOptions)
    publicFinishFunc(handle.getOrThrow(), finishOptions)
    publicDeleteKeyFunc(srcKeyAlias, huksOptions)
}

```