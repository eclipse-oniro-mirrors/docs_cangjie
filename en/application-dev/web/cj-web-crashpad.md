# Using Crashpad to Collect Web Component Crash Information

Web components support using Crashpad to record process crash information. Crashpad is a process crash information handling tool provided by the Chromium kernel. When a process crash occurs due to the use of web components (including the application's main process and web rendering process), Crashpad writes a minidump file in the application's main process sandbox directory. This file is in binary format with a `.dmp` extension, recording the cause of the process crash, thread information, register information, etc. Applications can use this file to analyze web component-related process crash issues.

Usage steps:

1. After a process crash occurs due to the use of web components, corresponding `.dmp` files will be generated in the application's main process sandbox directory. The sandbox path is as follows:

    ```text
    /data/storage/el2/log/crashpad
    ```

2. The application can access this path to obtain the `.dmp` files and then parse them. Specific steps are as follows:

    * Use the `minidump_stackwalk` tool to parse the `.dmp` file, which will provide the corresponding process crash information (crash cause, thread information, register information, etc.). Example (Linux environment):

        ```text
        ./minidump_stackwalk b678e0b5-894b-4794-9ab3-fb5d6dda06a3.dmp > parsed_stacktrace.txt
        ```

        The `minidump_stackwalk` tool is compiled from the Breakpad project source code. For compilation methods, refer to the project repository: [Breakpad Repository](https://chromium.googlesource.com/breakpad/breakpad).

    * View the parsed file. The following example shows partial content:

        ```c
        Crash reason:  SIGSEGV /SEGV_MAPERR    // Indicates the signal causing the crash; in this example, it's a segmentation fault
        Crash address: 0x0
        Process uptime: 12 seconds

        Thread 0 (crashed)                     // Indicates Thread 0 crashed
         0  libweb_engine.so + 0x2e0b340       // Layer 0 call stack; 0x2e0b340 is the SO offset address, which can be used to decompile and analyze the crash source (requires unstripped SO)
             x0 = 0x00000006a5719ff8    x1 = 0x000000019a5a28c0
             x2 = 0x0000000000020441    x3 = 0x00000000000001b6
             x4 = 0x0000000000000018    x5 = 0x0000000000008065
             x6 = 0x0000000000008065    x7 = 0x63ff686067666d60
             x8 = 0x0000000000000000    x9 = 0x5f129cf9e7bf008c
            x10 = 0x0000000000000001   x11 = 0x0000000000000000
            x12 = 0x000000069bfcc6d8   x13 = 0x0000000009a1746e
            x14 = 0x0000000000000000   x15 = 0x0000000000000000
            x16 = 0x0000000690df4850   x17 = 0x000000010c0d47f8
            x18 = 0x0000000000000000   x19 = 0x0000005eea827db8
            x20 = 0x0000005eea827c38   x21 = 0x00000006a56b1000
            x22 = 0x00000006a8b85020   x23 = 0x00000020002103c0
            x24 = 0x00000006a56b8a70   x25 = 0x0000000000000000
            x26 = 0x00000006a8b84e00   x27 = 0x0000000000000001
            x28 = 0x0000000000000000    fp = 0x0000005eea827c10
             lr = 0x000000069fa4b33c    sp = 0x0000005eea827c10
             pc = 0x000000069fa4b340
            Found by: given as instruction pointer in context
         1  libweb_engine.so + 0x2e0b338
             fp = 0x0000005eea827d80    lr = 0x000000069fa48d44
             sp = 0x0000005eea827c20    pc = 0x000000069fa4b33c
            Found by: previous frame's frame pointer
         2  libweb_engine.so + 0x2e08d40
             fp = 0x0000005eea827e50    lr = 0x00000006a385cef8
             sp = 0x0000005eea827d90    pc = 0x000000069fa48d44
            Found by: previous frame's frame pointer
         3  libweb_engine.so + 0x6c1cef4
             fp = 0x0000005eea828260    lr = 0x00000006a0f11298
             sp = 0x0000005eea827e60    pc = 0x00000006a385cef8
         ......
        ```

    * Use the LLVM toolchain to parse the crash source location. Example (Linux environment):

        ```c
        ./llvm-addr2line -Cfpie libweb_engine.so 0x2e0b340
        ```

        The `llvm-addr2line` toolchain is located in the SDK.