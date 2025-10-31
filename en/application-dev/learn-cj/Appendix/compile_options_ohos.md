# `cjc` Compilation Options

This chapter introduces commonly used `cjc` compilation options. If an option is also applicable to `cjc-frontend`, it will be marked with a <sup>[frontend]</sup> superscript; if the behavior differs between `cjc-frontend` and `cjc`, additional explanations will be provided.

- Options starting with two hyphens are long options, such as `--xxxx`.  
  If a long option has an optional parameter, the option and parameter must be connected with an equals sign, e.g., `--xxxx=<value>`.  
  If a long option has a required parameter, the option and parameter can be separated by either a space or an equals sign, e.g., `--xxxx <value>` is equivalent to `--xxxx=<value>`.

- Options starting with one hyphen are short options, such as `-x`.  
  For short options, if they are followed by a parameter, the option and parameter can be separated by a space or not, e.g., `-x <value>` is equivalent to `-x<value>`.

## Basic Options

### `--output-type=[exe|staticlib|dylib]` <sup>[frontend]</sup>

Specifies the type of output file. In `exe` mode, an executable file is generated; in `staticlib` mode, a static library file (`.a` file) is generated; in `dylib` mode, a dynamic library file is generated (`.so` on Linux, `.dll` on Windows, and `.dylib` on macOS). `cjc` defaults to `exe` mode.

In addition to compiling `.cj` files into executable files, they can also be compiled into static or dynamic link libraries. For example:

```shell
$ cjc tool.cj --output-type=dylib
```

This compiles `tool.cj` into a dynamic link library. On Linux, `cjc` generates a dynamic link library file named `libtool.so`.

