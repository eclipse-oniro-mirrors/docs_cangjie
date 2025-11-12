# Packaging Tool

The packaging tool is used to package compiled files after program compilation for installation and distribution. Developers can use DevEco Studio for packaging or utilize the JAR package of the packaging tool, which is typically located in the `toolchains` directory under the SDK path.

The packaging tool supports generating:
- Ability-type module packages (HAP)
- Dynamic shared packages (HSP)
- Application packages (App)
- Quick fix module packages (HQF)
- Quick fix packages (APPQF)

> **Note:**
>
> Currently, Cangjie only supports developing HAR and HAP packages and does not support HSP packages. Therefore, HSP-related features in this tool are unavailable in Cangjie programs.

The files in packaging commands are sourced from [DevEco Studio compilation build artifacts](https://developer.huawei.com/consumer/en/doc/harmonyos-guides/ide-compile-build). The file path can be checked as follows:

1. In the `/hvigor/hvigor-config.json5` file under the DevEco Studio project root directory, modify the `"level"` field under `"logging"` to `"debug"`.
2. In the DevEco Studio menu bar, select **Build > Clean Project**.
3. In the DevEco Studio menu bar, select **Build > Build APP(s)**.
4. In the DevEco Studio **Build** window at the bottom, search for `"app_packing_tool.jar"` to confirm the file paths in the packaging parameters.

## Constraints and Limitations

The packaging tool requires Java 8 or higher to run.

## HAP Packaging Command

Developers can use the JAR package of the packaging tool to package modules by passing packaging options and file paths to generate the required HAP package.

- Stage model example:

    ```bash
    java -jar app_packing_tool.jar --mode hap --json-path <path> [--resources-path <path>] [--ets-path <path>] [--index-path <path>] [--pack-info-path <path>] [--lib-path <path>] --out-path <path> [--force true] [--compress-level 5] [--pkg-context-path <path>] [--hnp-path <path>]
    ```

**Table 1** HAP Packaging Command Parameter Descriptions

| Command | Required | Option | Description | Remarks |
|---------|----------|--------|-------------|---------|
| `--mode` | Yes | `hap` | Packaging type. | NA |
| `--json-path` | Yes | NA | Path to the `.json` file. For Stage models, the filename must be `module.json`. | NA |
| `--profile-path` | No | NA | Path to the `CAPABILITY.profile` file. | NA |
| `--maple-so-path` | No | NA | Input path for Maple SO files. The filename must end with `.so`. Multiple SO files should be separated by commas. | NA |
| `--maple-so-dir` | No | NA | Input directory path for Maple SO files. | NA |
| `--dex-path` | No | NA | Path to the `.dex` file(s). The filename must end with `.dex`. Multiple DEX files should be separated by commas. The path can also be a directory. | NA |
| `--lib-path` | No | NA | Path to the library files. | NA |
| `--resources-path` | No | NA | Path to the `resources` package. | NA |
| `--index-path` | No | NA | Path to the `.index` file. The filename must be `resources.index`. | NA |
| `--pack-info-path` | No | NA | Path to the `pack.info` file. The filename must be `pack.info`. | NA |
| `--rpcid-path` | No | NA | Path to the `rpcid.sc` file. The filename must be `rpcid.sc`. | NA |
| `--js-path` | No | NA | Directory path for storing JS files. | Only effective for Stage models. |
| `--ets-path` | No | NA | Directory path for storing ETS files. | Only effective for Stage models. |
| `--out-path` | Yes | NA | Target file path. The filename must end with `.hap`. | NA |
| `--force` | No | `true` or `false` | Default is `false`. If `true`, forces deletion if the target file exists. | NA |
| `--an-path` | No | NA | Path for storing [AN files](https://developer.huawei.com/consumer/en/doc/harmonyos-faqs-V5/faqs-arkts-52-V5). | Only effective for Stage models. |
| `--ap-path` | No | NA | Path for storing [AP files](https://developer.huawei.com/consumer/en/doc/harmonyos-faqs-V5/faqs-arkts-52-V5). | Only effective for Stage models. |
| `--dir-list` | No | NA | Specifies a list of target directories to include in the HAP package. | NA |
| `--compress-level` | No | `number` | Compression level, default is `1`. Valid levels: `1-9`. Takes effect when `compressNativeLibs` is set to `true`. Higher values yield better compression but slower speeds. | NA |
| `--pkg-context-path` | No | NA | Path to the context information table file. The filename must be `pkgContextInfo.json`. | Only effective for Stage models. |
| `--hnp-path` | No | NA | Path to the native software package file to include in the HAP package. | NA |

## HSP Packaging Command

HSP packages enable file sharing among multiple HAPs. Developers can use the JAR package of the packaging tool to package applications by passing packaging options and file paths to generate the required HSP package.

Example:

```bash
java -jar app_packing_tool.jar --mode hsp --json-path <path> [--resources-path <path>] [--ets-path <path>] [--index-path <path>] [--pack-info-path <path>] [--lib-path <path>] --out-path <path> [--force true] [--compress-level 5] [--pkg-context-path <path>]
```

**Table 2** HSP Packaging Command Parameter Descriptions

| Command | Required | Option | Description |
|---------|----------|--------|-------------|
| `--mode` | Yes | `hsp` | Packaging type. |
| `--json-path` | Yes | NA | Path to the `.json` file. The filename must be `module.json`. |
| `--profile-path` | No | NA | Path to the `CAPABILITY.profile` file. |
| `--dex-path` | No | NA | 1. Path to the `.dex` file(s). The filename must end with `.dex`. Multiple DEX files should be separated by commas.<br>2. The path can also be a directory. |
| `--lib-path` | No | NA | Path to the library files. |
| `--resources-path` | No | NA | Path to the `resources` package. |
| `--index-path` | No | NA | Path to the `.index` file. The filename must be `resources.index`. |
| `--pack-info-path` | No | NA | Path to the `pack.info` file. The filename must be `pack.info`. |
| `--js-path` | No | NA | Directory path for storing JS files. |
| `--ets-path` | No | NA | Directory path for storing ETS files. |
| `--out-path` | Yes | NA | Target file path. The filename must end with `.hsp`. |
| `--force` | No | `true` or `false` | Default is `false`. If `true`, forces deletion if the target file exists. |
| `--compress-level` | No | `number` | Compression level, default is `1`. Valid levels: `1-9`. Takes effect when `compressNativeLibs` is set to `true`. Higher values yield better compression but slower speeds. |
| `--pkg-context-path` | No | NA | Path to the context information table file. The filename must be `pkgContextInfo.json`. |

## App Packaging Command

Developers can use the JAR package of the packaging tool to package applications by passing packaging options and file paths to generate the required App package. App packages are used for publishing to the app store.

**HAP Validity Check for App Packaging:** When packaging HAPs into an App package, ensure that each HAP has the same `bundleName`, `versionCode`, `minCompatibleVersionCode`, `debug`, `minAPIVersion`, and `targetAPIVersion` in their JSON files, and that `moduleName` is unique. HAP modules must have the same `apiReleaseType`, while HSP modules do not require this check.

**Compression Rules for App Packaging:** When packaging an App, HAP and HSP packages in `release` mode are compressed, while those in `debug` mode are not.

> **Note:**
>
> Starting from API version 12, App packaging no longer validates `versionName`.

Example:

```bash
java -jar app_packing_tool.jar --mode app [--hap-path <path>] [--hsp-path <path>] --out-path <path> [--signature-path <path>] [--certificate-path <path>] --pack-info-path <path> [--pack-res-path <path>] [--force true] [--encrypt-path <path>]
```

**Table 3** App Packaging Command Parameter Descriptions

| Command | Required | Option | Description |
|---------|----------|--------|-------------|
| `--mode` | Yes | `app` | Multiple HAPs must pass the HAP validity check. |
| `--hap-path` | No | NA | Path to the `.hap` file(s). The filename must end with `.hap`. Multiple HAPs should be separated by commas. The path can also be a directory. |
| `--hsp-path` | No | NA | Path to the `.hsp` file(s). The filename must end with `.hsp`. Multiple HSPs should be separated by commas. The path can also be a directory. |
| `--pack-info-path` | Yes | NA | The filename must be `pack.info`. |
| `--out-path` | Yes | NA | Target file path. The filename must end with `.app`. |
| `--signature-path` | No | NA | Path to the signature file. |
| `--certificate-path` | No | NA | Path to the certificate file. |
| `--pack-res-path` | No | NA | Path to the `pack.res` snapshot file. |
| `--force` | No | `true` or `false` | Default is `false`. If `true`, forces deletion if the target file exists. |
| `--encrypt-path` | No | NA | The filename must be `encrypt.json`. |

## Multi-Project Packaging Command

Multi-project packaging is suitable for scenarios where multiple teams develop the same application but cannot easily share code. Developers can pass pre-built HAP, HSP, and App packages to combine them into a final App package for publishing to the app store.

**HAP Validity Check for Multi-Project Packaging:** Ensure that each HAP has the same `bundleName`, `versionCode`, `minCompatibleVersionCode`, and `debug` attributes in their JSON files, and that `minAPIVersion`, `targetAPIVersion`, `compileSdkVersion`, and `compileSdkType` are the same. `moduleName` must be unique, and each device must have a unique `entry`. HAP modules must have the same `apiReleaseType`, while HSP modules do not require this check.

> **Note:**
>
> Starting from API version 12, multi-project packaging no longer validates `versionName`.

Example:

```bash
java -jar app_packing_tool.jar --mode multiApp [--hap-list <path>] [--hsp-list <path>] [--app-list <path>] --out-path <option> [--force true] [--encrypt-path <path>]
```

**Table 4** Multi-Project Packaging Command Parameter Descriptions

| Command | Required | Option | Description |
|---------|----------|--------|-------------|
| `--mode` | Yes | `multiApp` | Packaging type. When combining multiple HAPs into one App, ensure each HAP passes the validity check. |
| `--hap-list` | No | HAP path(s) | Path to the `.hap` file(s). The filename must end with `.hap`. Multiple HAPs should be separated by commas. The path can also be a directory. |
| `--hsp-list` | No | HSP path(s) | Path to the `.hsp` file(s). The filename must end with `.hsp`. Multiple HSPs should be separated by commas. The path can also be a directory. |
| `--app-list` | No | App path(s) | Path to the `.app` file(s). The filename must end with `.app`. Multiple Apps should be separated by commas. The path can also be a directory.<br>`--hap-list`, `--hsp-list`, and `--app-list` cannot all be empty. |
| `--out-path` | Yes | NA | Target file path. The filename must end with `.app`. |
| `--force` | No | `true` or `false` | Default is `false`. If `true`, forces deletion if the target file exists. |
| `--encrypt-path` | No | Path to `encrypt.json` | The filename must be `encrypt.json`. |

## HQF Packaging Command

HQF packages are used for urgent fixes when issues arise in an application. Developers can use the JAR package of the packaging tool to package applications by passing packaging options and file paths to generate the required HQF package.

Example:

```bash
java -jar app_packing_tool.jar --mode hqf --json-path <path> [--lib-path <path>] [--ets-path <path>] [--resources-path <path>] --out-path <path> [--force true]
```

**Table 5** HQF Packaging Command Parameter Descriptions

| Command | Required | Option | Description |
|---------|----------|--------|-------------|
| `--mode` | Yes | `hqf` | Packaging type. |
| `--json-path` | Yes | NA | Path to the `.json` file. The filename must be `patch.json`. |
| `--lib-path` | No | NA | Path to the library files. |
| `--ets-path` | No | NA | Directory path for storing ETS files. |
| `--resources-path` | No | NA | Path to the `resources` package. |
| `--out-path` | Yes | NA | Target file path. The filename must end with `.hqf`. |
| `--force` | No | `true` or `false` | Default is `false`. If `true`, forces deletion if the target file exists. |

## APPQF Packaging Command

An APPQF package consists of one or more HQF files. These HQF packages are split from the APPQF package in the app store and distributed to specific devices. Developers can use the JAR package of the packaging tool to package applications by passing packaging options and file paths to generate the required APPQF package.

Example:

```bash
java -jar app_packing_tool.jar --mode appqf --hqf-list <path> --out-path <path> [--force true]
```

**Table 6** APPQF Packaging Command Parameter Descriptions

| Command | Required | Option | Description |
|---------|----------|--------|-------------|
| `--mode` | Yes | `appqf` | Packaging type. |
| `--hqf-list` | Yes | NA | Path to [HQF files](#hqf-packaging-command). Multiple HQFs should be separated by commas. |
| `--out-path` | Yes | NA | Target file path. The filename must end with `.appqf`. |
| `--force` | No | `true` or `false` | Default is `false`. If `true`, forces deletion if the target file exists. |

## Version Normalization Command (`versionNormalize`)

All HAP and HSP packages in the same App must have the same `versionName` and `versionCode`. When only one HAP or HSP needs modification or upgrade, this command can be used to unify the versions of multiple HAPs and HSPs. This command modifies the version numbers and names of the input HAPs and HSPs, generates modified HAPs and HSPs with the same names in the specified directory, and creates a `version_record.json` file to record the original version numbers and names.

Example:

```bash
java -jar path\app_packing_tool.jar --mode versionNormalize --input-list 1.hap,2.hsp --version-code 1000001 --version-name 1.0.1 --out-path path\out\
```

**Table 7** `versionNormalize` Command Parameter Descriptions

| Command | Required | Option | Description |
|---------|----------|--------|-------------|
| `--mode` | Yes | `versionNormalize` | Command type. |
| `--input-list` | Yes | HAP or HSP path(s) | 1. Path to the `.hap` or `.hsp` file(s). The filename must end with `.hap` or `.hsp`. Multiple HAPs or HSPs should be separated by commas.<br>2. If a directory is provided, all HAP and HSP files in the directory will be read. |
| `--version-code` | Yes | Version number | Specified version number. HAP and HSP version numbers will be modified to this value. Must be an integer and not less than the version numbers of all input HAPs and HSPs. |
| `--version-name` | Yes | Version name | Specified version name. HAP and HSP version names will be modified to this value. |
| `--out-path` | Yes | NA | Target file path. Must be a directory. |

## Package Name Normalization Command (`packageNormalize`)

This command modifies the package names and version numbers of input HSPs and generates modified HSPs with the same names in the specified directory.

Example:

```bash
java -jar path\app_packing_tool.jar --mode packageNormalize --hsp-list path\1.hsp,path\2.hsp --bundle-name com.example.myapplication --version-code 1000001 --out-path path\out\
```

**Table 8** Parameter Descriptions and Specifications

| Command | Required | Option | Description |
|---------|----------|--------|-------------|
| `--mode` |