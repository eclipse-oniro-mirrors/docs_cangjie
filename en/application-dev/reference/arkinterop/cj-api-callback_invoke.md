# ohos.callback_invoke (Generic Callback Information)

## class Callback0Argument

```cangjie
public abstract class Callback0Argument <: CallbackObject {}
```

**Description:** Abstract class for callback functions without parameters.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException)

```cangjie
public open func invoke(err: ?BusinessException): Unit
```

**Description:** Abstract class constraint requiring implementation of callback methods.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Description |
|:----|:---|:---|:------|
| err | ?BusinessException  | Yes | Exception information. |

## class Callback1Argument

```cangjie
public abstract class Callback1Argument<A> <: CallbackObject {}
```

**Description:** Abstract class for callback functions with one parameter.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException, A)

```cangjie
public open func invoke(err: ?BusinessException, arg: A): Unit
```

**Description:** Abstract class constraint requiring implementation of single-parameter callback methods.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Description |
|:---|:---|:---|:-----------|
| err | ?BusinessException  | Yes | Exception information. |
| arg | A  | Yes | Parameter required by the callback function. |

## class Callback1ArgumentWithReturn

```cangjie
public abstract class Callback1ArgumentWithReturn<A, B> <: CallbackObject {}
```

**Description:** Abstract class for callback functions with one parameter and a return value.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException, A)

```cangjie
public open func invoke(err: ?BusinessException, arg1: A): B
```

**Description:** Abstract class constraint requiring implementation of single-parameter callback methods.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:-----------|
| err | ?BusinessException  | Yes | - | Exception information. |
| arg1 | A | Yes | - | Parameter required by the callback function. |

**Return Value:**

| Type | Description |
|:----|:---------|
| B | Return value of the callback function. |

## class Callback2Argument

```cangjie
public abstract class Callback2Argument<A, B> <: CallbackObject {}
```

**Description:** Abstract class for callback functions with two parameters.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException, A, B)

```cangjie
public open func invoke(err: ?BusinessException, arg1: A, arg2: B): Unit
```

**Description:** Abstract class constraint requiring implementation of dual-parameter callback methods.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:--------------|
| err | ?BusinessException  | Yes | - | Exception information. |
| arg1 | A | Yes | - | First parameter required by the callback function. |
| arg2 | B | Yes | - | Second parameter required by the callback function. |

## class Callback3ArgumentWithReturn

```cangjie
public abstract class Callback3ArgumentWithReturn<A, B, C, D> <: CallbackObject {}
```

**Description:** Abstract class for callback functions with three parameters and a return value.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException, A, B, C)

```cangjie
public open func invoke(err: ?BusinessException, arg1: A, arg2: B, arg3: C): D
```

**Description:** Abstract class constraint requiring implementation of three-parameter callback methods.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:--------------|
| err | ?BusinessException  | Yes | - | Exception information. |
| arg1 | A | Yes | - | First parameter required by the callback function. |
| arg2 | B | Yes | - | Second parameter required by the callback function. |
| arg3 | C | Yes | - | Third parameter required by the callback function. |

**Return Value:**

| Type | Description |
|:----|:----------|
| D | Return value of the callback function. |

## class CallbackObject

```cangjie
public abstract class CallbackObject {}
```

**Description:** Abstract base class for callback functions.

**System Capability:** SystemCapability.Base

**Since:** 22

## class CallbackWithReturn

```cangjie
public abstract class CallbackWithReturn<A> <: CallbackObject {}
```

**Description:** Abstract class for callback functions with a return value.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parent Type:**

- [CallbackObject](#class-callbackobject)

### func invoke(?BusinessException)

```cangjie
public open func invoke(err: ?BusinessException): A
```

**Description:** Abstract class constraint requiring implementation of callback methods.

**System Capability:** SystemCapability.Base

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Description |
|:----|:---|:---|:------|
| err | ?BusinessException  | Yes | Exception information. |

**Return Value:**

| Type | Description |
|:----|:----------|
| A | Return value of the callback function. |

## type Callback

```cangjie
public type Callback<T>=(T) -> Unit
```

**Description:** Callback function type.

**System Capability:** SystemCapability.Base

**Since:** 22