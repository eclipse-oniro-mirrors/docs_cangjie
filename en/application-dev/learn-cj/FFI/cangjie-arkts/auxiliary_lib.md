# Cangjie-ArkTS Interoperability Helper Library

To assist developers in writing Cangjie-ArkTS interoperability code more conveniently, Cangjie provides an interoperability helper library. This library offers a richer set of APIs for developers to call. For example, in scenarios where a Cangjie application needs to use existing ArkTS libraries, when the interface in the ArkTS module that the developer wants to call requires a `context` parameter, the `getJSContext` function provided by the helper library can be used to obtain it.

For instance, the following shows the declaration of the `pick` method in the ArkTS [Camera Picker](https://docs.openharmony.cn/pages/v5.1/en/application-dev/reference/apis-camera-kit/js-apis-cameraPicker.md) module, where the first parameter type is `common.Context`.

```typescript
declare namespace cameraPicker {
  // ...
  function pick(context: Context, mediaTypes: Array<PickerMediaType>, pickerProfile: PickerProfile): Promise<PickerResult>;
}
```

For such interoperability scenarios, the helper library provides a `getJSContext` interface, which can convert a `UIAbilityContext`-type context into a `JSValue` that can be called for interoperability.

```cangjie
public func getJSContext(runtime: JSRuntime, abilityContext: UIAbilityContext): JSValue
```

The following example illustrates its usage:

1. After creating a [Cangjie] Empty Ability project, add a global instance of `UIAbilityContext` in the `entry->src->main->cangjie->main_ability.cj` file and assign it in the `onCreate` function:

    ```cangjie
    import ohos.ability.UIAbilityContext

    // Global instance of UIAbilityContext
    var globalAbilityContext: ?UIAbilityContext = None

    class MainAbility <: UIAbility {
        // ...
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            // Save the context instance when UIAbility is created
            globalAbilityContext = context
        }
        // ...
    }
    ```

2. Use the helper library interface in Cangjie code:

    ```cangjie
    import ohos.ark_interop.*
    import ohos.ark_interop_helper.*
    import ohos.ability.UIAbilityContext

    var runtime = Option<JSRuntime>.None

    // Get JSRuntime from global variable or create a new one
    func getRuntime() {
        return match (runtime) {
            case Some(v) => v
            case None =>
                let v = JSRuntime()
                runtime = v
                v
        }
    }

    // Get UIAbilityContext from global variable
    func getContext(): UIAbilityContext {
        match (globalAbilityContext) {
            case Some(context) =>
                context
            case _ =>
                AppLog.error("####getContext err ")
                throw Exception("get globalAbilityContext failed")
        }
    }

    // Create JSValue using the helper library interface getJSContext
    func getJSContextCase(): JSValue {
        let runtime = getRuntime()
        let abilityContext = getContext()
        getJSContext(runtime, abilityContext)
    }
    ```