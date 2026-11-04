# User-Agent Development Guide

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

<!--RP1-->
User-Agent (abbreviated as UA) is a special string containing key information such as device type, operating system, and its version. In web development, this string enables servers to identify the source device and its characteristics of a request, thereby providing customized content and services accordingly. If a page fails to correctly recognize the UA, various anomalies may occur. For instance, a page layout optimized for mobile devices might display incorrectly on desktop devices, and vice versa. Additionally, certain browser features or CSS styles may only be supported in specific browser versions. If the page cannot make correct judgments based on the UA string, rendering issues or logical errors may arise.

## Default User-Agent Structure

- Default User-Agent Definition

  ```text
  Mozilla/5.0 ({DeviceType}; {OSName} {OSVersion}) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/{ChromeCompatibleVersion}.0.0.0 Safari/537.36  ArkWeb/{ArkWeb VersionCode} {DeviceCompat} {Extension Area}
  ```

- Example

  ```text
  Mozilla/5.0 (Phone; OpenHarmony 5.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36  ArkWeb/4.1.6.1 Mobile
  ```

- Field Descriptions

  | Field                  | Description                                                                 |
  | :--------------------- | :-------------------------------------------------------------------------- |
  | DeviceType            | Current device type.<br>Valid values:<br>- Phone: Mobile phone<br>- Tablet: Tablet device<br>- PC: 2-in-1 device |
  | OSName                | Base operating system name.<br>Default value: OpenHarmony                  |
  | OSVersion             | Base operating system version, two-digit format (M.S).<br>Parsed from the system parameter `const.ohos.fullname`, taking the first two digits of the version number (M.S).<br>Default value: e.g., 5.0  |
  | ChromeCompatibleVersion | Chrome-compatible major version number, starting from version 114.<br>Default value: 114            |
  | ArkWeb                | OpenHarmony version Web kernel name.<br>Default value: ArkWeb             |
  | ArkWeb VersionCode    | ArkWeb version number, format a.b.c.d.<br>Default value: e.g., 4.1.6.1         |
  | DeviceCompat          | Forward compatibility field.<br>Default value: Mobile                          |
  | Extension Area        | Fields extendable by third-party applications.<br>When using the ArkWeb component, third-party applications can extend the UA, such as adding APP-related information identifiers. |

> **Note:**
>
> - Currently, there are two spaces before the ArkWeb field in the default User-Agent.
> - Currently, the presence of the "Mobile" field in the User-Agent determines whether the `viewport` attribute in the frontend HTML page's meta tag is enabled. When the User-Agent does not contain the "Mobile" field, the `viewport` attribute in the meta tag is disabled by default. In this case, you can override this state by explicitly setting the [metaViewport](../reference/arkui-cj/cj-web-web.md#func-metaviewportbool) attribute to `true`.
> - It is recommended to identify OpenHarmony devices using the `OpenHarmony` keyword and to recognize the device type via `DeviceType` to adapt page displays for different devices (the `ArkWeb` keyword indicates the Web kernel used by the device, while the `OpenHarmony` keyword indicates the operating system used by the device. Therefore, it is recommended to use the `OpenHarmony` keyword to identify OpenHarmony devices).

## Custom User-Agent Structure

In the following example, the default User-Agent information provided by the interface serves as a foundation, allowing developers to customize or extend it.

<!-- compile -->

```cangjie
// index.cj
import kit.PerformanceAnalysisKit.Hilog
import kit.ArkWeb.WebviewController
import kit.ArkUI.Web
import kit.CangjieKit.*

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

func loggerError(str: String) {
    Hilog.error(0, "CangjieTest", str)
}

@Entry
@Component
class EntryView {
    let webController = WebviewController()

    func build() {
        Column {
            Button("getUserAgent").onClick ({ evt =>
                try {
                    let userAgent = webController.getUserAgent()
                    loggerInfo("userAgent: ${userAgent}")
                } catch (e: BusinessException) {
                    loggerError("getUserAgent ErrorCode: ${e.code},  Message: ${e.message}")
                }
            })
            Web(src: 'www.example.com', controller: webController)
        }
    }
}
```

## Related User-Agent Interface Priorities

| Interface Name | Priority | Description |
| :-------- | :-------- | :-------- |
| setCustomUserAgent | Highest | Applies to the invoked Web component. |
| ArkWeb Default UA | Lowest | Applies to all Web components in the application, read-only, obtained via `getDefaultUserAgent`. |

## Frequently Asked Questions

### How to Identify Different Devices in OpenHarmony OS via User-Agent

OpenHarmony device identification primarily relies on three dimensions in the User-Agent: system, system version, and device type. It is recommended to check all three to ensure more accurate device identification.

1. System Identification

   Identify the OpenHarmony system via the `{OSName}` field in the User-Agent.

   ```html
   const isOpenHarmony = () => /OpenHarmony/i.test(navigator.userAgent);
   ```

2. System Version Identification

   Identify the OpenHarmony system and its version via the `{OSName}` and `{OSVersion}` fields in the User-Agent. The format is: OpenHarmony + version number.

   ```html
   const matches = navigator.userAgent.match(/OpenHarmony (\d+\.?\d*)/);  
   matches?.length && Number(matches[1]) >= 5;  
   ```

3. Device Type Identification

   Identify different device types via the `deviceType` field.

   ```html
   // Check if it is a mobile phone
   const isPhone = () => /Phone/i.test(navigator.userAgent);

   // Check if it is a tablet  
   const isTablet = () => /Tablet/i.test(navigator.userAgent);

   // Check if it is a 2-in-1 device  
   const is2in1 = () => /PC/i.test(navigator.userAgent);
   ```

### How to Simulate OpenHarmony OS User-Agent for Frontend Debugging

On Windows/Mac/Linux and other operating systems, you can simulate the OpenHarmony User-Agent using the User-Agent override capability provided by DevTools in browsers like Chrome/Edge/Firefox.
<!--RP1End-->