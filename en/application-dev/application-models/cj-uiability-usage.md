# Basic Usage of UIAbility Component

The basic usage of the [UIAbility](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) component includes: specifying the startup page for UIAbility and obtaining the context information of UIAbility [UIAbilityContext](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext).

## Specifying the Startup Page for UIAbility

When launching an application's [UIAbility](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability), a startup page must be specified. Otherwise, the application may display a blank screen due to the absence of a default loaded page. The startup page can be set in the [onWindowStageCreate()](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#func-onwindowstagecreatewindowstage) lifecycle callback of UIAbility using the [loadContent()](../../../en/application-dev/reference/arkui-cj/cj-apis-window.md#class-windowstage) method of the [WindowStage](../../../en/application-dev/reference/arkui-cj/cj-apis-window.md#class-windowstage) object.

<!-- compile -->

```cangjie
import kit.AbilityKit.UIAbility
import kit.ArkUI.WindowStage

class MainAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        // Main window is created, set main page for this ability
        windowStage.loadContent("EntryView")
    }
    // ...
}
```

> **Note:**
>
> In DevEco Studio, the UIAbility instance created by default loads the Index page. Replace the Index page class name with the desired page class name as needed.

## Obtaining Context Information of UIAbility

The [UIAbility](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) class has its own context information, which is an instance of the [UIAbilityContext](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) class. The [UIAbilityContext](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) class includes properties such as `abilityInfo` and `currentHapModuleInfo`. Through AbilityContext, you can obtain relevant configuration information of the Ability, such as the package code path, Bundle name, Ability name, and environmental state required by the application. Additionally, you can access methods to operate the Ability instance (e.g., [startAbility()](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#func-startabilitywant), [terminateSelf()](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#func-terminateself)).

- In UIAbility, you can obtain the context information of the UIAbility instance via `this.context`.

  <!-- compile -->

  ```cangjie
  import kit.AbilityKit.{UIAbility, UIAbilityContext, Want, LaunchParam}
  import kit.ArkUI.WindowStage

  var globalContext : ?UIAbilityContext = None

  class MainAbility <: UIAbility {
      public override func onWindowStageCreate(windowStage: WindowStage): Unit {
          // Get the context of the Ability instance
          globalContext = this.context
          windowStage.loadContent("EntryView")
    }
  }
  ```

- To obtain the context information of the UIAbility instance in a page, two steps are required: importing the dependent resource context module and defining a context variable in the component.

  <!-- compile -->

  ```cangjie
  import kit.AbilityKit.{UIAbilityContext, Want}

  func getContext(): UIAbilityContext {
      return globalContext.getOrThrow()
  }

  @Entry
  @Component
  class EntryView {
      @State
      var context: UIAbilityContext = getContext()

      func startAbilityTest(): Unit {
          let want = Want(
              // Want parameter information
          )
          context.startAbility(want)
      }

      // Page display
      func build() {
          // ...
      }
  }
  ```

  Alternatively, after importing the dependent resource context module, you can define the variable before using [UIAbilityContext](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext).
  
  <!-- compile -->

  ```cangjie
  import kit.AbilityKit.{UIAbilityContext, Want}

  func getContext(): UIAbilityContext {
      return globalContext.getOrThrow()
  }

  @Entry
  @Component
  class EntryView {
      func startAbilityTest(): Unit {
          let context = getContext()
          let want = Want(
              // Want parameter information
          )
          context.startAbility(want)
      }

      // Page display
      func build() {
          // ...
      }
  }
  ```

- After completing the business logic, if developers wish to terminate the current [UIAbility](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) instance, they can do so by calling the [terminateSelf()](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-ui_ability.md#func-terminateself) method.

  <!-- compile -->

  ```cangjie
  internal import kit.PerformanceAnalysisKit.Hilog
  import kit.AbilityKit.{UIAbilityContext, Want}

  func getContext(): UIAbilityContext {
      return globalContext.getOrThrow()
  }

  @Entry
  @Component
  class EntryView {
      func build() {
          Row {
              Column {
                  Text("")
                      .fontSize(50)
                      .fontWeight(FontWeight.Bold)
                      .onClick {
                          evt =>
                          let context = getContext()
                          try {
                              // Execute normal business
                              context.terminateSelf()
                          } catch (e: Exception) {
                              // Handle business logic errors
                              Hilog.error(0, "terminateSelf failed", " message is ${e.toString()}")
                          }
                      }
              }.width(100.percent)
          }.height(100.percent)
      }
  }
  ```