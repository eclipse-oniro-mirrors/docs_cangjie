# Message Digest Calculation MD5

For the corresponding algorithm specifications, please refer to [Message Digest Calculation Algorithm Specifications](./cj-crypto-generate-message-digest-overview.md#supported-algorithms-and-specifications).

## Development Steps

When passing data through the update interface, you can either [pass all data at once](#digest-algorithm-single-pass) or manually segment the data and then [update in segments](#segmented-digest-algorithm). For the same segment of data, the calculation results will be identical. For large volumes of data, developers can choose whether to pass the data in segments based on actual requirements.

Example codes for both approaches are provided below.

### Digest Algorithm (Single Pass)

1. Call [createMd](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createmdstring), specify the MD5 digest algorithm, and generate a digest instance (Md).

2. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-2), pass the custom message, and perform digest update calculation. There is no limit on the length of a single update.

3. Call [digest](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-digest) to obtain the digest calculation result.

4. Call [getMdLength](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getmdlength) to get the digest calculation length in bytes.

### Example: Single Pass Data Input to Obtain Digest Result

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.hilog.Hilog

func doMd() {
    let mdAlgName = 'MD5' // Digest algorithm name.
    let message = 'mdTestMessage' // Data to be digested.
    let md = createMd(mdAlgName)
    // When the data volume is small, you can perform a single update and pass all data at once. The interface does not limit the input length.
    md.update(DataBlob(message.toArray()))
    let mdResult = md.digest()
    Hilog.info(0,"",'[Sync]:Md result: ${mdResult.data}')
    let mdLen = md.getMdLength()
    Hilog.info(0,"","md len: ${mdLen}")
}
```

### Segmented Digest Algorithm

1. Call [createMd](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createmdstring), specify the MD5 digest algorithm, and generate a digest instance (Md).

2. Pass the custom message, set the single-pass data volume to 20 bytes, and call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-2) multiple times to perform segmented digest update calculations.

3. Call [digest](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-digest) to obtain the digest calculation result.

4. Call [getMdLength](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getmdlength) to get the digest calculation length in bytes.

### Example: Segmented Data Input to Obtain Digest Result

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.hilog.Hilog

func doLoopMd() {
    let mdAlgName = "MD5" // Digest algorithm name.
    let md = createMd(mdAlgName)
    // Assume the total message is 43 bytes, which remains 43 bytes after UTF-8 decoding.
    let messageText = "aaaaa.....bbbbb.....ccccc.....ddddd.....eee"
    let messageData = messageText.toArray()
    let updateLength = 20 // Assume segmenting updates in 20-byte units (no actual requirement exists).
    let size = messageData.size
    for (i in 0..size : updateLength) {
        let len = if (i + updateLength > size) {
            size
        } else {
            i + updateLength
        }
        let updateMessage = messageData[i..len]
        let updateMessageBlob: DataBlob = DataBlob(updateMessage)
        md.update(updateMessageBlob)
    }
    let mdOutput = md.digest()
    Hilog.info(0,"",'[Sync]:Md result: ${mdOutput.data}')
    let mdLen = md.getMdLength()
    Hilog.info(0,"","md len: ${mdLen}")
}
```