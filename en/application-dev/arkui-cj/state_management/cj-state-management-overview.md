# State Management Overview

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

To build a dynamic and interactive interface, the concept of "state" must be introduced.

**Figure 1** Demonstration  

![state_manage_overview1](figures/state-mangement-overview1.gif)  

In the above example, user interaction with the application triggers a change in text state, which in turn causes UI rendering to update, changing the UI from "Hello World" to "Hello Cangjie."  

In declarative UI programming frameworks, the UI is the runtime result of the program's state. Developers construct a UI model where the application's runtime states serve as parameters. When these parameters change, the UI, as the output, will correspondingly update. These runtime state changes that lead to UI re-rendering are collectively referred to as the state management mechanism in Cangjie.  

Custom components can have variables, which must be decorated by decorators to become state variables. Changes to state variables will trigger UI re-rendering. Without state variables, the UI can only render during initialization and will not refresh afterward. The diagram below illustrates the relationship between State and View (UI).  

![state_manage_overview2](figures/state-mangement-overview2.png)  

- **View (UI)**: UI rendering refers to mapping the UI descriptions within the `build` method and `@Builder`-decorated methods to the interface.  
- **State**: State refers to the data that drives UI updates. Users change state data by triggering component event methods, and changes in state data cause the UI to re-render.  

Before reading the state management documentation, developers should have a basic understanding of UI paradigm syntax. It is recommended to review the following topics in advance:  
- Basic Syntax Overview  
- Declarative UI Description  
- Custom Components - Creating Custom Components  

## Basic Concepts  

- **State Variable**: A variable decorated by a state decorator. Changes to its value will trigger UI re-rendering. Example: `@State var num: Int32 = 1`, where `@State` is the state decorator and `num` is the state variable.  
- **Regular Variable**: A variable not decorated by a state decorator, typically used for auxiliary calculations. Changes to it will never trigger UI updates. In the example below, `increaseBy` is a regular variable.  
- **Data Source/Sync Source**: The original source of state variables, which can be synchronized across different state data. Usually refers to data passed from a parent component to a child component. In the example below, the data source is `count: 1`.  
- **Named Parameter Mechanism**: The primary method for passing state variables from parent to child components. Example: `CompA(aProp: this.aProp)`.  
- **Initialization from Parent Component**: The parent component uses the named parameter mechanism to pass specific parameters to the child component. The child component's default initialization values will be overwritten if the parent provides values. Example:  

<!-- run -->  

```cangjie  
package ohos_app_cangjie_entry  
import kit.ArkUI.*  
import ohos.arkui.state_macro_manage.*  

@Component  
class MyComponent {  
    @State var count: Int32 = 0  
    private var increaseBy: Int32 = 1  
    func build() {}  
}  
@Entry  
@Component  
class Parent {  
    func build() {  
        Column() {  
            // Initialize from parent component, overriding locally defined defaults  
            MyComponent(count: 1, increaseBy: 2)  
        }  
    }  
}  
```  

- **Child Component Initialization**: State variables from the parent component can be passed to initialize corresponding state variables in the child component. Example as above.  
- **Local Initialization**: Assigning a value at the time of variable declaration serves as the default value. Example: `@State count: Int32 = 0`.  

> **Note:**  
>  
> Current state management features are only supported in the UI main thread and cannot be used in child threads, workers, or task pools.  

## State Management (V1)  

Developers can choose to use State Management V1 for application development.  

### Decorator Overview  

Cangjie State Management V1 provides multiple decorators. By using these decorators, state variables can not only observe changes within a component but also propagate across different component hierarchies, such as parent-child components or cross-component levels, and even observe changes globally. Based on the scope of influence, decorators can be broadly categorized as:  

- **Component-Level State Decorators**: Manage state within a component tree (i.e., the same page), observing changes in variables within the same component or across different component levels.  
- **Application-Level State Decorators**: Manage state across the entire application, observing changes across different pages or even different UIAbilities, providing global state management.  

From the perspective of data transfer and synchronization types, decorators can also be divided into:  

- **Read-only unidirectional transfer**  
- **Mutable bidirectional transfer**  

The diagram below illustrates this classification. For detailed descriptions of specific decorators, refer to [Managing Component-Owned State](./cj-macro-state.md) and [Managing Application-Owned State](./cj-application-state-management-overview.md). Developers can flexibly leverage these capabilities to achieve data-UI synchronization.  

![state_manage_overview3](figures/state-mangement-overview3.png)  

[Managing Component-Owned State](./cj-macro-state.md), i.e., Components-level state management:  

- [@State](./cj-macro-state.md): Variables decorated with `@State` hold the state of their owning component and can serve as data sources for unidirectional or bidirectional synchronization with child components. Changes to their values trigger re-rendering of related components.  
- [@Prop](./cj-macro-prop.md): Variables decorated with `@Prop` can establish unidirectional synchronization with parent components. They are mutable, but modifications do not propagate back to the parent.  
- [@Link](./cj-macro-link.md): Variables decorated with `@Link` can establish bidirectional synchronization with parent components. Changes in child components propagate to the parent's data source, and parent updates propagate to the `@Link`-decorated variable.  
- [@Provide/@Consume](./cj-macro-provide-and-consume.md): Variables decorated with `@Provide/@Consume` enable state synchronization across component hierarchies (multi-level components) without requiring named parameter passing, using aliases or property name binding.  
- [@Observed](./cj-macro-observed-and-publish.md): `@Observed` decorates a class. Classes requiring observation in nested scenarios must be decorated with `@Observed`. Alone, `@Observed` has no effect; it must be used with `@Publish`.  
- [@Publish](./cj-macro-observed-and-publish.md): `@Publish` decorates member variables of classes decorated with `@Observed`, applicable to multi-level nested scenarios. Assignment changes to decorated member variables can be observed, triggering UI updates.  

> **Note:**  
>  
> Only [@Observed/@Publish](./cj-macro-observed-and-publish.md) can observe nested scenarios. Other state variables can only observe the first layer. For details, refer to the "Observing Changes and Behavior" sections in each decorator's documentation.  

[Managing Application-Owned State](./cj-application-state-management-overview.md), i.e., Application-level state management:  

- [AppStorage](./cj-appstorage.md) is a special singleton [LocalStorage](./cj-localstorage.md) object, serving as an application-level database bound to the process. It interacts with components via [@StorageProp](./cj-appstorage.md#StorageProp) and [@StorageLink](./cj-appstorage.md#StorageLink) decorators.  
- AppStorage acts as the "hub" for application state, storing data that interacts with components (UI), such as persistent data [PersistentStorage](./cj-persiststorage.md) and environment variables [Environment](./cj-environment.md). The UI accesses this data through AppStorage's decorators or APIs.  
- The framework also provides LocalStorage, where AppStorage is a specialized singleton. LocalStorage is an in-memory "database" for application state, typically used for page-level state sharing, interacting with the UI via [@LocalStorageProp](./cj-localstorage.md#LocalStorageProp) and [@LocalStorageLink](./cj-localstorage.md#LocalStorageLink) decorators.  

### Other State Management V1 Features  

[@Watch](./cj-macro-watch.md) is used to listen for changes in state variables.