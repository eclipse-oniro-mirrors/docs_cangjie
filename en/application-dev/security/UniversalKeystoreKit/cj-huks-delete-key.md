# Key Deletion (Cangjie)

To ensure data security, keys should be deleted when they are no longer needed.

## Development Procedure

Taking the deletion of an HKDF256 key as an example.

1. Determine the key alias `keyAlias`. The maximum length of a key alias is 128 bytes.

2. Initialize the key property set. Used to specify [key property TAG](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag) during deletion. When deleting a single key, the TAG field can be left empty.

3. Call the [deleteKeyItem](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-deletekeyitemstring-huksoptions) interface to delete the key.

## Example

<!--compile-->
```cangjie
/*
 * The following demonstrates operations using an HKDF256 key as an example
 */
import kit.UniversalKeystoreKit.*

/* 1. Determine key alias */
let keyAlias = "test_Key"

/* 2. Construct empty object */
let huksOptions: HuksOptions = HuksOptions.NONE

class throwObject {
    var isThrow: Bool = false

    init(isThrow: Bool) {
        this.isThrow = isThrow
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

/* 3. Delete key */
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
    publicDeleteKeyFunc(keyAlias, huksOptions)
}
```