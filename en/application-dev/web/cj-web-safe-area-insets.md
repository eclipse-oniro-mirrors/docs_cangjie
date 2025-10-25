# Safe Area Calculation and Adaptation in Web Pages

## Overview

The safe area is defined as the display region of a page that does not overlap with system-defined non-safe areas (such as the status bar or navigation bar) by default, ensuring that interfaces designed by developers are laid out within the safe area. However, when the Web component enables immersive mode, webpage elements may overlap with the status bar or navigation bar. As shown in Figure 1, the area enclosed by the red dashed line represents the safe area, while the top status bar, screen cutout area, and bottom navigation bar are defined as non-safe areas. When the Web component enables immersive effects, bottom elements within the webpage may overlap with the navigation bar.

**Figure 1** Bottom elements overlapping with the navigation bar when the Web component enables immersive effects

![web-safe-area](figures/arkweb_safearea2.png)

The Web component provides the capability to calculate and adapt to safe areas using W3C CSS, supporting normal display of pages on devices with irregular screens under immersive effects. Web developers can use this capability to avoid overlapping elements. The ArkWeb kernel continuously monitors the position and dimensions of the Web component and system safe areas, calculating the current safe area of the Web component and the specific distances to avoid in each direction based on their overlapping regions.

## Implementation Scenarios

### Enabling Immersive Effects for the Web Component

Developers can enable immersive effects using [expandSafeArea](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-expandsafearea.md#func-expandsafeareaarraysafeareatype-arraysafeareaedge).

<!-- compile -->

```cangjie
// index.cj
import ohos.arkui.state_macro_manage.*
import ohos.web.webview.WebviewController
import kit.ArkUI.{ Web, SafeAreaType, SafeAreaEdge }

@Entry
@Component
class EntryView {
    let webController = WebviewController()

    func build() {
        Column {
            Web(src: 'www.example.com', controller: this.webController)
                .width(100.percent)
                .height(100.percent)
                .expandSafeArea(types: [SafeAreaType.System], edges: [SafeAreaEdge.Top, SafeAreaEdge.Bottom])
        }
    }
}
```

### Setting the Layout Mode of the Webpage in the Viewport

`viewport-fit` is used to constrain the display mode of the webpage within the safe area. The default value is `auto`, which behaves the same as `contain`, indicating that the viewport fully contains the webpage content, i.e., all content is displayed within the safe area. `cover` means the webpage content fully covers the viewport, i.e., the content is displayed not only in the safe area but also in non-safe areas, potentially overlapping with the status bar and navigation bar. Only in this scenario does the webpage require adaptation to avoid overlaps. The setting is as follows:

```html
<meta name='viewport' content='viewport-fit=cover'>
```

### Avoiding Overlaps for Webpage Elements

The adaptation to avoid overlaps for webpage elements primarily relies on the `env()` CSS function, which inserts user-defined variables into CSS. This allows developers to place content within the safe area of the viewport. The `safe-area-inset-*` values defined in the specification ensure content is fully displayed even in non-rectangular viewports. The syntax is as follows:

```html
/* safe-area-inset-* can be set for top, right, bottom, and left directions */
env(safe-area-inset-top);
env(safe-area-inset-right);
env(safe-area-inset-bottom);
env(safe-area-inset-left);

/* Using fallback values with safe-area-inset-* for all directions */
/* For length units, refer to: https://developer.mozilla.org/en-US/docs/Web/CSS/length */
env(safe-area-inset-top, 20px);
env(safe-area-inset-right, 1em);
env(safe-area-inset-bottom, 0.5vh);
env(safe-area-inset-left, 1.4rem);
```

> **Note:**
>
> `safe-area-inset-*` consists of four environment variables that define the `top`, `right`, `bottom`, and `left` insets from the edges of the viewport, ensuring content can be safely placed without being cut off by non-rectangular display areas. In rectangular viewports (e.g., standard 2-in-1 device displays), these values are zero. For non-rectangular displays (e.g., circular watch faces, mobile device screens), all content will be visible within the rectangular area formed by the four values set by the user agent.

Unlike other CSS properties, user agent-defined property names are case-sensitive. Additionally, note that `env()` must be used with `viewport-fit=cover`.

For e-commerce websites, the bottom of the homepage often contains absolutely positioned tab elements. In immersive mode, these elements require bottom adaptation to prevent overlap with the system navigation bar. The adaptation effect is shown in Figure 2:

```html
.tab-bottom {
    padding-bottom: env(safe-area-inset-bottom);
}
```

Furthermore, `env()` can be combined with CSS math functions like `calc()`, `min()`, and `max()` for composite calculations, e.g.:

```html
.tab-bottom {
    padding-bottom: max(env(safe-area-inset-bottom), 30px);
}
```

**Figure 2** Bottom elements avoiding the navigation bar area when the Web component enables immersive effects

![web-safe-area](figures/arkweb_safearea1.png)