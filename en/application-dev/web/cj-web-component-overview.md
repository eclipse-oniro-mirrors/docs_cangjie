# Introduction to ArkWeb

## Usage Scenarios

ArkWeb (Ark Web) provides Web components for displaying Web page content within applications. Common usage scenarios include:

- **Application-integrated Web pages**: Applications can embed Web page content using Web components to reduce development costs and improve development and operational efficiency.
- **Web browsing in browser applications**: Browser-type applications can use Web components to open third-party web pages, enable incognito mode for browsing, and set up ad-blocking, among other features.
- **Mini-programs**: Mini-program host applications can use Web components to render mini-program pages.

## Capabilities

The Web component offers developers extensive control over Web pages, including:

- **Web page loading**: Declarative loading of Web pages and off-screen loading of Web pages.
- **Lifecycle management**: Component lifecycle state changes, notifications of Web page loading status changes, etc.
- **Common properties and events**: User-Agent management, Cookie and storage management, font and dark mode management, permission management, etc.
- **Interaction with application interfaces**: Custom text selection menus, context menus, file upload interfaces, and other interactive capabilities with the application interface.
- **JavaScript interaction**: Applications can interact with Web pages via JavaScriptProxy.
- **Security and privacy**: Incognito browsing mode, ad-blocking, Shield Protection mode, etc.
- **Debugging capabilities**: Debugging with [DevTools](cj-web-debugging-with-devtools.md) and collecting Web component crash information using crashpad.
- **Other advanced capabilities**: Same-layer rendering with native components, network hosting for Web components, media playback hosting for Web components, and custom input method invocation for Web component input fields<!--RP1--><!--RP1End-->, among others.

## Constraints and Limitations

**Web engine version**: ArkWeb is developed based on the Google Chromium engine, with the current Chromium version being M114.