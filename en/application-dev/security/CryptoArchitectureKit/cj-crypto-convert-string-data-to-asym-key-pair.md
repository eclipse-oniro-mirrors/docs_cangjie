# Converting PEM String Data to an Asymmetric Key Pair

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Taking RSA as an example, an asymmetric key pair (KeyPair) is generated based on the specified asymmetric key string data.

> **Note:**
>
> For the convertPemKey operation on asymmetric keys:
>
> - Public keys must comply with X.509 specifications, PKCS\#1 specifications, and PEM encoding format.
>
> - Private keys must comply with PKCS\#8 specifications, PKCS\#1 specifications, and PEM encoding format.

## Converting PEM String Data to a Key Pair

For the corresponding algorithm specifications, see [Asymmetric Key Generation and Conversion Specifications](./cj-crypto-asym-key-generation-conversion-spec.md).

1. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring), specifying the string parameter 'RSA1024', to create an asymmetric key generator (AsyKeyGenerator) with RSA key type RSA1024 and 2 primes.

   When generating RSA asymmetric keys, the default number of primes is 2, so the parameter PRIMES_2 is omitted here.

2. Call [convertPemKey](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-convertpemkeyasynccallbackkeypairoptionstringoptionstring), passing in the PEM format string key data to generate an asymmetric key object (KeyPair).

3. Call [getEncodedPem](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencodedpemstring) to convert the public key in the asymmetric key object to PKCS #1 or X.509 format, and the private key to PKCS #1 or PKCS #8 format.

The following example uses converting an RSA PEM key pair:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

func testConvertPemKey() {
    let priKeyPkcs1Str = "-----BEGIN RSA PRIVATE KEY-----\n" +
        "MIICXQIBAAKBgQCwIN3mr21+N96ToxnVnaS+xyK9cNRAHiHGgrbjHw6RAj3V+l+W\n" +
        "Y68IhIe3DudVlzE9oMjeOQwkMkq//HCxNlIlFR6O6pa0mrXSwPRE7YKG97CeKk2g\n" +
        "YOS8YEh8toAvm7xKbiLkXuuMlxrjP2j/mb5iI/UASFSPZiQ/IyxDr0AQaQIDAQAB\n" +
        "AoGAEvBFzBNa+7J4PXnRQlYEK/tvsd0bBZX33ceacMubHl6WVZbphltLq+fMTBPP\n" +
        "LjXmtpC+aJ7Lvmyl+wTi/TsxE9vxW5JnbuRT48rnZ/Xwq0eozDeEeIBRrpsr7Rvr\n" +
        "7ctrgzr4m4yMHq9aDgpxj8IR7oHkfwnmWr0wM3FuiVlj650CQQDineeNZ1hUTkj4\n" +
        "D3O+iCi3mxEVEeJrpqrmSFolRMb+iozrIRKuJlgcOs+Gqi2fHfOTTL7LkpYe8SVg\n" +
        "e3JxUdVLAkEAxvcZXk+byMFoetrnlcMR13VHUpoVeoV9qkv6CAWLlbMdgf7uKmgp\n" +
        "a1Yp3QPDNQQqkPvrqtfR19JWZ4uy1qREmwJALTU3BjyBoH/liqb6fh4HkWk75Som\n" +
        "MzeSjFIOubSYxhq5tgZpBZjcpvUMhV7Zrw54kwASZ+YcUJvmyvKViAm9NQJBAKF7\n" +
        "DyXSKrem8Ws0m1ybM7HQx5As6l3EVhePDmDQT1eyRbKp+xaD74nkJpnwYdB3jyyY\n" +
        "qc7A1tj5J5NmeEFolR0CQQCn76Xp8HCjGgLHw9vg7YyIL28y/XyfFyaZAzzK+Yia\n" +
        "akNwQ6NeGtXSsuGCcyyfpacHp9xy8qXQNKSkw03/5vDO\n" +
        "-----END RSA PRIVATE KEY-----\n"
    let pubKeyPkcs1Str = "-----BEGIN RSA PUBLIC KEY-----\n" +
        "MIGJAoGBALAg3eavbX433pOjGdWdpL7HIr1w1EAeIcaCtuMfDpECPdX6X5ZjrwiE\n" +
        "h7cO51WXMT2gyN45DCQySr/8cLE2UiUVHo7qlrSatdLA9ETtgob3sJ4qTaBg5Lxg\n" +
        "SHy2gC+bvEpuIuRe64yXGuM/aP+ZvmIj9QBIVI9mJD8jLEOvQBBpAgMBAAE=\n" +
        "-----END RSA PUBLIC KEY-----\n"
    let asyKeyGenerator = createAsyKeyGenerator("RSA1024")
    try {
        asyKeyGenerator.convertPemKey({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let priPemKey = kp.priKey
                let pubPemKey = kp.pubKey
                let priString = priPemKey.getEncodedPem("PKCS8")
                let pubString = pubPemKey.getEncodedPem("X509")
                Hilog.info(0, "", "priString output: ${priString}")
                Hilog.info(0, "", "pubString output: ${pubString}")
            }
        }, pubKeyPkcs1Str, priKeyPkcs1Str)
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```
