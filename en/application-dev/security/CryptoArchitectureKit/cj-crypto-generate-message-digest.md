# SHA256 Message Digest Calculation

For corresponding algorithm specifications, please refer to [Message Digest Calculation Algorithm Specifications](./cj-crypto-generate-message-digest-overview.md#supported-algorithms-and-specifications).

> **Note:**
>
> Starting from API version 12, lightweight smart wearable devices support message digest calculation and operations.

## Development Steps

When passing data through the update interface, you can either [pass all data at once](#one-time-digest-algorithm) or manually segment the data and then [update in segments](#segmented-digest-algorithm). For the same segment of data, the calculation results will be identical. For large volumes of data, developers can choose whether to pass data in segments based on actual requirements.

Example codes for both approaches are provided below.

### One-time Digest Algorithm

1. Call [createMd](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createmdstring), specify the SHA256 digest algorithm to generate a digest instance (Md).

2. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-2), pass custom messages for digest update calculation. There is no length limit for a single update.

3. Call [digest](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-digest) to obtain the digest calculation result.

4. Call [getMdLength](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getmdlength) to get the digest calculation length in bytes.

### Example: One-time Data Input for Digest Calculation

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*

func doMd() {
    let mdAlgName = 'SHA256' // Digest algorithm name.
    let message = 'mdTestMessage' // Data to be digested.
    let md = createMd(mdAlgName)
    // For small data volumes, perform a single update with all data passed at once. No length restriction on input parameters.
    md.update(DataBlob(message.toArray()))
    let mdResult = md.digest()
    AppLog.info('[Sync]:Md result: ${mdResult.data}')
    let mdLen = md.getMdLength()
    AppLog.info("md len: ${mdLen}")
}
```

### Segmented Digest Algorithm

1. Call [createMd](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createmdstring), specify the SHA256 digest algorithm to generate a digest instance (Md).

2. Pass custom messages, set the single-pass data volume to 20 bytes, and call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-2) multiple times for segmented digest update calculation.

3. Call [digest](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-digest) to obtain the digest calculation result.

4. Call [getMdLength](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getmdlength) to get the digest calculation length in bytes.

### Example: Segmented Data Input for Digest Calculation

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*

func doLoopMd() {
    let mdAlgName = "SHA256" // Digest algorithm name.
    let md = createMd(mdAlgName)
    // Assuming the message is 43 bytes in total, which remains 43 bytes after UTF-8 decoding.
    let messageText = "aaaaa.....bbbbb.....ccccc.....ddddd.....eee"
    let messageData = messageText.toArray()
    let updateLength = 20 // Assuming segmentation in 20-byte units for update (no actual requirement).
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
    AppLog.info('[Sync]:Md result: ${mdOutput.data}')
    let mdLen = md.getMdLength()
    AppLog.info("md len: ${mdLen}")
}
```