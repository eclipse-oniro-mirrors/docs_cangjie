# ohos.font (Custom Font)

This module provides the capability to register custom fonts.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class Font

```cangjie
public class Font {}
```

**Description:** This class provides global methods for registering and retrieving custom fonts.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func getFontByName(String)

```cangjie
public func getFontByName(fontName: String): ?FontInfo
```

**Description:** Retrieves detailed information about a system font based on the specified font name.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type   | Required | Default | Description          |
|:----------|:-------|:---------|:--------|:---------------------|
| fontName  | String | Yes      | -       | The name of the system font. |

**Return Value:**

| Type                  | Description               |
|:----------------------|:--------------------------|
| ?[FontInfo](#class-fontinfo) | Detailed font information. |

### func getSystemFontList()

```cangjie
public func getSystemFontList(): Array<String>
```

**Description:** Retrieves the list of system fonts.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

| Type           | Description            |
|:---------------|:-----------------------|
| Array\<String> | List of system fonts.  |

### func registerFont(ResourceStr, ResourceStr)

```cangjie
public func registerFont(familyName!: ResourceStr, familySrc!: ResourceStr): Unit
```

**Description:** Registers a custom font in the font management system.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter  | Type                                                                 | Required | Default | Description                                                                 |
|:-----------|:---------------------------------------------------------------------|:---------|:--------|:----------------------------------------------------------------------------|
| familyName | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes      | -       | **Named parameter.** The name of the font to be registered.                 |
| familySrc  | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes      | -       | **Named parameter.** The file path of the font to be registered.           |

## class FontInfo

```cangjie
public class FontInfo {
    public var path: String
    public var postScriptName: String
    public var fullName: String
    public var family: String
    public var subfamily: String
    public var weight: UInt32
    public var width: UInt32
    public var italic: Bool
    public var monoSpace: Bool
    public var symbolic: Bool
}
```

**Description:** Represents font information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var family

```cangjie
public var family: String
```

**Description:** Describes the font family of the system font.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var fullName

```cangjie
public var fullName: String
```

**Description:** Represents the full name of the system font.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var italic

```cangjie
public var italic: Bool
```

**Description:** Indicates whether the system font is italic.

**Type:** Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var monoSpace

```cangjie
public var monoSpace: Bool
```

**Description:** Indicates whether the system font is monospaced.

**Type:** Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var path

```cangjie
public var path: String
```

**Description:** Describes the file path of the system font.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var postScriptName

```cangjie
public var postScriptName: String
```

**Description:** Represents the PostScript name of the system font.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var subfamily

```cangjie
public var subfamily: String
```

**Description:** Represents the subfamily of the system font.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var symbolic

```cangjie
public var symbolic: Bool
```

**Description:** Indicates whether the system font supports symbolic characters.

**Type:** Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var weight

```cangjie
public var weight: UInt32
```

**Description:** When weight > 0, it indicates that this font set only contains fonts with the specified weight. When weight = 0, it indicates that this font set contains all fonts.

**Type:** UInt32

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var width

```cangjie
public var width: UInt32
```

**Description:** Represents the width of the system font in pixels (px).

**Type:** UInt32

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

## Example Code

### Example 1 (Register Custom Font)

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    protected func onAppear() {
        getUIContext().getFont().registerFont(
            familyName: "Deyihei",
            familySrc: "/resources/rawfile/SmileySans-Oblique.ttf"
        )
    }

    func build() {
        Row {
            Column {
                Text("HelloWorld").fontFamily("Deyihei")
                Text("HelloWorld")
            }.width(100.percent)
        }.height(100.percent)
    }
}
```

![font1](figures/registerFont.png)

### Example 2 (Get System Font List)

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    func build() {
        Row {
            Column {
                Button("HelloWorld")
                .onClick {evt =>
                    let list = getUIContext().getFont().getSystemFontList()
                    Hilog.info(0, "AppLogCj", "${list.size}")
                }
            }.width(100.percent)
        }.height(100.percent)
    }
}
```

### Example 3 (Get Font Details)

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    func build() {
        Row {
            Column {
                Button("HelloWorld")
                .onClick {evt =>
                    let info = getUIContext().getFont().getFontByName("HarmonyOS Sans Italic")
                    match (info) {
                        case Some(v) =>
                            Hilog.info(0, "AppLogCj", "${v.path}")
                            Hilog.info(0, "AppLogCj", "${v.postScriptName}")
                            Hilog.info(0, "AppLogCj", "${v.fullName}")
                            Hilog.info(0, "AppLogCj", "${v.family}")
                            Hilog.info(0, "AppLogCj", "${v.subfamily}")
                            Hilog.info(0, "AppLogCj", "${v.weight}")
                            Hilog.info(0, "AppLogCj", "${v.width}")
                            Hilog.info(0, "AppLogCj", "${v.italic}")
                            Hilog.info(0, "AppLogCj", "${v.monoSpace}")
                            Hilog.info(0, "AppLogCj", "${v.symbolic}")
                        case None => Hilog.error(0, "AppLogCj", "None")
                    }
                }
            }.width(100.percent)
        }.height(100.percent)
    }
}
```