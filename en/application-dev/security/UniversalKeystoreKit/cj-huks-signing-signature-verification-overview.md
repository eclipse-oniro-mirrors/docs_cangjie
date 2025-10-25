# Signature/Verification Introduction and Algorithm Specifications  

To achieve data integrity protection and non-repudiation, generated/imported keys can be used to perform signature/verification operations on data.  

## Supported Algorithms  

The following are the specifications supported for key signature/verification.  

<!--Del-->  
For OpenHarmony vendor adaptation, the Key Management Service specifications are divided into mandatory and optional specifications. Mandatory specifications are algorithm specifications supported by all vendors. For optional specifications, vendors will decide whether to implement them based on actual circumstances. If needed, please refer to the specific vendor's documentation to ensure compatibility before use.  

**Developers are advised to use mandatory specifications for application development to ensure full platform compatibility.**  
<!--DelEnd-->  

### Standard Device Specifications  

| Algorithm/Digest Algorithm/Padding Mode | Remarks | API Level | <!--DelCol4-->Mandatory Specification |  
| :-------- | :-------- | :-------- | :-------- |  
| <!--DelRow-->RSA/MD5/PKCS1_V1_5<br/>RSA/SHA1/PKCS1_V1_5<br/>RSA/SHA224/PKCS1_V1_5<br/>RSA/SHA224/PSS | For PSS mode, the salt length can be set to the digest length or the maximum length (maximum length = key length - digest length - 2). For corresponding enum values, refer to [HuksRsaPssSaltLenType](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksrsapsssaltlentype). | 15+ | No |  
| RSA/SHA256/PKCS1_V1_5<br/>RSA/SHA384/PKCS1_V1_5<br/>RSA/SHA512/PKCS1_V1_5<br/>RSA/SHA256/PSS<br/>RSA/SHA384/PSS<br/>RSA/SHA512/PSS | For PSS mode, the salt length can be set to the digest length or the maximum length (maximum length = key length - digest length - 2). For corresponding enum values, refer to [HuksRsaPssSaltLenType](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksrsapsssaltlentype). | 15+ | Yes |  
| RSA/NoDigest/PKCS1_V1_5 | NoDigest requires specifying the TAG HuksKeyDigest.HUKS_DIGEST_NONE. The service must hash the plaintext and pass the hashed data, which must comply with the digest algorithm specifications supported by RSA signature/verification. | 15+ | Yes |  
| <!--DelRow-->DSA/SHA1<br/>DSA/SHA224<br/>DSA/SHA256<br/>DSA/SHA384<br/>DSA/SHA512 | - | 15+ | No |  
| <!--DelRow-->DSA/NoDigest | NoDigest requires specifying the TAG HuksKeyDigest.HUKS_DIGEST_NONE. | 15+ | No |  
| <!--DelRow-->ECC/SHA1<br/>ECC/SHA224 | The signature is in ASN1 format. | 15+ | No |  
| ECC/SHA256<br/>ECC/SHA384<br/>ECC/SHA512 | The signature is in ASN1 format.<br/>Supported elliptic curve functions for ECC algorithm include: P-256, P-384, P-521. | 15+ | Yes |  
| <!--DelRow-->ECC/NoDigest | The signature is in ASN1 format.<br/>NoDigest requires specifying the TAG HuksKeyDigest.HUKS_DIGEST_NONE. | 15+ | No |  
| ED25519/NoDigest | NoDigest requires specifying the TAG HuksKeyDigest.HUKS_DIGEST_NONE. | 15+ | Yes |  
| SM2/SM3 | The signature is in ASN1 format. | 15+ | Yes |  

### Lightweight Device Specifications  

<!--Del-->  
For lightweight devices, the listed specifications will be implemented by OEM vendors based on actual circumstances. If needed, please refer to the specific vendor's documentation to ensure compatibility before use.  
<!--DelEnd-->  

| Algorithm/Digest Algorithm/Padding Mode | Remarks | API Level |  
| :-------- | :-------- | :-------- |  
| RSA/SHA256/PKCS1_V1_5 | - | 15+ |  
| RSA/SHA256/PSS | - | 15+ |  
| RSA/SHA1/ISO_IEC_9796_2 | Minimum data length = key length - 21 bytes | 15+ |  

<!--RP1--><!--RP1End-->