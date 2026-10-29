# Character Processing

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Function Introduction

Character rules vary greatly in different languages. Character processing ensures that text is processed with similar logic under different language rules. Cangjie provides the [Transliterator](../reference/LocalizationKit/cj-apis-i18n.md#class-transliterator) class to create transliterator objects and convert the input text from the source format to the target format.

## How to Develop

For details about how to use the APIs, see the API document of [Transliterator](../reference/LocalizationKit/cj-apis-i18n.md#class-transliterator).

1. Import the modules.

   <!-- compile -->

   ```cangjie
   import kit.LocalizationKit.*
   import kit.PerformanceAnalysisKit.Hilog
   ```

2. Use cases.

- Transliteration: Transliteration refers to the process of converting text represented by one writing system or alphabet into text represented by another writing system or alphabet with the same pronunciation. It is distinct from translation. You can implement transliteration by using the `transform` method of `Transliterator`. The sample code is as follows:

  > **Note:**
  >
  > This module supports converting Chinese characters into pinyin. However, when the Chinese text contains polyphonic characters, some of these characters may fail to be converted into pinyin with the accurate pronunciation.
  >
  > If the conversion ID passed to `getInstance` is not supported, an exception with error code 8900001 is thrown.

  <!-- compile -->

  ```cangjie
  // index.cj

  // Transliterate the text into the Latn format.
  let transliterator = Transliterator.getInstance("Any-Latn")
  let transliterateLatn = transliterator.transform("中国") // transliterateLatn = 'zhōng guó'
  Hilog.info(0, "test", "transliterateLatn=${transliterateLatn}")

  // Chinese transliteration with tones removed.
  let asciiTransliterator = Transliterator.getInstance("Any-Latn;Latin-Ascii")
  let transliterateAscii = asciiTransliterator.transform("中国") // transliterateAscii = 'zhong guo'
  Hilog.info(0, "test", "transliterateAscii=${transliterateAscii}")
  ```
