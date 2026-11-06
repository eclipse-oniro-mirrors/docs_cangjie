# Key Deletion (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

To ensure data security, keys should be deleted when they are no longer needed.

## Development Procedure

Taking the deletion of an HKDF256 key as an example:

1. Determine the key alias `keyAlias`. The maximum length of a key alias is 128 bytes.

2. Initialize the key attribute set. Used to specify [Key Attribute TAG](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag) during deletion. When deleting a single key, the TAG field can be left empty.

3. Call the [deleteKeyItem](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-deletekeyitemstring-huksoptions) interface to delete the key.

## Example

<!-- compile -->

```cangjie
/*
 * The following demonstrates operations using an HKDF256 key as an example
 */
import kit.PerformanceAnalysisKit.Hilog
import kit.UniversalKeystoreKit.*

/* 1. Determine key alias */
let keyAlias = "test_Key"

/* 2. Construct empty object */
let huksOptions: HuksOptions = HuksOptions()

class ThrowObject {
    var isThrow: Bool = false

    init(isThrow: Bool) {
        this.isThrow = isThrow
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

/* 3. Delete key */
func publicDeleteKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
    Hilog.info(1, "info", "enter deleteKeyItem")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        deleteKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        Hilog.error(1, "info", "deleteKeyItem input arg invalid, ${e}")
    }
}

func testDerive() {
    publicDeleteKeyFunc(keyAlias, huksOptions)
}
```