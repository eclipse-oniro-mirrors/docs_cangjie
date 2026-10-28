# 字符处理

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

## 功能介绍

在不同语言中，字符规则差异较大。通过字符处理，可以保证在不同语言规则下，以相似的逻辑处理文本。仓颉侧提供[Transliterator](../reference/LocalizationKit/cj-apis-i18n.md#class-transliterator)类，用于创建音译对象并将输入文本从源格式转换为目标格式。

## 开发步骤

接口具体使用方法和说明请参考[Transliterator](../reference/LocalizationKit/cj-apis-i18n.md#class-transliterator)的API接口文档。

1. 导入模块。

   <!-- compile -->

   ```cangjie
   import kit.LocalizationKit.*
   import kit.PerformanceAnalysisKit.Hilog
   ```

2. 使用场景。

- 音译：是指将采用某个文字系统或字母表表示的文本转换为发音相同的采用另一个文字系统或字母表表示的文本的过程，并不等同于翻译。使用`Transliterator`的`transform`方法可以实现音译功能。示例代码如下：

  > **说明：**
  >
  > 本模块支持中文汉字转拼音，但当中文文本中包含多音字时，可能出现部分多音字无法按照正确的发音转换为拼音的问题。
  >
  > 调用`getInstance`时，若传入的转换ID不受支持，将抛出8900001异常。

  <!-- compile -->

  ```cangjie
  // index.cj

  // 音译成Latn格式
  let transliterator = Transliterator.getInstance("Any-Latn")
  let transliterateLatn = transliterator.transform("中国") // transliterateLatn = 'zhōng guó'
  Hilog.info(0, "test", "transliterateLatn=${transliterateLatn}")

  // 汉语音译去声调
  let asciiTransliterator = Transliterator.getInstance("Any-Latn;Latin-Ascii")
  let transliterateAscii = asciiTransliterator.transform("中国") // transliterateAscii = 'zhong guo'
  Hilog.info(0, "test", "transliterateAscii=${transliterateAscii}")
  ```
