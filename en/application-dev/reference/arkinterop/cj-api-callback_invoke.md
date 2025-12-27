# ohos.callback_invoke (Generic Callback Information)

## class Callback0Argument

```cangjie
public abstract class Callback0Argument <: CallbackObject {}
```

**Description:** Abstract class for callback functions with no parameters.

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException)

```cangjie
public open func invoke(err: ?BusinessException): Unit
```

**Description:** Abstract class constraint requiring implementation of callback methods.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Description |
|:---------|:-----|:---------|:------------|
| err | ?BusinessException  | Yes | Exception information. |

## class Callback1Argument\<A>

```cangjie
public abstract class Callback1Argument<A> <: CallbackObject {}
```

**Description:** Abstract class for callback functions with one parameter.

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException, A)

```cangjie
public open func invoke(err: ?BusinessException, arg: A): Unit
```

**Description:** Abstract class constraint requiring implementation of single-parameter callback methods.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Description |
|:---------|:-----|:---------|:------------|
| err | ?BusinessException  | Yes | Exception information. |
| arg | A  | Yes | Parameter required by the callback function. |

## class Callback1ArgumentWithReturn\<A, B>

```cangjie
public abstract class Callback1ArgumentWithReturn<A, B> <: CallbackObject {}
```

**Description:** Abstract class for callback functions with one parameter and a return value.

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException, A)

```cangjie
public open func invoke(err: ?BusinessException, arg1: A): B
```

**Description:** Abstract class constraint requiring implementation of single-parameter callback methods.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---------|:-----|:---------|:--------------|:------------|
| err | ?BusinessException  | Yes | - | Exception information. |
| arg1 | A | Yes | - | Parameter required by the callback function. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| B | Return value of the callback function. |

## class Callback2Argument\<A, B>

```cangjie
public abstract class Callback2Argument<A, B> <: CallbackObject {}
```

**Description:** Abstract class for callback functions with two parameters.

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException, A, B)

```cangjie
public open func invoke(err: ?BusinessException, arg1: A, arg2: B): Unit
```

**Description:** Abstract class constraint requiring implementation of dual-parameter callback methods.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---------|:-----|:---------|:--------------|:------------|
| err | ?BusinessException  | Yes | - | Exception information. |
| arg1 | A | Yes  | - | First parameter required by the callback function. |
| arg2 | B | Yes  | - | Second parameter required by the callback function. |

## class Callback3ArgumentWithReturn\<A, B, C, D>

```cangjie
public abstract class Callback3ArgumentWithReturn<A, B, C, D> <: CallbackObject {}
```

**Description:** Abstract class for callback functions with three parameters and a return value.

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException, A, B, C)

```cangjie
public open func invoke(err: ?BusinessException, arg1: A, arg2: B, arg3: C): D
```

**Description:** Abstract class constraint requiring implementation of three-parameter callback methods.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---------|:-----|:---------|:--------------|:------------|
| err | ?BusinessException  | Yes | - | Exception information. |
| arg1 | A | Yes  | - | First parameter required by the callback function. |
| arg2 | B | Yes  | - | Second parameter required by the callback function. |
| arg3 | C | Yes  | - | Third parameter required by the callback function. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| D | Return value of the callback function. |

## class CallbackObject

```cangjie
public abstract class CallbackObject {}
```

**Description:** Abstract base class for callback functions.

**Since:** 22

## class CallbackWithReturn\<A>

```cangjie
public abstract class CallbackWithReturn<A> <: CallbackObject {}
```

**Description:** Abstract class for callback functions with a return value.

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException)

```cangjie
public open func invoke(err: ?BusinessException): A
```

**Description:** Abstract class constraint requiring implementation of callback methods.

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Description |
|:---------|:-----|:---------|:------------|
| err | ?BusinessException  | Yes | Exception information. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| A | Return value of the callback function. |

## type Callback\<T>

```cangjie
public type Callback<T> = (arg: T) -> Unit
```

**Description:** Callback function type.
