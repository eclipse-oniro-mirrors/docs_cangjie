# ohos.telephony.sim (SIM Card Management)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The SIM card management module defines the CardType and SimState enums for card types and card states. The enums support equality comparison and conversion to strings. The current version does not provide APIs to query SIM card information or change SIM card state.

## Import Module

```cangjie
import kit.TelephonyKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Sample Code Notes](../cj-development-intro.md#cangjie-sample-code-notes).

## enum CardType

```cangjie
public enum CardType {
    | CtNationalRoamingCard
    | CuDualModeCard
    | DualModeCgCard
    | DualModeTelecomLteCard
    | DualModeUgCard
    | SingleModeIsimCard
    | SingleModeRuimCard
    | SingleModeSimCard
    | SingleModeUsimCard
    | UnknownCard
    | ...
}
```

**Description:** Card type.

**Extended Types:**

- [extend CardType <: ToString](#extend-cardtype--tostring)
- [extend CardType <: Equatable\<CardType>](#extend-cardtype--equatablecardtype)

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### CtNationalRoamingCard

```cangjie
CtNationalRoamingCard
```

**Description:** China Telecom internal roaming card.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### CuDualModeCard

```cangjie
CuDualModeCard
```

**Description:** China Unicom dual-mode card.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### DualModeCgCard

```cangjie
DualModeCgCard
```

**Description:** Dual-card mode C+G.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### DualModeTelecomLteCard

```cangjie
DualModeTelecomLteCard
```

**Description:** China Telecom dual-mode LTE card.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### DualModeUgCard

```cangjie
DualModeUgCard
```

**Description:** Dual-mode UG card.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### SingleModeIsimCard

```cangjie
SingleModeIsimCard
```

**Description:** Single-mode ISIM card type.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### SingleModeRuimCard

```cangjie
SingleModeRuimCard
```

**Description:** Single-mode RUIM card.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### SingleModeSimCard

```cangjie
SingleModeSimCard
```

**Description:** Single-mode SIM card.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### SingleModeUsimCard

```cangjie
SingleModeUsimCard
```

**Description:** Single-mode USIM card.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### UnknownCard

```cangjie
UnknownCard
```

**Description:** Unknown type.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

## enum SimState

```cangjie
public enum SimState {
    | SimStateLoaded
    | SimStateLocked
    | SimStateNotPresent
    | SimStateNotReady
    | SimStateReady
    | SimStateUnknown
    | ...
}
```

**Description:** SIM card state.

**Extended Types:**

- [extend SimState <: ToString](#extend-simstate--tostring)
- [extend SimState <: Equatable\<SimState>](#extend-simstate--equatablesimstate)

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### SimStateLoaded

```cangjie
SimStateLoaded
```

**Description:** Indicates that the SIM card is in the loaded state, that is, the SIM card is present and all card files have been loaded.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### SimStateLocked

```cangjie
SimStateLocked
```

**Description:** Indicates that the SIM card is in the locked state, that is, the SIM card is locked by a PIN, PUK, or network lock.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### SimStateNotPresent

```cangjie
SimStateNotPresent
```

**Description:** Indicates that the SIM card is in the not present state, that is, no SIM card is inserted in the card slot.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### SimStateNotReady

```cangjie
SimStateNotReady
```

**Description:** Indicates that the SIM card is in the not ready state, that is, the SIM card is present but cannot work properly.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### SimStateReady

```cangjie
SimStateReady
```

**Description:** Indicates that the SIM card is in the ready state, that is, the SIM card is present and works properly.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### SimStateUnknown

```cangjie
SimStateUnknown
```

**Description:** The SIM card state is unknown, that is, the accurate state cannot be obtained.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

## extend CardType <: Equatable\<CardType>

```cangjie
extend CardType <: Equatable<CardType>
```

**Description:** Extends the CardType type with the Equatable\<CardType> interface to support equality comparison.

**Extended Type:**

- [CardType](#enum-cardtype)

**Extended Interfaces:**

- Equatable\<[CardType](#enum-cardtype)>

### func ==(CardType)

```cangjie
public operator func ==(other: CardType): Bool
```

**Description:** Checks whether two CardType values are equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [CardType](#enum-cardtype) | Yes | - | The CardType object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two CardType values are equal; otherwise, returns false. |

### func !=(CardType)

```cangjie
public operator func !=(other: CardType): Bool
```

**Description:** Checks whether two CardType values are not equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [CardType](#enum-cardtype) | Yes | - | The CardType object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two CardType values are not equal; otherwise, returns false. |

## extend CardType <: ToString

```cangjie
extend CardType <: ToString
```

**Description:** Extends the CardType type with the ToString interface to support string conversion.

**Extended Type:**

- [CardType](#enum-cardtype)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |

## extend SimState <: Equatable\<SimState>

```cangjie
extend SimState <: Equatable<SimState>
```

**Description:** Extends the SimState type with the Equatable\<SimState> interface to support equality comparison.

**Extended Type:**

- [SimState](#enum-simstate)

**Extended Interfaces:**

- Equatable\<[SimState](#enum-simstate)>

### func ==(SimState)

```cangjie
public operator func ==(other: SimState): Bool
```

**Description:** Checks whether two SimState values are equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [SimState](#enum-simstate) | Yes | - | The SimState object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two SimState values are equal; otherwise, returns false. |

### func !=(SimState)

```cangjie
public operator func !=(other: SimState): Bool
```

**Description:** Checks whether two SimState values are not equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [SimState](#enum-simstate) | Yes | - | The SimState object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two SimState values are not equal; otherwise, returns false. |

## extend SimState <: ToString

```cangjie
extend SimState <: ToString
```

**Description:** Extends the SimState type with the ToString interface to support string conversion.

**Extended Type:**

- [SimState](#enum-simstate)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |
