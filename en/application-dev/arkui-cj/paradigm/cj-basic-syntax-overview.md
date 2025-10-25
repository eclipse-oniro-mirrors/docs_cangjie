# Overview of Basic Syntax

After gaining a preliminary understanding of the Cangjie language, let's illustrate its fundamental components through a concrete example. As shown in the figure below, when a developer clicks a button, the text content changes from "Hello World" to "Hello Cangjie."

> **Note:**  
>
> Custom variables must not duplicate the names of basic common properties/events.  

- **Macros**: Used to modify classes, structures, methods, and variables, assigning them special meanings. For example, in the above example, `@Entry`, `@Component`, and `@State` are all macros. `@Component` denotes a custom component, `@Entry` indicates that the custom component is the entry component, and `@State` represents a state variable within the component. Changes to state variables trigger UI refreshes.  

- **UI Description**: Describes the structure of the UI in a declarative manner, such as the code block within the `build()` method.  

- **Custom Components**: Reusable UI units that can combine other components, such as the `class EntryView` decorated with `@Component` in the example above.  

- **System Components**: Default built-in basic and container components in the ArkUI framework, which developers can directly invoke, such as `Column` and `Button` in the example.  

- **Property Methods**: Components can configure multiple properties through chained calls, such as `fontSize()`, `width()`, `height()`, and `backgroundColor()`.  

- **Event Methods**: Components can set response logic for multiple events through chained calls, such as `onClick()` following `Button`.  

In addition, Cangjie extends various syntax paradigms to make development more convenient:  

- **@Builder/@BuilderParam**: Special methods for encapsulating UI descriptions, enabling fine-grained encapsulation and reuse of UI descriptions.