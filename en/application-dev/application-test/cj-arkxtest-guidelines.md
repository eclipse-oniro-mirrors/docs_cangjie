# Automated Testing Framework Usage Guide

## Overview

The Cangjie Automated Testing Framework consists of two components: the Cangjie OpenHarmony Unit Testing Framework and UiTest.

The Cangjie OpenHarmony Unit Testing Framework is implemented based on the std.unittest library native to the Cangjie language, providing fundamental capabilities for writing unit test cases, executing them, and generating test reports. Building upon std.unittest, TestRunner has been adapted for the OH platform, enabling its use within applications.

UiTest offers capabilities for locating and manipulating UI components. By invoking UiTest APIs, users can write test scripts to achieve UI automation testing. The UiTest framework also provides auxiliary testing functionalities via hdc shell commands, including screen capture, control tree retrieval, user operation recording, and UI simulation injection.

This guide introduces the main features, implementation principles, environment setup, and methods for writing and executing test scripts in the Cangjie Automated Testing Framework.

## Implementation Principles

The testing framework is divided into a unit testing framework and a UI testing framework.

The unit testing framework serves as the foundational layer, providing basic capabilities for test case identification, scheduling, execution, and result aggregation.

The UI testing framework primarily exposes UiTest APIs for developers to invoke in corresponding test scenarios, while its script execution still relies on the unit testing framework.

### Unit Testing Framework

- Main Features of Unit Testing Framework

  ![UnitTest.jpg](figures/UnitTest.jpg)

- Basic Script Flow

    - Locate the corresponding TestRunner.registerCreator based on the `-s unittest` parameter, instantiate TestRunner, and sequentially execute `onPrepare` and `onRun`.
    - During `onRun`, parse startup parameters to identify which test cases to execute, along with timeout and other information.
    - Initialize the test suite using the Cangjie kernel unittest and execute it. Test results are saved in XML format on the device at `/data/app/el1/100/base/${bundleName}/tests`.
    - After all specified test suites are executed, read the XML test report and print it to the terminal and hilog logs.

### UI Testing Framework

- Main Features of UI Testing Framework

![Uitest.png](figures/Uitest.png)

## Writing and Executing Tests in Cangjie

### Environment Setup

