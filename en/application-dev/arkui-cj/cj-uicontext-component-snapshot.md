# Using Component Snapshot (ComponentSnapshot)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Capability Introduction

Component snapshotting is the capability to generate a bitmap ([PixelMap](../reference/ImageKit/cj-apis-image.md#class-pixelmap)) from the rendering result of a component node tree in an application. Currently, snapshotting of components that are mounted on the tree and displayed is supported.

> **Note:**
>
> - Component snapshotting depends on the UI context. First obtain a [ComponentSnapshot](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-componentsnapshot) instance using the [getComponentSnapshot()](../reference/arkui-cj/cj-apis-uicontext-uicontext.md#func-getcomponentsnapshot) method from [UIContext](../reference/arkui-cj/cj-apis-uicontext-uicontext.md#class-uicontext), and then call the corresponding methods through this instance.

### Snapshotting a Mounted Component

To snapshot a component that is explicitly mounted on the tree, use the [get](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#func-getstring-asynccallbackpixelmap-snapshotoptions) method and pass in the component ID (which needs to be configured in advance through the [.id](../reference/arkui-cj/cj-universal-attribute-componentid.md) universal attribute) to specify the component root node. When the system searches for the component to be snapshotted by the specified ID, it only traverses components that are mounted on the tree, and does not search for cache or offscreen components. The system takes the first found result, so the application must ensure the uniqueness of the component ID.

The snapshot can only capture the drawing content of the latest frame. If the snapshot is called at the same time that the component triggers an update, the updated rendering content will not be captured, and the snapshot returns the drawing content of the previous frame.

> **Note:**
>
> Avoid triggering a refresh of the component to be snapshotted while using the snapshot, to prevent interference with the snapshot content.

## Component Snapshot Best Practices

### Controlling the Snapshot Timing

When implementing the snapshot function, note that the rendering process of a component is not completed at one time. When the system builds and displays a component, it goes through multiple complex steps such as measurement, layout, and command submission, and finally presents it on the screen during one hardware refresh. Therefore, in specific cases, if the snapshot is called immediately after the component refresh, the expected content may not be obtained or a snapshot failure error may be reported.

To ensure accurate snapshot results, it is recommended to execute the snapshot operation after the component is fully rendered.

**Explicitly Wait for Drawing to Complete**

The main factor affecting the snapshot expectation is the time difference between the snapshot timing and the execution of the drawing instructions by the system service. When a snapshot call is initiated, all drawing instructions previously submitted by the application may not have been actually executed by the graphics service. To this end, you can specify `waitUntilRenderFinished` in the [SnapshotOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotoptions) parameter as true to ensure that the system waits for all previous drawing instructions to complete when executing the snapshot request, so as to capture more complete content.

> **Note:**
>
> It is recommended to always enable the `waitUntilRenderFinished` parameter.

**Understanding the Impact of Resource Loading on Snapshots**

Another common reason that affects snapshot expectations is the loading of image resources. Image components support online resource links and local resources, and the vast majority of image resources are in compressed formats such as PNG and JPEG. These resources need to be decoded by the system into a bitmap format that can be submitted for drawing. This process is performed on asynchronous I/O threads by default, so the snapshot may not meet expectations due to the uncertainty of the time consumed by this process.

The application can optimize in the following ways:
1. Parse the image into the PixelMap format in advance, and configure the PixelMap to the image component; this method is recommended for optimization first.
2. Set the syncLoad attribute of the image component to true to force synchronous loading, so that when the component is built, the resource can be directly submitted.

### Saving and Releasing the Bitmap Object in a Timely Manner

To release resources in a timely manner, when the PixelMap object returned by the snapshot interface is no longer used, assign it to null (None).

### Controlling the Sampling Precision

Do not snapshot an excessively large image. It is not recommended that the snapshot exceed the screen size. When the target length and width of the image to be captured exceed the underlying limit, the snapshot fails. You can control the `scale` parameter in [SnapshotOptions](../reference/arkui-cj/cj-apis-uicontext-componentsnapshot.md#class-snapshotoptions) to reduce the sampling precision, which can greatly save memory and greatly improve snapshot efficiency.
