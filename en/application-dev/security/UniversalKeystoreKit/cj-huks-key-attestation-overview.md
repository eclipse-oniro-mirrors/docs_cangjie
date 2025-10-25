# Key Attestation Introduction and Algorithm Specifications  

## Key Attestation Introduction  

HUKS provides key legitimacy attestation capabilities, primarily used for attesting the public keys of asymmetric keys.  

Based on PKI certificate chain technology, HUKS can issue certificates for the public keys of asymmetric key pairs stored in HUKS to attest their legitimacy. Services can use the system-provided root CA certificate to verify the key attestation certificates issued by HUKS level by level, ensuring that the public keys in the certificates and their corresponding private keys indeed originate from legitimate hardware devices and are stored and managed in HUKS. Additionally, the output key certificates include key owner information in the following format:  

| Key Owner | Format | Description |  
| :-------- | :-------- | :-------- |  
| HAP Application | {appId:"xxx", bundleName:"xxx"} | bundleName is the application package name. |  
| System Service | {processName:"xxx", APL:"system_basic \| system_core"} | APL is the [System Service Level](../AccessToken/cj-app-permission-mgmt-overview.md#key-concepts-in-permission-mechanism). |  

> **Note:**  
>  
> - When the caller is a system service with an APL level of normal, key attestation is temporarily unsupported. In this case, the processName and APL fields will be left empty.  
> - Key attestation is not supported in emulator scenarios.  
> - Lightweight devices do not support key attestation.  
> - Key attestation is supported for both generated and imported keys. Service providers must verify whether the key source meets expectations by checking the key source field in the service certificate on the server side. The OID for the key source field and its values are: `1.3.6.1.4.1.2011.2.376.2.1.5`.  

The key sources and their corresponding OID field values are as follows:  

| Key Source | OID Field Value |  
| :-------- | :-------- |  
| Imported | 1 |  
| Generated | 2 |  

## Key Attestation Process  

1. The service passes the specified key alias and the labels of the key attributes to be attested to HUKS.  

2. HUKS generates an X.509 certificate chain for the application, consisting of the root CA certificate, device CA certificate, device certificate, and key certificate in sequence.  

3. The certificate chain is transmitted to a trusted server, where its validity is parsed and verified, including checking whether individual certificates are revoked.  

<!--RP2-->  
Currently, two key attestation methods are provided.  

- **Anonymous Key Attestation**: Does not disclose device information and has no permission management. Open to all applications. To protect user device information, third-party application developers can only use anonymous key attestation.  
- **Non-Anonymous Key Attestation**: Reveals caller device information and has permission controls. Requires the [ohos.permission.ATTEST_KEY](../AccessToken/cj-permissions-for-system-apps.md#ohospermissionattest_key) permission.  

<!--RP2End-->  

Currently, emulators<!--Del--> and development boards<!--DelEnd--> support anonymous certificates. Certificates used in debugging environments are not real device certificates. The cloud side must distinguish this scenario to avoid misuse.  

## Supported Algorithms  

The following are the specifications supported for key attestation.  

<!--Del-->  
For OpenHarmony, vendor adaptation of key management service specifications is divided into mandatory and optional specifications. Mandatory specifications are algorithm specifications supported by all vendors. For optional specifications, vendors decide whether to implement them based on actual conditions. If needed, refer to the specific vendor's documentation to ensure support before use.  

**Developers are advised to use mandatory specifications for application development to ensure full platform compatibility.**  
<!--DelEnd-->  

<!--Del-->  
**Anonymous Key Attestation:**  
<!--DelEnd-->  

| Algorithm | Remarks | API Level | <!--DelCol4-->Mandatory Specification |  
| :-------- | :-------- | :-------- | :-------- |  
| RSA | Supports keys with PSS and PKCS1_V1_5 padding | 15+ | Yes |  
| ECC | - | 15+ | Yes |  
| SM2 | - | 15+ | Yes |  

<!--Del-->  
**Non-Anonymous Key Attestation:**  

| Algorithm | Remarks | API Level | Mandatory Specification |  
| :-------- | :-------- | :-------- | :-------- |  
| RSA | Supports keys with PSS and PKCS1_V1_5 padding | 15+ | Yes |  
| ECC | - | 15+ | Yes |  
| X25519 | - | 15+ | Yes |  
| SM2 | - | 15+ | Yes |  
<!--DelEnd-->