Download and configure DevEco Studio as described on its [official website](https://developer.huawei.com/consumer/en/deveco-studio/#download).

### Creating and Writing Test Scripts

#### Creating Test Scripts

<!--RP1-->
In DevEco Studio, create a new application development project. The `ohosTest` directory is where test scripts reside.
<!--RP1End-->

#### Writing Unit Test Scripts

This section describes the capabilities supported by the unit testing framework and how to use them.

A unit test script must include the following basic elements:

1. Import dependencies to use the required testing interfaces.
2. Test code logic, such as interface invocations.
3. Assertion interface calls to set checkpoints in the test code. Without checkpoints, it cannot be considered a complete test script.

    The following example demonstrates launching a test page and verifying whether the currently displayed page matches the expected page.

    <!-- compile -->

    ```cangjie
    //example_test.cj
    import kit.TestKit.*
    import kit.AbilityKit.*
    import std.unittest.*
    import std.unittest.common.*
    import std.unittest.testmacro.*

    @Test
    class TestExample00 {
        @TestCase
        func testUiExample(): Unit {
            let delegator = AbilityDelegatorRegistry.getAbilityDelegator()
            let bundleName = AbilityDelegatorRegistry
                .getArguments()
                .bundleName
            Hilog.info(1, "info", "uitest: TestUiExample begin")
            //start tested ability
            let want = Want(bundleName: bundleName, abilityName: 'EntryAbility')
            delegator.startAbility(want)
            sleep(Duration.second * 5)
            //check top display ability
            let ability = delegator.getCurrentTopAbility()
            Hilog.info(1, "info", "get top ability")
            @Expect(ability.context.abilityInfo.name, 'EntryAbility')
        }
    }
    ```

#### Writing UI Test Scripts

This section introduces the capabilities supported by the UI testing framework and how to use its APIs.

UI tests build upon unit tests, extending unit test scripts with UiTest interfaces. Refer to the [API documentation](../reference/TestKit/cj-apis-ui_test.md) for details.

The following example extends the unit test script above to implement a scenario: clicking a button on the launched application page and verifying whether the page changes as expected.

1. Write `index.cj` page code as the demo under test.

    <!-- compile -->

    ```cangjie
    import ohos.base.*
    import ohos.arkui.component.*
    import ohos.arkui.state_management.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        @State
        var message: String = "Hello World"

        func build() {
            Row {
                Column {
                    Text(this.message)
                        .fontSize(50)
                        .fontWeight(FontWeight.Bold)
                    Text("Next")
                        .fontSize(50)
                        .margin(top: 20)
                        .fontWeight(FontWeight.Bold)
                    Text("after click")
                        .fontSize(50)
                        .margin(top: 20)
                        .fontWeight(FontWeight.Bold)
                }.width(100.percent)
            }.height(100.percent)
        }
    }
    ```

2. Write the test code in the `example_test.cj` file under `ohosTest > cangjie`.

    <!-- compile -->

    ```cangjie
    import kit.TestKit.*
    import kit.AbilityKit.*
    import std.unittest.*
    import std.unittest.common.*
    import std.unittest.testmacro.*

    @Test
    class TestExample00 {
        @TestCase
        func testUiExample(): Unit {
            let delegator = AbilityDelegatorRegistry.getAbilityDelegator()
            let bundleName = AbilityDelegatorRegistry
                .getArguments()
                .bundleName
            Hilog.info(1, "info", "uitest: TestUiExample begin")
            //start tested ability
            let want = Want(bundleName: bundleName, abilityName: 'EntryAbility')
            delegator
                .startAbility(want)
                .get()
            sleep(Duration.second * 5)
            //check top display ability
            let ability = delegator.getCurrentTopAbility()
            Hilog.info(1, "info", "get top ability")
            @Expect(ability.context.abilityInfo.name, 'EntryAbility')
            // ui test code
            // init driver
            let driver = Driver.create()
            driver.delayMs(1000)
            let button = driver.findComponent(On().text('Next'))
            //click button
            button.click()
            driver.delayMs(1000)
            //check text
            driver.assertComponentExist(On().text('after click'))
            driver.pressBack()
        }
    }
    ```

### Executing Test Scripts

#### Executing in DevEco Studio

Script execution requires a connected hardware device. Click the button to execute all test cases defined in the test suite (testClass methods).

![Execute.png](figures/Execute.png)

**Viewing Test Results**

After execution, test results can be viewed directly in DevEco Studio, as shown in the example below.

![TestResult.png](figures/Test_Result.png)

#### Executing via CMD

Script execution requires a connected hardware device. Install the test package on the device and execute the `aa` command in a CMD window to run the tests.

> **Note:**
>
> Using CMD requires configuring hdc-related environment variables.

**aa test Command Parameters**

| Full Parameter | Short Parameter | Description | Example |
| ------------- | ------ | ------- | ------------ |
| --bundleName  | -b   | Application bundle name.  | -b com.test.example    |
| --packageName | -p  | Application module name (for FA model applications). | -p com.test.example.entry         |
| --moduleName  | -m   | Application module name (for Stage model applications).        | -m entry     |
| NA    | -s  | Specific parameters passed as `<key, value>` pairs. | -s unittest OpenHarmonyTestRunner |

The framework currently supports multiple test execution modes, triggered by the key-value pairs passed after the `-s` parameter, as shown below.

| Parameter Name | Description | Values | Example |
| ------------ | ------------------- | ------------- | -------- |
| unittest| OpenHarmonyTestRunner object used for test execution.| OpenHarmonyTestRunner or custom runner name | -s unittest OpenHarmonyTestRunner   |
| class |Specifies test suites or test cases to execute.| {testClassName}#{testCaseName},{testClassName}  | -s class attributeTest#testAttributeIt|

Currently, only test suite (TestClass) granularity is supported; individual test case (TestCase) granularity is not supported.

**Executing test Commands in CMD**

> **Note:**
>
> Parameters and commands are based on the Stage model.

Example 1: Execute all test cases.

```shell
hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner
```

Example 2: Execute specified TestClass test suites (multiple suites separated by commas).

```shell
  hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s class s1,s2
```

**Viewing Test Results**

- After CMD execution completes, the following log information will be printed.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<testsuite name="default.TestExample00" tests="1" failures="0" errors="0" skipped="0" time="7.990736" timestamp="2025-05-22T10:42:47.544499427+08:00">
        <testcase name="testUiExample" classname="default.TestExample00" assertions="1" time="7.989778"/>
</testsuite>
```

| Log Field | Description |
| -----------| --------------|
| testsuite.name | Name of the executed test suite.|
| testsuite.tests    | Total number of test cases in the suite. |
| testsuite.failures | Number of failed test cases. |
| testsuite.errors | Number of test cases with errors. |
| testsuite.skipped | Number of skipped test cases. |
| testsuite.time | Test suite execution duration (seconds). |
| testsuite.timestamp | Test suite execution start timestamp. |
| testcase.name | Test case name. |
| testcase.classname | Name of the test suite to which the case belongs. |
| testcase.assertions | Number of actual assertions in the case. |
| testcase.time | Test case execution duration (seconds). |

> **Note:**
>
> In breakOnError mode, when a test case encounters an error, check the Ignore and interruption descriptions.

## Testing via Shell Commands

During development, if quick screen capture, screen recording, UI simulation injection, or control tree retrieval is needed, shell commands can be used for more convenient testing.

> **Note:**
>
> Using CMD requires configuring hdc-related environment variables.

**Command List**

| Command  | Parameters |Description |
|-------|-------------|-------|
| help   | help|  Displays supported commands in uitest.  |
| screenCap       |[-p] | Captures the screen. Optional.<br>Specifies the storage path and filename (only under `/data/local/tmp/`).<br>Default path: `/data/local/tmp`, filename: timestamp + .png. |
| dumpLayout      |[-p] \<-i \| -a>|Retrieves the control tree during daemon runtime.<br> **-p** : Specifies storage path and filename (only under `/data/local/tmp/`). Default: `/data/local/tmp`, filename: timestamp + .json.<br> **-i** : Does not filter invisible controls or merge windows.<br> **-a** : Saves BackgroundColor, Content, FontColor, FontSize, and extraAttrs attributes.<br> **Default** : Does not save these attributes.<br> **-a and -i** cannot be used together. |
| uiRecord        | uiRecord \<record \| read>|Records UI operations.  <br> **record** : Starts recording; saves operations to `/data/local/tmp/record.csv`. Use Ctrl+C to stop.<br> **read** : Reads and prints recorded data.<br>Refer to [User Recording Operations](#user-recording-operations) for parameter details.|
| uiInput| \<help \| click \| doubleClick \| longClick \| fling \| swipe \| drag \| dircFling \| inputText \| keyEvent>| Injects UI simulation operations.<br>Refer to [Injecting UI Simulation Operations](#injecting-ui-simulation-operations) for details.   |
| --version | --version|Retrieves the current tool version.   |
| start-daemon|start-daemon| Starts the uitest daemon process. |

### Screen Capture Example

```bash
# Default path: /data/local/tmp, filename: timestamp + .png.
hdc shell uitest screenCap
# Specifies path and filename (under /data/local/tmp/).
hdc shell uitest screenCap -p /data/local/tmp/1.png
```

### Control Tree Retrieval Example

```bash
hdc shell uitest dumpLayout -p /data/local/tmp/1.json
```

### User Recording Operations

> **Note:**
>
> During recording, wait for the current operation's recognition result to appear in the command line before proceeding.

```bash
# Records operations to /data/local/tmp/record.csv. Use Ctrl+C to stop.
hdc shell uitest uiRecord record
# Reads and prints recorded data.
hdc shell uitest uiRecord read
```

Example record data fields and their meanings (for reference):

```text
{
  "ABILITY": "com.ohos.launcher.MainAbility", // Foreground application interface
  "BUNDLE": "com.ohos.launcher", // Application under operation
  "CENTER_X": "", // Reserved field (unused)
  "CENTER_Y": "", // Reserved field (unused)
  "EVENT_TYPE": "pointer", //
  "LENGTH": "0", // Total step length
  "OP_TYPE": "click", // Event type (supports click, double-click, long-press, drag, swipe, fling)
  "VELO": "0.000000", // Release velocity
  "direction.X": "0.000000",// Total X-axis movement
  "direction.Y": "0.000000", // Total Y-axis movement
  "duration": 33885000.0, // Gesture operation duration
  "fingerList": [{
    "LENGTH": "0", // Total step length
    "MAX_VEL": "40000", // Maximum velocity
    "VELO": "0.000000", // Release velocity
    "W1_BOUNDS": "{"bottom":361,"left":37,"right":118,"top":280}", // Start control bounds
    "W1_HIER": "ROOT,3,0,0,0,0,0,0,0,0,5,0,0,0,0,0,0,0", // Start control hierarchy
    "W1_ID": "", // Start control ID
    "W1_Text": "", // Start control text
    "W1_Type": "Image", // Start control type
    "W2_BOUNDS": "{"bottom":361,"left":37,"right":118,"top":280}", // End control bounds
    "W2_HIER": "ROOT,3,0,0,0,0,0,0,0,0,5,0,0,0,0,0,0,0", // End control hierarchy
    "W2_ID": "", // End control ID
    "W2_Text": "", // End control text
    "W2_Type": "Image", // End control type
    "X2_POSI": "47", // End X position
    "X_POSI": "47", // Start X position
    "Y2_POSI": "301", // End Y position
    "Y_POSI": "301", // Start Y position
    "direction.X": "0.000000", // X-axis movement
    "direction.Y": "0.000000" // Y-axis movement
  }],
  "fingerNumber": "1" // Number of fingers
}
```

### Injecting UI Simulation Operations

| Command   | Required | Description    |
|------|------|-----------------|
| help   | Yes    | Displays help for uiInput commands. |
| click   | Yes    | Simulates a single click.      |
| doubleClick   | Yes    | Simulates a double click.      |
| longClick   | Yes    | Simulates a long press.     |
| fling   | Yes    | Simulates a fast swipe.   |
| swipe   | Yes    | Simulates a slow swipe.     |
| drag   | Yes    | Simulates a drag operation.     |
| dircFling   | Yes    | Simulates a directional swipe.     |
| inputText   | Yes    | Simulates text input into a text field.     |
| keyEvent   | Yes    | Simulates physical key events (e.g., keyboard, power button, back, home) and key combinations.     |

#### uiInput click/doubleClick/longClick Example

| Parameter    | Required | Description   |
|---------|------|-----------------|
| point_x | Yes      | X-coordinate of the click. |
| point_y | Yes       | Y-coordinate of the click. |

```shell
# Single click.
hdc shell uitest uiInput click 100 100

# Double click.
hdc shell uitest uiInput doubleClick 100 100

# Long press.
hdc shell uitest uiInput longClick 100 100
```

#### uiInput fling Example

| Parameter  | Required   | Description      |
|------|------------------|-----------------|
| from_x   | Yes  | Starting X-coordinate. |
| from_y   | Yes    | Starting Y-coordinate. |
| to_x   | Yes   | Ending X-coordinate. |
| to_y   | Yes   | Ending Y-coordinate. |
| swipeVelocityPps_   | No      | Swipe speed (px/s, range: 200-40000).<br> Default: 600. |
| stepLength## Frequently Asked Questions

### Common Issues in UI Test Cases

**1. Error log shows "Get windows failed/GetRootByWindow failed" message**

**Issue Description**  

The UI test case execution failed, and the hilog log contains the error message "Get windows failed/GetRootByWindow failed."

**Possible Causes**  

The system ArkUI switch is not enabled, preventing the generation of the control tree information for the tested interface.

**Solution**  

Execute the following command and restart the device before running the test case again.

```shell
hdc shell param set persist.ace.testmode.enabled 1
```

**2. Error log shows "uitest-api does not allow calling concurrently" message**

**Issue Description**  

The UI test case execution failed, and the hilog log contains the error message "uitest-api does not allow calling concurrently."

**Possible Causes**  

1. The test case involves multi-threaded concurrent calls to UITest-related APIs, which are not supported for concurrent invocation.  
2. The test environment has multiple processes concurrently executing UITest cases, leading to multiple UITest processes being launched. The framework does not support multi-process calls.  

**Solution**  

1. Review the test case implementation to avoid multi-threaded concurrent calls to UITest-related APIs.  
2. Check the test environment to prevent multiple processes from executing UITest-related cases simultaneously.  

**3. Error log shows "does not exist on current UI! Check if the UI has changed after you got the widget object" message**

**Issue Description**  

The UI test case execution failed, and the hilog log contains the error message "does not exist on current UI! Check if the UI has changed after you got the widget object."

**Possible Causes**  

After the test code locates the target control, the device interface changes, causing the located control to be lost and preventing further simulated operations.  

**Solution**  

Re-execute the UI test case.