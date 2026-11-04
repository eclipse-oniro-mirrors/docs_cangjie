# 使用RSA密钥对验签

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

对应的算法规格请参见[签名验签算法规格：RSA](./cj-crypto-sign-sig-verify-overview.md#rsa)。

> **说明：**
>
> 当前仓颉侧仅提供验签能力（Verify），签名操作请通过ArkTS侧的[cryptoFramework.createSign](../../reference/apis-crypto-architecture-kit/js-apis-cryptoFramework.md#cryptoframeworkcreatesign)完成，签名数据传入仓颉侧进行验签。

## 使用RSA密钥对（PKCS1模式）验签

1. 调用[createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring)、[generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair)，生成密钥算法为RSA、密钥长度为1024位、素数个数为2的非对称密钥对象（KeyPair），包括公钥（PubKey）和私钥（PriKey）。

   如何生成RSA非对称密钥，开发者可参考下文示例，并结合[非对称密钥生成和转换规格：RSA](./cj-crypto-asym-key-generation-conversion-spec.md#rsa)和[随机生成非对称密钥对](./cj-crypto-generate-asym-key-pair-randomly.md)理解，参考文档与当前示例可能存在入参差异，请在阅读时注意区分。

2. 调用[createVerify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createverifystring)，指定字符串参数'RSA1024|PKCS1|SHA256'，创建非对称密钥类型为RSA1024、填充模式为PKCS1、摘要算法为SHA256的Verify实例，用于完成验签操作。

3. 调用[Verify.initialize](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializepubkey-asynccallbackunit)，使用公钥（PubKey）初始化Verify实例。

4. 调用[Verify.update](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-asynccallbackunit)，传入待验证的数据。

   当前单次update长度没有限制，开发者可以根据数据量判断如何调用update。

   - 当待验签的数据较短时，可以在init完成后直接调用verify。
   - 当数据量较大时，可以多次调用update，即[分段验签](#使用rsa密钥对pkcs1模式分段验签)。

5. 调用[Verify.verify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-verifydatablob-datablob-asynccallbackbool)，对数据进行验签。

以PKCS1模式验签为例，签名数据从外部获取（此处用占位数据示意，实际使用时需替换为ArkTS侧签名生成的真实签名数据）：

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

// 完整的明文被拆分为input1和input2
let input1: Array<UInt8> = "This is Sign test plan1".toUtf8Array()
let input2: Array<UInt8> = "This is Sign test plan2".toUtf8Array()
// 签名数据，需从ArkTS侧签名获得，此处为占位示意
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
                        // 验签，传入剩余明文和签名数据
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

## 使用RSA密钥对（PKCS1模式）OnlyVerify模式验签

OnlyVerify模式适用于已预先计算摘要的场景，验签时直接传入摘要数据而非原始明文。

1. 调用[createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring)、[generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair)，生成RSA非对称密钥对（KeyPair）。

2. 调用[createVerify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createverifystring)，指定字符串参数'RSA1024|PKCS1|SHA256|OnlyVerify'，创建非对称密钥类型为RSA1024、填充模式为PKCS1、摘要算法为SHA256、验签模式为OnlyVerify的Verify实例。

3. 调用[Verify.initialize](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializepubkey-asynccallbackunit)，使用公钥（PubKey）初始化Verify实例。

4. 调用[Verify.verify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-verifydatablob-datablob-asynccallbackbool)，传入摘要数据和签名数据进行验签。

以OnlyVerify模式验签为例：

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testRsaOnlyVerify() {
    // 摘要数据，需预先通过Md计算或从外部获取
    let digestData: Array<UInt8> = Array<UInt8>(32, item: 0)
    // 签名数据，需从ArkTS侧签名获得
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
                    // OnlyVerify模式下直接传入摘要数据进行验签
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

## 使用RSA密钥对（PKCS1模式）签名恢复

签名恢复（Recover模式）可从签名数据中恢复出原始数据。

1. 调用[createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring)、[generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair)，生成RSA非对称密钥对（KeyPair）。

2. 调用[createVerify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createverifystring)，指定字符串参数'RSA1024|PKCS1|NoHash|Recover'，创建非对称密钥类型为RSA1024、填充模式为PKCS1、验签模式为Recover的Verify实例。

3. 调用[Verify.initialize](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializepubkey-asynccallbackunit)，使用公钥（PubKey）初始化Verify实例。

4. 调用[Verify.recover](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-recoverdatablob-asynccallbackdatablob)，从签名数据中恢复原始数据。

以PKCS1模式签名恢复为例：

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testRsaRecover() {
    // 签名数据，需从ArkTS侧通过OnlySign模式签名获得
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

## 使用RSA密钥对（PKCS1模式）分段验签

1. 调用[createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring)、[generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair)，生成RSA非对称密钥对（KeyPair）。

2. 调用[createVerify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createverifystring)，指定字符串参数'RSA1024|PKCS1|SHA256'，创建Verify实例。

3. 调用[Verify.initialize](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializepubkey-asynccallbackunit)，使用公钥（PubKey）初始化Verify实例。

4. 多次调用[Verify.update](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-asynccallbackunit)，传入待验证的数据。当前单次update长度没有限制，开发者可以根据数据量判断如何调用update。

5. 调用[Verify.verify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-verifydatablob-asynccallbackbool-optiondatablob)的重载（data参数为None），对已通过update追加的数据进行验签。

以PKCS1模式分段验签为例：

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testRsaVerifyBySegment() {
    let message = "This is a long plainText! This is a long plainText! This is a long plainText!" +
        "This is a long plainText! This is a long plainText! This is a long plainText! This is a long plainText!" +
        "This is a long plainText! This is a long plainText! This is a long plainText! This is a long plainText!" +
        "This is a long plainText! This is a long plainText! This is a long plainText! This is a long plainText!"
    let plainText: Array<UInt8> = message.toUtf8Array()
    let textSplitLen = 64 // 自定义的数据拆分长度
    // 签名数据，需从ArkTS侧签名获得
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
                    // 递归分段update
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
                            // 已通过分段传入所有明文，使用verify重载，data参数为None
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

## 使用RSA密钥对（PSS模式）验签

1. 调用[createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring)、[generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair)，生成RSA非对称密钥对（KeyPair）。

2. 调用[createVerify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createverifystring)，指定字符串参数'RSA2048|PSS|SHA256|MGF1_SHA256'，创建非对称密钥类型为RSA2048、填充模式为PSS、摘要算法为SHA256、掩码算法为MGF1_SHA256的Verify实例。

3. 调用[Verify.setVerifySpec](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-setverifyspecsignspecitem-int32)，设置验签参数。此处设置盐值长度（SignSpecItem.PssSaltLenNum），需与签名侧保持一致。

4. 调用[Verify.getVerifySpec](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getverifyspecsignspecitem)，获取验签参数。

5. 调用[Verify.initialize](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializepubkey-asynccallbackunit)，使用公钥（PubKey）初始化Verify实例。

6. 调用[Verify.update](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-asynccallbackunit)，传入待验证的数据。当前单次update长度没有限制，开发者可以根据数据量判断如何调用update。

7. 调用[Verify.verify](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-verifydatablob-datablob-asynccallbackbool)，对数据进行验签。

以PSS模式验签为例：

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testRsaPssVerify() {
    let input1: Array<UInt8> = "This is Sign test plan1".toUtf8Array()
    let input2: Array<UInt8> = "This is Sign test plan2".toUtf8Array()
    // 签名数据，需从ArkTS侧签名获得
    let signDataArr: Array<UInt8> = Array<UInt8>(256, item: 0)

    let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
    try {
        asyKeyGenerator.generateKeyPair({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let verifier = createVerify("RSA2048|PSS|SHA256|MGF1_SHA256")
                // 设置盐值长度，需与签名侧保持一致
                verifier.setVerifySpec(SignSpecItem.PssSaltLenNum, 32)
                // 获取盐值长度参数
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
