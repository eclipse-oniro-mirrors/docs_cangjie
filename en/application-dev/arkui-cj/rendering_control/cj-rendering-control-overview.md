# Overview of Rendering Control

ArkUI constructs corresponding UI through declarative UI description statements in the [custom component](../paradigm/cj-create-custom-components.md)'s build() function and [@Builder macro](../paradigm/cj-macro-builder.md). In declarative description statements, developers can not only use system components but also employ rendering control statements to assist in UI construction. These rendering control statements include:
- Conditional rendering statements that control component visibility
- Loop rendering statements that quickly generate components based on array data
- Data lazy loading statements for large data volume scenarios
- Component rendering statements for hybrid development patterns.