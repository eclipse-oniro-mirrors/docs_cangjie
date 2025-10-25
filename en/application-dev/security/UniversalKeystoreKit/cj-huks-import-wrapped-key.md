# Encrypted Key Import (Cangjie)

Taking the encrypted import of an ECDH key pair as an example, operations such as [key generation](./cj-huks-key-generation-overview.md) and [agreement](./cj-huks-key-agreement-overview.md) involving business-side encryption keys are not reflected in this example.

For specific scenario descriptions and supported algorithm specifications, please refer to [Supported Algorithms for Key Import](./cj-huks-key-import-overview.md#supported-algorithms).

## Development Steps

1. Device A (importing device) converts the key to be imported into the [HUKS Key Material Format](./cj-huks-concepts.md#key-material-format) To_Import_Key (only for asymmetric keys; if the key to be imported is symmetric, this step can be omitted).

2. Device B (imported device) generates an asymmetric key pair Wrapping_Key (public key Wrapping_Pk, private key Wrapping_Sk) for encrypted import purposes, used for agreement. The key usage is set to unwrap. The public key material Wrapping_Pk of Wrapping_Key is exported and saved.

3. Device A uses the same algorithm as Device B to generate an asymmetric key pair Caller_Key (public key Caller_Pk, private key Caller_Sk) for encrypted import purposes, used for agreement. The public key material Caller_Pk of Caller_Key is exported and saved.

4. Device A generates a symmetric key Caller_Kek, which will subsequently be used to encrypt To_Import_Key.

5. Device A derives the Shared_Key based on the private key Caller_Sk of Caller_Key and the public key Wrapping_Pk of Device B's Wrapping_Key.

6. Device A encrypts To_Import_Key using Caller_Kek to generate To_Import_Key_Enc.

7. Device A encrypts Caller_Kek using Shared_Key to generate Caller_Kek_Enc.

8. Device A encapsulates the encrypted import key materials such as Caller_Pk, Caller_Kek_Enc, and To_Import_Key_Enc and sends them to Device B. The format of the encrypted import key materials can be found in [Encrypted Import Key Material Format](./cj-huks-key-import-overview.md#encrypted-import-key-material-format).

9. Device B imports the encapsulated encrypted key materials.

10. Devices A and B delete the keys used for encrypted import.

## Example

<!-- compile -->

```cangjie
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.UniversalKeystoreKit.*
import std.collection.*

let IV = '0000000000000000'
let AAD = "abababababababab"
let NONCE = "hahahahahaha"
let TAG_SIZE = 16
let FIELD_LENGTH = 4
let importedAes192PlainKey = "The aes192 key to import"
let callerAes256Kek = "This is kek to encrypt aes192 key"
let callerKeyAlias = "test_caller_key_ecdh_aes192"
let callerKekAliasAes256 = "test_caller_kek_ecdh_aes256"
let callerAgreeKeyAliasAes256 = "test_caller_agree_key_ecdh_aes256"
let importedKeyAliasAes192 = "test_import_key_ecdh_aes192"
var huksPubKey: ?Array<UInt8> = None
var callerSelfPublicKey: ?Array<UInt8> = None
var outSharedKey: ?Array<UInt8> = []
var outPlainKeyEncData: ?Array<UInt8> = None
var outKekEncData: ?Array<UInt8> = None
var outKekEncTag: ?Array<UInt8> = None
var outAgreeKeyEncTag: ?Array<UInt8> = None
var mask = [0x000000FF, 0x0000FF00, 0x00FF0000, 0xFF000000]

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

func subUint8ArrayOf(arrayBuf: Array<UInt8>, start: Int64, end: Int64) {
    let realEnd = min(end, arrayBuf.size)
    let list = ArrayList<UInt8>()
    for (i in start..realEnd) {
        list.add(arrayBuf[i])
    }
    return list.toArray()
}

func stringToUint8Array(str: String) {
    return str.toArray()
}

func assignLength(length: Int64, arrayBuf: Array<UInt8>, startIndex: Int64) {
    var index = startIndex
    for (i in 0..4) {
        arrayBuf[index] = UInt8((length & mask[i]) >> (i * 8))
        index++
    }
    return 4
}

func assignData(data: Array<UInt8>, arrayBuf: Array<UInt8>, startIndex: Int64) {
    var index = startIndex
    for (i in 0..data.size) {
        arrayBuf[index] = data[i]
        index++
    }
    return data.size
}

let genWrappingKeyParams: HuksOptions = HuksOptions(
    properties: [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_ECC
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_UNWRAP
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_CURVE25519_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HuksTagPadding,
            HuksKeyPadding.HUKS_PADDING_NONE
        )
    ],
    inData: Bytes()
)
let genCallerEcdhParams: HuksOptions = HuksOptions(
    properties: [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_ECC
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_CURVE25519_KEY_SIZE_256
        )
    ],
    inData: Bytes()
)
let importParamsCallerKek: HuksOptions = HuksOptions(
    properties: [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_AES
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_AES_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HuksTagPadding,
            HuksKeyPadding.HUKS_PADDING_NONE
        ),
        HuksParam(
            HuksTag.HuksTagBlockMode,
            HuksCipherMode.HUKS_MODE_GCM
        ),
        HuksParam(
            HuksTag.HuksTagDigest,
            HuksKeyDigest.HUKS_DIGEST_NONE
        ),
        HuksParam(
            HuksTag.HuksTagIv,
            HuksParamValue.BytesValue(IV.toArray())
        )
    ],
    inData: stringToUint8Array(callerAes256Kek)
)
var importParamsAgreeKey: HuksOptions = HuksOptions(
    properties: [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_AES
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_AES_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HuksTagPadding,
            HuksKeyPadding.HUKS_PADDING_NONE
        ),
        HuksParam(
            HuksTag.HuksTagBlockMode,
            HuksCipherMode.HUKS_MODE_GCM
        ),
        HuksParam(
            HuksTag.HuksTagDigest,
            HuksKeyDigest.HUKS_DIGEST_NONE
        ),
        HuksParam(
            HuksTag.HuksTagIv,
            HuksParamValue.BytesValue(IV.toArray())
        )
    ],
    inData: Bytes()
)
let callerAgreeParams: HuksOptions = HuksOptions(
    properties: [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_ECDH
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_CURVE25519_KEY_SIZE_256
        )
    ],
    inData: Bytes()
)
var encryptKeyCommonParams: HuksOptions = HuksOptions(
    properties: [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_AES
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_AES_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HuksTagPadding,
            HuksKeyPadding.HUKS_PADDING_NONE
        ),
        HuksParam(
            HuksTag.HuksTagBlockMode,
            HuksCipherMode.HUKS_MODE_GCM
        ),
        HuksParam(
            HuksTag.HuksTagNonce,
            HuksParamValue.BytesValue(NONCE.toArray())
        ),
        HuksParam(
            HuksTag.HuksTagAssociatedData,
            HuksParamValue.BytesValue(AAD.toArray())
        )
    ],
    inData: Bytes()
)
var importWrappedAes192Params: HuksOptions = HuksOptions(
    properties: [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_AES
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksParamValue.Uint32Value(1 | 2)
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_AES_KEY_SIZE_192
        ),
        HuksParam(
            HuksTag.HuksTagPadding,
            HuksKeyPadding.HUKS_PADDING_NONE
        ),
        HuksParam(
            HuksTag.HuksTagBlockMode,
            HuksCipherMode.HUKS_MODE_CBC
        ),
        HuksParam(
            HuksTag.HuksTagDigest,
            HuksKeyDigest.HUKS_DIGEST_NONE
        ),
        HuksParam(
            HuksTag.HuksTagUnwrapAlgorithmSuite,
            HuksUnwrapSuite.HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NOPADDING
        ),
        HuksParam(
            HuksTag.HuksTagIv,
            HuksParamValue.BytesValue(IV.toArray())
        )
    ],
    inData: Bytes()
)

func publicGenerateItemFunc(keyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter generateKeyItem")
    try {
        generateKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        loggerInfo("generateKeyItem invalid, ${e}")
    }
}

func publicImportKeyItemFunc(keyAlias: String, HuksOptions: HuksOptions) {
    loggerInfo("enter importKeyItem")
    try {
        importKeyItem(keyAlias, HuksOptions)
    } catch (e: Exception) {
        loggerInfo("importKeyItem input arg invalid, ${e}")
    }
}

func publicDeleteKeyItemFunc(KeyAlias: String, HuksOptions: HuksOptions) {
    loggerInfo("enter deleteKeyItem")
    try {
        deleteKeyItem(KeyAlias, HuksOptions)
    } catch (e: Exception) {
        loggerInfo("deleteKeyItem input arg invalid, ${e}")
    }
}

func importWrappedKeyItem(keyAlias: String, wrappingKeyAlias: String, huksOptions: HuksOptions): Unit {
    try {
        importWrappedKeyItem(keyAlias, wrappingKeyAlias, huksOptions)
    } catch (e: Exception) {
        loggerInfo("importWrappedKeyItem invalid, ${e}")
    }
}

func publicImportWrappedKeyFunc(keyAlias: String, wrappingKeyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter importWrappedKeyItem")
    for (i in 0..huksOptions
            .inData
            .size) {
    }
    try {
        importWrappedKeyItem(keyAlias, wrappingKeyAlias, huksOptions)
    } catch (e: Exception) {
        loggerInfo("importWrappedKeyItem input arg invalid, ${e}")
    }
}

func publicImportWrappedKey(keyAlias: String, wrappingKeyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter importWrappedKeyItem")
    try {
        importWrappedKeyItem(keyAlias, wrappingKeyAlias, huksOptions)
    } catch (e: Exception) {
        loggerInfo("importWrappedKeyItem input arg invalid, ${e}")
    }
}

func publicInitFunc(srcKeyAlias: String, HuksOptions: HuksOptions): HuksHandleId {
    var handle: ?HuksHandleId = None
    loggerInfo("enter doInit")
    try {
        handle = initSession(srcKeyAlias, HuksOptions).handle
    } catch (e: Exception) {
        loggerInfo("doInit input arg invalid, ${e}")
    }
    return handle.getOrThrow()
}

func publicUpdateSessionfunc(handle: HuksHandleId, huksOptions: HuksOptions): Array<UInt8> {
    let maxUpdateSize = 64
    let inData = huksOptions
        .inData
    let lastInDataPosition = inData.size - 1
    var inDataSegSize = maxUpdateSize
    var inDataSegPosition = 0
    var isFinished = false
    var outData: ?Array<UInt8> = None

    var newHuksOptions = huksOptions
    while (inDataSegPosition <= lastInDataPosition) {
        if (inDataSegPosition + maxUpdateSize > lastInDataPosition) {
            isFinished = true
            inDataSegSize = lastInDataPosition - inDataSegPosition + 1
            loggerInfo("enter doUpdate")
            break
        }
        newHuksOptions.inData = inData.slice(inDataSegPosition, inDataSegSize)
        loggerInfo("enter doUpdate")
        try {
            outData = updateSession(handle, huksOptions)
        } catch (e: Exception) {
            loggerInfo("doUpdate input arg invalid, ${e}")
        }
        if ((!isFinished) && (inDataSegPosition + maxUpdateSize > lastInDataPosition)) {
            loggerInfo("update size invalid isFinished = ${isFinished}")
            loggerInfo("inDataSegPosition = ${inDataSegPosition}")
            loggerInfo("lastInDataPosition = ${lastInDataPosition}")
            return Array<UInt8>()
        }
        inDataSegPosition += maxUpdateSize
    }
    return outData.getOrThrow()
}

func publicFinishSession(handle: HuksHandleId, huksOptions: HuksOptions, inData: Array<UInt8>) {
    var outData: ?Array<UInt8> = None
    loggerInfo("enter doFinish")
    try {
        outData = finishSession(handle, huksOptions)
    } catch (e: Exception) {
        loggerInfo("doFinish input arg invalid, ${e}")
    }
    return outData.getOrThrow()
}

func cipherfunc(keyAlias: String, huksOptions: HuksOptions) {
    let handle = publicInitFunc(keyAlias, huksOptions)
    let tmpData = publicUpdateSessionfunc(handle, huksOptions)
    let outData = publicFinishSession(handle, huksOptions, tmpData)
    return outData
}

func agreefunc(keyAlias: String, huksOptions: HuksOptions, huksPublicKey: Array<UInt8>) {
    let handle = publicInitFunc(keyAlias, huksOptions)
    var newhuksOptions = huksOptions
    newhuksOptions.inData = huksPublicKey
    loggerInfo("enter doUpdate")
    try {
        updateSession(handle, newhuksOptions)
    } catch (e: Exception) {
        loggerInfo("doUpdate input arg invalid, ${e}")
    }
    loggerInfo("enter doInit")
    var outSharedKey: ?Array<UInt8> = []
    try {
        outSharedKey = finishSession(handle, newhuksOptions)
    } catch (e: Exception) {
        loggerInfo("doInit input arg invalid, ${e}")
    }
    return outSharedKey
}

func ImportKekAndAgreeSharedSecret(callerKekAlias: String, importKekParams: HuksOptions, callerKeyAlias: String,
    huksPublicKey: Array<UInt8>, agreeParams: HuksOptions) {
    publicImportKeyItemFunc(callerKekAlias, importKekParams)
    outSharedKey = agreefunc(callerKeyAlias, agreeParams, huksPublicKey)
    importParamsAgreeKey.inData = outSharedKey.getOrThrow()
    publicImportKeyItemFunc(callerAgreeKeyAliasAes256, importParamsAgreeKey)
}

func generateAndExportPublicKey(keyAlias: String, HuksOptions: HuksOptions, caller: Bool) {
    publicGenerateItemFunc(keyAlias, HuksOptions)
    try {
        exportKeyItem(keyAlias, HuksOptions)
    } catch (e: Exception) {
        loggerInfo("generate pubKey failed, ${e}")
    }
}

func EncryptImportedPlainKeyAndKek(keyAlias: String) {
    encryptKeyCommonParams.inData = stringToUint8Array(keyAlias)
    let plainKeyEncData = cipherfunc(callerKekAliasAes256, encryptKeyCommonParams)
    outKekEncTag = subUint8ArrayOf(plainKeyEncData, plainKeyEncData.size - TAG_SIZE, plainKeyEncData.size)
    outPlainKeyEncData = subUint8ArrayOf(plainKeyEncData, 0, plainKeyEncData.size - TAG_SIZE)
    encryptKeyCommonParams.inData = stringToUint8Array(callerAes256Kek)
    let kekEncData = cipherfunc(callerAgreeKeyAliasAes256, encryptKeyCommonParams)
    outAgreeKeyEncTag = subUint8ArrayOf(kekEncData, kekEncData.size - TAG_SIZE, kekEncData.size)
    outKekEncData = subUint8ArrayOf(kekEncData, 0, kekEncData.size - TAG_SIZE)
}

func BuildWrappedDataAndImportWrappedKey(plainKey: String) {
    let plainKeySizeBuff = Array<UInt8>(4, repeat: 0)
    assignLength(plainKey.size, plainKeySizeBuff, 0)
    let wrappedData = Array<UInt8>(
        FIELD_LENGTH + huksPubKey
            .getOrThrow()
            .size + FIELD_LENGTH + AAD.size + FIELD_LENGTH + NONCE.size + FIELD_LENGTH + TAG_SIZE + FIELD_LENGTH + outKekEncData
            .getOrThrow()
            .size + FIELD_LENGTH + AAD.size + FIELD_LENGTH + NONCE.size + FIELD_LENGTH + TAG_SIZE + FIELD_LENGTH + plainKeySizeBuff
            .size + FIELD_LENGTH + outPlainKeyEncData
            .getOrThrow()
            .size, repeat: 0)
    var index = 0
    let AADUint8Array = stringToUint8Array(AAD)
    let NonceArray = stringToUint8Array(NONCE)
    index += assignLength(callerSelfPublicKey
        .getOrThrow()
        .size, wrappedData, index) // 4
    index += assignData(callerSelfPublicKey.getOrThrow(), wrappedData, index) // 91
    index += assignLength(AADUint8Array.size, wrappedData, index) // 4
    index += assignData(AADUint8Array, wrappedData, index) // 16
    index += assignLength(NonceArray.size, wrappedData, index) // 4
    index += assignData(NonceArray, wrappedData, index) // 12
    index += assignLength(outAgreeKeyEncTag
        .getOrThrow()
        .size, wrappedData, index) // 4
    index += assignData(outAgreeKeyEncTag.getOrThrow(), wrappedData, index) // 16
    index += assignLength(outKekEncData
        .getOrThrow()
        .size, wrappedData, index) // 4
    index += assignData(outKekEncData.getOrThrow(), wrappedData, index) // 32
    index += assignLength(AADUint8Array.size, wrappedData, index) // 4
    index += assignData(AADUint8Array, wrappedData, index) // 16
    index += assignLength(NonceArray.size, wrappedData, index) // 4
    index += assignData(NonceArray, wrappedData, index) // 12
    index += assignLength(outKekEncTag
        .getOrThrow()
        .size, wrappedData, index) // 4
    index += assignData(outKekEncTag.getOrThrow(), wrappedData, index) // 16
    index += assignLength(plainKeySizeBuff.size, wrappedData, index) // 4
    index += assignData(plainKeySizeBuff, wrappedData, index) // 4
    index += assignLength(outPlainKeyEncData
        .getOrThrow()
        .size, wrappedData, index) // 4
    index += assignData(outPlainKeyEncData.getOrThrow(), wrappedData, index) // 24
    return wrappedData
}

/* Simulating encrypted key import scenario: Device A is the remote device (importing device), Device B is the local device (imported device) */
func ImportWrappedKey() {
    /**
     * 1. Device A converts the key to be imported into HUKS key material format To_Import_Key 
     *    (only for asymmetric keys; symmetric keys can skip this step).
     *    This example uses importedAes192PlainKey (symmetric key) for simulation.
     */

    /* 2. Device B generates an asymmetric key pair Wrapping_Key (public key Wrapping_Pk, private key Wrapping_Sk) 
          for encrypted import purposes, with key usage set to unwrap. Exports the public key Wrapping_Pk into variable huksPubKey */
    let srcKeyAliasWrap = 'HUKS_Basic_Capability_Import_0200'
    generateAndExportPublicKey(srcKeyAliasWrap, genWrappingKeyParams, false)

    /* 3. Device A uses the same algorithm as Device B to generate an asymmetric key pair Caller_Key 
          (public key Caller_Pk, private key Caller_Sk) for encrypted import purposes. 
          Exports the public key Caller_Pk into variable callerSelfPublicKey */
    generateAndExportPublicKey(callerKeyAlias, genCallerEcdhParams, true)

    /**
     * 4. Device A generates a symmetric key Caller_Kek, which will be used to encrypt To_Import_Key
     * 5. Device A derives Shared_Key using Caller_Key's private key Caller_Sk and Wrapping_Key's public key Wrapping_Pk
     */
    ImportKekAndAgreeSharedSecret(callerKekAliasAes256, importParamsCallerKek, callerKeyAlias, huksPubKey.getOrThrow(),
        callerAgreeParams)

    /**
     * 6. Device A encrypts To_Import_Key using Caller_Kek to produce To_Import_Key_Enc
     * 7. Device A encrypts Caller_Kek using Shared_Key to produce Caller_Kek_Enc
     */
    EncryptImportedPlainKeyAndKek(importedAes192PlainKey)

    /* 8. Device A packages encrypted import materials including Caller_Pk, To_Import_Key_Enc, Caller_Kek_Enc 
          and sends them to Device B. This example stores them in variables callerSelfPublicKey, outPlainKeyEncData, outKekEncData */
    let wrappedData = BuildWrappedDataAndImportWrappedKey(importedAes192PlainKey)
    importWrappedAes192Params.inData = wrappedData

    /* 9. Device B imports the packaged encrypted key material */
    publicImportWrappedKeyFunc(importedKeyAliasAes192, srcKeyAliasWrap, importWrappedAes192Params)

    /* 10. Devices A and B delete keys used for encrypted import */
    publicDeleteKeyItemFunc(srcKeyAliasWrap, genWrappingKeyParams)
    publicDeleteKeyItemFunc(callerKeyAlias, genCallerEcdhParams)
    publicDeleteKeyItemFunc(importedKeyAliasAes192, importWrappedAes192Params)
    publicDeleteKeyItemFunc(callerKekAliasAes256, callerAgreeParams)
}
```