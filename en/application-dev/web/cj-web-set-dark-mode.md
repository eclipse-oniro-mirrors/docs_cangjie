# Setting Dark Mode

The Web component supports dark mode configuration for frontend pages.

- The [darkMode()](../../../en/application-dev/reference/arkui-cj/cj-web-web.md#func-darkmodewebdarkmode) interface can be used to configure different dark modes, which is disabled by default. When dark mode is enabled, the Web component will apply the dark styles defined in the webpage's media query `prefers-color-scheme`. If the webpage doesn't define dark styles, it will remain unchanged. To enable forced dark mode, it is recommended to use it in conjunction with [forceDarkAccess()](../../../en/application-dev/reference/arkui-cj/cj-web-web.md#func-forcedarkaccessbool). The [WebDarkMode.Off](../../../en/application-dev/reference/arkui-cj/cj-common-types.md#enum-webdarkmode) mode indicates that dark mode is disabled. [WebDarkMode.On](../../../en/application-dev/reference/arkui-cj/cj-common-types.md#enum-webdarkmode) indicates that dark mode is enabled and follows the frontend page. [WebDarkMode.Auto](../../../en/application-dev/reference/arkui-cj/cj-common-types.md#enum-webdarkmode) indicates that dark mode is enabled and follows the system.

    In the following example, the [darkMode()](../../../en/application-dev/reference/arkui-cj/cj-web-web.md#func-darkmodewebdarkmode) interface is used to configure the page's dark mode to follow the system.

    <!-- compile -->

    ```cangjie
    // index.cj
    import ohos.web.webview.WebviewController
    import kit.ArkUI.{Web, WebDarkMode}
    import ohos.arkui.state_macro_manage.rawfile

    @Entry
    @Component
    class EntryView {
        let webController = WebviewController()

        func build() {
            Column {
                Web(src: @rawfile("index.html"), controller: webController)
                    .darkMode(WebDarkMode.Auto)
            }
        }
    }
    ```

- The [forceDarkAccess()](../../../en/application-dev/reference/arkui-cj/cj-web-web.md#func-forcedarkaccessbool) interface can be used to forcibly configure the frontend page to dark mode. Forced dark mode cannot guarantee that all color conversions will meet expectations, and the dark mode does not follow the frontend page or the system. When configuring this mode, the dark mode must be set to `WebDarkMode.On`.

    In the following example, the [forceDarkAccess()](../../../en/application-dev/reference/arkui-cj/cj-web-web.md#func-forcedarkaccessbool) interface is used to forcibly configure the page to dark mode.

    <!-- compile -->

    ```cangjie
    // index.cj
    import ohos.web.webview.WebviewController
    import kit.ArkUI.{Web, WebDarkMode}
    import ohos.arkui.state_macro_manage.rawfile

    @Entry
    @Component
    class EntryView {
        let webController = WebviewController()

        func build() {
            Column {
                Web(src: @rawfile("index.html"), controller: webController)
                    .darkMode(WebDarkMode.On)
                    .forceDarkAccess(true)
            }
        }
    }
    ```

- index.html page code:

    ```html
    <!-- resources/rawfile/index.html -->
    <!DOCTYPE html>
    <html>
    <head>
        <meta name="viewport" content="width=device-width,
                                        initial-scale=1.0,
                                        maximum-scale=1.0,
                                        user-scalable=no">
        <style type="text/css">
            @media (prefers-color-scheme: dark) {
                .contentCss{ background:  #000000; color: white; }
                .hrefCss{ color: #317AF7; }
            }
        </style>
    </head>
    <body class="contentCss">
    <div style="text-align:center">
        <p>Dark mode debug page</p>
    </div>
    </body>
    </html>
    ```