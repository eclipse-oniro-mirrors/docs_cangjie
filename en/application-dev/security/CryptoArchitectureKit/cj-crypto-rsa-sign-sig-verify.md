# RSA Key Pair Signature Verification

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

For the corresponding algorithm specifications, see [Signature/Verification Algorithm Specifications: RSA](./cj-crypto-sign-sig-verify-overview.md#rsa).

> **Note:**
>
> Currently, the Cangjie side only provides verification (Verify) capability. For signing operations, use [cryptoFramework.createSign](../../reference/apis-crypto-architecture-kit/js-apis-cryptoFramework.md#cryptoframeworkcreatesign) on the ArkTS side, and pass the signature data to the Cangjie side for verification.

## RSA Key Pair (PKCS1 Mode) Signature Verification

1. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring) and [generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair) to generate an asymmetric key object (KeyPair) with key algorithm RSA, key length 1024 bits, and 2 primes, including the public key (PubKey) and private key (PriKey).

   For how to generate RSA asymmetric keys, developers can refer to the example below and [Asymmetric Key Generation and Conversion Specifications: RSA](./cj-crypto-asym-key-generation-conversion-spec.md#rsa) and [Randomly Generating an Asymmetric Key Pair](./cj-crypto-generate-asym-key-pair-randomly.md). Note that there may be differences in input parameters between the reference documents and this example.

2. Call [createVerify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createverifystring), specifying the string parameter 'RSA1024|PKCS1|SHA256', to create a Verify instance with asymmetric key type RSA1024, padding mode PKCS1, and digest algorithm SHA256, for performing the verification operation.

3. Call [Verify.initialize](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializepubkey-asynccallbackunit) to initialize the Verify instance using the public key (PubKey).

4. Call [Verify.update](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-asynccallbackunit), passing in the data to be verified.

   There is no limit on the length of a single update. Developers can decide how to call update based on the data volume.

   - When the data to be verified is short, verify can be called directly after init.
   - When the data volume is large, update can be called multiple times, i.e., [segmented verification](#rsa-key-pair-pkcs1-mode-segmented-verification).

5. Call [Verify.verify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-verifydatablob-datablob-asynccallbackbool) to verify the signature.

The following example uses PKCS1 mode verification, where the signature data is obtained externally (placeholder data is used here for illustration; in actual use, replace it with the real signature data generated on the ArkTS side):

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

// The complete plaintext is split into input1 and input2
let input1: Array<UInt8> = "This is Sign test plan1".toUtf8Array()
let input2: Array<UInt8> = "This is Sign test plan2".toUtf8Array()
// Signature data, obtained from ArkTS-side signing; placeholder here for illustration
let signDataArr: Array<UInt8> = Array<UInt8>(128, item: 0)

func testRsaVerify() {
    let asyKeyGenerator = createAsyKeyGenerator("RSA1024")
    try {
        asyKeyGenerator.generateKeyPair({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let verifyAlg = "RSA1024|PKCS1|SHA256"
                let verifier = createVerify(verifyAlg)
                verifier.initialize(kp.pubKey, { err1 =>
                    if (let Some(e1) <- err1) {
                        throw e1
                    }
                    verifier.update(DataBlob(input1), { err2 =>
                        if (let Some(e2) <- err2) {
                            throw e2
                        }
                        // Verify, passing in the remaining plaintext and signature data
                        verifier.verify(DataBlob(input2), DataBlob(signDataArr), { err3, res =>
                            if (let Some(e3) <- err3) {
                                throw e3
                            }
                            if (let Some(r) <- res) {
                                if (r) {
                                    Hilog.info(0, "", "verify result: success.")
                                } else {
                                    Hilog.error(0, "", "verify result: failed.")
                                }
                            }
                        })
                    })
                })
            }
        })
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```

## RSA Key Pair (PKCS1 Mode) OnlyVerify Mode

The OnlyVerify mode is suitable for scenarios where the digest has been pre-computed. During verification, the digest data is passed in directly instead of the original plaintext.

1. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring) and [generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair) to generate an RSA asymmetric key pair (KeyPair).

2. Call [createVerify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createverifystring), specifying the string parameter 'RSA1024|PKCS1|SHA256|OnlyVerify', to create a Verify instance with asymmetric key type RSA1024, padding mode PKCS1, digest algorithm SHA256, and verification mode OnlyVerify.

3. Call [Verify.initialize](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializepubkey-asynccallbackunit) to initialize the Verify instance using the public key (PubKey).

4. Call [Verify.verify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-verifydatablob-datablob-asynccallbackbool), passing in the digest data and signature data for verification.

The following example uses OnlyVerify mode verification:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

func testRsaOnlyVerify() {
    // Digest data, must be pre-computed via Md or obtained externally
    let digestData: Array<UInt8> = Array<UInt8>(32, item: 0)
    // Signature data, obtained from ArkTS-side signing
    let signDataArr: Array<UInt8> = Array<UInt8>(128, item: 0)

    let asyKeyGenerator = createAsyKeyGenerator("RSA1024")
    try {
        asyKeyGenerator.generateKeyPair({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let verifier = createVerify("RSA1024|PKCS1|SHA256|OnlyVerify")
                verifier.initialize(kp.pubKey, { err1 =>
                    if (let Some(e1) <- err1) {
                        throw e1
                    }
                    // In OnlyVerify mode, pass in digest data directly for verification
                    verifier.verify(DataBlob(digestData), DataBlob(signDataArr), { err2, res =>
                        if (let Some(e2) <- err2) {
                            throw e2
                        }
                        if (let Some(r) <- res) {
                            if (r) {
                                Hilog.info(0, "", "verify result: success.")
                            } else {
                                Hilog.error(0, "", "verify result: failed.")
                            }
                        }
                    })
                })
            }
        })
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```

## RSA Key Pair (PKCS1 Mode) Signature Recovery

Signature recovery (Recover mode) can recover the original data from the signature data.

1. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring) and [generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair) to generate an RSA asymmetric key pair (KeyPair).

2. Call [createVerify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createverifystring), specifying the string parameter 'RSA1024|PKCS1|NoHash|Recover', to create a Verify instance with asymmetric key type RSA1024, padding mode PKCS1, and verification mode Recover.

3. Call [Verify.initialize](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializepubkey-asynccallbackunit) to initialize the Verify instance using the public key (PubKey).

4. Call [Verify.recover](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-recoverdatablob-asynccallbackdatablob) to recover the original data from the signature data.

The following example uses PKCS1 mode signature recovery:

```cangjie
<!-- compile -->
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

func testRsaRecover() {
    // Signature data, obtained from ArkTS-side signing via OnlySign mode
    let signDataArr: Array<UInt8> = Array<UInt8>(128, item: 0)

    let asyKeyGenerator = createAsyKeyGenerator("RSA1024")
    try {
        asyKeyGenerator.generateKeyPair({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let verifier = createVerify("RSA1024|PKCS1|NoHash|Recover")
                verifier.initialize(kp.pubKey, { err1 =>
                    if (let Some(e1) <- err1) {
                        throw e1
                    }
                    verifier.recover(DataBlob(signDataArr), { err2, rawData =>
                        if (let Some(e2) <- err2) {
                            throw e2
                        }
                        if (let Some(data) <- rawData) {
                            Hilog.info(0, "", "recover result size: ${data.data.size}")
                        } else {
                            Hilog.error(0, "", "recover result is null.")
                        }
                    })
                })
            }
        })
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```

## RSA Key Pair (PKCS1 Mode) Segmented Verification

1. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring) and [generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair) to generate an RSA asymmetric key pair (KeyPair).

2. Call [createVerify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createverifystring), specifying the string parameter 'RSA1024|PKCS1|SHA256', to create a Verify instance.

3. Call [Verify.initialize](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializepubkey-asynccallbackunit) to initialize the Verify instance using the public key (PubKey).

4. Call [Verify.update](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-asynccallbackunit) multiple times, passing in the data to be verified. There is no limit on the length of a single update. Developers can decide how to call update based on the data volume.

5. Call the overload of [Verify.verify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-verifydatablob-asynccallbackbool-optiondatablob) (with the data parameter set to None) to verify the data that has been appended via update.

The following example uses PKCS1 mode segmented verification:

<!-- compile -->

import kit.CangjieKit.AsyncCallback
```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testRsaVerifyBySegment() {
    let message = "This is a long plainText! This is a long plainText! This is a long plainText!" +
        "This is a long plainText! This is a long plainText! This is a long plainText! This is a long plainText!" +
        "This is a long plainText! This is a long plainText! This is a long plainText! This is a long plainText!" +
        "This is a long plainText! This is a long plainText! This is a long plainText! This is a long plainText!"
    let plainText: Array<UInt8> = message.toUtf8Array()
    let textSplitLen = 64 // Custom data split length
    // Signature data, obtained from ArkTS-side signing
    let signDataArr: Array<UInt8> = Array<UInt8>(128, item: 0)

    let asyKeyGenerator = createAsyKeyGenerator("RSA1024")
    try {
        asyKeyGenerator.generateKeyPair({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let verifier = createVerify("RSA1024|PKCS1|SHA256")
                verifier.initialize(kp.pubKey, { err1 =>
                    if (let Some(e1) <- err1) {
                        throw e1
                    }
                    // Recursive segmented update
                    func doVerifyUpdate(index: Int64) {
                        if (index < Int64(plainText.size)) {
                            let end = min(index + Int64(textSplitLen), Int64(plainText.size))
                            let segment = plainText[index..end]
                            verifier.update(DataBlob(segment), { err2 =>
                                if (let Some(e2) <- err2) {
                                    throw e2
                                }
                                doVerifyUpdate(end)
                            })
                        } else {
                            // All plaintext has been passed in via segments, use the verify overload with data parameter set to None
                            verifier.verify(DataBlob(signDataArr), { err3, res =>
                                if (let Some(e3) <- err3) {
                                    throw e3
                                }
                                if (let Some(r) <- res) {
                                    if (r) {
                                        Hilog.info(0, "", "verify result: success.")
                                    } else {
                                        Hilog.error(0, "", "verify result: failed.")
                                    }
                                }
                            }, None)
                        }
                    }
                    doVerifyUpdate(0)
                })
            }
        })
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```

## RSA Key Pair (PSS Mode) Signature Verification

1. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring) and [generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair) to generate an RSA asymmetric key pair (KeyPair).

2. Call [createVerify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createverifystring), specifying the string parameter 'RSA2048|PSS|SHA256|MGF1_SHA256', to create a Verify instance with asymmetric key type RSA2048, padding mode PSS, digest algorithm SHA256, and mask algorithm MGF1_SHA256.

3. Call [Verify.setVerifySpec](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-setverifyspecsignspecitem-int32) to set verification parameters. Here, the salt length (SignSpecItem.PssSaltLenNum) is set, which must be consistent with the signing side.

4. Call [Verify.getVerifySpec](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getverifyspecsignspecitem) to obtain verification parameters.

5. Call [Verify.initialize](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializepubkey-asynccallbackunit) to initialize the Verify instance using the public key (PubKey).

6. Call [Verify.update](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-asynccallbackunit), passing in the data to be verified. There is no limit on the length of a single update. Developers can decide how to call update based on the data volume.

7. Call [Verify.verify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-verifydatablob-datablob-asynccallbackbool) to verify the signature.

The following example uses PSS mode verification:

<!-- compile -->
import kit.CangjieKit.AsyncCallback

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testRsaPssVerify() {
    let input1: Array<UInt8> = "This is Sign test plan1".toUtf8Array()
    let input2: Array<UInt8> = "This is Sign test plan2".toUtf8Array()
    // Signature data, obtained from ArkTS-side signing
    let signDataArr: Array<UInt8> = Array<UInt8>(256, item: 0)

    let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
    try {
        asyKeyGenerator.generateKeyPair({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let verifier = createVerify("RSA2048|PSS|SHA256|MGF1_SHA256")
                // Set the salt length, must be consistent with the signing side
                verifier.setVerifySpec(SignSpecItem.PssSaltLenNum, 32)
                // Obtain the salt length parameter
                let saltLenSpec = verifier.getVerifySpec(SignSpecItem.PssSaltLenNum)
                match (saltLenSpec) {
                    case ResultSpec.Int32Value(v) => Hilog.info(0, "", "saltLen: ${v}")
                    case _ => ()
                }
                verifier.initialize(kp.pubKey, { err1 =>
                    if (let Some(e1) <- err1) {
                        throw e1
                    }
                    verifier.update(DataBlob(input1), { err2 =>
                        if (let Some(e2) <- err2) {
                            throw e2
                        }
                        verifier.verify(DataBlob(input2), DataBlob(signDataArr), { err3, res =>
                            if (let Some(e3) <- err3) {
                                throw e3
                            }
                            if (let Some(r) <- res) {
                                if (r) {
                                    Hilog.info(0, "", "verify result: success.")
                                } else {
                                    Hilog.error(0, "", "verify result: failed.")
                                }
                            }
                        })
                    })
                })
            }
        })
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```
