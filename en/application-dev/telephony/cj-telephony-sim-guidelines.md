# Using SIM Card Type and State Enums

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Overview

Since 26.1.0, ohos.telephony.sim provides CardType and SimState to represent SIM card types and states. Both enums support equality comparison, inequality comparison, and conversion to strings with toString.

The current module only defines enums. It does not provide APIs to read card types, read SIM card states, or change SIM card states. Creating an enum value neither queries the device nor changes its SIM card.

## Basic Concepts

CardType represents a card type. For example, SingleModeSimCard represents a SIM card, SingleModeUsimCard represents a USIM card, and UnknownCard represents an unknown type. For all members, see [CardType](../reference/TelephonyKit/cj-apis-telephony-sim.md#enum-cardtype).

SimState represents a SIM card state:

| Member | Meaning |
| :--- | :--- |
| SimStateUnknown | Unknown state. |
| SimStateNotPresent | No SIM card is present. |
| SimStateLocked | The SIM card is locked. |
| SimStateNotReady | The SIM card is not ready. |
| SimStateReady | The SIM card is ready. |
| SimStateLoaded | SIM card data has been loaded. |

A ready SIM card does not necessarily mean the device is registered with a cellular network. To query registration state, see [Obtaining Cellular Network Information](cj-telephony-network-guidelines.md).

## Development Steps

1. Import CardType and SimState from TelephonyKit. Comparing enum values and converting them to strings do not require a permission.
2. Use == or != to compare values, or match to select logic for each state. Keep a wildcard branch because these enums allow future extensions.
3. Use toString for logging or convert the state to application display text. Do not use log strings to identify a card type or state.

## Sample Code

This example manually creates a USIM card type value and a ready state value. It demonstrates enum usage and does not read the actual SIM card state. Add the functions to a Cangjie project and call useSimEnums.

```cangjie
import kit.TelephonyKit.{CardType, SimState}
import kit.PerformanceAnalysisKit.Hilog

func describeSimState(state: SimState): String {
    match (state) {
        case SimState.SimStateUnknown => return "Unknown"
        case SimState.SimStateNotPresent => return "Not present"
        case SimState.SimStateLocked => return "Locked"
        case SimState.SimStateNotReady => return "Not ready"
        case SimState.SimStateReady => return "Ready"
        case SimState.SimStateLoaded => return "Loaded"
        case _ => return "Other state"
    }
}

func useSimEnums(): Unit {
    let cardType = CardType.SingleModeUsimCard
    let state = SimState.SimStateReady
    if (cardType == CardType.SingleModeUsimCard && state != SimState.SimStateNotPresent) {
        Hilog.info(0, "TelephonyExample", "Card: ${cardType.toString()}, state: ${describeSimState(state)}", [])
    }
}
```

For all enum members, operators, and version information, see [ohos.telephony.sim](../reference/TelephonyKit/cj-apis-telephony-sim.md).
