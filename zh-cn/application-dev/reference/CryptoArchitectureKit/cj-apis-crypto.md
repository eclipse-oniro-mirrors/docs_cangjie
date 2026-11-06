# ohos.security.crypto_framework（加解密算法库框架）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

crypto_framework模块向上提供统一的密码算法库加解密相关接口，以屏蔽底层硬件和算法库。

## 导入模块

```cangjie
import kit.CryptoArchitectureKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func createCipher(String)

```cangjie
public func createCipher(transformation: String): Cipher
```

**功能：** 通过指定算法名称，获取相应的[Cipher](#class-cipher)实例。

支持的规格详见[对称密钥加解密算法规格](../../security/CryptoArchitectureKit/cj-crypto-sym-encrypt-decrypt-spec.md)和[非对称密钥加解密算法规格](../../security/CryptoArchitectureKit/cj-crypto-asym-encrypt-decrypt-spec.md)。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|transformation|String|是|-|待生成Cipher的算法名称（含密钥长度）、加密模式以及填充方法的组合。|

> **说明：**
>
> 1. 目前对称加解密中，PKCS5和PKCS7的实现相同，其padding长度和分组长度保持一致。在3DES中均按8字节填充，在AES中均按16字节填充。另有NoPadding表示不填充。
>
> 开发者需要自行了解密码学不同分组模式的差异，以便选择合适的参数规格。例如选择ECB和CBC模式时，建议启用填充，否则必须确保明文长度是分组大小的整数倍；选择其他模式时，可以不启用填充，此时密文长度和明文长度一致（即可能不是分组大小的整数倍）。
> 2. 使用RSA或SM2进行非对称加解密时，必须创建两个Cipher对象，分别进行加密和解密操作，不能对同一个Cipher对象进行加解密。对称加解密没有此要求，只要算法规格一致，可以对同一个Cipher对象进行加解密操作。

**返回值：**

|类型|说明|
|:----|:----|
|[Cipher](#class-cipher)|返回加解密生成器的对象。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let cipherAlgName = "3DES192|ECB|PKCS7"
    let cipher = createCipher(cipherAlgName)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createMac(String)

```cangjie
public func createMac(algName: String): Mac
```

**功能：** 生成Mac实例，用于消息认证码的计算与操作。

**系统能力：** SystemCapability.Security.CryptoFramework.Mac

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|algName|String|是|-|指定摘要算法。|

**返回值：**

|类型|说明|
|:----|:----|
|[Mac](#class-mac)|返回由输入算法指定生成的[Mac](#class-mac)对象。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var mac = createMac("SHA256")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createMd(String)

```cangjie
public func createMd(algName: String): Md
```

**功能：** 生成Md实例，用于进行消息摘要的计算与操作。

**系统能力：** SystemCapability.Security.CryptoFramework.MessageDigest

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|algName|String|是|-|指定摘要算法。|

**返回值：**

|类型|说明|
|:----|:----|
|[Md](#class-md)|返回由输入算法指定生成的[Md](#class-md)对象。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let md = createMd("SHA256")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createRandom()

```cangjie
public func createRandom(): Random
```

**功能：** 生成Random实例，用于进行随机数的计算与设置种子。

**系统能力：** SystemCapability.Security.CryptoFramework.Rand

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[Random](#class-random)|返回由输入算法指定生成的[Random](#class-random)对象。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let rand = createRandom()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createSymKeyGenerator(String)

```cangjie
public func createSymKeyGenerator(algName: String): SymKeyGenerator
```

**功能：** 通过指定算法名称获取相应的对称密钥生成器实例。

支持的规格详见[对称密钥生成和转换规格](../../security/CryptoArchitectureKit/cj-crypto-sym-key-generation-conversion-spec.md)。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|algName|String|是|-|待生成对称密钥生成器的算法名称。具体取值详见[对称密钥生成和转换规格](../../security/CryptoArchitectureKit/cj-crypto-sym-key-generation-conversion-spec.md)一节中的“字符串参数”。|

**返回值：**

|类型|说明|
|:----|:----|
|[SymKeyGenerator](#class-symkeygenerator)|返回对称密钥生成器的对象。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let symKeyGenerator = createSymKeyGenerator("3DES192")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createAsyKeyGenerator(String)

```cangjie
public func createAsyKeyGenerator(algName: String): AsyKeyGenerator
```

**功能：** 用于生成非对称密钥生成器实例。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|algName|String|是|-|指定非对称密钥算法。格式：`算法名+\|+密钥生成规格`，例如 "RSA2048"、"EC224"、"X25519"。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [AsyKeyGenerator](#class-asykeygenerator) | 返回非对称密钥生成器实例。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
    Hilog.info(0, "", "createAsyKeyGenerator success.")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createVerify(String)

```cangjie
public func createVerify(algName: String): Verify
```

**功能：** 用于生成签名验签实例。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|algName|String|是|-|指定签名验签算法。格式：`算法名+\|+签名验签规格`，例如 "RSA2048\|PKCS1\|SHA256"、"ECC224\|SHA256"。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [Verify](#class-verify) | 返回签名验签实例。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let verify = createVerify("RSA2048|PKCS1|SHA256")
    Hilog.info(0, "", "verify algName: ${verify.algName}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface Key

```cangjie
public interface Key {
    prop format: String
    prop algName: String
    func getEncoded(): DataBlob
}
```

**功能：** 密钥（父类），在运行密码算法（如加解密）时需要提前生成其子类对象，并传入[Cipher](#class-cipher)实例的[initialize()](#func-initializecryptomode-key-paramsspec)方法。

密钥可以通过密钥生成器来生成。

**系统能力：** SystemCapability.Security.CryptoFramework.Key

**起始版本：** 22

### prop algName

```cangjie
prop algName: String
```

**功能：** 密钥对应的算法名（如果是对称密钥，则含密钥长度，否则不含密钥长度）。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Security.CryptoFramework.Key

**起始版本：** 22

### prop format

```cangjie
prop format: String
```

**功能：** 密钥的格式。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Security.CryptoFramework.Key

**起始版本：** 22

### func getEncoded()

```cangjie
func getEncoded(): DataBlob
```

**功能：** 获取密钥数据的字节流。密钥可以是对称密钥、公钥或私钥。公钥格式需符合ASN.1语法、X.509规范和DER编码；私钥格式需符合ASN.1语法、PKCS#8规范和DER编码。

> **说明：**
>
> RSA算法使用密钥参数生成私钥时，私钥对象支持getEncoded。

**系统能力：** SystemCapability.Security.CryptoFramework.Key

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#class-datablob)|用于查看密钥的具体内容。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let generator = createSymKeyGenerator("3DES192") // The key is generated by a key generator. The generation process is omitted here.
    let key = generator.generateSymKey()
    let encodedKey = key.getEncoded()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class ParamsSpec

```cangjie
public open class ParamsSpec {
    public var algName: String
}
```

**功能：** 加解密参数，在进行对称加解密时需要构造其子类对象，并将子类对象传入[initialize()](#func-initializecryptomode-key-paramsspec)方法。

适用于需要iv等参数的对称加解密模式（对于无iv等参数的模式如ECB模式，无需构造，在[initialize()](#func-initializecryptomode-key-paramsspec)中传入None即可）。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### var algName

```cangjie
public var algName: String
```

**功能：** 指明对称加解密参数的算法模式。可选值如下：

"IvParamsSpec"：适用于CBC\|CTR\|OFB\|CFB模式。

"GcmParamsSpec"：适用于GCM模式。

"CcmParamsSpec"：适用于CCM模式。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

## class Cipher

```cangjie
public class Cipher {}
```

**功能：** 提供加解密的算法操作功能，按序调用本类中的[initialize()](#func-initializecryptomode-key-paramsspec)、[update()](#func-updatedatablob)、[doFinal()](#func-dofinaldatablob)方法，可以实现对称加密/对称解密/非对称加密/非对称解密。

一次完整的加/解密流程在对称加密和非对称加密中略有不同：

- 对称加解密：initialize为必选，update为可选（且允许多次update加/解密大数据），doFinal为必选；doFinal结束后可以重新initialize开始新一轮加/解密流程。
- RSA、SM2非对称加解密：initialize为必选，不支持update操作，doFinal为必选（允许连续多次doFinal加/解密大数据）；RSA不支持重复initialize，切换加解密模式或填充方式时，需要重新创建Cipher对象。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### prop algName

```cangjie
public prop algName: String
```

**功能：** 加解密生成器指定的算法名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### func initialize(CryptoMode, Key, ?ParamsSpec)

```cangjie
public func initialize(opMode: CryptoMode, key: Key, params: ?ParamsSpec): Unit
```

**功能：** 初始化加解密的[Cipher](#class-cipher)对象。initialize、update、doFinal为三段式接口，需要成组使用。其中initialize和doFinal必选，update可选。

必须在使用[createCipher](#func-createcipherstring)创建[Cipher](#class-cipher)实例后，才能使用本函数。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|opMode|[CryptoMode](#enum-cryptomode)|是|-|加密或者解密模式。|
|key|[Key](#interface-key)|是|-|指定加密或解密的密钥。|
|params|?[ParamsSpec](#class-paramsspec)|是|-|指定加密或解密的参数，对于ECB等没有参数的算法模式，可以传入None。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to convert parameters between cj and c. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let skg = createSymKeyGenerator("AES128")
    let sk = skg.convertKey(DataBlob([83, 217, 231, 76, 28, 113, 23, 219, 250, 71, 209, 210, 205, 97, 32, 159]))
    let encoder = createCipher("AES128|CBC|PKCS7")
    let ivBlob = DataBlob([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])
    var ivParamsSpec = IvParamsSpec("IvParamsSpec", ivBlob)
    ivParamsSpec.algName = "IvParamsSpec"
    ivParamsSpec.iv = ivBlob
    encoder.initialize(CryptoMode.EncryptMode, sk, ivParamsSpec)
    let message = "This is a test"
    let blob = DataBlob(message.toArray())
    let encryptText = encoder.doFinal(blob)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func doFinal(?DataBlob)

```cangjie
public func doFinal(data: ?DataBlob): DataBlob
```

**功能：** 用于结束加解密操作，返回加密或解密的数据。

（1）在对称加解密中，doFinal加/解密（分组模式产生的）剩余数据和本次传入的数据，最后结束加密或者解密数据操作，获取加密或者解密数据。

如果数据量较小，可以在doFinal中一次性传入数据，而不使用update；如果在本次加解密流程中，已经使用update传入过数据，可以在doFinal的data参数处传入None。

根据对称加解密的模式不同，doFinal的输出有如下区别：

- 对于GCM和CCM模式的对称加密：一次加密流程中，如果将每次update和doFinal的结果拼接起来，会得到“密文 + authTag”。即末尾的16字节（GCM模式）或12字节（CCM模式）是authTag，其余部分均为密文。也就是说，如果doFinal的data参数传入None，则doFinal的结果就是 authTag。

  authTag需要填入解密时的[GcmParamsSpec](#class-gcmparamsspec)或[CcmParamsSpec](#class-ccmparamsspec)；密文则作为解密时的入参data。
- 对于其他模式的对称加解密、GCM和CCM模式的对称解密：一次加/解密流程中，每一次update和doFinal的结果拼接起来，得到完整的明文/密文。

（2）在RSA和SM2非对称加解密中，doFinal用于加解密本次传入的数据，获取加密或解密后的数据。如果数据量超过单次处理能力，可以多次调用doFinal，并将结果拼接以获得完整的明文或密文。

> **说明：**
>
> 1. 对称加解密中，调用doFinal标志着一次加解密流程已经完成，即[Cipher](#class-cipher)实例的状态被清除，因此当后续开启新一轮加解密流程时，需要重新调用initialize()并传入完整的参数列表进行初始化
> （比如即使是对同一个Cipher实例，采用同样的对称密钥，进行加密然后解密，则解密中调用initialize的时候仍需填写params参数，而不能直接省略为None）。
> 2. 如果遇到解密失败，需检查加解密数据和initialize时的参数是否匹配，包括GCM模式下加密得到的authTag是否填入解密时的GcmParamsSpec等。
>
> 对于加密，CFB、OFB和CTR模式，如果doFinal传None, 则返回结果为空。
>
> 对于解密，GCM、CCM、CFB、OFB和CTR模式，如果doFinal传None，则返回结果为空；对于解密，其他模式，如果明文是加密块大小的整倍数，调用update传入所有密文，调用doFinal传None, 则返回结果为空。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|data|?[DataBlob](#class-datablob)|是|-|加密或解密的数据。在对称加解密中可为None，但不可传入{data: Array\<UInt8>()}。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#class-datablob)|加/解密结果DataBlob。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to convert parameters between cj and c. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let skg = createSymKeyGenerator("AES128")
    let sk = skg.convertKey(DataBlob([83, 217, 231, 76, 28, 113, 23, 219, 250, 71, 209, 210, 205, 97, 32, 159]))
    let encoder = createCipher("AES128|CBC|PKCS7")
    let ivBlob = DataBlob([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])
    var ivParamsSpec = IvParamsSpec("IvParamsSpec", ivBlob)
    ivParamsSpec.algName = "IvParamsSpec"
    ivParamsSpec.iv = ivBlob
    encoder.initialize(CryptoMode.EncryptMode, sk, ivParamsSpec)
    let message = "This is a test"
    let blob = DataBlob(message.toArray())
    let encryptText = encoder.doFinal(blob)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func update(DataBlob)

```cangjie
public func update(data: DataBlob): DataBlob
```

**功能：** 分段更新加密或者解密数据操作，获取加/解密数据。

> **说明：**
>
> 必须在对[Cipher](#class-cipher)实例使用[initialize()](#func-initializecryptomode-key-paramsspec)初始化后，才能使用本函数。

- 在进行对称加解密操作时，如果开发者对各分组模式不够熟悉，建议每次调用update和doFinal后，都判断结果是否为空。如果结果不为空，则取出其中的数据进行拼接，以形成完整的密文或明文。这是因为选择的分组模式等各项规格可能会影响update和doFinal的结果。

    例如，对于ECB和CBC模式，不论update传入的数据是否为分组长度的整数倍，都会以分组作为基本单位进行加/解密，并输出本次update新产生的加/解密分组结果。

    可以理解为，update只要凑满一个新的分组就会有输出，如果没有凑满则此次update输出为空数组，把当前还没被加/解密的数据留着，等下一次update/doFinal传入数据的时候，拼接起来继续凑分组。

    最后doFinal的时候，会把剩下的还没加/解密的数据，根据[createCipher](#func-createcipherstring)时设置的padding模式进行填充，补齐到分组的整数倍长度，再输出剩余加解密结果。

    而对于可以将分组密码转化为流模式实现的模式，还可能出现密文长度和明文长度相同的情况等。

- 根据数据量，可以不调用update（即initialize完成后直接调用doFinal）或多次调用update。

    算法库目前没有对update（单次或累计）的数据量设置大小限制，建议对于大数据量的对称加解密，可以采用多次update的方式传入数据。

    AES使用多次update操作的示例代码详见[使用AES对称密钥分段加解密](../../security/CryptoArchitectureKit/cj-crypto-aes-sym-encrypt-decrypt-gcm-by-segment.md)。

- RSA、SM2非对称加解密不支持update操作。
- 对于CCM模式的对称加解密算法，加密时只能调用1次update接口加密数据并调用doFinal接口获取tag，或直接调用doFinal接口加密数据并获取tag，解密时只能调用1次update接口或调用1次doFinal接口解密数据并验证tag。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|data|[DataBlob](#class-datablob)|是|-|加密或者解密的数据。data不允许传入{data: Array\<UInt8>()}。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#class-datablob)|返回此次更新的加/解密结果DataBlob。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to convert parameters between cj and c. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let skg = createSymKeyGenerator("AES128")
    let sk = skg.convertKey(DataBlob([83, 217, 231, 76, 28, 113, 23, 219, 250, 71, 209, 210, 205, 97, 32, 159]))
    let cipher = createCipher("AES128|CBC|PKCS7")
    let ivBlob = DataBlob([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])
    var ivParamsSpec = IvParamsSpec("IvParamsSpec", ivBlob)
    ivParamsSpec.algName = "IvParamsSpec"
    ivParamsSpec.iv = ivBlob
    cipher.initialize(CryptoMode.EncryptMode, sk, ivParamsSpec)
    let plainText: DataBlob = DataBlob("this is test".toArray())
    cipher.update(plainText)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class Mac

```cangjie
public class Mac {}
```

**功能：** Mac类，调用Mac方法可以进行MAC（Message Authentication Code）加密计算。调用前，需要通过[createMac](#func-createmacstring)构造Mac实例。

**系统能力：** SystemCapability.Security.CryptoFramework.Mac

**起始版本：** 22

### prop algName

```cangjie
public prop algName: String
```

**功能：** 代表指定的摘要算法名。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Security.CryptoFramework.Mac

**起始版本：** 22

### func initialize(SymKey)

```cangjie
public func initialize(key: SymKey): Unit
```

**功能：** 使用对称密钥初始化Mac计算。initialize、update、doFinal为三段式接口，需要成组使用。其中initialize和doFinal必选，update可选。

> **说明：**
>
> - 建议通过[HMAC密钥生成规格](../../security/CryptoArchitectureKit/cj-crypto-sym-key-generation-conversion-spec.md#hmac)创建对称密钥生成器，调用[generateSymKey](#func-createsymkeygeneratorstring)随机生成对称密钥或调用[convertKey](#func-convertkeydatablob)传入与密钥规格长度一致的二进制密钥数据生成密钥。
> - 当指定“HMAC”生成对称密钥生成器时，仅支持调用[convertKey](#func-convertkeydatablob)传入长度在[1,4096]范围内（单位为byte）的任意二进制密钥数据生成密钥。

**系统能力：** SystemCapability.Security.CryptoFramework.Mac

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|key|[SymKey](#class-symkey)|是|-|对称密钥。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let skg = createSymKeyGenerator("AES128")
    let sk = skg.generateSymKey()
    let mac = createMac("SHA256")
    mac.initialize(sk)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func doFinal()

```cangjie
public func doFinal(): DataBlob
```

**功能：** 返回Mac的计算结果。

**系统能力：** SystemCapability.Security.CryptoFramework.Mac

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#class-datablob)|返回Mac的计算结果。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to convert parameters between cj and c. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let mac = createMac("SHA256")

    let skg = createSymKeyGenerator("AES128")
    let sk = skg.generateSymKey()
    mac.initialize(sk)
    let blob = DataBlob("this is test!".toArray())
    mac.update(blob)
    mac.doFinal()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getMacLength()

```cangjie
public func getMacLength(): UInt32
```

**功能：** 获取Mac消息认证码的长度（字节数）。

**系统能力：** SystemCapability.Security.CryptoFramework.Mac

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|UInt32|返回mac计算结果的字节长度。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |
  | 17620002 | failed to convert parameters between cj and c. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let mac = createMac("SHA256")
    let skg = createSymKeyGenerator("AES128")
    let sk = skg.generateSymKey()
    mac.initialize(sk)
    let blob = DataBlob("this is test!".toArray())
    mac.update(blob)
    mac.doFinal()
    var macLen = mac.getMacLength()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func update(DataBlob)

```cangjie
public func update(input: DataBlob): Unit
```

**功能：** 传入消息进行Mac更新消息认证码状态。

**系统能力：** SystemCapability.Security.CryptoFramework.Mac

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|input|[DataBlob](#class-datablob)|是|-|传入的消息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let mac = createMac("SHA256")
    let skg = createSymKeyGenerator("AES128")
    let sk = skg.generateSymKey()
    mac.initialize(sk)
    let blob = DataBlob("this is test!".toArray())
    mac.update(blob)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class Md

```cangjie
public class Md {}
```

**功能：** Md类，调用Md方法可以进行MD（Message Digest）摘要计算。调用前，需要通过[createMd](#func-createmdstring)构造Md实例。

**系统能力：** SystemCapability.Security.CryptoFramework.MessageDigest

**起始版本：** 22

### prop algName

```cangjie
public prop algName: String
```

**功能：** 代表指定的摘要算法名。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Security.CryptoFramework.MessageDigest

**起始版本：** 22

### func digest()

```cangjie
public func digest(): DataBlob
```

**功能：** 返回Md的计算结果。

**系统能力：** SystemCapability.Security.CryptoFramework.MessageDigest

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#class-datablob)|返回计算结果DataBlob。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to convert parameters between cj and c. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let md = createMd("SHA256")
    let blob: DataBlob = DataBlob("test".toArray())
    md.update(blob)
    let res = md.digest()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getMdLength()

```cangjie
public func getMdLength(): UInt32
```

**功能：** 获取Md消息摘要长度（字节数）。

**系统能力：** SystemCapability.Security.CryptoFramework.MessageDigest

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|UInt32|返回md计算结果的字节长度。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |
  | 17620002 | failed to convert parameters between cj and c. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let md = createMd("SHA256")
    let mdLen = md.getMdLength()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func update(DataBlob)

```cangjie
public func update(input: DataBlob): Unit
```

**功能：** 传入消息进行Md更新摘要状态。update和digest为两段式接口，需要成组使用。其中digest必选，update可选。

**系统能力：** SystemCapability.Security.CryptoFramework.MessageDigest

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|input|[DataBlob](#class-datablob)|是|-|传入的消息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let md = createMd("SHA256")
    let blob: DataBlob = DataBlob("test".toArray())
    md.update(blob)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class Random

```cangjie
public class Random {}
```

**功能：** Random类，调用Random方法可以进行随机数计算。调用前，需要通过[createRandom](#func-createrandom)构造Random实例。

**系统能力：** SystemCapability.Security.CryptoFramework.Rand

**起始版本：** 22

### prop algName

```cangjie
public prop algName: String
```

**功能：** 代表当前使用的随机数生成算法，目前只支持“CTR_DRBG"。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Security.CryptoFramework.Rand

**起始版本：** 22

### func generateRandom(Int32)

```cangjie
public func generateRandom(len: Int32): DataBlob
```

**功能：** 生成指定长度的随机数。

**系统能力：** SystemCapability.Security.CryptoFramework.Rand

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|len|Int32|是|-|表示生成随机数的长度，单位为byte，范围在[1, INT32_MAX]。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#class-datablob)|表示生成的随机数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let rand = createRandom()
    let randomData = rand.generateRandom(12)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setSeed(DataBlob)

```cangjie
public func setSeed(seed: DataBlob): Unit
```

**功能：** 设置指定的种子。

**系统能力：** SystemCapability.Security.CryptoFramework.Rand

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|seed|[DataBlob](#class-datablob)|是|-|设置的种子。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let rand = createRandom()
    rand.setSeed(DataBlob("test".toArray()))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class SymKey

```cangjie
public class SymKey <: Key {}
```

**功能：** 对称密钥，是[Key](#interface-key)的子类，在对称加解密时需要将其对象传入[Cipher](#class-cipher)实例的[initialize()](#func-initializecryptomode-key-paramsspec)方法使用。

对称密钥可以通过对称密钥生成器[SymKeyGenerator](#class-symkeygenerator)来生成。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**父类型：**

- [Key](#interface-key)

### prop algName

```cangjie
public prop algName: String
```

**功能：** 对称密钥生成器指定的算法名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

### prop format

```cangjie
public prop format: String
```

**功能：** 密钥的格式。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

### func clearMem()

```cangjie
public func clearMem(): Unit
```

**功能：** 将系统底层内存中的密钥内容清零。建议在不再使用对称密钥实例时调用此函数，避免密钥数据在内存中存留过久。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let generator = createSymKeyGenerator("3DES192")
    let key = generator.generateSymKey()
    var encodedKey = key.getEncoded()
    Hilog.info(0, "AppLogCj", "key blob: ${encodedKey.data}") // Display key content.
    key.clearMem()
    encodedKey = key.getEncoded()
    Hilog.info(0, "AppLogCj", "key blob: ${encodedKey.data}") // Display all 0s.
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getEncoded()

```cangjie
public func getEncoded(): DataBlob
```

**功能：** 获取密钥数据的字节流。密钥可以为对称密钥，公钥或者私钥。其中，公钥格式满足ASN.1语法、X.509规范、DER编码格式；私钥格式满足ASN.1语法，PKCS#8规范、DER编码方式。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#class-datablob)|用于查看密钥的具体内容。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let generator = createSymKeyGenerator("3DES192")
    let key = generator.generateSymKey()
    var encodedKey = key.getEncoded()
    Hilog.info(0, "AppLogCj", "key blob: ${encodedKey.data}") // Display key content.
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class SymKeyGenerator

```cangjie
public class SymKeyGenerator {}
```

**功能：** 对称密钥生成器。

在使用该类的方法前，需要先使用[createSymKeyGenerator](#func-createsymkeygeneratorstring)方法构建一个symKeyGenerator实例。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

### prop algName

```cangjie
public prop algName: String
```

**功能：** 对称密钥生成器指定的算法名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

### func convertKey(DataBlob)

```cangjie
public func convertKey(key: DataBlob): SymKey
```

**功能：** 根据指定数据生成对称密钥。

必须在使用[createSymKeyGenerator](#func-createsymkeygeneratorstring)创建对称密钥生成器后，才能使用本函数。

> **说明：**
>
> 对于HMAC算法的对称密钥，如果在创建对称密钥生成器时指定了具体哈希算法（如“HMAC|SHA256”），则需要传入与哈希长度一致的二进制密钥数据（如SHA256对应的256位密钥数据）。如果在创建对称密钥生成器时未指定具体哈希算法，如仅指定“HMAC”，则支持传入长度在1到4096字节范围内的任意二进制密钥数据。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|key|[DataBlob](#class-datablob)|是|-|指定的密钥材料数据。|

**返回值：**

|类型|说明|
|:----|:----|
|[SymKey](#class-symkey)|对称密钥。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let arr: Array<UInt8> = [0xba, 0x3d, 0xc2, 0x71, 0x21, 0x1e, 0x30, 0x56, 0xad, 0x47, 0xfc, 0x5a,
        0x46, 0x39, 0xee, 0x7c, 0xba, 0x3b, 0xc2, 0x71, 0xab, 0xa0, 0x30, 0x72] // keyLen = 192 (24 bytes)
    let symAlgName = "3DES192"
    let symKeyGenerator = createSymKeyGenerator(symAlgName)
    symKeyGenerator.convertKey(DataBlob(arr))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func generateSymKey()

```cangjie
public func generateSymKey(): SymKey
```

**功能：** 获取对称密钥生成器随机生成的密钥。

必须在使用[createSymKeyGenerator](#func-createsymkeygeneratorstring)创建对称密钥生成器后，才能使用本函数。

目前支持使用OpenSSL的RAND_priv_bytes()作为底层能力生成随机密钥。

> **说明：**
>
> - 对于HMAC算法的对称密钥，如果已经在创建对称密钥生成器时指定了具体哈希算法（如指定“HMAC|SHA256”），则会随机生成与哈希长度一致的二进制密钥数据（如指定“HMAC|SHA256”会随机生成256位的密钥数据）。
> - 如果在创建对称密钥生成器时没有指定具体哈希算法，如仅指定“HMAC”，则不支持随机生成对称密钥数据，可通过[convertKey](#func-convertkeydatablob)方式生成对称密钥数据。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[SymKey](#class-symkey)|返回对称密钥SymKey。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let symAlgName = "AES128"
    let symKeyGenerator = createSymKeyGenerator(symAlgName)
    let symKey = symKeyGenerator.generateSymKey()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class AsyKeyGenerator

```cangjie
public class AsyKeyGenerator {}
```

**功能：** 非对称密钥生成器，提供生成非对称密钥对、转换非对称密钥的能力。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### prop algName

```cangjie
public prop algName: String
```

**功能：** 获取非对称密钥生成器的算法名。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### func generateKeyPair(AsyncCallback<KeyPair>)

```cangjie
public func generateKeyPair(callback: AsyncCallback<[KeyPair](#class-keypair)>): Unit
```

**功能：** 异步生成非对称密钥对，通过回调返回结果。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|AsyncCallback&lt;[KeyPair](#class-keypair)&gt;|是|-|回调函数，接收生成结果或错误。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let pubKey = kp.pubKey
            let priKey = kp.priKey
            Hilog.info(0, "", "generateKeyPair success, pubKey algName: ${pubKey.algName}")
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func convertKey(AsyncCallback<KeyPair>, Option<DataBlob>, Option<DataBlob>)

```cangjie
public func convertKey(callback: AsyncCallback<[KeyPair](#class-keypair)>, pubKey!: Option<[DataBlob](#class-datablob)> = None, priKey!: Option<[DataBlob](#class-datablob)> = None): Unit
```

**功能：** 异步将传入的公钥和私钥转换为非对称密钥对，通过回调返回结果。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|AsyncCallback&lt;[KeyPair](#class-keypair)&gt;|是|-|回调函数，接收转换结果或错误。|
|pubKey!|Option&lt;[DataBlob](#class-datablob)&gt;|否|None|公钥数据，可为空。|
|priKey!|Option&lt;[DataBlob](#class-datablob)&gt;|否|None|私钥数据，可为空。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let pubEncoded = kp.pubKey.getEncoded()
            let priEncoded = kp.priKey.getEncoded()
            asyKeyGenerator.convertKey({ err1, keyPair1 =>
                if (let Some(e1) <- err1) {
                    throw e1
                }
                if (let Some(kp1) <- keyPair1) {
                    Hilog.info(0, "", "convertKey success, pubKey format: ${kp1.pubKey.format}")
                }
            }, pubKey!: Some(pubEncoded), priKey!: Some(priEncoded))
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func convertPemKey(AsyncCallback<KeyPair>, Option<String>, Option<String>)

```cangjie
public func convertPemKey(callback: AsyncCallback<[KeyPair](#class-keypair)>, pubKey!: Option<String> = None, priKey!: Option<String> = None): Unit
```

**功能：** 异步将 PEM 格式的公钥和私钥字符串转换为非对称密钥对，通过回调返回结果。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|AsyncCallback&lt;[KeyPair](#class-keypair)&gt;|是|-|回调函数，接收转换结果或错误。|
|pubKey!|Option&lt;String&gt;|否|None|PEM 格式公钥字符串，可为空。|
|priKey!|Option&lt;String&gt;|否|None|PEM 格式私钥字符串，可为空。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
let pubKeyPem = "-----BEGIN PUBLIC KEY-----\nMFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEXN...\n-----END PUBLIC KEY-----"
let priKeyPem = "-----BEGIN PRIVATE KEY-----\nMIGHAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBG0w...\n-----END PRIVATE KEY-----"
try {
    asyKeyGenerator.convertPemKey({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            Hilog.info(0, "", "convertPemKey success, priKey algName: ${kp.priKey.algName}")
        }
    }, pubKey!: Some(pubKeyPem), priKey!: Some(priKeyPem))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class PriKey

```cangjie
public class PriKey <: Key {}
```

**功能：** 非对称私钥，提供获取私钥参数、编码、清除内存等能力。

**父类型：**

- [Key](#interface-key)

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### prop format

```cangjie
public prop format: String
```

**功能：** 获取私钥的格式。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### prop algName

```cangjie
public prop algName: String
```

**功能：** 获取私钥的算法名。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### func getAsyKeySpec(AsyKeySpecItem)

```cangjie
public func getAsyKeySpec(itemType: AsyKeySpecItem): ResultSpec
```

**功能：** 获取非对称私钥的指定参数。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|itemType|[AsyKeySpecItem](#enum-asykeyspecitem)|是|-|指定要获取的密钥参数项。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [ResultSpec](#enum-resultspec) | 返回密钥参数值包装类型。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let priKey = kp.priKey
            let resultSpec = priKey.getAsyKeySpec(AsyKeySpecItem.RsaNBn)
            match (resultSpec) {
                case ResultSpec.BigintValue(v) => Hilog.info(0, "", "RsaNBn: ${v.toString()}")
                case _ => ()
            }
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getEncodedDer(String)

```cangjie
public func getEncodedDer(format: String): DataBlob
```

**功能：** 获取私钥的 DER 格式编码。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|format|String|是|-|指定密钥编码的格式，例如 "PKCS8"、"X.509"。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#class-datablob)|返回 DER 格式编码的密钥数据。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let priKey = kp.priKey
            let priDer = priKey.getEncodedDer("PKCS8")
            Hilog.info(0, "", "priKey DER data size: ${priDer.data.size}")
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getEncodedPem(String)

```cangjie
public func getEncodedPem(format: String): String
```

**功能：** 获取私钥的 PEM 格式编码。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|format|String|是|-|指定密钥编码的格式，例如 "PKCS8"、"X.509"。|

**返回值：**

|类型|说明|
|:----|:----|
|String|返回 PEM 格式编码的密钥字符串。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let priKey = kp.priKey
            let priPem = priKey.getEncodedPem("PKCS8")
            Hilog.info(0, "", "priKey PEM: ${priPem}")
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getEncoded()

```cangjie
public func getEncoded(): DataBlob
```

**功能：** 获取私钥的编码数据。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [DataBlob](#class-datablob) | 返回编码后的密钥数据。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let priKey = kp.priKey
            let priEncoded = priKey.getEncoded()
            Hilog.info(0, "", "priKey encoded data size: ${priEncoded.data.size}")
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func clearMem()

```cangjie
public func clearMem(): Unit
```

**功能：** 清除私钥的内存数据，达到安全销毁的目的。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            kp.priKey.clearMem()
            Hilog.info(0, "", "priKey clearMem success.")
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class PubKey

```cangjie
public class PubKey <: Key {}
```

**功能：** 非对称公钥，提供获取公钥参数、编码等能力。

**父类型：**

- [Key](#interface-key)

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### prop format

```cangjie
public prop format: String
```

**功能：** 获取公钥的格式。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### prop algName

```cangjie
public prop algName: String
```

**功能：** 获取公钥的算法名。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### func getAsyKeySpec(AsyKeySpecItem)

```cangjie
public func getAsyKeySpec(itemType: AsyKeySpecItem): ResultSpec
```

**功能：** 获取非对称公钥的指定参数。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|itemType|[AsyKeySpecItem](#enum-asykeyspecitem)|是|-|指定要获取的密钥参数项。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [ResultSpec](#enum-resultspec) | 返回密钥参数值包装类型。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |
  | 801 | this operation is not supported. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let pubKey = kp.pubKey
            let resultSpec = pubKey.getAsyKeySpec(AsyKeySpecItem.RsaNBn)
            match (resultSpec) {
                case ResultSpec.BigintValue(v) => Hilog.info(0, "", "pubKey RsaNBn: ${v.toString()}")
                case _ => ()
            }
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getEncodedDer(String)

```cangjie
public func getEncodedDer(format: String): DataBlob
```

**功能：** 获取公钥的 DER 格式编码。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|format|String|是|-|指定密钥编码的格式，例如 "X.509"、"PKCS8"。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#class-datablob)|返回 DER 格式编码的密钥数据。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let pubKey = kp.pubKey
            let pubDer = pubKey.getEncodedDer("X.509")
            Hilog.info(0, "", "pubKey DER data size: ${pubDer.data.size}")
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getEncodedPem(String)

```cangjie
public func getEncodedPem(format: String): String
```

**功能：** 获取公钥的 PEM 格式编码。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|format|String|是|-|指定密钥编码的格式，例如 "X.509"、"PKCS8"。|

**返回值：**

|类型|说明|
|:----|:----|
|String|返回 PEM 格式编码的密钥字符串。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let pubKey = kp.pubKey
            let pubPem = pubKey.getEncodedPem("X.509")
            Hilog.info(0, "", "pubKey PEM: ${pubPem}")
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getEncoded()

```cangjie
public func getEncoded(): DataBlob
```

**功能：** 获取公钥的编码数据。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [DataBlob](#class-datablob) | 返回编码后的密钥数据。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let pubKey = kp.pubKey
            let pubEncoded = pubKey.getEncoded()
            Hilog.info(0, "", "pubKey encoded data size: ${pubEncoded.data.size}")
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class KeyPair

```cangjie
public class KeyPair {}
```

**功能：** 非对称密钥对，包含公钥和私钥。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### prop pubKey

```cangjie
public prop pubKey: PubKey
```

**功能：** 获取密钥对中的公钥。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### prop priKey

```cangjie
public prop priKey: PriKey
```

**功能：** 获取密钥对中的私钥。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

## class Verify

```cangjie
public class Verify {}
```

**功能：** 签名验签器，提供验签初始化、更新数据、验签、恢复数据、设置/获取验签参数的能力。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### prop algName

```cangjie
public prop algName: String
```

**功能：** 获取验签器的算法名。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### func initialize(PubKey, AsyncCallback<Unit>)

```cangjie
public func initialize(pubKey: PubKey, callback: AsyncCallback<Unit>): Unit
```

**功能：** 使用指定公钥异步初始化验签器，通过回调返回结果。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|pubKey|[PubKey](#class-pubkey)|是|-|用于验签的公钥。|
|callback|AsyncCallback&lt;Unit&gt;|是|-|回调函数，接收初始化结果或错误。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to obtain the native object or convert parameters. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let verify = createVerify("RSA2048|PKCS1|SHA256")
let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            let pubKey = kp.pubKey
            verify.initialize(pubKey, { err1 =>
                if (let Some(e1) <- err1) {
                    throw e1
                }
                Hilog.info(0, "", "verify initialize success, algName: ${verify.algName}")
            })
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func update(DataBlob, AsyncCallback<Unit>)

```cangjie
public func update(data: DataBlob, callback: AsyncCallback<Unit>): Unit
```

**功能：** 异步追加待验签数据，通过回调返回结果。在 initialize 之后、verify 之前调用。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|data|[DataBlob](#class-datablob)|是|-|待验签的数据。|
|callback|AsyncCallback&lt;Unit&gt;|是|-|回调函数，接收更新结果或错误。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to obtain the native object or convert parameters. |
  | 17630001 | Crypto operation error. |
  | 17620004 | Invalid function call. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let verify = createVerify("RSA2048|PKCS1|SHA256")
let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
let input: Array<UInt8> = "This is test data".toUtf8Array()
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            verify.initialize(kp.pubKey, { err1 =>
                if (let Some(e1) <- err1) {
                    throw e1
                }
                verify.update(DataBlob(input), { err2 =>
                    if (let Some(e2) <- err2) {
                        throw e2
                    }
                    Hilog.info(0, "", "verify update success, data size: ${input.size}")
                })
            })
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func verify(DataBlob, DataBlob, AsyncCallback<Bool>)

```cangjie
public func verify(data: DataBlob, signatureData: DataBlob, callback: AsyncCallback<Bool>): Unit
```

**功能：** 异步验证数据与签名是否匹配，通过回调返回验签结果。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|data|[DataBlob](#class-datablob)|是|-|待验签的数据。|
|signatureData|[DataBlob](#class-datablob)|是|-|待验证的签名数据。|
|callback|AsyncCallback&lt;Bool&gt;|是|-|回调函数，接收验签结果或错误。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to obtain the native object or convert parameters. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let verify = createVerify("RSA2048|PKCS1|SHA256")
let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
let input: Array<UInt8> = "This is test data".toUtf8Array()
let signDataArr: Array<UInt8> = Array<UInt8>(256, item: 0)
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            verify.initialize(kp.pubKey, { err1 =>
                if (let Some(e1) <- err1) {
                    throw e1
                }
                verify.verify(DataBlob(input), DataBlob(signDataArr), { err2, res =>
                    if (let Some(e2) <- err2) {
                        throw e2
                    }
                    if (let Some(r) <- res) {
                        Hilog.info(0, "", "verify result: ${r}")
                    }
                })
            })
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func verify(DataBlob, AsyncCallback<Bool>, Option<DataBlob>)

```cangjie
public func verify(signatureData: DataBlob, callback: AsyncCallback<Bool>, data!: Option<[DataBlob](#class-datablob)> = None): Unit
```

**功能：** 异步验证签名是否匹配，通过回调返回验签结果。此重载适用于已通过 update 追加数据后调用，data 参数可为空。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|signatureData|[DataBlob](#class-datablob)|是|-|待验证的签名数据。|
|callback|AsyncCallback&lt;Bool&gt;|是|-|回调函数，接收验签结果或错误。|
|data!|Option&lt;[DataBlob](#class-datablob)&gt;|否|None|待验签的数据，可为空（适用于已 update 场景）。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to obtain the native object or convert parameters. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let verify = createVerify("RSA2048|PKCS1|SHA256")
let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
let input: Array<UInt8> = "This is test data".toUtf8Array()
let signDataArr: Array<UInt8> = Array<UInt8>(256, item: 0)
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            verify.initialize(kp.pubKey, { err1 =>
                if (let Some(e1) <- err1) {
                    throw e1
                }
                verify.update(DataBlob(input), { err2 =>
                    if (let Some(e2) <- err2) {
                        throw e2
                    }
                    // 已通过update追加数据，data参数传None
                    verify.verify(DataBlob(signDataArr), { err3, res =>
                        if (let Some(e3) <- err3) {
                            throw e3
                        }
                        if (let Some(r) <- res) {
                            Hilog.info(0, "", "verify result: ${r}")
                        }
                    }, None)
                })
            })
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func recover(DataBlob, AsyncCallback<?DataBlob>)

```cangjie
public func recover(signatureData: DataBlob, callback: AsyncCallback<?DataBlob>): Unit
```

**功能：** 异步从签名数据中恢复原始数据，通过回调返回结果。仅适用于 RSA 等支持签名恢复的算法。当恢复结果为空时，回调返回 None。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|signatureData|[DataBlob](#class-datablob)|是|-|待恢复的签名数据。|
|callback|AsyncCallback&lt;?[DataBlob](#class-datablob)&gt;|是|-|回调函数，接收恢复的原始数据或错误，数据为空时返回 None。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to obtain the native object or convert parameters. |
  | 17630001 | Crypto operation error. |
  | 17620004 | Invalid function call. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

let verify = createVerify("RSA2048|PKCS1|NoHash|Recover")
let asyKeyGenerator = createAsyKeyGenerator("RSA2048")
let signDataArr: Array<UInt8> = Array<UInt8>(256, item: 0)
try {
    asyKeyGenerator.generateKeyPair({ err, keyPair =>
        if (let Some(e) <- err) {
            throw e
        }
        if (let Some(kp) <- keyPair) {
            verify.initialize(kp.pubKey, { err1 =>
                if (let Some(e1) <- err1) {
                    throw e1
                }
                verify.recover(DataBlob(signDataArr), { err2, rawData =>
                    if (let Some(e2) <- err2) {
                        throw e2
                    }
                    if (let Some(data) <- rawData) {
                        Hilog.info(0, "", "recover data size: ${data.data.size}")
                    }
                })
            })
        }
    })
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setVerifySpec(SignSpecItem, Int32)

```cangjie
public func setVerifySpec(itemType: SignSpecItem, itemValue: Int32): Unit
```

**功能：** 设置验签参数，参数值为 Int32 类型。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|itemType|[SignSpecItem](#enum-signspecitem)|是|-|指定要设置的参数项。|
|itemValue|Int32|是|-|参数值。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

let verify = createVerify("RSA2048|PSS|SHA256|MGF1_SHA256")
try {
    verify.setVerifySpec(SignSpecItem.PssSaltLenNum, 32)
    Hilog.info(0, "", "setVerifySpec PssSaltLenNum success.")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setVerifySpec(SignSpecItem, Array<UInt8>)

```cangjie
public func setVerifySpec(itemType: SignSpecItem, itemValue: Array<UInt8>): Unit
```

**功能：** 设置验签参数，参数值为字节数组类型。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|itemType|[SignSpecItem](#enum-signspecitem)|是|-|指定要设置的参数项。|
|itemValue|Array&lt;UInt8&gt;|是|-|参数值。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |
  | 17620002 | Failed to obtain the native object or convert parameters. |
  | 17620003 | Parameter check failed. |
  | 17620004 | Invalid function call. |
  | 17630001 | Crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

let verify = createVerify("SM2_256|SM3")
let userId: Array<UInt8> = "testUserId".toUtf8Array()
try {
    verify.setVerifySpec(SignSpecItem.Sm2UserIdUint8arr, userId)
    Hilog.info(0, "", "setVerifySpec Sm2UserId success.")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getVerifySpec(SignSpecItem)

```cangjie
public func getVerifySpec(itemType: SignSpecItem): ResultSpec
```

**功能：** 获取验签参数。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|itemType|[SignSpecItem](#enum-signspecitem)|是|-|指定要获取的参数项。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [ResultSpec](#enum-resultspec) | 返回参数值包装类型。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | Memory operation failed. |
  | 17630001 | Crypto operation error. |
  | 17620003 | Parameter check failed. |

**示例：**

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

let verify = createVerify("RSA2048|PSS|SHA256|MGF1_SHA256")
try {
    verify.setVerifySpec(SignSpecItem.PssSaltLenNum, 32)
    let saltLenSpec = verify.getVerifySpec(SignSpecItem.PssSaltLenNum)
    match (saltLenSpec) {
        case ResultSpec.Int32Value(v) => Hilog.info(0, "", "saltLen: ${v}")
        case _ => ()
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class CcmParamsSpec

```cangjie
public class CcmParamsSpec <: ParamsSpec {
    public var authTag: DataBlob
    public var aad: DataBlob
    public var iv: DataBlob
    public init(algName: String, iv: DataBlob, aad: DataBlob, authTag: DataBlob)
}
```

**功能：** 加解密参数[ParamsSpec](#class-paramsspec)的子类，用于在对称加解密时作为[initialize()](#func-initializecryptomode-key-paramsspec)方法的参数。

适用于CCM模式。

> **说明：**
>
> 传入[initialize()](#func-initializecryptomode-key-paramsspec)方法前需要指定其algName属性（来源于父类[ParamsSpec](#class-paramsspec)）。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**父类型：**

- [ParamsSpec](#class-paramsspec)

### var aad

```cangjie
public var aad: DataBlob
```

**功能：** 指明加解密参数aad，长度为8字节。

**类型：** [DataBlob](#class-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### var authTag

```cangjie
public var authTag: DataBlob
```

**功能：** 指定加解密参数authTag，长度为12字节。

在CCM模式加密时，需从[doFinal()](#func-dofinaldatablob)输出的[DataBlob](#class-datablob)末尾提取12字节，作为[initialize()](#func-initializecryptomode-key-paramsspec)方法的参数[CcmParamsSpec](#class-ccmparamsspec)中的authTag。

**类型：** [DataBlob](#class-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### var iv

```cangjie
public var iv: DataBlob
```

**功能：** 指明加解密参数iv，长度为7字节。

**类型：** [DataBlob](#class-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### init(String, DataBlob, DataBlob, DataBlob)

```cangjie
public init(algName: String, iv: DataBlob, aad: DataBlob, authTag: DataBlob)
```

**功能：** 创建CcmParamsSpec实例。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|algName|String|是|-|指明对称加解密参数的算法模式。|
|iv|[DataBlob](#class-datablob)|是|-|指明加解密参数iv，长度为7字节。|
|aad|[DataBlob](#class-datablob)|是|-|指明加解密参数aad，长度为8字节。|
|authTag|[DataBlob](#class-datablob)|是|-|指定加解密参数authTag，长度为12字节。<br/>在CCM模式加密时，需从[doFinal()](#func-dofinaldatablob)输出的[DataBlob](#class-datablob)末尾提取12字节，作为[initialize()](#func-initializecryptomode-key-paramsspec)方法的参数[CcmParamsSpec](#class-ccmparamsspec)中的authTag。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ccm = CcmParamsSpec("CcmParamsSpec", DataBlob(Array<UInt8>(7, repeat: 1)), DataBlob(Array<UInt8>(8, repeat: 1)), DataBlob(Array<UInt8>(12, repeat: 1)))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class DataBlob

```cangjie
public class DataBlob {
    public var data: Array<UInt8>
    public init(data: Array<UInt8>)
}
```

**功能：** buffer数组，提供blob数据类型。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

### var data

```cangjie
public var data: Array<UInt8>
```

**功能：** 数据。

**类型：** Array\<UInt8>

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

### init(Array\<UInt8>)

```cangjie
public init(data: Array<UInt8>)
```

**功能：** 创建DataBlob对象。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|data|Array\<UInt8>|是|-|存储的数组。|

## class GcmParamsSpec

```cangjie
public class GcmParamsSpec <: ParamsSpec {
    public var aad: DataBlob
    public var iv: DataBlob
    public var authTag: DataBlob
    public init(algName: String, iv: DataBlob, aad: DataBlob, authTag: DataBlob)
}
```

**功能：** 加解密参数[ParamsSpec](#class-paramsspec)的子类，用于在对称加解密时作为[initialize()](#func-initializecryptomode-key-paramsspec)方法的参数。

适用于GCM模式。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**父类型：**

- [ParamsSpec](#class-paramsspec)

> **说明：**
> 
> 1. 传入[initialize()](#func-initializecryptomode-key-paramsspec)方法前需要指定其algName属性（来源于父类[ParamsSpec](#class-paramsspec)）。
> 2. 对于1~16字节长度的iv，加解密算法库无额外限制，但结果取决于底层openssl的支持情况。
> 3. 当aad参数不需要使用或aad长度为0时，可以将aad的data属性设置为一个空的Array\<UInt8>，来构造GcmParamsSpec，写法为aad: { data: Array\<UInt8>() }。

### var aad

```cangjie
public var aad: DataBlob
```

**功能：** 指明加解密参数aad，长度为0~INT32_MAX字节，常用为16字节。

**类型：** [DataBlob](#class-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### var authTag

```cangjie
public var authTag: DataBlob
```

**功能：** 指明加解密参数authTag，长度为16字节。

采用GCM模式加密时，需从[doFinal()](#func-dofinaldatablob)输出的[DataBlob](#class-datablob)中提取末尾16字节，作为[initialize()](#func-initializecryptomode-key-paramsspec)方法中GcmParamsSpec的authTag。

**类型：** [DataBlob](#class-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### var iv

```cangjie
public var iv: DataBlob
```

**功能：** 指明加解密参数iv，长度为1~16字节，常用为12字节。

**类型：** [DataBlob](#class-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### init(String, DataBlob, DataBlob, DataBlob)

```cangjie
public init(algName: String, iv: DataBlob, aad: DataBlob, authTag: DataBlob)
```

**功能：** 创建GcmParamsSpec实例。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|algName|String|是|-|指明对称加解密参数的算法模式。|
|iv|[DataBlob](#class-datablob)|是|-|指明加解密参数iv，长度为1~16字节，常用为12字节。|
|aad|[DataBlob](#class-datablob)|是|-|指明加解密参数aad，长度为0~INT32_MAX字节，常用为16字节。|
|authTag|[DataBlob](#class-datablob)|是|-|指明加解密参数authTag，长度为16字节。<br/>采用GCM模式加密时，需从[doFinal()](#func-dofinaldatablob)输出的[DataBlob](#class-datablob)中提取末尾16字节，作为[initialize()](#func-initializecryptomode-key-paramsspec)方法中GcmParamsSpec的authTag。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let gcm = GcmParamsSpec("GcmParamsSpec", DataBlob(Array<UInt8>(12, repeat: 1)), DataBlob(Array<UInt8>(8, repeat: 1)), DataBlob(Array<UInt8>(16, repeat: 1)))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class IvParamsSpec

```cangjie
public class IvParamsSpec <: ParamsSpec {
    public var iv: DataBlob
    public init(algName: String, iv: DataBlob)
}
```

**功能：** 加解密参数[ParamsSpec](#class-paramsspec)的子类，用于在对称加解密时作为[initialize()](#func-initializecryptomode-key-paramsspec)方法的参数。

适用于CBC、CTR、OFB、CFB、Poly1305这些需要iv作为参数的加解密模式。

> **说明：**
> 
> 传入[initialize()](#func-initializecryptomode-key-paramsspec)方法前需要指定其algName属性（来源于父类[ParamsSpec](#class-paramsspec)）。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**父类型：**

- [ParamsSpec](#class-paramsspec)

### var iv

```cangjie
public var iv: DataBlob
```

**功能：** 指明加解密参数iv。常见取值如下：

AES的CBC\|CTR\|OFB\|CFB模式：iv长度为16字节。

3DES的CBC\|OFB\|CFB模式：iv长度为8字节。

SM4的CBC\|CTR\|OFB\|CFB模式：iv长度为16字节。

**类型：** [DataBlob](#class-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### init(String, DataBlob)

```cangjie
public init(algName: String, iv: DataBlob)
```

**功能：** 创建IvParamsSpec实例。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|algName|String|是|-|指明对称加解密参数的算法模式。|
|iv|[DataBlob](#class-datablob)|是|-|指明加解密参数iv。常见取值如下：<br/>- AES的CBC\|CTR\|OFB\|CFB模式：iv长度为16字节。<br/>- 3DES的CBC\|OFB\|CFB模式：iv长度为8字节。<br/>- SM4的CBC\|CTR\|OFB\|CFB模式：iv长度为16字节。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let iv = IvParamsSpec("IvParamsSpec", DataBlob(Array<UInt8>(8, repeat: 1)))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## enum CryptoMode

```cangjie
public enum CryptoMode <: Equatable<CryptoMode> & ToString {
    | EncryptMode
    | DecryptMode
    | ...
}
```

**功能：** 表示加解密操作的枚举。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**父类型：**

- Equatable\<[CryptoMode](#enum-cryptomode)>
- ToString

### DecryptMode

```cangjie
DecryptMode
```

**功能：** 表示进行解密操作。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### EncryptMode

```cangjie
EncryptMode
```

**功能：** 表示进行加密操作。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### func !=(CryptoMode)

```cangjie
public operator func !=(other: CryptoMode): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[CryptoMode](#enum-cryptomode)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(CryptoMode)

```cangjie
public operator func ==(other: CryptoMode): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[CryptoMode](#enum-cryptomode)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum CipherSpecItem

```cangjie
public enum CipherSpecItem <: Equatable<CipherSpecItem> & ToString {
    | OaepMdNameStr
    | OaepMgfNameStr
    | OaepMgf1MdStr
    | OaepMgf1PsrcUint8Arr
    | ...
}
```

**功能：** 表示加解密参数的枚举。

当前只支持RSA算法和SM2算法。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**父类型：**

- Equatable\<[CipherSpecItem](#enum-cipherspecitem)>
- ToString

### OaepMdNameStr

```cangjie
OaepMdNameStr
```

**功能：** 表示RSA算法中，使用PKCS1_OAEP模式时，消息摘要功能的算法名。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### OaepMgfNameStr

```cangjie
OaepMgfNameStr
```

**功能：** 表示RSA算法中，使用PKCS1_OAEP模式时，掩码生成算法（目前仅支持MGF1）。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### OaepMgf1MdStr

```cangjie
OaepMgf1MdStr
```

**功能：** 表示RSA算法中，使用PKCS1_OAEP模式时，MGF1掩码生成功能的消息摘要算法。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### OaepMgf1PsrcUint8Arr

```cangjie
OaepMgf1PsrcUint8Arr
```

**功能：** 表示RSA算法中，使用PKCS1_OAEP模式时，pSource的字节流。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### func !=(CipherSpecItem)

```cangjie
public operator func !=(other: CipherSpecItem): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[CipherSpecItem](#enum-cipherspecitem)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(CipherSpecItem)

```cangjie
public operator func ==(other: CipherSpecItem): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[CipherSpecItem](#enum-cipherspecitem)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum AsyKeySpecItem

```cangjie
public enum AsyKeySpecItem {
    | DsaPBn
    | DsaQBn
    | DsaGBn
    | DsaSkBn
    | DsaPkBn
    | EccFpPBn
    | EccABn
    | EccBBn
    | EccGXBn
    | EccGYBn
    | EccNBn
    | EccHNum
    | EccSkBn
    | EccPkXBn
    | EccPkYBn
    | EccFieldTypeStr
    | EccFieldSizeNum
    | EccCurveNameStr
    | RsaNBn
    | RsaSkBn
    | RsaPkBn
    | DhPBn
    | DhGBn
    | DhLNum
    | DhSkBn
    | DhPkBn
    | Ed25519SkBn
    | Ed25519PkBn
    | X25519SkBn
    | X25519PkBn
    | ...
}
```

**功能：** 非对称密钥参数的枚举，用于指定获取非对称密钥的某个参数。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### DsaPBn

```cangjie
DsaPBn
```

**功能：** DSA算法中素数p。p是公开参数，指定位长度。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### DsaQBn

```cangjie
DsaQBn
```

**功能：** DSA算法中160位素数q，q是p-1的因子。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### DsaGBn

```cangjie
DsaGBn
```

**功能：** DSA算法中参数g，g是公开参数，是模p的子群的生成元。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### DsaSkBn

```cangjie
DsaSkBn
```

**功能：** DSA算法中私钥sk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### DsaPkBn

```cangjie
DsaPkBn
```

**功能：** DSA算法中公钥pk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccFpPBn

```cangjie
EccFpPBn
```

**功能：** ECC算法中素数域的素数p。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccABn

```cangjie
EccABn
```

**功能：** ECC算法中椭圆曲线参数a。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccBBn

```cangjie
EccBBn
```

**功能：** ECC算法中椭圆曲线参数b。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccGXBn

```cangjie
EccGXBn
```

**功能：** ECC算法中基点G的x坐标。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccGYBn

```cangjie
EccGYBn
```

**功能：** ECC算法中基点G的y坐标。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccNBn

```cangjie
EccNBn
```

**功能：** ECC算法中基点G的阶n。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccHNum

```cangjie
EccHNum
```

**功能：** ECC算法中余因子h。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccSkBn

```cangjie
EccSkBn
```

**功能：** ECC算法中私钥sk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccPkXBn

```cangjie
EccPkXBn
```

**功能：** ECC算法中公钥Pk的x坐标。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccPkYBn

```cangjie
EccPkYBn
```

**功能：** ECC算法中公钥Pk的y坐标。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccFieldTypeStr

```cangjie
EccFieldTypeStr
```

**功能：** ECC算法中域类型。当前只支持Fp域。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccFieldSizeNum

```cangjie
EccFieldSizeNum
```

**功能：** ECC算法中域大小。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### EccCurveNameStr

```cangjie
EccCurveNameStr
```

**功能：** ECC算法中曲线名称。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### RsaNBn

```cangjie
RsaNBn
```

**功能：** RSA算法中模数n。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### RsaSkBn

```cangjie
RsaSkBn
```

**功能：** RSA算法中私钥指数sk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### RsaPkBn

```cangjie
RsaPkBn
```

**功能：** RSA算法中公钥指数pk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### DhPBn

```cangjie
DhPBn
```

**功能：** DH算法中素数p。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### DhGBn

```cangjie
DhGBn
```

**功能：** DH算法中参数g。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### DhLNum

```cangjie
DhLNum
```

**功能：** DH算法中素数p的位长度l。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### DhSkBn

```cangjie
DhSkBn
```

**功能：** DH算法中私钥sk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### DhPkBn

```cangjie
DhPkBn
```

**功能：** DH算法中公钥pk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### Ed25519SkBn

```cangjie
Ed25519SkBn
```

**功能：** Ed25519算法中私钥sk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### Ed25519PkBn

```cangjie
Ed25519PkBn
```

**功能：** Ed25519算法中公钥pk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### X25519SkBn

```cangjie
X25519SkBn
```

**功能：** X25519算法中私钥sk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### X25519PkBn

```cangjie
X25519PkBn
```

**功能：** X25519算法中公钥pk。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### prop value

```cangjie
public prop value: Int32
```

**功能：** 获取枚举的Int32类型值。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|Int32|枚举的Int32类型值。|

### func !=(AsyKeySpecItem)

```cangjie
public operator func !=(other: AsyKeySpecItem): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[AsyKeySpecItem](#enum-asykeyspecitem)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(AsyKeySpecItem)

```cangjie
public operator func ==(other: AsyKeySpecItem): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[AsyKeySpecItem](#enum-asykeyspecitem)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的说明。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum ResultSpec

```cangjie
public enum ResultSpec {
    | BigintValue(BigInt)
    | Int32Value(Int32)
    | StringValue(String)
    | Uint8ArrayValue(Array<UInt8>)
    | ...
}
```

**功能：** 非对称密钥参数返回值的枚举，用于包装不同类型的密钥参数返回值。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### BigintValue(BigInt)

```cangjie
BigintValue(BigInt)
```

**功能：** 表示返回值为BigInt类型的密钥参数。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### Int32Value(Int32)

```cangjie
Int32Value(Int32)
```

**功能：** 表示返回值为Int32类型的密钥参数。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### StringValue(String)

```cangjie
StringValue(String)
```

**功能：** 表示返回值为String类型的密钥参数。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### Uint8ArrayValue(Array<UInt8>)

```cangjie
Uint8ArrayValue(Array<UInt8>)
```

**功能：** 表示返回值为Array<UInt8>类型的密钥参数。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

### func !=(ResultSpec)

```cangjie
public operator func !=(other: ResultSpec): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[ResultSpec](#enum-resultspec)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(ResultSpec)

```cangjie
public operator func ==(other: ResultSpec): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[ResultSpec](#enum-resultspec)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的说明。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.AsymKey

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum SignSpecItem

```cangjie
public enum SignSpecItem {
    | PssMdNameStr
    | PssMgfNameStr
    | PssMgf1MdStr
    | PssSaltLenNum
    | PssTrailerFieldNum
    | Sm2UserIdUint8arr
    | MlDsaDeterministicBool
    | MlDsaMuBool
    | MlDsaContextUint8arr
    | ...
}
```

**功能：** 签名验签参数的枚举，用于指定签名验签过程中的特定参数项。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### PssMdNameStr

```cangjie
PssMdNameStr
```

**功能：** RSA-PSS签名验签中，用于指定消息摘要算法。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### PssMgfNameStr

```cangjie
PssMgfNameStr
```

**功能：** RSA-PSS签名验签中，用于指定掩码生成函数（MGF）。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### PssMgf1MdStr

```cangjie
PssMgf1MdStr
```

**功能：** RSA-PSS签名验签中，用于指定MGF1的消息摘要算法。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### PssSaltLenNum

```cangjie
PssSaltLenNum
```

**功能：** RSA-PSS签名验签中，用于指定盐长度。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### PssTrailerFieldNum

```cangjie
PssTrailerFieldNum
```

**功能：** RSA-PSS签名验签中，用于指定尾部字段。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### Sm2UserIdUint8arr

```cangjie
Sm2UserIdUint8arr
```

**功能：** SM2签名验签中，用于指定用户ID。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### MlDsaDeterministicBool

```cangjie
MlDsaDeterministicBool
```

**功能：** ML-DSA签名验签过程中是否使用确定性签名。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### MlDsaMuBool

```cangjie
MlDsaMuBool
```

**功能：** ML-DSA签名验签过程中的mu参数值。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### MlDsaContextUint8arr

```cangjie
MlDsaContextUint8arr
```

**功能：** ML-DSA签名验签过程中的上下文数据。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

### prop value

```cangjie
public prop value: Int32
```

**功能：** 获取枚举的Int32类型值。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|Int32|枚举的Int32类型值。|

### func !=(SignSpecItem)

```cangjie
public operator func !=(other: SignSpecItem): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[SignSpecItem](#enum-signspecitem)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(SignSpecItem)

```cangjie
public operator func ==(other: SignSpecItem): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[SignSpecItem](#enum-signspecitem)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的说明。

**系统能力：** SystemCapability.Security.CryptoFramework.Signature

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|
