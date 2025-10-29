# HLE工具命令行使用

仓颉语言支持与ArkTS的高效跨语言互操作，允许开发者在仓颉代码中调用ArkTS的第三方库，用户可以通过使用HLE(Hyper-Lang extension)工具,解析ArkTS的接口，自动生成被仓颉调用的跨语言封装代码。

## 使用方式

HLE命令行的参数含义:

| 参数            | 含义                                        | 参数类型 | 说明                 |
| --------------- | ------------------------------------------- | -------- | -------------------- |
| `-i`            | d.ts或者d.ets文件输入的绝对路径             | 可选参数 | 和`-d`参数二选一或者两者同时存在                     |
| `-r`            | typescript编译器的绝对路径                  | 必选参数 |                      |
| `-d`            | d.ts或者d.ets文件输入所在文件夹的绝对路径    | 可选参数 | 和`-i`参数二选一或者两者同时存在                     |
| `-o`            | 输出保存互操作代码的目录                    | 可选参数 | 缺省时输出至当前目录 |
| `-j`            | 分析d.t或者d.ets文件的路径                 | 可选参数 |                      |
| `--module-name` | 自定义生成的仓颉包名                        | 可选参数 |                      |
| `--lib`         | 生成三方库代码                              | 可选参数 |                      |
| `--help`        | 帮助选项                                   | 可选参数 |                      |

## 使用示例

下面以通过HLE工具生成[lz4js](https://ohpm.openharmony.cn/#/cn/detail/lz4js)三方库的仓颉胶水层代码为例展示详细的使用步骤。

1. 安装HLE工具的依赖

    进入到仓颉sdk的工具的dtsparser目录

    ![hle_install](../../figures/HLE_install.png)

    执行安装命令：

    ```sh
    npm install
    ```

2. 配置lz4js三方库依赖

    在dtsparser目录中的package.json中添加lz4js三方库依赖。

    ```json
    "dependencies": {
        // ...
        "lz4js": "^0.2.0",
        "@types/lz4js": "^0.2.1"
        // ...
    },
    ```

3. 命令行使用工具生成仓颉封装层

   进入到仓颉sdk的工具的bin目录，如果是windows平台，那么执行命令：

    ```sh
    .\hle.exe -j /path/to/tools/dtsparser/analysis.js -i /path/to/index.d.ts --lib --module-name lz4cj -o /path/to/output
    ```

    - -j参数指定分析ArkTS源码的分析文件的路径
    - -i参数指定.d.ts或者.d.ets文件的绝对路径
    - --lib参数执行生成的是ArkTS三方库的仓颉胶水代码
    - --module-name参数指定生成的仓颉包名
    - -o参数指定仓颉胶水层代码的生成目录
