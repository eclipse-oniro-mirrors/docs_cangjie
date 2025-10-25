# Transition Animation Overview

Transition animation refers to applying animations to components that are about to appear or disappear. For components that remain visible, [property animation](./cj-attribute-animation-overview.md) should be used instead. The primary purpose of transition animation is to free developers from the cumbersome management of disappearing nodes. If property animation is used for component transitions, developers would need to delete component nodes in the animation end callback. Additionally, since deleted component nodes might reappear before the animation ends, state checks for these nodes must also be added to the end callback.

Transition animations are categorized into basic transitions and advanced templated transitions, including the following types:

- [Appear/Disappear Transition](./cj-enter-exit-transition.md): Implements animation effects for newly added or disappearing controls, serving as a universal basic transition effect.

- [Modal Transition](./cj-modal-transition.md): An animation where the new interface overlays the old one without the old interface disappearing. Examples include dialog boxes, which are typical modal transition animations.

- [Shared Element Transition (One-Shot Effect)](./cj-shared-element-transition.md): A transition effect that matches the position and size of identical or similar elements during interface switching.

- [Page Transition Animation (Not Recommended)](./cj-page-transition-animation.md): A page routing transition method where custom entry and exit animations can be defined in the `pageTransition` function. For better transition effects, it is recommended to use [Modal Transition](./cj-modal-transition.md) instead.

- [Screen Rotation Animation](./cj-rotation-transition-animation.md): Primarily divided into two types: [Layout Switch Screen Rotation Animation](./cj-rotation-transition-animation.md#layout-switch-screen-rotation-animation) and [Opacity Change Screen Rotation Animation](./cj-rotation-transition-animation.md#opacity-change-screen-rotation-animation), designed to achieve smooth transitions during screen orientation changes.