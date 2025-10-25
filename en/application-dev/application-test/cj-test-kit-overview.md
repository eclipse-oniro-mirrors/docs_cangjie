# Introduction to Test Kit  

Test Kit provides developers with an automated testing framework that supports both unit testing and UI testing capabilities. It enables the creation of unit and UI automated test scripts for the Cangjie language, allowing developers to verify the implementation effects of corresponding features through test results.  

**Unit Testing Capabilities:**  

The framework offers fundamental interfaces and execution mechanisms for automated testing, with the following key features:  

- Provides interfaces for defining automated test cases, including test suite definition and test case definition.  
- Offers assertion interfaces for automated test cases, supporting multiple assertion methods and enabling flexible usage in automated scripts.  
- Includes interfaces for executing setup/teardown actions, supporting execution at both the test suite and test case levels.  
- Supports multiple test execution modes, such as selective execution of specified test cases, random execution, and stress testing.  

**UI Testing Capabilities:**  

The framework provides UI automated testing capabilities, with script execution built upon the unit testing framework. Key features include:  

- Provides control lookup interfaces, supporting multiple methods such as searching by control attributes or relative positions.  
- Offers simulated UI operation interfaces, supporting various actions like clicking, double-clicking, swiping, and pinch-to-zoom, as well as simulating input from peripherals such as mice and keyboards.  
- Includes simulated window operation interfaces, enabling actions like resizing and moving windows.  
- Supports shell command-based UI operations, such as clicking, double-clicking, and swiping.  
- Provides the ability to monitor system dialogs/toasts and retrieve notification text.  

For detailed usage instructions, please refer to the [Automated Testing Framework Guide](./cj-arkxtest-guidelines.md).