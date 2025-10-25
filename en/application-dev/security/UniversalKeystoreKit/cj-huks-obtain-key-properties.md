# Get Key Attributes (Cangjie)

HUKS provides interfaces for applications to retrieve relevant attributes of specified keys. Before obtaining the attributes of a specified key, ensure that the key has been generated or imported into HUKS with persistent storage.

> **Note:**
>
> Lightweight devices do not support the key attribute retrieval functionality.

## Development Steps

1. Specify the key alias `keyAlias` to be queried. The maximum length of a key alias is 128 bytes.

2. Call the interface [getKeyItemProperties](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-getkeyitempropertiesstring-huksoptions), passing the parameters `keyAlias` and `options`. The `options` parameter is reserved and can currently be passed as an empty value.

3. The return value is an object of type `Array<[HuksParam](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksparam)>`. The retrieved attribute collection is stored in the `properties` field.

## Example

<!-- compile -->

```cangjie
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.UniversalKeystoreKit.*

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

func test() {
    /* 1. Set key alias */
    let keyAlias = "keyAlias"
    /* Pass empty options object */
    let emptyOptions: HuksOptions = HuksOptions(properties: [], inData: Bytes())
    try {
        /* 2. Retrieve key attributes */
        getKeyItemProperties(keyAlias, emptyOptions)
        loggerInfo("getKeyItemProperties success")
    } catch (e: Exception) {
        loggerInfo("getKeyItemProperties input arg invalid, ${e.toString()}")
    }
}
```