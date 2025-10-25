# Restrictions on Access Modifiers for Custom Component Member Properties

In state management, when component developers encapsulate custom components, the absence of clear input/output identifiers makes it impossible for callers to uniformly determine which variables should be passed as component parameters. In state management, qualifiers cannot be used to modify state variables.

Cangjie validates the access modifiers (private/public/protected) used for member variables in custom components. When these access modifiers are not used according to specifications, corresponding log messages will be generated.

Before reading this document, it is recommended to first read: [State Management Overview](../state_management/cj-state-management-overview.md).

## Usage Restrictions

- Initialization rules for [@State](../state_management/cj-macro-state.md)/[@Prop](../state_management/cj-macro-prop.md)/[@Provide](../state_management/cj-macro-provide-and-consume.md)/[@BuilderParam](./cj-macro-builderparam.md)/regular member variables (ordinary variables not involved in updates) allow external initialization.

- Initialization rules for [@StorageLink](../state_management/cj-appstorage.md#storagelink)/[@StorageProp](../state_management/cj-appstorage.md#storageprop)/[@LocalStorageLink](../state_management/cj-localstorage.md#localstoragelink)/[@LocalStorageProp](../state_management/cj-localstorage.md#localstorageprop)/[@Consume](../state_management/cj-macro-provide-and-consume.md) variables prohibit external initialization.

- Initialization rules for [@Link](../state_management/cj-macro-link.md) variables require external initialization and prohibit local initialization.

## Usage Scenarios

1. When a member variable is modified with both the private access modifier and @State/@Prop/@Provide/@BuilderParam macros, Cangjie will validate and generate an error.

    **Counter Example**

    ```cangjie
    package ohos_app_cangjie_entry

    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Column {
                ComponentChild(state_value: "Hello", prop_value: "Hello", provide_value: "Hello", builder_value: buildTest,
                    regular_value: "Hello")
            }.width(100.percent)
        }
    }

    @Component
    class ComponentChild {
        // Using private modifier here will cause an error
        @State
        private var state_value: String = "Hello"
        // Using private modifier here will cause an error
        @Prop
        private var prop_value: String
        // Using private modifier here will cause an error
        @Provide
        private var provide_value: String = "Hello"
        // Using private modifier here will cause an error
        @BuilderParam
        private var builder_value: () -> Unit = buildTest
        // This usage is correct
        private var regular_value: String = "Hello"

        func build() {
            Column() {
                Text("Hello")
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
            }
        }
    }

    @Builder
    func buildTest() {
        Text("Child builder")
    }
    ```

    **Correct Example**

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry

    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Column {
                ComponentChild(state_value: "Hello", prop_value: "Hello", provide_value: "Hello", builder_value: buildTest,
                    regular_value: "Hello")
            }.width(100.percent)
        }
    }

    @Component
    class ComponentChild {
        @State
        var state_value: String = "Hello"
        @Prop
        var prop_value: String
        @Provide
        var provide_value: String = "Hello"
        @BuilderParam
        var builder_value: () -> Unit = buildTest
        var regular_value: String = "Hello"

        func build() {
            Column() {
                Text("Hello")
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
            }
        }
    }

    @Builder
    func buildTest() {
        Text("Child builder")
    }
    ```

2. When a member variable is modified with both the public access modifier and @StorageLink/@StorageProp/@LocalStorageLink/@LocalStorageProp/@Consume macros, Cangjie will validate and generate an error.

    **Counter Example**

    ```cangjie
    package ohos_app_cangjie_entry

    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    let storage = LocalStorage()

    @Entry[storage]
    @Component
    class EntryView {
        @Provide var consume_value: String = "Hello"

        func build() {
            Column {
                ComponentChild()
            }
            .width(100.percent)
        }
    }

    @Component
    class ComponentChild {
        // Using public modifier here will cause an error
        @LocalStorageProp["sessionLocalProp"] public let local_prop_value: String = "Hello"
        // Using public modifier here will cause an error
        @LocalStorageLink["sessionLocalLink"] public var local_link_value: String = "Hello"
        // Using public modifier here will cause an error
        @StorageProp["sessionProp"] public let storage_prop_value: String = "Hello"
        // Using public modifier here will cause an error
        @StorageLink["sessionLink"] public var storage_link_value: String = "Hello"
        // Using public modifier here will cause an error
        @Consume public var consume_value: String

        func build() {
            Column {
                Text("Hello")
                .fontSize(50)
                .fontWeight(FontWeight.Bold)
            }
        }
    }
    ```

    **Correct Example**

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry

    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    let storage = LocalStorage()

    @Entry[storage]
    @Component
    class EntryView {
        @Provide var consume_value: String = "Hello"

        func build() {
            Column {
                ComponentChild()
            }
            .width(100.percent)
        }
    }

    @Component
    class ComponentChild {
        @LocalStorageProp["sessionLocalProp"] let local_prop_value: String = "Hello"
        @LocalStorageLink["sessionLocalLink"] var local_link_value: String = "Hello"
        @StorageProp["sessionProp"] let storage_prop_value: String = "Hello"
        @StorageLink["sessionLink"] var storage_link_value: String = "Hello"
        @Consume var consume_value: String

        func build() {
            Column {
                Text("Hello")
                .fontSize(50)
                .fontWeight(FontWeight.Bold)
            }
        }
    }
    ```

3. When a member variable is modified with both the private access modifier and @Link macro, Cangjie will validate and generate an error.

    **Counter Example**

    ```cangjie
    package ohos_app_cangjie_entry

    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        @State var link_value: String = "Hello"

        func build() {
            Column {
                ComponentChild(link_value: this.link_value)
            }
            .width(100.percent)
        }
    }

    @Component
    class ComponentChild {
        // Using private modifier here will cause an error
        @Link private var link_value: String

        func build() {
            Column {
                Text("Hello")
                .fontSize(50)
                .fontWeight(FontWeight.Bold)
            }
        }
    }
    ```

    **Correct Example**

     <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry

    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        @State var link_value: String = "Hello"

        func build() {
            Column {
                ComponentChild(link_value: this.link_value)
            }
            .width(100.percent)
        }
    }

    @Component
    class ComponentChild {
        @Link var link_value: String

        func build() {
            Column {
                Text("Hello")
                .fontSize(50)
                .fontWeight(FontWeight.Bold)
            }
        }
    }
    ```