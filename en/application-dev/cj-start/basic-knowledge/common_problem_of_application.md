# Application Package FAQ

## How to Obtain Fingerprint Information from Signature

1. Obtain via API call.

    You can call [bundleManager.getBundleInfoForSelf](../../../../en/application-dev/reference/AbilityKit/cj-apis-bundle_manager.md#static-func-getbundleinfoforselfint32) to retrieve your own BundleInfo, which contains signatureInfo. The signatureInfo includes fingerprint information.

    ```cangjie
    import ohos.base.*
    import kit.AbilityKit.*

    let bundleFlags =  GET_BUNDLE_INFO_WITH_APPLICATION.getValue() | GET_BUNDLE_INFO_WITH_SIGNATURE.getValue()
    try {
        let res = BundleManager.getBundleInfoForSelf(bundleFlags)
        let fingerprint = res.signatureInfo.fingerprint
        AppLog.info("getBundleInfoForSelf successfully, fingerprint: ${fingerprint}")
    } catch (e: BusinessException)  {
        AppLog.error("Failed to getBundleInfoForSelf. Code is ${e.code}, message is ${e.message}")
    }
    ```

2. Obtain fingerprint information via [bm tool](../../tools/cj-bm-tool.md#bm-tool).

    ```shell
    hdc shell
    # Replace com.example.myapplication with your actual package name
    bm dump -n com.example.myapplication | grep fingerprint
    ```

    ![alt text](figures/get_fingerprint.png)

3. Obtain via .cer certificate file. Refer to [APP Filing FAQ](https://developer.huawei.com/consumer/cn/doc/app/50130) for details on how to obtain public key and signature information for OpenHarmony applications/services.

4. Obtain via keytool. For details, refer to [Generating Signature Certificate Fingerprint](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/appgallerykit-preparation-game-0000001055356911#section147011294331).

## What is appIdentifier

appIdentifier is a field in the [Profile file](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-releaseprofile-0000001914714796), serving as the unique identifier of an application. It is generated during application signing, where:

1. When generated via DevEco Studio's [auto-signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237), the appIdentifier field is randomly generated. Signing on different devices or re-signing will result in different appIdentifier values.

2. When using manual signing and applying for certificates through AppGallery Connect, the [debug certificate](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-debugcert-0000001914263178) or [release certificate](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-releasecert-0000001946273961) obtained will have a fixed appIdentifier field. This value comes from the [APP ID](https://developer.huawei.com/consumer/cn/doc/app/agc-help-createharmonyapp-0000001945392297) generated when creating the application on AppGallery Connect, which is uniformly assigned by the cloud. In this case, the appIdentifier remains unchanged throughout the application lifecycle, including version upgrades, certificate changes, developer key changes, and application transfers.

Therefore, for scenarios requiring consistent appIdentifier across devices (e.g., cross-device debugging, cross-application interaction debugging, or multi-developer collaboration with shared keys), manual signing is recommended. For specific scenarios, refer to [Usage Scenario Description](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section54361623194519).

## How to Obtain appIdentifier from Application Information

1. Call [bundleManager.getBundleInfoForSelf](../../../../en/application-dev/reference/AbilityKit/cj-apis-bundle_manager.md#static-func-getbundleinfoforselfint32) to retrieve your own BundleInfo, which contains signatureInfo. The signatureInfo includes appIdentifier information.

    ```cangjie
    import ohos.base.*
    import kit.AbilityKit.*

    let bundleFlags =  GET_BUNDLE_INFO_WITH_APPLICATION.getValue() | GET_BUNDLE_INFO_WITH_SIGNATURE.getValue()
    try {
        let res = BundleManager.getBundleInfoForSelf(bundleFlags)
        let appIdentifier = res.signatureInfo.appIdentifier
        AppLog.info("getBundleInfoForSelf successfully, appIdentifier: ${appIdentifier}")
    } catch (e: BusinessException)  {
        AppLog.error("Failed to getBundleInfoForSelf. Code is ${e.code}, message is ${e.message}")
    }
    ```

2. Obtain via [bm tool](../../tools/cj-bm-tool.md#bm-tool).

    ```shell
    hdc shell
    # Replace com.example.myapplication with your actual package name
    bm dump -n com.example.myapplication | grep appIdentifier
    ```

    ![alt text](figures/get_appIdentifier.png)