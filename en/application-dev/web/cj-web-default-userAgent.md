# User-Agent Development Guide

<!--RP1-->
User-Agent (UA) is a special string containing key information such as device type, operating system, and its version. In web development, this string enables servers to identify the source device and its characteristics, thereby providing customized content and services. If a page fails to correctly recognize the UA, various anomalies may occur. For example, a mobile-optimized page layout may display incorrectly on desktop devices, and vice versa. Additionally, certain browser features or CSS styles may only be supported in specific browser versions. If the page cannot make correct judgments based on the UA string, rendering issues or logical errors may arise.

## Default User-Agent Structure

- Default User-Agent Definition

  ```text
  Mozilla/5.0 ({DeviceType}; {OSName} {OSVersion}) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/{ChromeCompatibleVersion}.0.0.0 Safari/537.36  ArkWeb/{ArkWeb VersionCode} {DeviceCompat} {Extension Field}
  ```

- Example

  ```text
  Mozilla/5.0 (Phone; OpenHarmony 5.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36  ArkWeb/4.1.6.1 Mobile
  ```

- Field Descriptions

  | Field                  | Description                                                                 |
  | :--------------------- | :-------------------------------------------------------------------------- |
  | DeviceType            | Current device type.<br>Valid values:<br>- Phone: Smartphone<br>- Tablet: Tablet device<br>- PC: 2-in-1 device |
  | OSName                | Base operating system name.<br>Default value: OpenHarmony                  |
  | OSVersion             | Base operating system version, two-digit format (M.S).<br>Parsed from the system parameter `const.ohos.fullname`, taking the first two digits of the version number (M.S).<br>Default value: e.g., 5.0  |
  | ChromeCompatibleVersion | Chrome-compatible major version number, starting from version 114.<br>Default value: 114            |
  | ArkWeb                | OpenHarmony version Web engine name.<br>Default value: ArkWeb             |
  | ArkWeb VersionCode    | ArkWeb version number, format a.b.c.d.<br>Default value: e.g., 4.1.6.1         |
  | DeviceCompat          | Forward compatibility field.<br>Default value: Mobile                          |
  | Extension Field       | Field extendable by third-party applications.<br>When using the ArkWeb component, third-party apps can extend the UA, such as adding APP-related information identifiers. |

> **Note:**
>
> - Currently, there are two spaces before the ArkWeb field in the default User-Agent.
> - The presence of the "Mobile" field in the User-Agent determines whether the `viewport` attribute in the frontend HTML page's meta tag is enabled. When the "Mobile" field is absent, the `viewport` attribute in the meta tag is disabled by default. This can be overridden by explicitly setting the [metaViewport](../../../en/application-dev/reference/arkui-cj/cj-web-web.md#func-metaviewportbool) attribute to `true`.
> - It is recommended to identify OpenHarmony devices using the `OpenHarmony` keyword and the device type using `DeviceType` to adapt page displays for different devices (the `ArkWeb` keyword indicates the Web engine used by the device, while the `OpenHarmony` keyword indicates the operating system. Therefore, it is recommended to use the `OpenHarmony` keyword to identify OpenHarmony devices).

## Custom User-Agent Structure

In the following example, the default User-Agent information provided by the interface serves as a foundation, allowing developers to customize or extend it.

<!-- compile -->

```cangjie
// index.cj
import kit.PerformanceAnalysisKit.Hilog
import kit.ArkWeb.WebviewController
import kit.ArkUI.{Web, BusinessException}

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
            Button("getUserAgent").onClick { evt =>
                try {
                    let userAgent = webController.getUserAgent()
                    loggerInfo("userAgent: ${userAgent}")
                } catch (e: BusinessException) {
                    loggerError("getUserAgent ErrorCode: ${e.code},  Message: ${e.message}")
                }
            }
            Web(src: 'www.example.com', controller: webController)
        }
    }
}
```

## User-Agent Interface Priority

| Interface Name | Priority | Description |
| :-------- | :-------- | :-------- |
| setCustomUserAgent | Highest | Applies to the invoked Web component. |
| ArkWeb Default UA | Lowest | Applies to all Web components in the application, read-only, obtained via `getDefaultUserAgent`. |

## FAQs

### How to Identify Different Devices in OpenHarmony OS Using User-Agent

OpenHarmony device identification primarily relies on three dimensions in the User-Agent: system, system version, and device type. It is recommended to check all three for more accurate identification.

1. System Identification

   Identify the OpenHarmony system using the `{OSName}` field in the User-Agent.

   ```html
   const isOpenHarmony = () => /OpenHarmony/i.test(navigator.userAgent);
   ```

2. System Version Identification

   Identify the OpenHarmony system and version using the `{OSName}` and `{OSVersion}` fields in the User-Agent. Format: OpenHarmony + version number.

   ```html
   const matches = navigator.userAgent.match(/OpenHarmony (\d+\.?\d*)/);  
   matches?.length && Number(matches[1]) >= 5;  
   ```

3. Device Type Identification

   Identify different device types using the `deviceType` field.

   ```html
   // Check if it is a smartphone
   const isPhone = () => /Phone/i.test(navigator.userAgent);

   // Check if it is a tablet  
   const isTablet = () => /Tablet/i.test(navigator.userAgent);

   // Check if it is a 2-in-1 device  
   const is2in1 = () => /PC/i.test(navigator.userAgent);
   ```

### How to Simulate OpenHarmony OS User-Agent for Frontend Debugging

On Windows/Mac/Linux or other operating systems, you can simulate the OpenHarmony User-Agent using the User-Agent override capability provided by DevTools in browsers like Chrome/Edge/Firefox.
<!--RP1End-->