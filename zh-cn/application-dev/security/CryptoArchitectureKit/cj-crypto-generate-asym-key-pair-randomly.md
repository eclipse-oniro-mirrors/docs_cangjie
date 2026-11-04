# 随机生成非对称密钥对

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

以RSA和SM2为例，随机生成非对称密钥对（KeyPair），并获得二进制数据。

非对称密钥对可用于后续加解密等操作，二进制数据可用于存储或传输。

## 随机生成RSA密钥对

对应的算法规格请参见[非对称密钥生成和转换规格：RSA](./cj-crypto-asym-key-generation-conversion-spec.md#rsa)。

1. 调用[createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring)，指定字符串参数'RSA1024|PRIMES_2'，创建RSA密钥类型为RSA1024、素数个数为2的非对称密钥生成器（AsyKeyGenerator）。

2. 调用[generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair)，随机生成非对称密钥对象（KeyPair）。

   KeyPair对象中包括公钥PubKey、私钥PriKey。

3. 调用[PubKey.getEncoded](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded)和[PriKey.getEncoded](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded)，分别获取密钥对象的二进制数据。

以随机生成RSA密钥对为例：

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testGenerateRSAKeyPair() {
    let asyKeyGenerator = createAsyKeyGenerator("RSA1024|PRIMES_2")
    try {
        asyKeyGenerator.generateKeyPair({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let pubKey = kp.pubKey
                let priKey = kp.priKey
                // 获取非对称密钥对的二进制数据
                let pkBlob = pubKey.getEncoded()
                let skBlob = priKey.getEncoded()
                Hilog.info(0, "", "pk bin data: ${pkBlob.data}")
                Hilog.info(0, "", "sk bin data: ${skBlob.data}")
            }
        })
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```

## 随机生成SM2密钥对

对应的算法规格请参见[非对称密钥生成和转换规格：SM2](./cj-crypto-asym-key-generation-conversion-spec.md#sm2)。

1. 调用[createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring)，指定字符串参数'SM2_256'，创建密钥算法为SM2、密钥长度为256位的非对称密钥生成器（AsyKeyGenerator）。

2. 调用[generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair)，随机生成非对称密钥对象（KeyPair）。

   KeyPair对象中包括公钥PubKey、私钥PriKey。

3. 调用[PubKey.getEncoded](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded)和[PriKey.getEncoded](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded)，分别获取密钥对象的二进制数据。

以随机生成SM2密钥对为例：

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testGenerateSM2KeyPair() {
    let asyKeyGenerator = createAsyKeyGenerator("SM2_256")
    try {
        asyKeyGenerator.generateKeyPair({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let pubKey = kp.pubKey
                let priKey = kp.priKey
                // 获取非对称密钥对的二进制数据
                let pkBlob = pubKey.getEncoded()
                let skBlob = priKey.getEncoded()
                Hilog.info(0, "", "pk bin data: ${pkBlob.data}")
                Hilog.info(0, "", "sk bin data: ${skBlob.data}")
            }
        })
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```
