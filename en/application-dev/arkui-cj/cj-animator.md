# Frame Animation (ohos.animator)

Frame animation features frame-by-frame callback capabilities, enabling developers to process properties requiring adjustment in each frame. By providing an onFrame callback to applications, frame animation allows developers to set property values in each frame of the application, thereby achieving smooth transitions in component property value changes and creating animation effects.

Compared to property animation, frame animation enables developers to perceive animation progress in real-time and adjust UI values instantly, offering advantages in immediate event response and pausability. However, it performs slightly worse than property animation in terms of performance. When property animation can meet requirements, it is recommended to prioritize using property animation interfaces. For property animation interfaces, refer to [Implementing Property Animation](cj-attribute-animation-apis.md).

| Name | Implementation | Event Response | Pausable | Performance |
|:---|:---|:---|:---|:---|
| Frame Animation (ohos.animator) | Developers can modify UI-side property values frame-by-frame, with real-time UI-side property updates | Real-time response | Yes | Poor |
| Property Animation | UI-side only calculates the final animation state; the animation process involves changing rendered values while the UI-side remains in the final animation state, unaware of real-time rendered values | Responds based on final state | No | Good |

As shown in the diagram, frame animation responds in real-time during the animation process, while property animation responds based on the final state.

![animator](figures/animator1.gif)

![animator](figures/animator2.gif)

## Implementing Animation Effects Using Frame Animation

Follow these steps to create a simple animator and print the current interpolation in each frame callback.

1. Import the necessary dependencies.

    ```cangjie
    import kit.ArkUI.*
    ```

2. Create the object to execute the animation.

    ```cangjie
    // Create initial parameters for the animation
    this.backAnimator = getUIContext.createAnimator(AnimatorOptions(
      duration: 1500,
      easing: "friction",
      delay: 0,
      fill: AnimatorFill.Forwards,
      direction: AnimatorDirection.Normal,
      iterations: 2,
      // Initial value for onFrame interpolation in the first frame
      begin: 200.0,
      // Final value for onFrame interpolation in the last frame
      end: 400.0
    ))
    // Set the callback for receiving frames; the onFrame callback is invoked for each frame during animation playback
    this.backAnimator?.onFrame =  {  progress: Float64 =>
      Hilog.info(0,"", "current value is: " + progress.toString())
    }
    ```

3. Play the animation.

    ```cangjie
    // Play the animation
    this.backAnimator?.play()
    ```

4. Manually release the AnimatorResult object after the animation completes.

    ```cangjie
    // Release the animation object
    this.backAnimator = None
    ```

## Implementing Parabolic Motion of a Ball Using Frame Animation

1. Import the necessary dependencies.

    ```cangjie
    import kit.ArkUI.*
    ```

2. Define the component to be animated.

    ```cangjie
    Button()
    .borderRadius(45.vp)
    .width(60)
    .height(60)
    .translate( x: this.translateX, y: this.translateY )
    ```

3. Create the AnimatorResult object in onPageShow.

    ```cangjie
    // Create the animatorResult object
    protected override func onPageShow() {
      this.backAnimator = getUIContext.createAnimator(AnimatorOptions(
        duration: 4000,
        easing: "ease",
        delay: 0,
        fill: AnimatorFill.Forwards,
        direction: AnimatorDirection.Normal,
        iterations: 1,
        begin: 0.0,
        end: 200.0
      ))
      this.backAnimator?.onFrame =  {  progress: Float64 =>
        this.translateX = Int64(progress)
        if (progress > this.topWidth && this.translateY < this.bottomHeight) {
          this.translateY = Int64(pow(Float64(progress - this.topWidth), 2) * this.g)
        }
      }
      // Method executed when the animation is canceled
      this.backAnimator?.onCancel = { =>
        this.animatorStatus = 'Canceled'
      }
      // Method executed when the animation completes
      this.backAnimator?.onFinish = { =>
        this.animatorStatus = 'Completed'
      }
      // Method executed when the animation repeats
      this.backAnimator?.onRepeat = { =>
          Hilog.info(0,"", "Animation repeated")
      }
    }
    ```

4. Define buttons for playing, resetting, and pausing the animation.

    ```cangjie
    Button('Play').onClick({ =>
      this.backAnimator?.play()
      this.animatorStatus = 'Playing'
    }).width(80).height(35)
    Button("Reset").onClick({ =>
      this.translateX = 0
      this.translateY = 0
    }).width(80).height(35)
    Button("Pause").onClick({ =>
      this.backAnimator?.pause()
      this.animatorStatus = 'Paused'
    }).width(80).height(35)
    ```

5. Release the animation object in the page hide or destroy lifecycle to avoid memory leaks.

    ```cangjie
    protected override func onPageHide() {
      this.backAnimator = None
    }
    ```

Complete example follows.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import std.math.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    var backAnimator: ?AnimatorResult = None
    @State
    var animatorStatus: String = 'Created'
    var topWidth: Float64 = 150.0
    var bottomHeight: Int64 = 100
    var g: Float64 = 0.18
    @State
    var translateX: Int64 = 0
    @State
    var translateY: Int64 = 0
    protected override func onPageShow() {
        this.backAnimator = getUIContext.createAnimator(AnimatorOptions(
          duration: 4000,
          easing: "ease",
          delay: 0,
          fill: AnimatorFill.Forwards,
          direction: AnimatorDirection.Normal,
          iterations: 1,
          begin: 0.0,
          end: 200.0
        ))
        this.backAnimator?.onFrame =  {  progress: Float64 =>
          this.translateX = Int64(progress)
          if (progress > this.topWidth && this.translateY < this.bottomHeight) {
            this.translateY = Int64(pow(Float64(progress - this.topWidth), 2) * this.g)
          }
        }
        this.backAnimator?.onCancel = { =>
          this.animatorStatus = 'Canceled'
        }
        this.backAnimator?.onFinish = { =>
          this.animatorStatus = 'Completed'
        }
        this.backAnimator?.onRepeat = { =>
            Hilog.info(0,"", "Animation repeated")
        }
    }
    protected override func onPageHide() {
        this.backAnimator = None
    }
    func build() {
        Column() {
          Column(space:30) {
            Button('Play').onClick({ evt=>
              this.backAnimator?.play()
              this.animatorStatus = 'Playing'
            }).width(80).height(35)
            Button("Reset").onClick({ evt=>
              this.translateX = 0
              this.translateY = 0
            }).width(80).height(35)
            Button("Pause").onClick({ evt=>
              this.backAnimator?.pause()
              this.animatorStatus = 'Paused'
            }).width(80).height(35)
          }.width(100.percent).height(25.percent)

          Stack() {
            Button()
              .borderRadius(45.vp)
              .width(60)
              .height(60)
              .translate( x: this.translateX, y: this.translateY )
          }
          .width(100.percent)
          .height(45.percent)
          .align(Alignment.Start)

          Text("Current animation status: " + this.animatorStatus)
        }.width(100.percent).height(100.percent)
    }
}
```

![animator](figures/animator3.gif)