# Drawing Custom Graphics with Canvas

Canvas provides a canvas component for custom graphic rendering. Developers can use the `CanvasRenderingContext2D` and `OffscreenCanvasRenderingContext2D` objects to draw on the Canvas component, supporting basic shapes, text, images, and more.

## Drawing Custom Graphics with Canvas Component

- Use the [CanvasRenderingContext2D](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md) object to draw on the Canvas.

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry

  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*

  @Entry
  @Component
  class EntryView {
      // Configures parameters for the CanvasRenderingContext2D object, including antialiasing (true enables antialiasing).
      var settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
      // Creates a CanvasRenderingContext2D object for drawing on the canvas.
      var context: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)
      func build() {
          Flex(direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center) {
              // Invokes the CanvasRenderingContext2D object on the canvas.
              Canvas(this.context)
                  .width(100.percent)
                  .height(100.percent)
                  .backgroundColor(0XF5DC62)
                  .onReady(
                      {
                          =>
                          // Drawing content can be added here.
                          this.context.lineWidth = 0.6
                          this.context.strokeRect(50.0, 50.0, 200.0, 150.0);
                      }
                  )
          }.width(100.percent).height(100.percent)
      }
  }
  ```

  ![Canvas](figures/Canvas.jpg)

## Initializing the Canvas Component

`onReady(() -> Unit)` is an event callback triggered when the Canvas component initializes or resizes. After this event is called, the exact width and height of the Canvas component can be obtained, allowing further use of `CanvasRenderingContext2D` and `OffscreenCanvasRenderingContext2D` objects to call relevant APIs for graphic rendering.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    // Configures parameters for the CanvasRenderingContext2D object, including antialiasing (true enables antialiasing).
    var settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
    // Creates a CanvasRenderingContext2D object for drawing on the canvas.
    var context: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)
    func build() {
        Canvas(this.context)
        .width(100.percent)
        .height(100.percent)
        .backgroundColor(0XF5DC62)
        .onReady({
            =>
            this.context.fillStyle(0X0097D4)
            this.context.fillRect(50.0, 50.0, 100.0, 100.0)
        })
    }
}
```

![Canvas1](figures/Canvas1.jpg)

## Canvas Component Drawing Methods

After calling the Canvas component's lifecycle interface `onReady()`, developers can directly use the Canvas component for drawing. Alternatively, they can define a `Path2D` object separately to construct an ideal path and then use the Canvas component for rendering after `onReady()` is called.

- Directly call relevant APIs using `CanvasRenderingContext2D` and `OffscreenCanvasRenderingContext2D` objects for drawing.

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry

  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*

  @Entry
  @Component
  class EntryView {
      private let settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
      private let context: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)

      func build() {
          Flex(direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center) {
              Canvas(this.context)
                  .width(100.percent)
                  .height(100.percent)
                  .backgroundColor(0XF5DC62)
                  .onReady(
                      {
                          =>
                          this.context.beginPath()
                          this.context.moveTo(50.0, 50.0)
                          this.context.lineTo(280.0, 160.0)
                          this.context.stroke()
                      }
                  )
          }.width(100.percent).height(100.percent)
      }
  }
  ```

  ![Canvas2](figures/Canvas2.jpg)

- First define a `Path2D` object to construct the desired path, then use the `stroke` or `fill` methods of `CanvasRenderingContext2D` or `OffscreenCanvasRenderingContext2D` for drawing. Refer to `Path2D` for specific usage.

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry

  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*

  @Entry
  @Component
  class EntryView {
      private let settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
      private let context: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)

      var region: Path2D = Path2D()
      func build() {
          Flex(direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center) {
              Canvas(this.context)
                  .width(100.percent)
                  .height(100.percent)
                  .backgroundColor(0XF5DC62)
                  .onReady(
                      {
                          =>
                          this.region.arc(100.0, 75.0, 50.0, 0.0, 6.28)
                          this.context.stroke(this.region)
                      }
                  )
          }.width(100.percent).height(100.percent)
      }
  }
  ```

  ![Canvas3](figures/Canvas3.jpg)

## Common Methods of Canvas Component

The `OffscreenCanvasRenderingContext2D` and `CanvasRenderingContext2D` objects provide numerous properties and methods for drawing text, graphics, pixel manipulation, etc., forming the core of the Canvas component. Common interfaces include [fill](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-fill) (fills a closed path), [clip](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-clip) (sets the current path as a clipping path), [stroke](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-stroke) (performs stroke operations), etc. Additionally, properties like [fillStyle](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-fillstylecanvasgradient) (specifies fill color), [globalAlpha](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-globalalphafloat64) (sets transparency), and [strokeStyle](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-strokestylecanvasgradient) (sets stroke color) modify rendering styles. Below are some common use cases:

