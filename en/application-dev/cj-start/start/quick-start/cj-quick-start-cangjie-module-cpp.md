# Calling C++ Files within Modules in Cangjie

> **Note:**
>
> To ensure optimal performance, this document uses **DevEco Studio 5.0.2 Release** and **DevEco Studio-Cangjie Plugin 5.0.9.100 Beta1** as examples. Click [here](https://developer.huawei.com/consumer/cn/download/) to obtain the download link for the latest version.

This document explains how to use the DevEco Studio Cangjie plugin to call C++ files within modules from Cangjie code.

## Development Example

1. Create a pure Cangjie "[Cangjie] Empty Ability" project

   ![cangjieTemplate](../../figures/cangjieTemplate.png)

2. Right-click the **entry** folder and select **New -> C/C++ File(Napi)**, as shown below:

   ![cangjiecangjieNewCpp](../../figures/cangjieNewCpp.png)

   This will automatically generate the **entry > src > main > cpp > napi_init.cpp** file.

3. Open the **napi_init.cpp** file and write the C++ code, as shown in the following example:

   ```cpp
   #include <stdint.h>
   #include <stdio.h>

   extern "C" int32_t sum(int32_t a, int32_t b) { return a + b; }

   extern "C" int32_t sub(int32_t a, int32_t b) {
       printf("sub\n");
       return a - b;
   }
   ```

4. Open the **entry > src > main > cangjie > index.cj** file and write the Cangjie code to call the C++ functions, as shown in the following example:

   ```cangjie
      package ohos_app_cangjie_entry
      internal import ohos.base.LengthProp
      internal import ohos.component.Column
      internal import ohos.component.Row
      internal import ohos.component.Text
      internal import ohos.component.CustomView
      internal import ohos.component.CJEntry
      internal import ohos.component.loadNativeView
      internal import ohos.component.FontWeight
      internal import ohos.state_manage.SubscriberManager
      internal import ohos.state_manage.ObservedProperty
      internal import ohos.state_manage.LocalStorage
      import ohos.state_macro_manage.Entry
      import ohos.state_macro_manage.Component
      import ohos.state_macro_manage.State
      import ohos.state_macro_manage.r
      foreign {
          func sum(a: Int32, b: Int32): Int32
          func sub(a: Int32, b: Int32): Int32
      }
      @Entry
      @Component
      class EntryView {
          @State
          var message: String = "1 + 2"
          func build() {
              Row {
                  Column {
                      Text(this.message)
                          .fontSize(50)
                          .fontWeight(FontWeight.Bold)
                          .onClick {
                              evt => unsafe {
                                  this.message = "result: ${sum(1, 2)}"
                              }
                          }
                  }.width(100.percent)
              }.height(100.percent)
          }
      }
      ```

5. Add C++ dependencies in cjpm.toml. Open the **entry > cjpm.toml** file and add the ffi.c configuration as shown below. Synchronize the project after configuration.

   ```toml
   [ffi]
     [ffi.c]
       [ffi.c.entry]
         path = "./libs/${ABI}"
   ```

## Running the Application on a Physical Device or Emulator

### Using a Local Physical Device

1. Connect a physical device running OpenHarmony to the development environment.
2. After successfully connecting the device, navigate to **File > Project Structure > Project > Signing Configs**, check **Support OpenHarmony** and **Automatically generate signature**, click **Sign In** as prompted, wait for the automatic signing to complete, and then click **OK**. The process is illustrated below:

   ![buildSign](../../figures/buildSign.png)

3. Click the ![runButton](../../figures/runButton.png) button in the toolbar at the top-right corner of the editor window to run the application. The result is shown below:

   ![hybridExampleRunning](../../figures/cangjieCppAdd.png)

### Using an Emulator

OpenHarmony applications/services written in Cangjie can run on the emulator (Emulator) provided by DevEco Studio.

1. Create an emulator device of the Phone type and select it from the device list in the top-right corner of DevEco Studio.

2. By default, Cangjie projects are compiled for the **arm64-v8a** architecture. Therefore, when using an **x86 emulator** (when the development environment is **Windows/x86_64** or **macOS/x86_64**), the Cangjie project and C++ files need to be compiled for the x86_64 architecture. In the **build-profile.json5** configuration file of the Cangjie module, add **x86_64** to the values of **cangjieOptions/abiFilters** and **externalNativeOptions/abiFilters**. The specific compilation configuration is as follows:

    ```json
    "buildOption": { // Configuration options used during the build process
      "cangjieOptions": { // Cangjie-related configurations
        "path": "./cjpm.toml", // Path to the cjpm configuration file, providing Cangjie build configurations
        "abiFilters": ["arm64-v8a", "x86_64"] // Custom Cangjie compilation architectures; the default is arm64-v8a
      }
      "externalNativeOptions": {
        "abiFilters":["arm64-v8a", "x86_64"], // Custom C++ compilation architectures; the default is arm64-v8a
        "path": "./src/main/cpp/CMakeLists.txt",
        "arguments": "",
        "cppFlags": "",
      }
    }
    ```

3. Click the ![runButton](../../figures/runButton.png) button in the toolbar at the top-right corner of the editor window to run the application. The result is the same as when using a physical device.