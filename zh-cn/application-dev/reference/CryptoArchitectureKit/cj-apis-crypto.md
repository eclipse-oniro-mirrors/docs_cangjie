# ohos.security.crypto_framework（加解密算法库框架）

为屏蔽底层硬件和算法库，向上提供统一的密码算法库加解密相关接口。

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

<!-- 支持的规格详见[对称密钥加解密算法规格](../cj-development-intro.md#对称密钥加解密算法规格)和[非对称密钥加解密算法规格](../cj-development-intro.md#非对称密钥加解密算法规格)。 -->
支持的规格详见[对称密钥加解密算法规格](../../../zh-cn/application-dev/security/CryptoArchitectureKit/cj-crypto-sym-encrypt-decrypt-spec.md#对称密钥加解密算法规格)和[非对称密钥加解密算法规格](../../../zh-cn/application-dev/security/CryptoArchitectureKit/cj-crypto-asym-encrypt-decrypt-spec.md#非对称密钥加解密算法规格)。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|transformation|String|是|-|待生成Cipher的算法名称（含密钥长度）、加密模式以及填充方法的组合。|

**返回值：**

|类型|说明|
|:----|:----|
|[Cipher](#class-cipher)|返回加解密生成器的对象。|

**异常：**

- BusinessException：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | memory error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let cipherAlgName = "3DES192|ECB|PKCS7"
let cipher = createCipher(cipherAlgName)
```

## func createMac(String)

```cangjie
public func createMac(algName: String): Mac
```

**功能：** 生成Mac实例，用于进行消息认证码的计算与操作。

**系统能力：** SystemCapability.Security.CryptoFramework.Mac

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|algName|String|是|-|指定摘要算法。|

**返回值：**

|类型|说明|
|:----|:----|
|[Mac](#class-mac)|返回由输入算法指定生成的Mac对象。|

**异常：**

- BusinessException：对应错误码的详细介绍请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  |错误码ID|错误信息|
  |:---|:---|
  |401|invalid parameters.|
  |17620001|memory error.|

**示例：**

<!-- compile -->

```cangjie
// index.cj
import kit.CryptoArchitectureKit.*

var mac = createMac("SHA256")
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

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj
import kit.CryptoArchitectureKit.*

let md = createMd("SHA256")
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

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj
import kit.CryptoArchitectureKit.*

let rand = createRandom()
```

## func createSymKeyGenerator(String)

```cangjie
public func createSymKeyGenerator(algName: String): SymKeyGenerator
```

**功能：** 通过指定算法名称的字符串，获取相应的对称密钥生成器实例。

支持的规格详见[对称密钥生成和转换规格](../../../zh-cn/application-dev/security/CryptoArchitectureKit/cj-crypto-sym-key-generation-conversion-spec.md)。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|algName|String|是|-|待生成对称密钥生成器的算法名称。具体取值详见[对称密钥生成和转换规格](../../../zh-cn/application-dev/security/CryptoArchitectureKit/cj-crypto-sym-key-generation-conversion-spec.md)一节中的“字符串参数”。|

**返回值：**

|类型|说明|
|:----|:----|
|[SymKeyGenerator](#class-symkeygenerator)|返回对称密钥生成器的对象。|

**异常：**

- BusinessException：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let symKeyGenerator = createSymKeyGenerator("3DES192")
```

## interface Key

```cangjie
public interface Key {
    prop format: String
    prop algName: String
    func getEncoded(): DataBlob
}
```

**功能：** 密钥（接口），在运行密码算法（如加解密）时需要提前生成其子类对象，并传入[Cipher](#class-cipher)实例的[createCipher(String)](#func-createcipherstring)方法。

密钥可以通过密钥生成器来生成。

**系统能力：** SystemCapability.Security.CryptoFramework.Key

**起始版本：** 22

### prop algName

```cangjie
prop algName: String
```

**功能：** 密钥对应的算法名（含长度）。

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

**功能：** 同步方法，获取密钥数据的字节流。密钥可以为对称密钥，公钥或者私钥。其中，公钥格式满足ASN.1语法、X.509规范、DER编码格式；私钥格式满足ASN.1语法，PKCS#8规范、DER编码方式。

> **说明：**
>
> RSA算法使用密钥参数生成私钥时，私钥对象不支持getEncoded。

**系统能力：** SystemCapability.Security.CryptoFramework.Key

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#struct-datablob)|用于查看密钥的具体内容。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let generator = createSymKeyGenerator("3DES192") // The key is generated by a key generator. The generation process is omitted here.
let key = generator.generateSymKey()
let encodedKey = key.getEncoded()
```

## class ParamsSpec

```cangjie
public class ParamsSpec {
    mut prop algName: String
    mut prop iv: DataBlob
}
```

**功能：** 加解密参数，在进行对称加解密时需要构造其子类对象，并将子类对象传入[createCipher(String)](#func-createcipherstring)方法。

适用于需要iv等参数的对称加解密模式（对于无iv等参数的模式如ECB模式，无需构造，在[createCipher(String)](#func-createcipherstring)中传入None即可）。

> **说明：**
>
> 由于[createCipher(String)](#func-createcipherstring)的params参数是ParamsSpec类型（父类），而实际需要传入具体的子类对象（如IvParamsSpec），因此在构造子类对象时应设置其父类ParamsSpec的algName参数，使算法库在init()时知道传入的是哪种子类对象。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### var algName

```cangjie
mut var algName: String
```

**功能：** 指明对称加解密参数的算法模式。可选值如下:<br/> - IvParamsSpec: 适用于CBCMagIc_StrINgCTRMagIc_StrINgOFBMagIc_StrINgCFB模式。<br/> - GcmParamsSpec: 适用于GCM模式。<br/> - CcmParamsSpec: 适用于CCM模式。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

## class Cipher

```cangjie
public class Cipher {}
```

**功能：** 提供加解密的算法操作功能，按序调用本类中的[createCipher(String)](#func-createcipherstring)、[update()](#func-updatedatablob)、[doFinal()](#func-dofinaldatablob)方法，可以实现对称加密/对称解密/非对称加密/非对称解密。

一次完整的加/解密流程在对称加密和非对称加密中略有不同：

- 对称加解密：init为必选，update为可选（且允许多次update加/解密大数据），doFinal为必选；doFinal结束后可以重新init开始新一轮加/解密流程。
- RSA、SM2非对称加解密：init为必选，不支持update操作，doFinal为必选（允许连续多次doFinal加/解密大数据）；RSA不支持重复init，切换加解密模式或填充方式时，需要重新创建Cipher对象。

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

**功能：** 初始化加解密的[cipher](#class-cipher)对象，通过注册回调函数获取结果。

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

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory error. |
  | 17620002 | runtime error. |
  | 17630001 | crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

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
```

### func doFinal(?DataBlob)

```cangjie
public func doFinal(data: ?DataBlob): DataBlob
```

**功能：** （1）在对称加解密中，doFinal加/解密（分组模式产生的）剩余数据和本次传入的数据，最后结束加密或者解密数据操作，获取加密或者解密数据。

如果数据量较小，可以在doFinal中一次性传入数据，而不使用update；如果在本次加解密流程中，已经使用update传入过数据，可以在doFinal的data参数处传入None。

根据对称加解密的模式不同，doFinal的输出有如下区别：

- 对于GCM和CCM模式的对称加密：一次加密流程中，如果将每一次update和doFinal的结果拼接起来，会得到“密文+authTag”，即末尾的16字节（GCM模式）或12字节（CCM模式）是authTag，而其余部分均为密文。（也就是说，如果doFinal的data参数传入None，则doFinal的结果就是authTag）authTag需要填入解密时的[GcmParamsSpec](#struct-gcmparamsspec)或[CcmParamsSpec](#struct-ccmparamsspec)；密文则作为解密时的入参data。
- 对于其他模式的对称加解密、GCM和CCM模式的对称解密：一次加/解密流程中，每一次update和doFinal的结果拼接起来，得到完整的明文/密文。

（2）在RSA、SM2非对称加解密中，doFinal加/解密本次传入的数据，获取加密或者解密数据。如果数据量较大，可以多次调用doFinal，拼接结果得到完整的明文/密文。

> **说明：**
>
> - 对称加解密中，调用doFinal标志着一次加解密流程已经完成，即[Cipher](#class-cipher)实例的状态被清除，因此当后续开启新一轮加解密流程时，需要重新调用init()并传入完整的参数列表进行初始化
>（比如即使是对同一个Cipher实例，采用同样的对称密钥，进行加密然后解密，则解密中调用init的时候仍需填写params参数，而不能直接省略为None）。
> - 如果遇到解密失败，需检查加解密数据和init时的参数是否匹配，包括GCM模式下加密得到的authTag是否填入解密时的GcmParamsSpec等。
> - doFinal的结果可能为空，因此使用.data字段访问doFinal结果的具体数据前，请记得先判断结果是否为空，避免产生异常。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|data|?[DataBlob](#struct-datablob)|是|-|加密或者解密的数据。data参数允许为None，但不允许传入{data: Array\<UInt8>() }。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#struct-datablob)|返回剩余数据的加/解密结果DataBlob。|

**异常：**

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory error. |
  | 17620002 | runtime error. |
  | 17630001 | crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

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
```

### func update(DataBlob)

```cangjie
public func update(data: DataBlob): DataBlob
```

**功能：** 分段更新加密或者解密数据操作，获取加/解密数据。

必须在对[Cipher](#class-cipher)实例使用[createCipher(String)](#func-createcipherstring)初始化后，才能使用本函数。

> **说明：**
>
> - 在进行对称加解密操作的时候，如果开发者对各个分组模式不够熟悉，建议对每次update和doFinal的结果都判断是否为空数组，并在结果不为空数组时取出其中的数据进行拼接，形成完整的密文/明文。这是因为选择的分组模式等各项规格都可能对update和doFinal结果产生影响。
>（例如对于ECB和CBC模式，不论update传入的数据是否为分组长度的整数倍，都会以分组作为基本单位进行加/解密，并输出本次update新产生的加/解密分组结果。
> 可以理解为，update只要凑满一个新的分组就会有输出，如果没有凑满则此次update输出为None，把当前还没被加/解密的数据留着，等下一次update/doFinal传入数据的时候，拼接起来继续凑分组。
> 最后doFinal的时候，会把剩下的还没加/解密的数据，根据[createCipher](#func-createcipherstring)时设置的padding模式进行填充，补齐到分组的整数倍长度，再输出剩余加解密结果。
> 而对于可以将分组密码转化为流模式实现的模式，还可能出现密文长度和明文长度相同的情况等。）
> - 根据数据量，可以不调用update（即init完成后直接调用doFinal）或多次调用update。
> 算法库目前没有对update（单次或累计）的数据量设置大小限制，建议对于大数据量的对称加解密，可以采用多次update的方式传入数据。
> - RSA、SM2非对称加解密不支持update操作。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|data|[DataBlob](#struct-datablob)|是|-|加密或者解密的数据。data不允许传入{data: Array\<UInt8>() }。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#struct-datablob)|返回此次更新的加/解密结果DataBlob。|

**异常：**

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory error. |
  | 17620002 | runtime error. |
  | 17630001 | crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

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

**功能：** 使用对称密钥初始化[Mac](#class-mac)计算，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Security.CryptoFramework.Mac

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|key|[SymKey](#class-symkey)|是|-|共享对称密钥。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let skg = createSymKeyGenerator("AES128")
let sk = skg.generateSymKey()
let mac = createMac("SHA256")
mac.initialize(sk)
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
|[DataBlob](#struct-datablob)|返回计算结果DataBlob。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let mac = createMac("SHA256")

let skg = createSymKeyGenerator("AES128")
let sk = skg.generateSymKey()
mac.initialize(sk)
let blob = DataBlob("this is test!".toArray())
mac.update(blob)
mac.doFinal()
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

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let mac = createMac("SHA256")
let skg = createSymKeyGenerator("AES128")
let sk = skg.generateSymKey()
mac.initialize(sk)
let blob = DataBlob("this is test!".toArray())
mac.update(blob)
mac.doFinal()
var macLen = mac.getMacLength()
```

### func update(DataBlob)

```cangjie
public func update(input: DataBlob): Unit
```

**功能：** 传入消息进行Mac更新计算。

**系统能力：** SystemCapability.Security.CryptoFramework.Mac

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|input|[DataBlob](#struct-datablob)|是|-|传入的消息。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let mac = createMac("SHA256")
let skg = createSymKeyGenerator("AES128")
let sk = skg.generateSymKey()
mac.initialize(sk)
let blob = DataBlob("this is test!".toArray())
mac.update(blob)
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
|[DataBlob](#struct-datablob)|返回计算结果DataBlob。|

**异常：**

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory error. |
  | 17630001 | crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let md = createMd("SHA256")
let blob: DataBlob = DataBlob("test".toArray())
md.update(blob)
let res = md.digest()
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

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17630001 | crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let md = createMd("SHA256")
let mdLen = md.getMdLength()
```

### func update(DataBlob)

```cangjie
public func update(input: DataBlob): Unit
```

**功能：** 传入消息进行Md更新计算。

**系统能力：** SystemCapability.Security.CryptoFramework.MessageDigest

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|input|[DataBlob](#struct-datablob)|是|-|传入的消息。|

**异常：**

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory operation failed. |
  | 17630001 | crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let md = createMd("SHA256")
let blob: DataBlob = DataBlob("test".toArray())
md.update(blob)
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

**功能：** 生成指定长度的随机数并返回。

**系统能力：** SystemCapability.Security.CryptoFramework.Rand

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|len|Int32|是|-|表示生成随机数的长度，单位为byte，范围在[1, INT32_MAX]。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#struct-datablob)|DataBlob对象。|

**异常：**

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory error. |
  | 17630001 | crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let rand = createRandom()
let promiseGenerateRand = rand.generateRandom(12)
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
|seed|[DataBlob](#struct-datablob)|是|-|设置的种子。|

**异常：**

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let rand = createRandom()
rand.setSeed(DataBlob("test".toArray()))
```

## class SymKey

```cangjie
public class SymKey <:  Key {}
```

**功能：** 对称密钥，是[Key](#interface-key)的子类，在对称加解密时需要将其对象传入[Cipher](#class-cipher)实例的[createCipher(String)](#func-createcipherstring)方法使用。

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

**功能：** 同步方法，将系统底层内存中的的密钥内容清零。建议在不需要使用对称密钥实例时，调用本函数，避免内存中密钥数据存留过久。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.PerformanceAnalysisKit.*

let generator = createSymKeyGenerator("3DES192")
let key = generator.generateSymKey()
var encodedKey = key.getEncoded()
Hilog.info(0, "AppLogCj", "key blob: ${encodedKey.data}") // Display key content.
key.clearMem()
encodedKey = key.getEncoded()
Hilog.info(0, "AppLogCj", "key blob: ${encodedKey.data}") // Display all 0s.
```

### func getEncoded()

```cangjie
public func getEncoded(): DataBlob
```

**功能：** 同步方法，获取密钥数据的字节流。密钥可以为对称密钥，公钥或者私钥。其中，公钥格式满足ASN.1语法、X.509规范、DER编码格式；私钥格式满足ASN.1语法，PKCS#8规范、DER编码方式。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[DataBlob](#struct-datablob)|用于查看密钥的具体内容。|

**异常：**

- BusinessException：对应错误码如下表，请参见[通用错误码](../cj-errorcode-universal.md)和[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | this operation is not supported. |
  | 17620001 | memory error. |
  | 17630001 | crypto operation error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*
import kit.PerformanceAnalysisKit.*

let generator = createSymKeyGenerator("3DES192")
let key = generator.generateSymKey()
var encodedKey = key.getEncoded()
Hilog.info(0, "AppLogCj", "key blob: ${encodedKey.data}") // Display key content.
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
> 对于HMAC算法的对称密钥，如果已经在创建对称密钥生成器时指定了具体哈希算法（如指定“HMAC|SHA256”），则需要传入与哈希长度一致的二进制密钥数据（如传入SHA256对应256位的密钥数据）。
> 如果在创建对称密钥生成器时没有指定具体哈希算法，如仅指定“HMAC”，则支持传入长度在[1,4096]范围内（单位为byte）的任意二进制密钥数据。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|key|[DataBlob](#struct-datablob)|是|-|指定的密钥材料数据。|

**返回值：**

|类型|说明|
|:----|:----|
|[SymKey](#class-symkey)|返回对称密钥SymKey。|

**异常：**

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let arr: Array<UInt8> = [0xba, 0x3d, 0xc2, 0x71, 0x21, 0x1e, 0x30, 0x56, 0xad, 0x47, 0xfc, 0x5a,
    0x46, 0x39, 0xee, 0x7c, 0xba, 0x3b, 0xc2, 0x71, 0xab, 0xa0, 0x30, 0x72] // keyLen = 192 (24 bytes)
let symAlgName = "3DES192"
let symKeyGenerator = createSymKeyGenerator(symAlgName)
symKeyGenerator.convertKey(DataBlob(arr))
```

### func generateSymKey()

```cangjie
public func generateSymKey(): SymKey
```

**功能：** 获取该对称密钥生成器随机生成的密钥。

必须在使用[createSymKeyGenerator](#func-createsymkeygeneratorstring)创建对称密钥生成器后，才能使用本函数。

目前支持使用OpenSSL的RAND_priv_bytes()作为底层能力生成随机密钥。

**系统能力：** SystemCapability.Security.CryptoFramework.Key.SymKey

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[SymKey](#class-symkey)|对称密钥SymKey。|

**异常：**

- BusinessException：对应错误码如下表，请参见[crypto framework错误码](./cj-errorcode-crypto.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 17620001 | memory error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let symAlgName = "AES128"
let symKeyGenerator = createSymKeyGenerator(symAlgName)
let symKey = symKeyGenerator.generateSymKey()
```

## struct CcmParamsSpec

```cangjie
public struct CcmParamsSpec <: ParamsSpec {
    public init(algName: String, iv: DataBlob, add: DataBlob, authTag: DataBlob)
}
```

**功能：** 加解密参数[ParamsSpec](#class-paramsspec)的子类，用于在对称加解密时作为[createCipher(String)](#func-createcipherstring)方法的参数。

适用于CCM模式。

> **说明：**
>
> 传入[createCipher(String)](#func-createcipherstring)方法前需要指定其algName属性（来源于父类[ParamsSpec](#class-paramsspec)）。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**父类型：**

- [ParamsSpec](#class-paramsspec)

### prop aad

```cangjie
public mut prop aad: DataBlob
```

**功能：** 指明加解密参数aad，长度为8字节。

**类型：** [DataBlob](#struct-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### prop authTag

```cangjie
public mut prop authTag: DataBlob
```

**功能：** 指明加解密参数authTag，长度为12字节。<br/>采用CCM模式加密时，需要获取[doFinal()](#func-dofinaldatablob)输出的[DataBlob](#struct-datablob)，取出其末尾12字节作为解密时[createCipher(String)](#func-createcipherstring)方法的入参[CcmParamsSpec](#struct-ccmparamsspec)中的authTag。

**类型：** [DataBlob](#struct-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### prop iv

```cangjie
public mut prop iv: DataBlob
```

**功能：** 指明加解密参数iv，长度为7字节。

**类型：** [DataBlob](#struct-datablob)

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
|algName|String|是|-|指明对称加解密参数的算法模式。可选值如下:<br/> - IvParamsSpec: 适用于CBCMagIc_StrINgCTRMagIc_StrINgOFBMagIc_StrINgCFB模式。<br/> - GcmParamsSpec: 适用于GCM模式。<br/> - CcmParamsSpec: 适用于CCM模式。|
|iv|[DataBlob](#struct-datablob)|是|-|指明加解密参数iv，长度为7字节。|
|aad|[DataBlob](#struct-datablob)|是|-|指明加解密参数aad，长度为8字节。|
|authTag|[DataBlob](#struct-datablob)|是|-|指明加解密参数authTag，长度为12字节。采用CCM模式加密时，需要获取doFinal()或doFinalSync()输出的DataBlob，取出其末尾12字节作为解密时init()或initSync()方法的入参CcmParamsSpec中的authTag。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let ccm = GcmParamsSpec("CcmParamsSpec", DataBlob(Array<UInt8>(7, repeat: 1)), DataBlob(Array<UInt8>(8, repeat: 1)), DataBlob(Array<UInt8>(12, repeat: 1)))
```

## struct DataBlob

```cangjie
public struct DataBlob {
    public DataBlob(
        public let data: Array<UInt8>
    )
}
```

**功能：** 存储数组的数据类型。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

### let data

```cangjie
public let data: Array<UInt8>
```

**功能：** 数据。

**类型：** Array\<UInt8>

**读写能力：** 只读

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

## struct GcmParamsSpec

```cangjie
public struct GcmParamsSpec <: ParamsSpec {
    public init(algName: String, iv: DataBlob, add: DataBlob, authTag: DataBlob)
}
```

**功能：** 加解密参数[ParamsSpec](#class-paramsspec)的子类，用于在对称加解密时作为[createCipher(String)](#func-createcipherstring)方法的参数。

适用于GCM模式。

> **说明：**
>
> 传入[createCipher(String)](#func-createcipherstring)方法前需要指定其algName属性（来源于父类[ParamsSpec](#class-paramsspec)）。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**父类型：**

- [ParamsSpec](#class-paramsspec)

### prop aad

```cangjie
public mut prop aad: DataBlob
```

**功能：** 指明加解密参数aad，长度为8字节。

**类型：** [DataBlob](#struct-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### prop authTag

```cangjie
public mut prop authTag: DataBlob
```

**功能：** 指明加解密参数authTag，长度为16字节。<br/>采用GCM模式加密时，需要获取[doFinal()](#func-dofinaldatablob)输出的[DataBlob](#struct-datablob)，取出其末尾16字节作为解密时[createCipher(String)](#func-createcipherstring)方法的入参[GcmParamsSpec](#struct-gcmparamsspec)中的的authTag。

**类型：** [DataBlob](#struct-datablob)

**读写能力：** 可读写

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

### prop iv

```cangjie
public mut prop iv: DataBlob
```

**功能：** 指明加解密参数iv，长度为12字节。

**类型：** [DataBlob](#struct-datablob)

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
|algName|String|是|-|指明对称加解密参数的算法模式。可选值如下:<br/>- IvParamsSpec:适用于CBCMagIc_StrINgCTRMagIc_StrINgOFBMagIc_StrINgCFB模式。<br/> - GcmParamsSpec: 适用于GCM模式。<br/> - CcmParamsSpec: 适用于CCM模式。|
|iv|[DataBlob](#struct-datablob)|是|-|指明加解密参数iv，长度为12字节。|
|aad|[DataBlob](#struct-datablob)|是|-|指明加解密参数aad，长度为8字节。|
|authTag|[DataBlob](#struct-datablob)|是|-|指明加解密参数authTag，长度为16字节。<br/>采用GCM模式加密时，需要获取[doFinal()](#func-dofinaldatablob)输出的[DataBlob](#struct-datablob)，取出其末尾16字节作为解密时[createCipher(String)](#func-createcipherstring)方法的入参[GcmParamsSpec](#struct-gcmparamsspec)中的的authTag。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let gcm = GcmParamsSpec("GcmParamsSpec", DataBlob(Array<UInt8>(12, repeat: 1)), DataBlob(Array<UInt8>(8, repeat: 1)), DataBlob(Array<UInt8>(16, repeat: 1)))
```

## struct IvParamsSpec

```cangjie
public struct IvParamsSpec <: ParamsSpec {
    public init(algName: String, iv: DataBlob)
}
```

**功能：** 加解密参数[ParamsSpec](#class-paramsspec)的子类，用于在对称加解密时作为[createCipher(String)](#func-createcipherstring)方法的参数。

适用于CBC、CTR、OFB、CFB这些仅使用iv作为参数的加解密模式。

> **说明：**
>
> 传入[createCipher(String)](#func-createcipherstring)方法前需要指定其algName属性（来源于父类[ParamsSpec](#class-paramsspec)）。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**父类型：**

- [ParamsSpec](#class-paramsspec)

### prop iv

```cangjie
public mut prop iv: DataBlob
```

**功能：** 指明加解密参数iv。常见取值如下：<br/>- AES的CBCMagIc_StrINgCTRMagIc_StrINgOFBMagIc_StrINgCFB模式：iv长度为16字节<br/>- 3DES的CBCMagIc_StrINgOFBMagIc_StrINgCFB模式：iv长度为8字节<br/>- SM4的CBCMagIc_StrINgCTRMagIc_StrINgOFBMagIc_StrINgCFB模式：iv长度为16字节。

**类型：** [DataBlob](#struct-datablob)

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
|algName|String|是|-|指明对称加解密参数的算法模式。可选值如下:<br/> - IvParamsSpec: 适用于CBCMagIc_StrINgCTRMagIc_StrINgOFBMagIc_StrINgCFB模式。<br/> - GcmParamsSpec: 适用于GCM模式。<br/> - CcmParamsSpec: 适用于CCM模式。|
|iv|[DataBlob](#struct-datablob)|是|-|指明加解密参数iv。常见取值如下：<br/>- AES的CBCMagIc_StrINgCTRMagIc_StrINgOFBMagIc_StrINgCFB模式：iv长度为16字节<br/>- 3DES的CBCMagIc_StrINgOFBMagIc_StrINgCFB模式：iv长度为8字节<br/>- SM4的CBCMagIc_StrINgCTRMagIc_StrINgOFBMagIc_StrINgCFB模式：iv长度为16字节。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CryptoArchitectureKit.*

let iv = IvParamsSpec("IvParamsSpec", DataBlob(Array<UInt8>(8, repeat: 1)))
```

## enum CryptoMode

```cangjie
public enum CryptoMode <: Equatable<CryptoMode> & ToString {
    | EncryptMode
    | DecryptMode
    | ...
}
```

**功能：** 表示加解密操作。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**父类型：**

- Equatable\<CryptoMode>
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

**功能：** 表示加解密参数的枚举。当前只支持RSA算法和SM2算法。

**系统能力：** SystemCapability.Security.CryptoFramework.Cipher

**起始版本：** 22

**父类型：**

- Equatable\<CipherSpecItem>
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

## enum Result

```cangjie
public enum Result <: ToString {
    | InvalidParams
    | NotSupport
    | ErrOutOfMemory
    | ErrRuntimeError
    | ErrCryptoOperation
    | ...
}
```

**功能：** 表示执行结果。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

**父类型：**

- ToString

### ErrCryptoOperation

```cangjie
ErrCryptoOperation
```

**功能：** 调用三方算法库API出错。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

### ErrOutOfMemory

```cangjie
ErrOutOfMemory
```

**功能：** 内存错误。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

### ErrRuntimeError

```cangjie
ErrRuntimeError
```

**功能：** 运行时外部错误。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

### InvalidParams

```cangjie
InvalidParams
```

**功能：** 非法入参。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

### NotSupport

```cangjie
NotSupport
```

**功能：** 操作不支持。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

### func getValue()

```cangjie
public func getValue(): Int32
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Int32|枚举的值。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Security.CryptoFramework

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|
