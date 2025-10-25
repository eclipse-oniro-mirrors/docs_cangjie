# Key Derivation (Cangjie)

Taking HKDF256 key as an example, complete key derivation. For specific scenario descriptions and supported algorithm specifications, please refer to [Supported Algorithms for Key Generation](./cj-huks-key-generation-overview.md#supported-algorithms).

## Development Steps

### Generate Key

1. Specify a key alias.

2. Initialize the key property set. You can optionally specify the parameter HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG to indicate whether keys derived from this key are managed by HUKS.

    - When the TAG is set to HUKS_STORAGE_ONLY_USED_IN_HUKS, it means that keys derived from this key are managed by HUKS, ensuring the derived keys remain within the secure environment throughout their lifecycle.

    - When the TAG is set to HUKS_STORAGE_KEY_EXPORT_ALLOWED, it means that keys derived from this key are returned to the caller for management, and the business is responsible for ensuring key security.

    - If the business does not set a specific value for TAG, it means that keys derived from this key can either be managed by HUKS or returned to the caller for management. The business can later choose how to protect the keys during subsequent derivations.

3. Call [generateKeyItem](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-generatekeyitemstring-huksoptions) to generate the key. For details, see [Key Generation](./cj-huks-key-generation-overview.md).

In addition, developers can also refer to [Key Import](./cj-huks-key-import-overview.md) to import existing keys.

### Key Derivation

1. Obtain the key alias and specify the corresponding property parameters in HuksOptions.

    You can optionally specify the parameter HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG to indicate whether the derived key is managed by HUKS.

    | Generation | Derivation | Specification |
    | :-------- | :-------- | :-------- |
    | HUKS_STORAGE_ONLY_USED_IN_HUKS | HUKS_STORAGE_ONLY_USED_IN_HUKS | Key managed by HUKS |
    | HUKS_STORAGE_KEY_EXPORT_ALLOWED | HUKS_STORAGE_KEY_EXPORT_ALLOWED | Key returned to caller for management |
    | TAG value not specified | HUKS_STORAGE_ONLY_USED_IN_HUKS | Key managed by HUKS |
    | TAG value not specified | HUKS_STORAGE_KEY_EXPORT_ALLOWED | Key returned to caller for management |
    | TAG value not specified | TAG value not specified | Key returned to caller for management |

    The TAG value specified during derivation must not conflict with the TAG value specified during generation. The table only lists valid specification methods.

2. Call [initSession](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-initsessionstring-huksoptions) to initialize the key session and obtain the session handle.

3. Call [updateSession](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-updatesessionhukshandle-huksoptions) to update the key session.

4. Call [finishSession](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-finishsessionhukshandle-huksoptions) to end the key session and complete the derivation.

### Delete Key

When a key is no longer needed, call [deleteKeyItem](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-deletekeyitemstring-huksoptions) to delete it. For details, see [Key Deletion](./cj-huks-delete-key.md).

## Development Example

### HKDF

<!--compile-->
```cangjie
/*
 * The following demonstrates the operation and usage of HKDF keys
 */
import kit.UniversalKeystoreKit.*

/*
 * Determine the key alias and encapsulate the key property parameter set
 */
let srcKeyAlias = "hkdf_Key"
let deriveHkdfInData = "deriveHkdfTestIndata"
var handle: ?HuksHandle = None
var finishOutData: ?Array<UInt8> = None
let HuksKeyDeriveKeySize: UInt32 = 32
/* Integrate key generation parameter set */
let properties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksKeyAlg.HUKS_ALG_AES,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksKeyPurpose.HUKS_KEY_PURPOSE_DERIVE,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksKeyDigest.HUKS_DIGEST_SHA256,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_SIZE,
        HuksKeySize.HUKS_AES_KEY_SIZE_128,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
        HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
    )
]
let huksOptions: HuksOptions = HuksOptions(
    properties,
    []
)
/* Integrate init key parameter set */
let initProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksKeyAlg.HUKS_ALG_HKDF,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksKeyPurpose.HUKS_KEY_PURPOSE_DERIVE,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksKeyDigest.HUKS_DIGEST_SHA256,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DERIVE_KEY_SIZE,
        uint32(HuksKeyDeriveKeySize),
    )
]
var initOptions: HuksOptions = HuksOptions(
    initProperties,
    None
)
/* Integrate finish key parameter set */
let finishProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
        HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_IS_KEY_ALIAS,
        boolean(true),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksKeyAlg.HUKS_ALG_AES,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_SIZE,
        HuksKeySize.HUKS_AES_KEY_SIZE_256,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksKeyDigest.HUKS_DIGEST_NONE,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_ALIAS,
        bytes(StringToUint8Array(srcKeyAlias)),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PADDING,
        HuksKeyPadding.HUKS_PADDING_NONE,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_BLOCK_MODE,
        HuksCipherMode.HUKS_MODE_ECB,
    )
]
let finishOptions: HuksOptions = HuksOptions(
    finishProperties,
    []
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

func generateKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: throwObject) {
    try {
        generateKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicGenKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
    AppLog.info("enter generateKeyItem")
    let throwObject: throwObject = throwObject(false)
    try {
        generateKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("generateKeyItem input arg invalid, ${e}")
    }
}

func initSession(keyAlias: String, huksOptions: HuksOptions, throwObject: throwObject) {
    return try {
        initSession(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicInitFunc(keyAlias: String, huksOptions: HuksOptions) {
    AppLog.info("enter doInit")
    let throwObject: throwObject = throwObject(false)
    try {
        handle = initSession(keyAlias, huksOptions, throwObject).handle
    } catch (e: Exception) {
        AppLog.error("doInit input arg invalid, ${e}")
    }
}

func updateSession(handle: HuksHandle, huksOptions: HuksOptions, throwObject: throwObject) {
    return try {
        updateSession(handle, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicUpdateFunc(handle: HuksHandle, huksOptions: HuksOptions) {
    AppLog.info("enter doUpdate")
    let throwObject: throwObject = throwObject(false)
    try {
        updateSession(handle, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("doUpdate input arg invalid, ${e}")
    }
}

func finishSession(handle: HuksHandle, huksOptions: HuksOptions, throwObject: throwObject) {
    return try {
        finishSession(handle, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicFinishFunc(handle: HuksHandle, huksOptions: HuksOptions) {
    AppLog.info("enter doFinish")
    let throwObject: throwObject = throwObject(false)
    try {
        finishSession(handle, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("doFinish input arg invalid, ${e}")
    }
}

func deleteKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: throwObject) {
    try {
        deleteKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicDeleteKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
    AppLog.info("enter deleteKeyItem")
    let throwObject: throwObject = throwObject(false)
    try {
        deleteKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("deleteKeyItem input arg invalid, ${e}")
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

<!--compile-->
```cangjie
/*
 * The following demonstrates the operation and usage of PBKDF2 keys
 */
import kit.UniversalKeystoreKit.*

/*
 * Determine the key alias and encapsulate the key property parameter set
 */
let srcKeyAlias = "pbkdf2_Key"
let salt = "mySalt"
let iterationCount: UInt32 = 10000
let derivedKeySize: UInt32 = 32
var handle: ?HuksHandle = None
var finishOutData: ?Array<UInt8> = None

/* Integrate key generation parameter set */
let properties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksKeyAlg.HUKS_ALG_AES,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksKeyPurpose.HUKS_KEY_PURPOSE_DERIVE,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksKeyDigest.HUKS_DIGEST_SHA256,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_SIZE,
        HuksKeySize.HUKS_AES_KEY_SIZE_128,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
        HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
    )
]
let huksOptions: HuksOptions = HuksOptions(
    properties,
    None
)

