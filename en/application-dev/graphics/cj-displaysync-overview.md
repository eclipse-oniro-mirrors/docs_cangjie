# Introduction to Variable Refresh Rate

With the continuous evolution of device screens, current mainstream devices adopt LTPO screens, which support switching screen refresh rates between multiple levels.

For rapidly changing content such as shooting games and interactive animations, higher display refresh rates result in smoother visuals but correspondingly higher power consumption.

For slowly changing content like game lobbies or clock update animations, where the screen update frequency is lower, using relatively lower display refresh rates won't make users perceive lag, while maintaining lower power consumption.

Based on the variable refresh rate capability of display content, devices equipped with LTPO screens can achieve a balance between performance experience and power consumption.

OpenHarmony supports variable refresh rate capability. Developers can leverage the power-saving benefits of this feature by using variable refresh rate APIs for relevant business development.

## Usage Scenarios

The variable refresh rate capability allows developers to customize frame rates for application services. Common usage scenarios include:

- Configuring frame rate property parameters for attribute animations/display animations for animation rendering. For details, see [Requesting Animation Rendering Frame Rate](./cj-displaysync-animation.md).

## Operation Mechanism

Variable refresh rate provides a basic frame rate configuration and capability for animation components and UI rendering in application development.

After developers set valid expected rendering frame rates, the system collects these requested frame rates, makes decisions, and distributes them. Frequency division is performed on the rendering pipeline to meet developers' expected frame rates as much as possible.

As shown in the diagram above, various UIs (animation components and UI rendering) at the application layer can connect to the frame control system through corresponding variable refresh rate APIs (`expectedFrameRateRange` and `displaySync`). The frame control system collects the expected rendering frame rates set by UIs and participates in the system-wide refresh rate decision-making at the framework layer. The server distributes the decided refresh rate results for rendering frame rates, which are then propagated level by level to various UIs at the application layer. Meanwhile, the hardware layer also completes the refresh rate switching of hardware components based on the system-wide refresh rate decision results.

## Constraints and Limitations

The expected frame rate values set by developers do not represent the final actual effect, as they are subject to system power-performance constraints and hardware limitations of screen refresh rate capabilities.