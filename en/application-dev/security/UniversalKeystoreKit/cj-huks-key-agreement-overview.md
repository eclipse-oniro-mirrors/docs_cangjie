# Key Agreement Introduction and Algorithm Specifications  

## Introduction to Key Agreement  

To prevent malicious third parties from obtaining confidential information, the key itself cannot be directly transmitted between devices. Typically, a key agreement mechanism is employed to securely share the key between two (or more) parties. During key agreement, only the public key portion of the key is transmitted, while the private key remains stored within the device to ensure data security and confidentiality.  

When performing key agreement between two devices, each device prepares an asymmetric key and exchanges the public keys of their asymmetric keys. Using the peer's public key and its own private key, a shared key is negotiated, which is identical on both devices.  

> **Note:**  
>  
> Lightweight devices do not support the key agreement function.  

## Supported Algorithms  

The following are the specifications supported for key agreement.  

<!--Del-->  
For OpenHarmony vendor adaptation, the key management service specifications are divided into mandatory and optional specifications. Mandatory specifications are algorithm specifications that all vendors must support. For optional specifications, vendors decide whether to implement them based on actual circumstances. If you intend to use optional specifications, please refer to the specific vendor's documentation to ensure compatibility before use.  

**Developers are advised to use mandatory specifications for application development to ensure full platform compatibility.**  
<!--DelEnd-->  

| Algorithm | Remarks | API Level | <!--DelCol4-->Mandatory Specification |  
| :-------- | :-------- | :-------- | :-------- |  
| ECDH | The negotiated key type is an ECC-based key. | 15+ | Yes |  
| DH | - | 15+ | Yes |  
| X25519 | - | 15+ | Yes |