/* Key parameter set for init integration */
let initProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksKeyAlg.HUKS_ALG_PBKDF2,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksKeyPurpose.HUKS_KEY_PURPOSE_DERIVE,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksKeyDigest.HUKS_DIGEST_SHA256,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DERIVE_KEY_SIZE,
        uint32(derivedKeySize),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_ITERATION,
        uint32(iterationCount),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_SALT,
        bytes(StringToUint8Array(salt)),
    )
]
let initOptions: HuksOptions = HuksOptions(
    initProperties,
    None
)

/* Key parameter set for finish integration */
let finishProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG,
        HuksKeyStorageType.HUKS_STORAGE_ONLY_USED_IN_HUKS,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_IS_KEY_ALIAS,
        boolean(true),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksKeyAlg.HUKS_ALG_AES,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_SIZE,
        HuksKeySize.HUKS_AES_KEY_SIZE_256,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksKeyDigest.HUKS_DIGEST_NONE,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_ALIAS,
        bytes(StringToUint8Array(srcKeyAlias)),
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PADDING,
        HuksKeyPadding.HUKS_PADDING_NONE,
    ),
    HuksParam(
        HuksTag.HUKS_TAG_BLOCK_MODE,
        HuksCipherMode.HUKS_MODE_ECB,
    )
]
let finishOptions: HuksOptions = HuksOptions(
    finishProperties,
    None
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

func generateKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: throwObject) {
    try {
        generateKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicGenKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
    AppLog.info("enter generateKeyItem")
    let throwObject: throwObject = throwObject(false)
    try {
        generateKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("generateKeyItem input arg invalid, ${e}")
    }
}

func initSession(keyAlias: String, huksOptions: HuksOptions, throwObject: throwObject) {
    return try {
        initSession(keyAlias, huksOptions).handle
    } catch (e: Exception) {
        throwObject.isThrow = true
        AppLog.error("init session failed")
        throw e
    }
}

func publicInitFunc(keyAlias: String, huksOptions: HuksOptions) {
    AppLog.info("enter doInit")
    let throwObject: throwObject = throwObject(false)
    try {
        handle = initSession(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("doInit input arg invalid, ${e}")
    }
}

func updateSession(handle: HuksHandle, huksOptions: HuksOptions, throwObject: throwObject) {
    return try {
        updateSession(handle, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicUpdateFunc(handle: HuksHandle, huksOptions: HuksOptions) {
    AppLog.info("enter doUpdate")
    let throwObject: throwObject = throwObject(false)
    try {
        updateSession(handle, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("doUpdate input arg invalid, ${e}")
    }
}

func finishSession(handle: HuksHandle, huksOptions: HuksOptions, throwObject: throwObject) {
    return try {
        finishSession(handle, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicFinishFunc(handle: HuksHandle, huksOptions: HuksOptions) {
    AppLog.info("enter doFinish")
    let throwObject: throwObject = throwObject(false)
    try {
        finishOutData = finishSession(handle, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("doFinish input arg invalid, ${e}")
    }
}

func deleteKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: throwObject) {
    try {
        deleteKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicDeleteKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
    AppLog.info("enter deleteKeyItem")
    let throwObject: throwObject = throwObject(false)
    try {
        deleteKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("deleteKeyItem input arg invalid, ${e}")
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