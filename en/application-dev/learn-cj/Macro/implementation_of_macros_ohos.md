# Implementation of Macros

This chapter introduces the definition and usage of Cangjie macros, which can be categorized into [Non-Attribute Macros](./implementation_of_macros_ohos.md#non-attribute-macros) and [Attribute Macros](./implementation_of_macros_ohos.md#attribute-macros). Additionally, this chapter will cover the behavior when macros are nested.

## Non-Attribute Macros

Non-attribute macros only accept the code to be transformed and do not take additional parameters (attributes). Their definition format is as follows:

```cangjie
import std.ast.*

public macro MacroName(args: Tokens): Tokens {
    ... // Macro body
}
```

The macro invocation format is:

```cangjie
@MacroName(...)
```

Macro calls are enclosed in `()`. The content inside the parentheses can be any valid `Tokens` or empty.

When a macro is applied to a declaration, the parentheses can generally be omitted. Refer to the following examples:

```cangjie
@MacroName func name1() {}       // Before a FuncDecl
@MacroName struct name2 {}       // Before a StructDecl
@MacroName class name3 {}        // Before a ClassDecl
@MacroName var a = 1             // Before a VarDecl
@MacroName enum e {}             // Before a Enum
@MacroName interface i {}        // Before a InterfaceDecl
@MacroName extend e <: i {}      // Before a ExtendDecl
class C {
    @MacroName prop i: Int64 {   // Before a PropDecl
        get() { 0 }
    }
} 
@MacroName @AnotherMacro(input)  // Before a macro call
```

Special notes on the legality of `Tokens` inside parentheses:

- The input must be a sequence of valid `Token`s. Symbols like "#", "`", "\\", etc., when used alone, are not valid Cangjie `Token`s and cannot be used as input values.

- If the input contains unmatched parentheses, they must be escaped using the escape symbol "\\".

- If "@" is intended to be part of the input `Token`, it must be escaped using "\\".

For examples of these special cases, refer to the following:

```cangjie
// Illegal input Tokens
@MacroName(#)    // Not a whole Token
@MacroName(`)    // Not a whole Token
@MacroName(()    // ( and ) not match
@MacroName(\[)   // Escape for unsupported symbol

// Legal input Tokens
@MacroName(#"abc"#)
@MacroName(`class`)
@MacroName([)
@MacroName([])
@MacroName(\()
@MacroName(\@)
```

Macro expansion operates on the Cangjie syntax tree. After expansion, the compiler continues with subsequent compilation steps. Therefore, the following rules must be observed:

- The expanded code must still be valid Cangjie code, and it must not contain package declarations or import statements, as this may cause compilation issues.
- When a macro is applied to a declaration and parentheses are omitted, the input must be a syntactically valid declaration.

Below are some typical examples of macro applications.

- Example 1

  Macro definition file `macro_definition.cj`

  <!-- verify -macro6 -->
  <!-- cfg="--compile-macro" -->

  ```cangjie
  macro package macro_definition

  import std.ast.*

  public macro testDef(input: Tokens): Tokens {
      println("I'm in macro body")
      return input
  }
  ```

  Macro invocation file `macro_call.cj`

  <!-- verify -macro6 -->
  <!-- cfg="--debug-macro" -->

  ```cangjie
  package macro_calling

  import macro_definition.*

  main(): Int64 {
      println("I'm in function body")
      let a: Int64 = @testDef(1 + 2)
      println("a = ${a}")
      return 0
  }
  ```

  The compilation process for the above code can be referred to in [Macro Compilation and Usage](./compiling_error_reporting_and_debugging_ohos.md#macro-compilation-and-usage).

  Print statements are added in the example. The `I'm in macro body` in the macro definition will be output during the compilation of `macro_call.cj`. Meanwhile, the macro invocation point is expanded. For example, compiling the following code:

  ```cangjie
  let a: Int64 = @testDef(1 + 2)
  ```

  The compiler updates the syntax tree at the invocation point with the `Tokens` returned by the macro, resulting in:

  ```cangjie
  let a: Int64 = 1 + 2
  ```

  In other words, the actual code in the executable becomes:

  ```cangjie
  main(): Int64 {
      println("I'm in function body")
      let a: Int64 = 1 + 2
      println("a = ${a}")
      return 0
  }
  ```

  The value of `a` is computed as 3, and when printed, it interpolates to 3. Thus, the program's output is:

  <!-- verify -macro6 -->

  ```text
  I'm in function body
  a = 3
  ```

Now let's look at a more meaningful example of using macros to process functions. The `ModifyFunc` macro adds an `id` parameter to `myFunc` and inserts code before and after `counter++`.

- Example 2

  Macro definition file `macro_definition.cj`

  <!-- verify -macro7 -->
  <!-- cfg="--compile-macro" -->

  ```cangjie
  // file macro_definition.cj
  macro package macro_definition

  import std.ast.*

  public macro ModifyFunc(input: Tokens): Tokens {
      println("I'm in macro body")
      let funcDecl = FuncDecl(input)
      return quote(
          func $(funcDecl.identifier)(id: Int64) {
              println("start ${id}")
              $(funcDecl.block.nodes)
              println("end")
          })
  }
  ```

  Macro invocation file `macro_call.cj`

  <!-- verify -macro7 -->
  <!-- cfg="--debug-macro" -->

  ```cangjie
  package macro_calling

  import macro_definition.*

  var counter = 0

  @ModifyFunc
  func myFunc() {
      counter++
  }

  func exModifyFunc() {
      println("I'm in function body")
      myFunc(123)
      println("myFunc called: ${counter} times")
      return 0
  }

  main(): Int64 {
      exModifyFunc()
  }
  ```

  Similarly, these two code segments are in separate files. First, compile the macro definition file `macro_definition.cj`, then compile the macro invocation `macro_call.cj` to generate the executable.

  In this example, the `ModifyFunc` macro takes a function declaration as input, so parentheses can be omitted:

  ```cangjie
  @ModifyFunc
  func myFunc() {
      counter++
  }
  ```

  After macro expansion, the code becomes:

  ```cangjie
  func myFunc(id: Int64) {
      println("start ${id}")
      counter++
      println("end")
  }
  ```

  `myFunc` is called in `main`, with the actual parameter defined in `main`, forming a valid Cangjie program. The runtime output is:

  <!-- verify -macro7 -->

  ```text
  I'm in function body
  start 123
  end
  myFunc called: 1 times
  ```

## Attribute Macros

Compared to non-attribute macros, attribute macros have an additional `Tokens` parameter, allowing developers to input extra information. For instance, developers might want different expansion strategies in different invocation contexts, which can be achieved by setting flags via this attribute parameter. Additionally, this parameter can pass arbitrary `Tokens`, which can be combined or concatenated with the code being modified by the macro. Here's a simple example:

<!-- run -macro72 -->
<!-- cfg="--compile-macro" -->

```cangjie
macro package define

// Macro definition with attribute
public macro Foo(attrTokens: Tokens, inputTokens: Tokens): Tokens {
    return attrTokens + inputTokens  // Concatenate attrTokens and inputTokens.
}
```

As shown above, an attribute macro has two parameters of type `Tokens`. Inside the macro definition, `attrTokens` and `inputTokens` can be transformed through various operations like combination or concatenation, and the new `Tokens` is returned.

Attribute macros are invoked similarly to non-attribute macros, with the additional `attrTokens` passed via `[]`. The invocation form is:

<!-- run -macro72 -->
<!-- cfg="--debug-macro" -->

```cangjie
import define.Foo

// attribute macro with parentheses
var a: Int64 = @Foo[1+](2+3)

// attribute macro without parentheses
@Foo[public]
struct Data {
    var count: Int64 = 100
}

main() {}
```

- For the `Foo` macro invocation with `2+3` as the parameter, it is concatenated with the attribute `1+` inside `[]`. After expansion, the result is `var a: Int64 = 1+2+3`.
- For the `Foo` macro invocation with `struct Data` as the parameter, it is concatenated with the attribute `public` inside `[]`. After expansion, the result is:

  ```cangjie
  public struct Data {
      var count: Int64 = 100
  }
  ```

Regarding attribute macros, note the following:

- Attribute macros can modify the same AST nodes as non-attribute macros. They can be seen as an enhancement to the parameters that can be passed.

- The legality rules for parameters inside parentheses in attribute macros are the same as those for non-attribute macros.

- Special notes on the legality rules for attribute parameters inside brackets:

    - The input must be a sequence of valid `Token`s. Symbols like "#", "`", "\\", etc., when used alone, are not valid Cangjie `Token`s and cannot be used as input values.

    - If the input contains unmatched square brackets, they must be escaped using "\\".

    - If "@" is intended to be part of the input `Token`, it must be escaped using "\\".

    ```cangjie
    // Illegal attribute Tokens
    @MacroName[#]()    // Not a whole Token
    @MacroName[`]()    // Not a whole Token
    @MacroName[@]()    // Not escape for @
    @MacroName[[]()    // [ and ] not match
    @MacroName[\(]()   // Escape for unsupported symbol

    // Legal attribute Tokens
    @MacroName[#"abc"#]()
    @MacroName[`class`]()
    @MacroName[(]()
    @MacroName[()]()
    @MacroName[\[]()
    @MacroName[\@]()
    ```

- The macro definition and invocation types must match: if a macro has two parameters (attribute macro), `[]` must be used during invocation (content can be empty); if a macro has one parameter (non-attribute macro), `[]` cannot be used.

## Nested Macros

The Cangjie language does not support nested macro definitions but conditionally supports nested macro invocations within macro definitions and invocations.

### Macro Invocations in Macro Definitions

Below is an example of a macro definition containing other macro invocations.

Macro package `pkg1` defines the `getIdent` macro:

<!-- compile -macro8 -->
<!-- cfg="--compile-macro" -->

```cangjie
macro package pkg1

import std.ast.*

public macro getIdent(attr:Tokens, input:Tokens):Tokens {
    return quote(
        let decl = (parseDecl(input) as VarDecl).getOrThrow()
        let name = decl.identifier.value
        let size = name.size - 1
        let $(attr) = Token(TokenKind.IDENTIFIER, name[0..size])
    )
}
```

Macro package `pkg2` defines the `Prop` macro, which nests the `getIdent` macro invocation:

<!-- compile -macro8 -->
<!-- cfg="--debug-macro --compile-macro" -->

```cangjie
macro package pkg2

import std.ast.*
import pkg1.*

public macro Prop(input:Tokens):Tokens {
    let v = parseDecl(input)
    @getIdent[ident](input)
    return quote(
        $(input)
        public prop $(ident): $(decl.declType) {
            get() {
                this.$(v.identifier)
            }
        }
    )
}
```

Macro invocation package `pkg3` calls the `Prop` macro:

<!-- compile -macro8 -->
<!-- cfg="--debug-macro" -->

```cangjie
package pkg3

import pkg2.*
class A {
    @Prop
    private let a_: Int64 = 1
}

main() {
    let b = A()
    println("${b.a}")
}
```

Note: Due to the constraint that macro definitions must be compiled before their invocation points, the compilation order for these three files must be: `pkg1` -> `pkg2` -> `pkg3`. The `Prop` macro definition in `pkg2`:

```cangjie
public macro Prop(input:Tokens):Tokens {
    let v = parseDecl(input)
    @getIdent[ident](input)
    return quote(
        $(input)
        public prop $(ident): $(decl.declType) {
            get() {
                this.$(v.identifier)
            }
        }
    )
}
```

Will first be expanded into the following code before compilation:

```cangjie
public macro Prop(input: Tokens): Tokens {
    let v = parseDecl(input)

    let decl = (parseDecl(input) as VarDecl).getOrThrow()
    let name = decl.identifier.value
    let size = name.size - 1
    let ident = Token(TokenKind.IDENTIFIER, name[0 .. size])

    return quote(
        $(input)
        public prop $(ident): $(decl.declType) {
            get() {
                this.$(v.identifier)
            }
        }
    )
}
```### Nested Macro Invocations within Macro Invocations

A common scenario for nested macros is when macro-decorated code blocks contain macro invocations. A concrete example is as follows:

The `pkg1` package defines the `Foo` and `Bar` macros:

<!-- run -macro9 -->
<!-- cfg="--compile-macro" -->

```cangjie
macro package pkg1

import std.ast.*

public macro Foo(input: Tokens): Tokens {
    return input
}

public macro Bar(input: Tokens): Tokens {
    return input
}
```

The `pkg2` package defines the `addToMul` macro:

<!-- run -macro9 -->
<!-- cfg="--compile-macro" -->

```cangjie
macro package pkg2

import std.ast.*

public macro addToMul(inputTokens: Tokens): Tokens {
    var expr: BinaryExpr = match (parseExpr(inputTokens) as BinaryExpr) {
        case Some(v) => v
        case None => throw Exception()
    }
    var op0: Expr = expr.leftExpr
    var op1: Expr = expr.rightExpr
    return quote(($(op0)) * ($(op1)))
}
```

The `pkg3` package uses the three macros defined above:

<!-- run -macro9 -->
<!-- cfg="--debug-macro" -->

```cangjie
package pkg3

import pkg1.*
import pkg2.*
@Foo
struct Data {
    let a = 2
    let b = @addToMul(2+3)

    @Bar
    public func getA() {
        return a
    }

    public func getB() {
        return b
    }
}

main(): Int64 {
    let data = Data()
    var a = data.getA() // a = 2
    var b = data.getB() // b = 6
    println("a: ${a}, b: ${b}")
    return 0
}
```

As shown in the code above, the `Foo` macro decorates `struct Data`, and within `struct Data`, macro invocations `addToMul` and `Bar` appear. In such nested scenarios, the code transformation rule is: expand the inner macros (`addToMul` and `Bar`) first, then expand the outer macro (`Foo`). Multiple layers of macro nesting are allowed, and the code transformation always proceeds from the innermost to the outermost macros.

Nested macros can appear in both parenthesized and unparenthesized macro invocations, and these can be combined. However, developers must ensure there is no ambiguity and that the macro expansion order is clear:

```cangjie
var a = @foo(@foo1(2 * 3)+@foo2(1 + 3))  // foo1, foo2 have to be defined.

@Foo1 // Foo2 expands first, then Foo1 expands.
@Foo2[attr: struct] // Attribute macro can be used in nested macro.
struct Data{
    @Foo3 @Foo4[123] var a = @bar1(@bar2(2 + 3) + 3)  // bar2, bar1, Foo4, Foo3 expands in order.
    public func getA() {
        return @foo(a + 2)
    }
}
```

### Message Passing Between Nested Macros

This refers to the nesting of macro invocations.

Inner macros can call the library function `assertParentContext` to ensure that the inner macro invocation is nested within a specific outer macro invocation. If the inner macro calls this function without being nested within the given outer macro invocation, the function will throw an error. The library function `InsideParentContext` is also used to check whether an inner macro invocation is nested within a specific outer macro invocation, returning a boolean value. Below is a simple example.

Macro definitions:

<!-- compile.error -macro92 -->
<!-- cfg="--compile-macro" -->

```cangjie
macro package define

public macro Outer(input: Tokens): Tokens {
    return input
}

public macro Inner(input: Tokens): Tokens {
    assertParentContext("Outer")
    return input
}
```

Macro invocations:

<!-- compile.error -macro92 -->
<!-- cfg="--debug-macro" -->

```cangjie
@Outer var a = 0
@Inner var b = 0 // Error, The macro call 'Inner' should with the surround code contains a call 'Outer'.
```

As shown in the code above, the `Inner` macro uses the `assertParentContext` function during definition to check whether it is nested within the `Outer` macro during invocation. In the example, since `Outer` and `Inner` are not nested in the invocation, the compiler reports an error.

Inner macros can also communicate with outer macros by sending key/value pairs. When an inner macro executes, it sends information to the outer macro by calling the standard library function `setItem`. Later, when the outer macro executes, it calls the standard library function `getChildMessages` to receive the information sent by each inner macro (a set of key/value pair mappings). Below is a simple example.

Macro definitions:

<!-- run -macro10 -->
<!-- cfg="--compile-macro" -->

```cangjie
macro package define

import std.ast.*

public macro Outer(input: Tokens): Tokens {
    let messages = getChildMessages("Inner")

    let getTotalFunc = quote(public func getCnt() {
                       )
    for (m in messages) {
        let identName = m.getString("identifierName")
        // let value = m.getString("key")            // Receive multiple messages
        getTotalFunc.append(Token(TokenKind.IDENTIFIER, identName))
        getTotalFunc.append(quote(+))
    }
    getTotalFunc.append(quote(0))
    getTotalFunc.append(quote(}))
    let funcDecl = parseDecl(getTotalFunc)

    let decl = (parseDecl(input) as ClassDecl).getOrThrow()
    decl.body.decls.add(funcDecl)
    return decl.toTokens()

}

public macro Inner(input: Tokens): Tokens {
    assertParentContext("Outer")
    let decl = parseDecl(input)
    setItem("identifierName", decl.identifier.value)
    // setItem("key", "value")                      // Multiple messages can be sent via different keys
    return input
}
```

Macro invocations:

<!-- run -macro10 -->
<!-- cfg="--debug-macro" -->

```cangjie
import define.*

@Outer
class Demo {
    @Inner var state = 1
    @Inner var cnt = 42
}

main(): Int64 {
    let d = Demo()
    println("${d.getCnt()}")
    return 0
}
```

In the code above, `Outer` receives the variable names sent by the two `Inner` macros and automatically adds the following content to the class:

```cangjie
public func getCnt() {
    state + cnt + 0
}
```

The specific process is as follows: the inner macro `Inner` sends information to the outer macro via `setItem`; the `Outer` macro receives a set of message objects (multiple `Inner` invocations can occur within `Outer`) via the `getChildMessages` function; finally, the corresponding values are retrieved using the `getString` function of the message objects.