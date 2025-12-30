# Application Package FAQ

## How to Obtain Fingerprint Information from Signature

1. Obtain via API call.

    You can call [bundleManager.getBundleInfoForSelf](../../reference/AbilityKit/cj-apis-bundle_manager.md#static-func-getbundleinfoforselfint32) to retrieve your own BundleInfo, which contains signatureInfo. The signatureInfo includes fingerprint information.

    <!-- compile -->

    ```cangjie
    import ohos.base.*
    import kit.AbilityKit.*

    let bundleFlags =  GET_BUNDLE_INFO_WITH_APPLICATION.getValue() | GET_BUNDLE_INFO_WITH_SIGNATURE.getValue()
    try {
        let res = BundleManager.getBundleInfoForSelf(bundleFlags)
        let fingerprint = res.signatureInfo.fingerprint
        Hilog.info(1, "info", "getBundleInfoForSelf successfully, fingerprint: ${fingerprint}")
    } catch (e: BusinessException)  {
        Hilog.error(1, "info", "Failed to getBundleInfoForSelf. Code is ${e.code}, message is ${e.message}")
    }
    ```

2. Obtain fingerprint information via the [bm tool](../../tools/cj-bm-tool.md#bm工具).

    ```shell
    hdc shell
    # Replace com.example.myapplication with the actual package name
    bm dump -n com.example.myapplication | grep fingerprint
    ```

    ![alt text](figures/get_fingerprint.png)

3. Obtain via .cer certificate file. Refer to [APP Filing FAQ](https://developer.huawei.com/consumer/en/doc/app/50111) for how to obtain public key and signature information for OpenHarmony applications/services.

4. Obtain via keytool. For details, refer to [Generating Signature Certificate Fingerprint](https://developer.huawei.com/consumer/en/doc/AppGallery-connect-Guides/appgallerykit-preparation-game-0000001055356911#section147011294331).

## What is appIdentifier

appIdentifier is a field in the <!--RP1-->[Profile Signature File](https://gitcode.com/openharmony/docs/blob/master/en/application-dev/security/app-provision-structure.md)<!--RP1End-->, serving as the unique identifier for an application. It is generated during application signing, where:

1. When generated via DevEco Studio's [Auto-Signing](https://developer.huawei.com/consumer/en/doc/harmonyos-guides/ide-signing#section18815157237), the appIdentifier field is randomly generated. Signing on different devices or re-signing will result in different appIdentifier values.

2. <!--RP2-->For manual signing configuration, refer to [Application Package Signing Tool Guide](https://gitcode.com/openharmony/docs/blob/master/en/application-dev/security/hapsigntool-guidelines.md). In this case, the appIdentifier field takes the value from the app-identifier field in the [HarmonyAppProvision Configuration File](https://gitcode.com/openharmony/docs/blob/master/en/application-dev/security/app-provision-structure.md).<!--RP2End-->

Therefore, for scenarios requiring consistent appIdentifier across devices (e.g., cross-device debugging, cross-application interaction debugging, or multi-user collaborative development with shared keys), manual signing is recommended. For specific scenarios, refer to [Usage Scenario Description](https://developer.huawei.com/consumer/en/doc/harmonyos-guides/ide-signing#section54361623194519).

## How to Obtain appIdentifier from Application Information

1. Call [bundleManager.getBundleInfoForSelf](../../reference/AbilityKit/cj-apis-bundle_manager.md#static-func-getbundleinfoforselfint32) to retrieve your own BundleInfo, which contains signatureInfo. The signatureInfo includes appIdentifier information.

    <!-- compile -->

    ```cangjie
    import ohos.base.*
    import kit.AbilityKit.*

    let bundleFlags =  GET_BUNDLE_INFO_WITH_APPLICATION.getValue() | GET_BUNDLE_INFO_WITH_SIGNATURE.getValue()
    try {
        let res = BundleManager.getBundleInfoForSelf(bundleFlags)
        let appIdentifier = res.signatureInfo.appIdentifier
        Hilog.info(1, "info", "getBundleInfoForSelf successfully, appIdentifier: ${appIdentifier}")
    } catch (e: BusinessException)  {
        Hilog.error(1, "info", "Failed to getBundleInfoForSelf. Code is ${e.code}, message is ${e.message}")
    }
    ```

2. Obtain via the [bm tool](../../tools/cj-bm-tool.md#bm工具).

    ```shell
    hdc shell
    # Replace com.example.myapplication with the actual package name
    bm dump -n com.example.myapplication | grep appIdentifier
    ```

    ![alt text](figures/get_appIdentifier.png)