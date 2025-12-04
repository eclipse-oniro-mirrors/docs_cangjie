# Overview of Transition Animations

Transition animations refer to animations applied to components that are about to appear or disappear. For components that remain visible, [property animations](./cj-attribute-animation-overview.md) should be used instead. The primary purpose of transition animations is to free developers from the cumbersome management of disappearing nodes. If property animations were used for component transitions, developers would need to delete component nodes in the animation end callback. Additionally, since deleted component nodes might reappear before the animation ends, it would also require adding state checks for nodes in the end callback.

Transition animations are divided into basic transitions and advanced templated transitions, including the following categories:

- [Appear/Disappear Transition](./cj-enter-exit-transition.md): Implements animation effects for newly added or disappearing controls, serving as a universal basic transition effect.

- [Modal Transition](./cj-modal-transition.md): An animation where the new interface overlays the old one without the old interface disappearing. Examples include pop-up dialogs, which are typical modal transition animations.

- [Shared Element Transition (One-Shot Effect)](./cj-shared-element-transition.md): A transition effect that matches the position and size of identical or similar elements during interface switching.

- [Page Transition Animation (Not Recommended)](./cj-page-transition-animation.md): A page routing transition method that allows customizing entry and exit transition effects via the `pageTransition` function. For better transition effects, it is recommended to use [Modal Transition](./cj-modal-transition.md) instead.

- [Screen Rotation Animation](./cj-rotation-transition-animation.md): [Layout Switch Rotation Animation](./cj-rotation-transition-animation.md#布局切换的旋转屏动画), designed to achieve smooth transitions during screen orientation changes.