- Basic Shape Drawing.

  Use interfaces like [arc](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-arcfloat64-float64-float64-float64-float64-bool) (draws an arc), [ellipse](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-ellipsefloat64-float64-float64-float64-float64-float64-float64-bool) (draws an ellipse), and [rect](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-rectfloat64-float64-float64-float64) (creates a rectangular path) to draw basic shapes.

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry

  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*
  import std.math.MathExtension

  @Entry
  @Component
  class EntryView {
  private let settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
  private let context: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)

  func build() {
      Flex(direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center) {
              Canvas(this.context)
              .width(100.percent)
              .height(100.percent)
              .backgroundColor(0XF5DC62)
              .onReady({
                  =>
                      // Draws a rectangle
                      this.context.beginPath()
                      this.context.rect(100.0, 50.0, 100.0, 100.0)
                      this.context.stroke()
                      // Draws a circle
                      this.context.beginPath()
                      this.context.arc(150.0, 250.0, 50.0, 0.0, 6.28)
                      this.context.stroke()
                      // Draws an ellipse
                      this.context.beginPath()
                      this.context.ellipse(150.0, 450.0, 50.0, 100.0, Float64.GetPI() * 0.25, Float64.GetPI() * 0.0, Float64.GetPI() * 2.0)
                      this.context.stroke()
              })
      }.width(100.percent).height(100.percent)
  }
  }
  ```

  ![Canvas4](figures/Canvas4.jpg)

- Text Drawing.

  Use interfaces like [fillText](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-filltextstring-float64-float64) (fills text) and [strokeText](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-stroketextstring-float64-float64) (strokes text) for text rendering. The example sets the font to a bold 50-pixel "sans-serif" and uses `fillText` to draw "Hello World!" at (50, 100). It then sets `strokeStyle` to red, `lineWidth` to 0.7, and the same font to stroke the text outline at (50, 120).

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry

  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*

  @Entry
  @Component
  class EntryView {
      private let settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
      private let context: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)

      func build() {
          Flex(direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center) {
              Canvas(this.context)
                  .width(100.percent)
                  .height(100.percent)
                  .backgroundColor(0XF5DC62)
                  .onReady({
                      =>
                      // Text fill
                      this.context.font(size: 50.px, weight: FontWeight.Bolder, family: "sans-serif")
                      this.context.fillText("Hello World!", 50.0, 100.0)
                      // Text stroke
                      this.context.strokeStyle(0Xff0000)
                      this.context.lineWidth = 0.7
                      this.context.font(size: 50.px, weight: FontWeight.Bolder, family: "sans-serif")
                      this.context.strokeText("Hello World!", 50.0, 120.0)
                      }
                  )
          }.width(100.percent).height(100.percent)
      }
  }
  ```

  ![Canvas5](figures/Canvas5.jpg)

- Other Methods.

  Canvas also provides other methods. Gradient-related methods include [createLinearGradient](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-createlineargradientfloat64-float64-float64-float64) (creates a linear gradient) and [createRadialGradient](../../../en/application-dev/reference/arkui-cj/cj-canvas-drawing-canvasrenderingcontext2d.md#func-createradialgradientfloat64-float64-float64-float64-float64-float64) (creates a radial gradient).

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry

  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*
  
  @Entry
  @Component
  class EntryView {
      private let settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
      private let context: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)

      func build() {
            Canvas(this.context)
                .width(100.percent)
                .height(100.percent)
                .backgroundColor(0XF5DC62)
                .onReady(
                    {
                        =>
                        // Creates a radial gradient CanvasGradient object
                        let grad = this.context.createRadialGradient(200.0, 200.0, 50.0, 200.0, 200.0, 200.0)
                        // Sets gradient stops for the CanvasGradient object, including offset and color
                        grad.addColorStop(0.0, 0XE87361)
                        grad.addColorStop(0.5, 0XFFFFF0)
                        grad.addColorStop(1.0, 0XBDDB69)
                        // Fills a rectangle with the CanvasGradient object
                        this.context.fillStyle(grad)
                        this.context.fillRect(0.0, 0.0, 400.0, 400.0)
                    }
                )
        }
  }
  ```

  ![Canvas6](figures/Canvas6.jpg)

## Usage Examples

- Regular Basic Shape Drawing.

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry

  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*

  @Entry
  @Component
  class EntryView {
      private let settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
      private let context: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)

      func build() {
          Flex(direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center) {
              Canvas(this.context)
                  .width(100.percent)
                  .height(100.percent)
                  .backgroundColor(0XF5DC62)
                  .onReady(
                      {
                      =>
                          // Sets fill style to blue
                          this.context.fillStyle(0X0097D4)
                          // Draws a 200x200 rectangle with top-left corner at (50, 50)
                          this.context.fillRect(50.0, 50.0, 200.0, 200.0)
                          // Clears a 150x100 area with top-left corner at (70, 70)
                          this.context.clearRect(70.0, 70.0, 150.0, 100.0)
                      }
                  )
          }.width(100.percent).height(100.percent)
      }
  }
  ```

  ![Canvas7](figures/Canvas7.jpg)

- Irregular Shape Drawing.

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry

  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*

  @Entry
  @Component
  class EntryView {
      private let settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
      private let context: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)

      // Constructs a pentagon using Path2D interfaces
      var path: Path2D = Path2D()
      func build() {
          Flex(direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center) {
              Canvas(this.context)
                  .width(100.percent)
                  .height(100.percent)
                  .backgroundColor(0XF5DC62)
                  .onReady(
                      {
                      =>
                      path.moveTo(150.0, 50.0)
                      path.lineTo(50.0, 150.0)
                      path.lineTo(100.0, 250.0)
                      path.lineTo(200.0, 250.0)
                      path.lineTo(250.0, 150.0)
                      path.closePath()
                      // Sets fill color to blue
                      this.context.fillStyle(0X0097D4)
                      // Fills the pentagon described by Path2D on the canvas
                      this.context.fill(path)
                      }
                  )
          }.width(100.percent).height(100.percent)
      }
  }
  ```

  ![Canvas8](figures/Canvas8.jpg)