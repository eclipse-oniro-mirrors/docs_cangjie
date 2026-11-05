# 使用组件截图（ComponentSnapshot）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

## 能力介绍

组件截图是将应用内一个组件节点树的渲染结果生成位图（[PixelMap](../reference/ImageKit/cj-apis-image.md#class-pixelmap)）的能力。当前支持对已挂树显示的组件进行截图。

> **说明：**
>
> - 组件截图依赖UI上下文，需先通过[UIContext](../reference/arkui-cj/cj-apis-uicontext-uicontext.md#class-uicontext)中的[getComponentSnapshot()](../reference/arkui-cj/cj-apis-uicontext-uicontext.md#func-getcomponentsnapshot)方法获取[ComponentSnapshot](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-componentsnapshot)实例，再通过该实例调用对应方法。

### 对挂树组件截图

对已明确挂树的组件进行截图，可通过[get](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#func-getstring-asynccallbackpixelmap-snapshotoptions)方法实现，传入组件标识（需提前通过[.id](../reference/arkui-cj/cj-universal-attribute-componentid.md)通用属性配置）以指定组件根节点。系统在通过指定的ID查找待截图组件时，仅遍历已挂树的组件，不对cache或离屏组件进行查找。系统以首个查找到的结果为准，故应用需**确保组件标识ID的唯一性**。

截图仅能获取最近一帧的绘制内容。若在组件触发更新的同时调用截图，更新的渲染内容不会被截取，截图将返回前一帧的绘制内容。

> **说明：**
>
> 尽量避免在使用截图时触发待截图组件的刷新，防止对截图内容的干扰。

## 组件截图最佳实践

### 合理控制截图时机

在实现截图功能时，需注意组件的渲染过程非一次性完成。系统在构建与显示组件时，将经过测量、布局、提交指令等多个复杂步骤，最终在一次硬件刷新时呈现于屏幕上。因此，在特定情况下，若在组件刷新后立即调用截图，可能无法获取预期内容或出现截图失败报错。

为了确保截图结果准确，建议在组件完全渲染后再执行截图操作。

**明确等待绘制完成**

影响截图预期的主要因素是截图时机与系统服务执行绘制指令的时间差。在发起截图调用时，应用侧之前提交的所有绘制指令可能尚未被图形服务真正执行。为此，可以通过指定[SnapshotOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotoptions)参数中的`waitUntilRenderFinished`为true，来确保系统在执行截图请求时等待所有之前的绘制指令均执行完毕，从而截取到更完整的内容。

> **说明：**
>
> 建议始终开启`waitUntilRenderFinished`参数。

**了解资源加载对截图的影响**

影响截图预期的另一个常见原因，是图片资源的加载。图片组件支持在线资源链接，也可指定本地资源，且绝大多数图片资源为PNG、JPEG等压缩格式。这些资源需要系统解码为可提交绘制的位图格式，此过程默认在异步IO线程上进行，因此可能由于该过程耗时的不确定性而导致截图不符合预期。

应用可通过以下几种方式进行优化：
1. 自行提前解析图片为PixelMap格式，将PixelMap配置给图片组件；建议优先以此方法进行优化。
2. 配置所使用的图片组件的syncLoad属性为true来强制同步加载，这样组件被构建时，即可确保资源可以直接被提交。

### 及时保存和释放位图对象

为了及时释放资源，当截图接口返回的PixelMap对象不再使用时，应将其赋值为空（None）。

### 合理控制采样精度

请不要截取过大尺寸的图片，截图不建议超过屏幕尺寸大小。当要截取的图片目标长宽超过底层限制时，截图会返回失败。可以通过控制[SnapshotOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotoptions)中的`scale`参数，减小采样精度，这可以在很大程度上节省内存，并大幅度提高截图的效率。