**Note:** If a dynamic library file is linked when compiling an executable program, both `--dy-std` and `--dy-libs` options must be specified. For details, refer to the [`--dy-std` option description](#--dy-std).

<sup>[frontend]</sup> In `cjc-frontend`, the compilation process stops at `LLVM IR`, so the output is always a `.bc` file. However, different `--output-type` values still affect the frontend compilation strategy.

### `--package`, `-p` <sup>[frontend]</sup>

Compiles a package. When using this option, a directory must be specified as input, and the source files in the directory must belong to the same package.

For example, given the file `log/printer.cj`:

<!-- compile -p -->
<!-- cfg="-p log --output-type=staticlib" -->

```cangjie
package log

public func printLog(message: String) {
    println("[Log]: ${message}")
}
```

And the file `main.cj`:

<!-- compile -p -->
<!-- cfg="liblog.a" -->

```cangjie
import log.*

main() {
    printLog("Everything is great")
}
```

You can compile the `log` package using:

```shell
$ cjc -p log --output-type=staticlib
```

`cjc` will generate a `liblog.a` file in the current directory.

Then, you can use the `liblog.a` file to compile `main.cj` with the following command:

```shell
$ cjc main.cj liblog.a
```

`cjc` will compile `main.cj` and `liblog.a` together into an executable file named `main`.

### `--module-name <value>` <sup>[frontend]</sup>

Specifies the name of the module to be compiled.

For example, given the file `MyModule/src/log/printer.cj`:

```cangjie
package log

public func printLog(message: String) {
    println("[Log]: ${message}")
}
```

And the file `main.cj`:

```cangjie
import MyModule.log.*

main() {
    printLog("Everything is great")
}
```

You can compile the `log` package and specify its module name as `MyModule` using:

```shell
$ cjc -p MyModule/src/log --module-name MyModule --output-type=staticlib -o MyModule/liblog.a
```

`cjc` will generate a `MyModule/liblog.a` file in the `MyModule` directory.

Then, you can use the `liblog.a` file to compile `main.cj`, which imports the `log` package, with the following command:

```shell
$ cjc main.cj MyModule/liblog.a
```

`cjc` will compile `main.cj` and `liblog.a` together into an executable file named `main`.

### `--output <value>`, `-o <value>`, `-o<value>` <sup>[frontend]</sup>

Specifies the path of the output file. The compiler's output will be written to the specified file.

For example, the following command names the output executable file `a.out`:

```shell
cjc main.cj -o a.out
```

### `--library <value>`, `-l <value>`, `-l<value>`

Specifies the library file to be linked.

The given library file will be directly passed to the linker. This option is typically used in conjunction with `--library-path <value>`.

The filename format should be `lib[arg].[extension]`. When linking library `a`, you can use the option `-l a`. The linker will search for files like `liba.a`, `liba.so` (or `liba.dll` on Windows) in the library search directories and link them as needed.

### `--library-path <value>`, `-L <value>`, `-L<value>`

Specifies the directory where the library files to be linked are located.

When using the `--library <value>` option, this option is typically also used to specify the directory containing the library files.

The path specified by `--library-path <value>` will be added to the linker's library search path. Additionally, paths specified in the `LIBRARY_PATH` environment variable will also be added to the linker's library search path, with paths specified via `--library-path` taking higher precedence.

For example, given a dynamic library file `libcProg.so` compiled from the following C source file:

```c
#include <stdio.h>

void printHello() {
    printf("Hello World\n");
}
```

And the Cangjie file `main.cj`:

```cangjie
foreign func printHello(): Unit

main(): Int64 {
  unsafe {
    printHello()
  }
  return 0
}
```

You can compile `main.cj` and specify the `cProg` library to link using:

```shell
cjc main.cj -L . -l cProg
```

`cjc` will output an executable file named `main`.  
Executing `main` will produce the following output:

```shell
$ LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH ./main
Hello World
```

**Note:** Since a dynamic library file is used, the directory containing the library must be added to `$LD_LIBRARY_PATH` to ensure dynamic linking during execution.

### `-g` <sup>[frontend]</sup>

Generates an executable or library file with debug information.

> **Note:**  
> `-g` can only be used with `-O0`. Higher optimization levels may cause debugging features to malfunction.

### `--trimpath <value>` <sup>[frontend]</sup>

Removes the specified prefix from source file path information in debug information.

When compiling Cangjie code, `cjc` saves the absolute path of source files (`.cj` files) to provide debugging and exception information during runtime.

This option removes the specified path prefix from the source file path information. The output file's source file path information will not include the user-specified prefix.

Multiple `--trimpath` options can be used to specify different prefixes. For each source file path, the compiler removes the first matching prefix.

### `--coverage` <sup>[frontend]</sup>

Generates an executable program that supports code coverage statistics. The compiler generates a `.gcno` code information file for each compilation unit. After execution, each compilation unit produces a `.gcda` execution statistics file. Using these files with the `cjcov` tool generates a code coverage report for the execution.

> **Note:**  
> `--coverage` can only be used with `-O0`. If a higher optimization level is specified, the compiler will issue a warning and force `-O0`. `--coverage` is for compiling executables; using it for static or dynamic libraries may cause linking errors in the final output.

### `--int-overflow=[throwing|wrapping|saturating]` <sup>[frontend]</sup>

Specifies the overflow strategy for fixed-precision integer operations. Defaults to `throwing`.

- In `throwing` mode, integer overflow throws an exception.
- In `wrapping` mode, integer overflow wraps around to the other end of the fixed-precision integer range.
- In `saturating` mode, integer overflow results in the extreme value of the fixed-precision range.

### `--diagnostic-format=[default|noColor|json]` <sup>[frontend]</sup>

> **Note:**  
> The Windows version currently does not support color-rendered error messages.

Specifies the output format for error messages. Defaults to `default`.

- `default`: Error messages are output in the default format (with color).
- `noColor`: Error messages are output in the default format (without color).
- `json`: Error messages are output in JSON format.

### `--verbose`, `-V` <sup>[frontend]</sup>

`cjc` prints compiler version information, toolchain dependency details, and commands executed during compilation.

### `--help`, `-h` <sup>[frontend]</sup>

Prints available compilation options.

When this option is used, the compiler only prints compilation option information and does not compile any input files.

### `--version`, `-v` <sup>[frontend]</sup>

Prints compiler version information.

When this option is used, the compiler only prints version information and does not compile any input files.

### `--save-temps <value>`

Retains intermediate files generated during compilation and saves them to the specified `<value>` path.

The compiler retains intermediate files like `.bc` and `.o` generated during compilation.

### `--import-path <value>` <sup>[frontend]</sup>

Specifies the search path for imported module AST files.

For example, given the following directory structure, where the `libs/myModule` directory contains the `myModule` library files and the AST export files for the `log` package:

```text
.
├── libs
|   └── myModule
|       ├── myModule.log.cjo
|       └── libmyModule.log.a
└── main.cj
```

And the `main.cj` file:

```cangjie
import myModule.log.printLog

main() {
    printLog("Everything is great")
}
```

You can add `./libs` to the AST file search path using `--import-path ./libs`. `cjc` will use the `./libs/myModule/myModule.log.cjo` file for semantic checking and compilation of `main.cj`.

`--import-path` provides the same functionality as the `CANGJIE_PATH` environment variable, but paths specified via `--import-path` take higher precedence.

### `--scan-dependency` <sup>[frontend]</sup>

The `--scan-dependency` command outputs direct dependencies and other information for a specified package source or `.cjo` file in JSON format.

```cangjie
// this file is placed under directory pkgA
macro package pkgA
import pkgB.*
import std.io.*
import pkgB.subB.*
```

```shell
cjc --scan-dependency --package pkgA
```

Or:

```shell
cjc --scan-dependency pkgA.cjo
```

```json
{
  "package": "pkgA",
  "isMacro": true,
  "dependencies": [
    {
      "package": "pkgB",
      "isStd": false,
      "imports": [
        {
          "file": "pkgA/pkgA.cj",
          "begin": {
            "line": 2,
            "column": 1
          },
          "end": {
            "line": 2,
            "column": 14
          }
        }
      ]
    },
    {
      "package": "pkgB.subB",
      "isStd": false,
      "imports": [
        {
          "file": "pkgA/pkgA.cj",
          "begin": {
            "line": 4,
            "column": 1
          },
          "end": {
            "line": 4,
            "column": 19
          }
        }
      ]
    },
    {
      "package": "std.io",
      "isStd": true,
      "imports": [
        {
          "file": "pkgA/pkgA.cj",
          "begin": {
            "line": 3,
            "column": 1
          },
          "end": {
            "line": 3,
            "column": 16
          }
        }
      ]
    }
  ]
}
```

### `--no-sub-pkg` <sup>[frontend]</sup>

Indicates that the current compilation package has no sub-packages.

Enabling this option allows the compiler to further reduce code size.

### `--warn-off`, `-Woff <value>` <sup>[frontend]</sup>

Disables all or specific categories of compilation warnings.

`<value>` can be `all` or a predefined warning category. When set to `all`, the compiler suppresses all warnings during compilation. When set to a specific category, the compiler suppresses warnings of that category.

Each warning includes a `#note` line indicating its category and how to disable it. Use `--help` to list all available warning categories.

### `--warn-on`, `-Won <value>` <sup>[frontend]</sup>

Enables all or specific categories of compilation warnings.

`<value>` for `--warn-on` has the same range as for `--warn-off`. `--warn-on` is typically used with `--warn-off`; for example, `-Woff all -Won <value>` enables only warnings of the specified category.

**Important:** The order of `--warn-on` and `--warn-off` matters. For the same category, the latter option overrides the former. For example, `-Won <value> -Woff all` will disable all warnings.

### `--error-count-limit <value>` <sup>[frontend]</sup>

Limits the maximum number of errors the compiler will print.

`<value>` can be `all` or a non-negative integer. When set to `all`, the compiler prints all errors. When set to an integer `N`, the compiler prints at most `N` errors. The default value is 8.

### `--output-dir <value>` <sup>[frontend]</sup>

Controls the directory where intermediate and final output files are saved.

For example, `.cjo` files are saved here. If both `--output-dir <path1>` and `--output <path2>` are specified, intermediate files are saved to `<path1>`, and the final output is saved to `<path1>/<path2>`.

> **Note:**  
> When this option is used with `--output`, the `--output` parameter must be a relative path.

### `--static-std`

Statically links the Cangjie library's std module.

This option only takes effect when compiling dynamic libraries or executables.

When compiling an executable (i.e., with `--output-type=exe`), `cjc` defaults to statically linking the std module.### <span id="--dy-std">`--dy-std`

Dynamically link the std module of the Cangjie library.

This option only takes effect when compiling dynamic libraries or executables.

When compiling a dynamic library (i.e., when `--output-type=dylib` is specified), `cjc` defaults to dynamically linking the std module of the Cangjie library.

**Important Notes:**

1. If both `--static-std` and `--dy-std` options are used together, only the last specified option will take effect.
2. The `--dy-std` option cannot be used with `--static-libs`, otherwise an error will occur.
3. When compiling an executable program that links to a Cangjie dynamic library (i.e., a product compiled with the `--output-type=dylib` option), the `--dy-std` option must be explicitly specified to dynamically link the standard library. Otherwise, multiple copies of the standard library may appear in the program, potentially causing runtime issues.

### `--static-libs`

Statically link non-std modules of the Cangjie library.

This option only takes effect when compiling dynamic libraries or executables. By default, `cjc` statically links non-std and non-runtime modules of the Cangjie library.

### `--dy-libs`

Dynamically link non-std modules of the Cangjie library.

This option only takes effect when compiling dynamic libraries or executables.

**Important Notes:**

1. If both `--static-libs` and `--dy-libs` options are used together, only the last specified option will take effect.
2. The `--static-std` option cannot be used with `--dy-libs`, otherwise an error will occur.
3. When `--dy-std` is used alone, the `--dy-libs` option will be enabled by default, with a corresponding warning message.
4. When `--dy-libs` is used alone, the `--dy-std` option will be enabled by default, with a corresponding warning message.

### `--stack-trace-format=[default|simple|all]`

Specify the exception stack trace printing format to control the display of stack frame information when an exception is thrown. The default format is `default`.

The stack trace formats are described as follows:

- `default` format: `Function name with generic parameters omitted (filename:line number)`
- `simple` format: `filename:line number`
- `all` format: `Full function name (filename:line number)`

### `--lto=[full|thin]`

Enable and specify the `LTO` (`Link Time Optimization`) compilation mode.

**Important Notes:**

1. This feature is not supported on `Windows` and `macOS` platforms.
2. When `LTO` is enabled, the following optimization compilation options cannot be used simultaneously: `-Os`, `-Oz`.

`LTO` supports two compilation modes:

- `--lto=full`: `Full LTO` merges all compilation modules together for global optimization. This mode offers the highest optimization potential but requires longer compilation time.
- `--lto=thin`: Compared to `full LTO`, `thin LTO` performs parallel optimization across multiple modules and supports incremental compilation by default. It has shorter compilation time than `full LTO` but less optimization effectiveness due to reduced global information.

    - Typical optimization effectiveness comparison: `full LTO` **>** `thin LTO` **>** conventional static linking compilation.
    - Typical compilation time comparison: `full LTO` **>** `thin LTO` **>** conventional static linking compilation.

`LTO` usage scenarios:

1. Compile an executable file using the following commands:

    ```shell
    $ cjc test.cj --lto=full
    or
    $ cjc test.cj --lto=thin
    ```

2. Compile a static library (`.bc` file) required for `LTO` mode and use it for executable compilation:

    ```shell
    # Generate a static library as a .bc file
    $ cjc pkg.cj --lto=full --output-type=staticlib -o libpkg.bc
    # Input the .bc file along with the source file to the Cangjie compiler for executable compilation
    $ cjc test.cj libpkg.bc --lto=full
    ```

    > **Note:**
    >
    > In `LTO` mode, the path to the static library (`.bc` file) must be provided to the Cangjie compiler.

3. In `LTO` mode, when statically linking the standard library (`--static-std` & `--static-libs`), the standard library code will participate in `LTO` optimization and be statically linked into the executable. When dynamically linking the standard library (`--dy-std` & `--dy-libs`), the dynamic library from the standard library will still be used for linking in `LTO` mode.

    ```shell
    # Static linking: standard library code participates in LTO optimization
    $ cjc test.cj --lto=full --static-std
    # Dynamic linking: dynamic library is used for linking, standard library code does not participate in LTO optimization
    $ cjc test.cj --lto=full --dy-std
    ```

### `--pgo-instr-gen`

Enable instrumentation compilation to generate an executable with instrumentation information.

This feature is not supported when compiling for macOS and Windows targets.

`PGO` (`Profile-Guided Optimization`) is a common compilation optimization technique that uses runtime profiling information to further improve program performance. `Instrumentation-based PGO` is a `PGO` optimization method that uses instrumentation information. It typically involves three steps:

1. The compiler performs instrumentation compilation on the source code to generate an instrumented executable.
2. Run the instrumented executable to generate a profile.
3. The compiler uses the profile to recompile the source code.

```shell
# Generate an executable `test` with instrumentation information for execution statistics
$ cjc test.cj --pgo-instr-gen -o test
# After running the executable `test`, generate a profile `test.profraw`
$ LLVM_PROFILE_FILE="test.profraw" ./test
```

> **Note:**
>
> Use the environment variable `LLVM_PROFILE_FILE="test%c.profraw"` to enable continuous mode, which generates profiles even if the program crashes or is killed by a signal. The `llvm-profdata` tool can be used to analyze such profiles. However, `PGO` currently does not support subsequent optimization steps in continuous mode.

### `--pgo-instr-use=<.profdata>`

Use the specified `profdata` profile to guide compilation and generate an optimized executable.

This feature is not supported when compiling for macOS targets.

> **Note:**
>
> The `--pgo-instr-use` compilation option only supports profiles in `profdata` format. Use the `llvm-profdata` tool to convert `profraw` profiles to `profdata` profiles.

```shell
# Convert `profraw` file to `profdata` file.
$ LD_LIBRARY_PATH=$CANGJIE_HOME/third_party/llvm/lib:$LD_LIBRARY_PATH $CANGJIE_HOME/third_party/llvm/bin/llvm-profdata merge test.profraw -o test.profdata
# Use the specified `test.profdata` profile to guide compilation and generate an optimized executable `testOptimized`
$ cjc test.cj --pgo-instr-use=test.profdata -o testOptimized
```

### `--target <value>` <sup>[frontend]</sup>

Specify the target platform triple for compilation.

The `<value>` parameter is typically a string in the following format: `<arch>(-<vendor>)-<os>(-<env>)`, where:

- `<arch>` represents the system architecture of the target platform, such as `aarch64`, `x86_64`, etc.
- `<vendor>` represents the vendor of the target platform, such as `apple`. If the vendor is unspecified or irrelevant, it is often written as `unknown` or omitted.
- `<os>` represents the operating system of the target platform, such as `Linux`, `Win32`, etc.
- `<env>` represents the ABI or standard specification of the target platform, used to distinguish between different runtime environments of the same OS, such as `gnu`, `musl`. If the OS does not require finer-grained distinction, this field can also be omitted.

Currently, `cjc` supports the following host and target platforms for cross-compilation:

| Host Platform       | Target Platform       |
| ------------------- | ------------------- |
| x86_64-windows-gnu  | aarch64-linux-ohos  |
| x86_64-windows-gnu  | x86_64-linux-ohos   |
| x86_64-apple-darwin | aarch64-linux-ohos  |
| x86_64-apple-darwin | x86_64-linux-ohos   |
| aarch64-apple-darwin | aarch64-linux-ohos  |

Before using `--target` to specify a target platform for cross-compilation, ensure that the corresponding cross-compilation toolchain and a compatible Cangjie SDK version for the target platform are available on the host platform.

### `--target-cpu <value>`

> **Note:**
>
> This option is experimental. Binaries generated with this option may have potential runtime issues. Use this option with caution. This option must be used with the `--experimental` option.

Specify the CPU type of the compilation target.

When specifying the CPU type, the compiler will attempt to use instruction sets specific to that CPU type and apply optimizations tailored for it. Binaries generated for a specific CPU type may lose portability and might not run on other CPUs (even those with the same architecture instruction set).

This option supports the following tested CPU types:

**x86-64 Architecture:**

- generic

**aarch64 Architecture:**

- generic
- tsv110

`generic` is the universal CPU type. When `generic` is specified, the compiler generates generic instructions for the architecture, ensuring the binary can run on various CPUs of that architecture (assuming the OS and dynamic dependencies are consistent). The default value for `--target-cpu` is `generic`.

This option also supports the following CPU types, but they are untested. Binaries generated for these CPU types may have runtime issues.

**x86-64 Architecture:**

- alderlake
- amdfam10
- athlon
- athlon-4
- athlon-fx
- athlon-mp
- athlon-tbird
- athlon-xp
- athlon64
- athlon64-sse3
- atom
- barcelona
- bdver1
- bdver2
- bdver3
- bdver4
- bonnell
- broadwell
- btver1
- btver2
- c3
- c3-2
- cannonlake
- cascadelake
- cooperlake
- core-avx-i
- core-avx2
- core2
- corei7
- corei7-avx
- geode
- goldmont
- goldmont-plus
- haswell
- i386
- i486
- i586
- i686
- icelake-client
- icelake-server
- ivybridge
- k6
- k6-2
- k6-3
- k8
- k8-sse3
- knl
- knm
- lakemont
- nehalem
- nocona
- opteron
- opteron-sse3
- penryn
- pentium
- pentium-m
- pentium-mmx
- pentium2
- pentium3
- pentium3m
- pentium4
- pentium4m
- pentiumpro
- prescott
- rocketlake
- sandybridge
- sapphirerapids
- silvermont
- skx
- skylake
- skylake-avx512
- slm
- tigerlake
- tremont
- westmere
- winchip-c6
- winchip2
- x86-64
- x86-64-v2
- x86-64-v3
- x86-64-v4
- yonah
- znver1
- znver2
- znver3

**aarch64 Architecture:**

- a64fx
- ampere1
- apple-a10
- apple-a11
- apple-a12
- apple-a13
- apple-a14
- apple-a7
- apple-a8
- apple-a9
- apple-latest
- apple-m1
- apple-s4
- apple-s5
- carmel
- cortex-a34
- cortex-a35
- cortex-a510
- cortex-a53
- cortex-a55
- cortex-a57
- cortex-a65
- cortex-a65ae
- cortex-a710
- cortex-a72
- cortex-a73
- cortex-a75
- cortex-a76
- cortex-a76ae
- cortex-a77
- cortex-a78
- cortex-a78c
- cortex-r82
- cortex-x1
- cortex-x1c
- cortex-x2
- cyclone
- exynos-m3
- exynos-m4
- exynos-m5
- falkor
- kryo
- neoverse-512tvb
- neoverse-e1
- neoverse-n1
- neoverse-n2
- neoverse-v1
- saphira
- thunderx
- thunderx2t99
- thunderx3t110
- thunderxt81
- thunderxt83
- thunderxt88

In addition to the above CPU types, this option supports `native` as the current CPU type. The compiler will attempt to identify the host machine's CPU type and generate binaries tailored for it.

### `--toolchain <value>`, `-B <value>`, `-B<value>`

Specify the path to the binary files in the compilation toolchain.

Binary files include: compilers, linkers, and C runtime object files (e.g., `crt0.o`, `crti.o`) provided by the toolchain.

After preparing the compilation toolchain, place it in a custom path and pass this path to the compiler using `--toolchain <value>`. This allows the compiler to invoke the binaries in that path for cross-compilation.

### `--sysroot <value>`

Specify the root directory path of the compilation toolchain.

For cross-compilation toolchains with fixed directory structures, if there is no need to specify paths for binaries, dynamic libraries, or static libraries outside this directory, you can directly use `--sysroot <value>` to pass the toolchain's root directory path to the compiler. The compiler will analyze the corresponding directory structure based on the target platform and automatically search for required binaries, dynamic libraries, and static libraries. Using this option eliminates the need to specify `--toolchain` or `--library-path`.

For example, when cross-compiling for a platform with the `triple` `arch-os-env`, and the cross-compilation toolchain has the following directory structure:

```text
/usr/sdk/arch-os-env
├── bin
|   ├── arch-os-env-gcc (cross-compiler)
|   ├── arch-os-env-ld  (linker)
|   └── ...
├── lib
|   ├── crt1.o          (C runtime object file)
|   ├── crti.o
|   ├── crtn.o
|   ├── libc.so         (dynamic library)
|   ├── libm.so
|   └── ...
└── ...
```

Given a Cangjie source file `hello.cj`, you can use the following command to cross-compile `hello.cj` for the `arch-os-env` platform:

```shell
cjc --target=arch-os-env --toolchain /usr/sdk/arch-os-env/bin --toolchain /usr/sdk/arch-os-env/lib --library-path /usr/sdk/arch-os-env/lib hello.cj -o hello
```

Alternatively, use the shorthand parameters:

```shell
cjc --target=arch-os-env -B/usr/sdk/arch-os-env/bin -B/usr/sdk/arch-os-env/lib -L/usr/sdk/arch-os-env/lib hello.cj -o hello
```

If the toolchain's directory structure follows conventions, you can omit `--toolchain` and `--library-path` and use the following command:

```shell
cjc --target=arch-os-env --sysroot /usr/sdk/arch-os-env hello.cj -o hello
```

### `--strip-all`, `-s`

When compiling an executable or dynamic library, specify this option to remove the symbol table from the output file.

### `--discard-eh-frame`

When compiling an executable or dynamic library, specify this option to remove the `eh_frame` section and part of the `eh_frame_hdr` section (information related to `crt` will not be processed). This reduces the size of the executable or dynamic library but may affect debugging information.

This feature is not supported when compiling for macOS targets.

### `--set-runtime-rpath`

Write the absolute path of the Cangjie runtime library directory into the RPATH/RUNPATH section of the binary. Using this option eliminates the need to set the `LD_LIBRARY_PATH` (for Linux) or `DYLD_LIBRARY_PATH` (for macOS) environment variables to locate the Cangjie runtime library when running the program in the build environment.

This feature is not supported when compiling for Windows targets.

### `--link-options <value>`<sup>1</sup>

Specify linker options.

`cjc` will pass the arguments of this option directly to the linker. Available arguments vary depending on the linker (system or specified). Multiple linker options can be specified by using `--link-options` multiple times.

<sup>1</sup> Superscript indicates that linker passthrough options may vary depending on the linker. Refer to the linker documentation for supported options.

### `--profile-compile-time` <sup>[frontend]</sup>

Print time consumption data for each compilation phase.

### `--profile-compile-memory` <sup>[frontend]</sup>

Print memory consumption data for each compilation phase.## Unit Test Options

### `--test` <sup>[frontend]</sup>

An entry point provided by the `unittest` testing framework, automatically generated by macros. When compiling with the `cjc --test` option, the program entry is no longer `main` but `test_entry`. For usage of the `unittest` testing framework, refer to the *Cangjie Programming Language Library API* documentation.

For the Cangjie file `a.cj` in the `pkgc` directory:
<!-- run -->

```cangjie
import std.unittest.*
import std.unittest.testmacro.*

@Test
public class TestA {
    @TestCase
    public func case1(): Unit {
        print("case1\n")
    }
}
```

You can use the following command in the `pkgc` directory:

```shell
cjc a.cj --test
```

to compile `a.cj`. Executing `main` will produce the following output:

> **Note:**
>
> The execution time of test cases is not guaranteed to be consistent across runs.

```text
case1
--------------------------------------------------------------------------------------------------
TP: default, time elapsed: 29710 ns, Result:
    TCS: TestA, time elapsed: 26881 ns, RESULT:
    [ PASSED ] CASE: case1 (16747 ns)
Summary: TOTAL: 1
    PASSED: 1, SKIPPED: 0, ERROR: 0
    FAILED: 0
--------------------------------------------------------------------------------------------------
```

For the following directory structure:

```text
application
├── src
├── pkgc
|   ├── a1.cj
|   └── a2.cj
└── a3.cj
```

You can use the `-p` compilation option in the `application` directory to compile the entire package:

```shell
cjc pkgc --test -p
```

to compile all test cases (`a1.cj` and `a2.cj`) under the `pkgc` package.

```cangjie
/*a1.cj*/
package a

import std.unittest.*
import std.unittest.testmacro.*

@Test
public class TestA {
    @TestCase
    public func caseA(): Unit {
        print("case1\n")
    }
}
```

```cangjie
/*a2.cj*/
package a

import std.unittest.*
import std.unittest.testmacro.*

@Test
public class TestB {
    @TestCase
    public func caseB(): Unit {
        throw IndexOutOfBoundsException()
    }
}
```

Executing `main` will produce the following output (**output is for reference only**):

```text
case1
--------------------------------------------------------------------------------------------------
TP: a, time elapsed: 367800 ns, Result:
    TCS: TestA, time elapsed: 16802 ns, RESULT:
    [ PASSED ] CASE: caseA (14490 ns)
    TCS: TestB, time elapsed: 347754 ns, RESULT:
    [ ERROR  ] CASE: caseB (345453 ns)
    REASON: An exception has occurred:IndexOutOfBoundsException
        at std/core.Exception::init()(std/core/exception.cj:23)
        at std/core.IndexOutOfBoundsException::init()(std/core/index_out_of_bounds_exception.cj:9)
        at a.TestB::caseB()(/home/houle/cjtest/application/pkgc/a2.cj:7)
        at a.lambda.1()(/home/houle/cjtest/application/pkgc/a2.cj:7)
        at std/unittest.TestCases::execute()(std/unittest/test_case.cj:92)
        at std/unittest.UT::run(std/unittest::UTestRunner)(std/unittest/test_runner.cj:194)
        at std/unittest.UTestRunner::doRun()(std/unittest/test_runner.cj:78)
        at std/unittest.UT::run(std/unittest::UTestRunner)(std/unittest/test_runner.cj:200)
        at std/unittest.UTestRunner::doRun()(std/unittest/test_runner.cj:78)
        at std/unittest.UT::run(std/unittest::UTestRunner)(std/unittest/test_runner.cj:200)
        at std/unittest.UTestRunner::doRun()(std/unittest/test_runner.cj:75)
        at std/unittest.entryMain(std/unittest::TestPackage)(std/unittest/entry_main.cj:11)
Summary: TOTAL: 2
    PASSED: 1, SKIPPED: 0, ERROR: 1
    FAILED: 0
--------------------------------------------------------------------------------------------------
```

### `--test-only` <sup>[frontend]</sup>

The `--test-only` option is used to compile only the test portion of a package.

If this option is enabled, the compiler will only compile test files (ending with `_test.cj`) in the package.

> **Note:**
>
> When using this option, the same package should first be compiled in regular mode, and then dependencies should be added via the `-L`/`-l` linking options or by adding dependent `.bc` files when using the `LTO` option. Otherwise, the compiler will report missing symbol errors.

Example:

```cangjie
/*main.cj*/
package my_pkg

func concatM(s1: String, s2: String): String {
    return s1 + s2
}

main() {
    println(concatM("a", "b"))
    0
}
```

```cangjie
/*main_test.cj*/
package my_pkg

@Test
class Tests {
    @TestCase
    public func case1(): Unit {
        @Expect("ac", concatM("a", "c"))
    }
}
```

The compilation commands are as follows:

```shell
# Compile the production part of the package first, only `main.cj` file would be compiled here
cjc -p my_pkg --output-type=staticlib -o=output/libmain.a
# Compile the test part of the package, Only `main_test.cj` file would be compiled here
cjc -p my_pkg --test-only -L output -lmain --import-path output
```

### `--mock <on|off|runtime-error>` <sup>[frontend]</sup>

If `on` is passed, the package will enable mock compilation, allowing classes in the package to be mocked in test cases. `off` is an explicit way to disable mocking.

**Notably**, mock support is automatically enabled for this package in test mode (when `--test` is enabled), and there is no need to explicitly pass the `--mock` option.

`runtime-error` is only available in test mode (when `--test` is enabled). It allows compiling packages with mock code but does not perform any mock-related processing in the compiler (which may introduce overhead and affect test runtime performance). This can be useful for benchmarking test cases with mock code. When using this compilation option, avoid compiling and running tests with mock code, as it will throw a runtime exception.

## Macro Options

`cjc` supports the following macro options. For more details on macros, refer to the <!--RP02-->[Macros](https://gitcode.com/Cangjie/cangjie_docs/blob/main/docs/dev-guide/source_en/Macro/macro_introduction.md)<!--RP02End--> section.

### `--compile-macro` <sup>[frontend]</sup>

Compile macro definition files to generate default macro definition dynamic library files.

### `--debug-macro` <sup>[frontend]</sup>

Generate Cangjie code files after macro expansion. This option can be used to debug macro expansion functionality.

### `--parallel-macro-expansion` <sup>[frontend]</sup>

Enable parallel macro expansion. This option can be used to reduce macro expansion compilation time.

## Conditional Compilation Options

`cjc` supports the following conditional compilation options. For more details on conditional compilation, refer to <!--RP02-->[Conditional Compilation](https://gitcode.com/Cangjie/cangjie_docs/blob/main/docs/dev-guide/source_en/compile_and_build/conditional_compilation.md)<!--RP02End-->.

### `--cfg <value>` <sup>[frontend]</sup>

Specify custom compilation conditions.

## Parallel Compilation Options

`cjc` supports the following parallel compilation options for higher compilation efficiency.

### `--jobs <value>`, `-j <value>` <sup>[frontend]</sup>

Set the maximum number of parallel jobs allowed during parallel compilation. `value` must be a reasonable non-negative integer. If `value` exceeds the hardware's maximum parallel capability, the compiler will use the hardware's maximum capability.

If this option is not set, the compiler will automatically calculate the maximum number of parallel jobs based on hardware capability.

> **Note:**
>
> `--jobs 1` means compiling entirely in serial mode.

### `--aggressive-parallel-compile`, `--apc`, `--aggressive-parallel-compile=<value>`, `--apc=<value>` <sup>[frontend]</sup>

When enabled, the compiler will adopt a more aggressive strategy (which may impact optimization and reduce program runtime performance) to achieve higher compilation efficiency. `value` is an optional parameter indicating the maximum number of parallel jobs for aggressive parallel compilation:

- If `value` is provided, it must be a reasonable non-negative integer. If `value` exceeds the hardware's maximum parallel capability, the compiler will automatically calculate the maximum number of parallel jobs based on hardware capability. It is recommended to set `value` to a non-negative integer less than the number of physical CPU cores.
- If `value` is not provided, aggressive parallel compilation is enabled by default, and the number of parallel jobs matches `--jobs`.

Additionally, if the same code is compiled twice with different `value` settings or different states of this option, the compiler does not guarantee binary consistency between the two outputs.

Rules for enabling/disabling aggressive parallel compilation:

- Aggressive parallel compilation will be forcibly disabled by the compiler in the following scenarios:
    - `--fobf-string`
    - `--fobf-const`
    - `--fobf-layout`
    - `--fobf-cf-flatten`
    - `--fobf-cf-bogus`
    - `--lto`
    - `--coverage`
    - Compiling for Windows targets
    - Compiling for macOS targets

- If `--aggressive-parallel-compile=<value>` or `--apc=<value>` is used, the state of aggressive parallel compilation is controlled by `value`:
    - `value <= 1`: Disable aggressive parallel compilation.
    - `value > 1`: Enable aggressive parallel compilation, with the number of parallel jobs determined by `value`.

- If `--aggressive-parallel-compile` or `--apc` is used, aggressive parallel compilation is enabled by default, and the number of parallel jobs matches `--jobs`.

- If this option is not set, the compiler will enable or disable aggressive parallel compilation by default based on the scenario:
    - `-O0` or `-g`: Aggressive parallel compilation is enabled by default, and the number of parallel jobs matches `--jobs`. It can be disabled by using `--aggressive-parallel-compile=<value>` or `--apc=<value>` with `value <= 1`.
    - Non-`-O0` and non-`-g`: Aggressive parallel compilation is disabled by default. It can be enabled by using `--aggressive-parallel-compile=<value>` or `--apc=<value>` with `value > 1`.

## Optimization Options

### `--fchir-constant-propagation` <sup>[frontend]</sup>

Enable CHIR constant propagation optimization.

### `--fno-chir-constant-propagation` <sup>[frontend]</sup>

Disable CHIR constant propagation optimization.

### `--fchir-function-inlining` <sup>[frontend]</sup>

Enable CHIR function inlining optimization.

### `--fno-chir-function-inlining` <sup>[frontend]</sup>

Disable CHIR function inlining optimization.

### `--fchir-devirtualization` <sup>[frontend]</sup>

Enable CHIR devirtualization optimization.

### `--fno-chir-devirtualization` <sup>[frontend]</sup>

Disable CHIR devirtualization optimization.

### `--fast-math` <sup>[frontend]</sup>

When enabled, the compiler will make aggressive (and potentially precision-losing) assumptions about floating-point operations to optimize them.

### `-O<N>` <sup>[frontend]</sup>

Use the specified code optimization level.

Higher optimization levels result in more aggressive code optimizations for better program performance but may require longer compilation times.

`cjc` uses O0-level optimization by default. Currently, `cjc` supports the following optimization levels: O0, O1, O2, Os, Oz.

When the optimization level is 2, `cjc` performs the corresponding optimizations and also enables the following options:
- `--fchir-constant-propagation`
- `--fchir-function-inlining`
- `--fchir-devirtualization`

When the optimization level is s, `cjc` performs O2-level optimizations and additionally optimizes for code size.

When the optimization level is z, `cjc` performs Os-level optimizations and further reduces code size.

> **Note:**
>
> When the optimization level is s or z, the link-time optimization option `--lto=[full|thin]` cannot be used simultaneously.

### `-O` <sup>[frontend]</sup>

Use O1-level code optimization, equivalent to `-O1`.

## Code Obfuscation Options

`cjc` supports code obfuscation for additional security protection. Code obfuscation is disabled by default.

`cjc` supports the following code obfuscation options:

### `--fobf-string`

Enable string obfuscation.

Obfuscates string constants in the code, making it impossible for attackers to statically read string data directly from the binary.

### `--fno-obf-string`

Disable string obfuscation.

### `--fobf-const`

Enable constant obfuscation.

Obfuscates numerical constants used in the code by replacing numerical operation instructions with equivalent but more complex instruction sequences.

### `--fno-obf-const`

Disable constant obfuscation.

### `--fobf-layout`

Enable layout obfuscation.

Layout obfuscation obfuscates symbols (including function names and global variable names), path names, line numbers, and function layout order in the code. When this option is enabled, `cjc` generates a symbol mapping output file `*.obf.map` in the current directory. If the `--obf-sym-output-mapping` option is configured, its parameter value will be used as the filename for the symbol mapping output file. The symbol mapping output file contains the mapping relationships between symbols before and after obfuscation, which can be used to deobfuscate obfuscated symbols.

> **Note:**
>
> Layout obfuscation conflicts with parallel compilation. Do not enable both simultaneously. If both are enabled, parallel compilation will be disabled.

### `--fno-obf-layout`

Disable layout obfuscation.

### `--obf-sym-prefix <string>`

Specify the prefix string added to symbols during layout obfuscation.

When this option is set, all obfuscated symbols will have this prefix added. This can be used to avoid symbol conflicts when obfuscating multiple Cangjie packages.

### `--obf-sym-output-mapping <file>`

Specify the symbol mapping output file for layout obfuscation.

The symbol mapping output file records the original names, obfuscated names, and file paths of symbols. It can be used to deobfuscate obfuscated symbols.

### `--obf-sym-input-mapping <file,...>`

Specify the symbol mapping input file for layout obfuscation.

Layout obfuscation uses the mapping relationships in these files to obfuscate symbols. Therefore, when compiling Cangjie packages with dependencies, use the symbol mapping output file of the dependent package as the parameter for the `--obf-sym-input-mapping` option to ensure consistent obfuscation results for the same symbols across packages.

### `--obf-apply-mapping-file <file>`

Provide a custom symbol mapping file for layout obfuscation. The layout obfuscation will obfuscate symbols according to the mappings in this file.

The file format is as follows:

```text
<original_symbol_name> <new_symbol_name>
```

Here, `original_symbol_name` is the name before obfuscation, and `new_symbol_name` is the name after obfuscation. `original_symbol_name` consists of multiple `field`s, which can be module names, package names, class names, struct names, enum names, function names, or variable names. `field`s are separated by the delimiter `'.'`. If `field` is a function name, the function's parameter types must be appended in parentheses `'()'`. For parameterless functions, the parentheses are empty. If `field` has generic parameters, they must also be appended in angle brackets `'<>'`.

Layout obfuscation will replace `original_symbol_name` in the Cangjie application with `new_symbol_name`. For symbols not in this file, layout obfuscation will use random names for replacement. If the mappings in this file conflict with those in `--obf-sym-input-mapping`, the compiler will throw an exception and stop compilation.

### `--fobf-export-symbols`

Allow layout obfuscation to obfuscate exported symbols. This option is enabled by default when layout obfuscation is enabled.

When enabled, layout obfuscation will obfuscate exported symbols.

### `--fno-obf-export-symbols`

Disallow layout obfuscation from obfuscating exported symbols.

### `--fobf-source-path`

Allow layout obfuscation to obfuscate path information in symbols. This option is enabled by default when layout obfuscation is enabled.

When enabled, layout obfuscation will obfuscate path information in exception stack traces, replacing path names with the string `"SOURCE"`.

### `--fno-obf-source-path`

Disallow layout obfuscation from obfuscating path information in stack traces.

### `--fobf-line-number`

Allow layout obfuscation to obfuscate line number information in stack traces.

When enabled, layout obfuscation will obfuscate line number information in exception stack traces, replacing line numbers with `0`.

### `--fno-obf-line-number`

Dis## Secure Compilation Options

`cjc` generates position-independent code by default and produces position-independent executables when compiling executable files.

When building Release versions, it is recommended to enable/disable compilation options according to the following rules to enhance security.

### Enable `--trimpath <value>` <sup>[frontend]</sup>

Removes specified absolute path prefixes from debugging and exception information. Using this option prevents build path information from being written into the binary.

After enabling this option, source code path information in the binary is usually no longer complete, which may affect debugging. It is recommended to disable this option when building debug versions.

### Enable `--strip-all`, `-s`

Removes the symbol table from the binary. Using this option deletes symbol-related information not required during runtime.

After enabling this option, the binary cannot be debugged. Please disable this option when building debug versions.

### Disable `--set-runtime-rpath`

If the executable will be distributed to different environments or if other regular users have write permissions to the directory of the currently used Cangjie runtime library, using this option may pose security risks. Therefore, disable this option.

This option is not applicable when compiling Windows targets.

### Enable `--link-options "-z noexecstack"`<sup>1</sup>

Sets the thread stack to be non-executable.

Only available when compiling Linux targets.

### Enable `--link-options "-z relro"`<sup>1</sup>

Sets the GOT table relocation to read-only.

Only available when compiling Linux targets.

### Enable `--link-options "-z now"`<sup>1</sup>

Enables immediate binding.

Only available when compiling Linux targets.

## Code Coverage Instrumentation Options

> **Note:**
>
> Windows and macOS versions currently do not support code coverage instrumentation options.

Cangjie supports code coverage instrumentation (SanitizerCoverage, hereafter referred to as SanCov), providing interfaces consistent with LLVM's SanitizerCoverage. The compiler inserts coverage feedback functions at the function or BasicBlock level. Users only need to implement the agreed callback functions to monitor program execution status during runtime.

Cangjie's SanCov functionality operates at the package level, meaning the entire package is either fully instrumented or not instrumented at all.

### `--sanitizer-coverage-level=0/1/2`

Instrumentation level: 0 means no instrumentation; 1 means function-level instrumentation, inserting callback functions only at function entries; 2 means BasicBlock-level instrumentation, inserting callback functions at various BasicBlocks.

If not specified, the default value is 2.

This compilation option only affects the instrumentation level of `--sanitizer-coverage-trace-pc-guard`, `--sanitizer-coverage-inline-8bit-counters`, and `--sanitizer-coverage-inline-bool-flag`.

### `--sanitizer-coverage-trace-pc-guard`

Enabling this option inserts a function call `__sanitizer_cov_trace_pc_guard(uint32_t *guard_variable)` at each Edge, influenced by `sanitizer-coverage-level`.

**Note:** This feature differs from gcc/llvm implementations: it does not insert `void __sanitizer_cov_trace_pc_guard_init(uint32_t *start, uint32_t *stop)` in the constructor. Instead, it inserts a function call `uint32_t *__cj_sancov_pc_guard_ctor(uint64_t edgeCount)` during package initialization.

The `__cj_sancov_pc_guard_ctor` callback function must be implemented by the developer. Packages with SanCov enabled will call this callback as early as possible. The input parameter is the number of Edges in the package, and the return value is typically a memory region created by calloc.

If `__sanitizer_cov_trace_pc_guard_init` needs to be called, it is recommended to call it within `__cj_sancov_pc_guard_ctor`, using a dynamically created buffer to compute the function's input parameters and return value.

A standard implementation of `__cj_sancov_pc_guard_ctor` is as follows:

```cpp
uint32_t *__cj_sancov_pc_guard_ctor(uint64_t edgeCount) {
    uint32_t *p = (uint32_t *) calloc(edgeCount, sizeof(uint32_t));
    __sanitizer_cov_trace_pc_guard_init(p, p + edgeCount);
    return p;
}
```

### `--sanitizer-coverage-inline-8bit-counters`

Enabling this option inserts an 8-bit counter at each Edge. Each time an Edge is traversed, the counter increments by one, influenced by `sanitizer-coverage-level`.

**Note:** This feature differs from gcc/llvm implementations: it does not insert `void __sanitizer_cov_8bit_counters_init(char *start, char *stop)` in the constructor. Instead, it inserts a function call `uint8_t *__cj_sancov_8bit_counters_ctor(uint64_t edgeCount)` during package initialization.

The `__cj_sancov_pc_guard_ctor` callback function must be implemented by the developer. Packages with SanCov enabled will call this callback as early as possible. The input parameter is the number of Edges in the package, and the return value is typically a memory region created by calloc.

If `__sanitizer_cov_8bit_counters_init` needs to be called, it is recommended to call it within `__cj_sancov_8bit_counters_ctor`, using a dynamically created buffer to compute the function's input parameters and return value.

A standard implementation of `__cj_sancov_8bit_counters_ctor` is as follows:

```cpp
uint8_t *__cj_sancov_8bit_counters_ctor(uint64_t edgeCount) {
    uint8_t *p = (uint8_t *) calloc(edgeCount, sizeof(uint8_t));
    __sanitizer_cov_8bit_counters_init(p, p + edgeCount);
    return p;
}
```

### `--sanitizer-coverage-inline-bool-flag`

Enabling this option inserts a boolean value at each Edge. The boolean value corresponding to a traversed Edge is set to True, influenced by `sanitizer-coverage-level`.

**Note:** This feature differs from gcc/llvm implementations: it does not insert `void __sanitizer_cov_bool_flag_init(bool *start, bool *stop)` in the constructor. Instead, it inserts a function call `bool *__cj_sancov_bool_flag_ctor(uint64_t edgeCount)` during package initialization.

The `__cj_sancov_bool_flag_ctor` callback function must be implemented by the developer. Packages with SanCov enabled will call this callback as early as possible. The input parameter is the number of Edges in the package, and the return value is typically a memory region created by calloc.

If `__sanitizer_cov_bool_flag_init` needs to be called, it is recommended to call it within `__cj_sancov_bool_flag_ctor`, using a dynamically created buffer to compute the function's input parameters and return value.

A standard implementation of `__cj_sancov_bool_flag_ctor` is as follows:

```cpp
bool *__cj_sancov_bool_flag_ctor(uint64_t edgeCount) {
    bool *p = (bool *) calloc(edgeCount, sizeof(bool));
    __sanitizer_cov_bool_flag_init(p, p + edgeCount);
    return p;
}
```

### `--sanitizer-coverage-pc-table`

This compilation option provides the correspondence between instrumentation points and source code, currently only offering function-level correspondence. It must be used with `--sanitizer-coverage-trace-pc-guard`, `--sanitizer-coverage-inline-8bit-counters`, or `--sanitizer-coverage-inline-bool-flag`. At least one of these options must be enabled, and multiple can be enabled simultaneously.

**Note:** This feature differs from gcc/llvm implementations: it does not insert `void __sanitizer_cov_pcs_init(const uintptr_t *pcs_beg, const uintptr_t *pcs_end);` in the constructor. Instead, it inserts a function call `void __cj_sancov_pcs_init(int8_t *packageName, uint64_t n, int8_t **funcNameTable, int8_t **fileNameTable, uint64_t *lineNumberTable)` during package initialization. The parameters are as follows:

- `int8_t *packageName`: A string representing the package name (C-style int8 arrays are used for strings in instrumentation parameters).
- `uint64_t n`: The number of functions instrumented.
- `int8_t **funcNameTable`: An array of strings of length n, where funcNameTable[i] is the function name corresponding to the i-th instrumentation point.
- `int8_t **fileNameTable`: An array of strings of length n, where fileNameTable[i] is the file name corresponding to the i-th instrumentation point.
- `uint64_t *lineNumberTable`: An array of uint64 of length n, where lineNumberTable[i] is the line number corresponding to the i-th instrumentation point.

If `__sanitizer_cov_pcs_init` needs to be called, you must manually convert Cangjie's pc-table to C-language pc-table.

### `--sanitizer-coverage-stack-depth`

Enabling this compilation option inserts a call to `__updateSancovStackDepth` at each function entry, as Cangjie cannot obtain the SP pointer value. Implementing this function on the C side allows access to the SP pointer.

A standard implementation of `updateSancovStackDepth` is as follows:

```cpp
thread_local void* __sancov_lowest_stack;

void __updateSancovStackDepth()
{
    register void* sp = __builtin_frame_address(0);
    if (sp < __sancov_lowest_stack) {
        __sancov_lowest_stack = sp;
    }
}
```

### `--sanitizer-coverage-trace-compares`

Enabling this option inserts callback functions before all compare and match instructions. The list of functions is consistent with LLVM's API functionality. Refer to Tracing data flow.

```cpp
void __sanitizer_cov_trace_cmp1(uint8_t Arg1, uint8_t Arg2);
void __sanitizer_cov_trace_const_cmp1(uint8_t Arg1, uint8_t Arg2);
void __sanitizer_cov_trace_cmp2(uint16_t Arg1, uint16_t Arg2);
void __sanitizer_cov_trace_const_cmp2(uint16_t Arg1, uint16_t Arg2);
void __sanitizer_cov_trace_cmp4(uint32_t Arg1, uint32_t Arg2);
void __sanitizer_cov_trace_const_cmp4(uint32_t Arg1, uint32_t Arg2);
void __sanitizer_cov_trace_cmp8(uint64_t Arg1, uint64_t Arg2);
void __sanitizer_cov_trace_const_cmp8(uint64_t Arg1, uint64_t Arg2);
void __sanitizer_cov_trace_switch(uint64_t Val, uint64_t *Cases);
```

### `--sanitizer-coverage-trace-memcmp`

This compilation option provides prefix comparison feedback for String and Array comparisons. Enabling this option inserts callback functions before String and Array comparison functions. The following APIs for Strings and Arrays will insert corresponding stub functions:

- String==: __sanitizer_weak_hook_memcmp
- String.startsWith: __sanitizer_weak_hook_memcmp
- String.endsWith: __sanitizer_weak_hook_memcmp
- String.indexOf: __sanitizer_weak_hook_strstr
- String.replace: __sanitizer_weak_hook_strstr
- String.contains: __sanitizer_weak_hook_strstr
- CString==: __sanitizer_weak_hook_strcmp
- CString.startswith: __sanitizer_weak_hook_memcmp
- CString.endswith: __sanitizer_weak_hook_strncmp
- CString.compare: __sanitizer_weak_hook_strcmp
- CString.equalsLower: __sanitizer_weak_hook_strcasecmp
- Array==: __sanitizer_weak_hook_memcmp
- ArrayList==: __sanitizer_weak_hook_memcmp

## Experimental Feature Options

### `--experimental` <sup>[frontend]</sup>

Enables experimental features, allowing the use of other experimental options on the command line.

> **Note:**
>
> Binaries generated using experimental features may have potential runtime issues. Please be aware of the risks when using this option.

## Additional Features

### Compiler Error Message Colors

For the Windows version of the Cangjie compiler, error messages are displayed in color only when running on Windows 10 version 1511 (Build 10586) or later systems. Otherwise, colors are not displayed.

### Setting build-id

Use `--link-options "--build-id=<arg>"`<sup>1</sup> to pass linker options for setting build-id.

This feature is not supported when compiling Windows targets.

### Setting rpath

Use `--link-options "-rpath=<arg>"`<sup>1</sup> to pass linker options for setting rpath.

This feature is not supported when compiling Windows targets.

### Incremental Compilation

Enable incremental compilation with `--incremental-compile`<sup>[frontend]</sup>. When enabled, `cjc` uses cache files from previous compilations to speed up the current compilation.

> **Note:**
>
> When this option is specified, incremental compilation cache and logs are saved to the `.cached` directory under the output file path.

## Environment Variables Used by `cjc`

This section introduces some environment variables that the Cangjie compiler may use during code compilation.

### `TMPDIR` or `TMP`

The Cangjie compiler places temporary files generated during compilation in a temporary directory. By default, Linux and macOS systems use `/tmp`, while Windows systems use `C:\Windows\Temp`. The compiler also supports custom temporary file directories. On Linux and macOS, set the `TMPDIR` environment variable; on Windows, set the `TMP` environment variable.

Example:
In Linux shell:

```shell
export TMPDIR=/home/xxxx
```

In Windows cmd:

```shell
set TMP=D:\\xxxx
```