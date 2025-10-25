# Application File Upload and Download

Applications can upload files to a web server or download network resource files to the local application file directory.

## Uploading Application Files

Developers can use the upload interface of the upload-download module ([ohos.request](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-request-agent.md)) to upload local files. The file upload process is completed using a system service proxy, which supports custom proxy address configuration.

> **Note:**
>
> Currently, the file upload functionality only supports uploading files from the application cache directory (cacheDir).
>
> To use the upload-download module, refer to [Permission Declaration](../../security/AccessToken/cj-declare-permissions.md): ohos.permission.INTERNET.

The following example demonstrates how to upload a file from the application cache directory to a web server:

<!-- compile -->

```cangjie
// pages/xxx.cj
import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.BasicServicesKit.{State as RState, Filter as RFilter, Action as RAction, Progress as RProgress, remove as rRemove}

func Upload(): Unit {
    // Get application file path
    let UiStageContext = Global.abilityContext
    let DefaultSandBoxCache = "/data/storage/el2/base/haps/entry/cache"
    // Create a new local application file
    let filePath = "${DefaultSandBoxCache}/test.txt"
    let file = FileIo.open(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    FileIo.write(file.fd, "hello world")
    FileIo.fdatasync(file.fd)
    let randomAccessFile = FileIo.createRandomAccessFile(file)
    randomAccessFile.close()
    let responseCallback = ProgressCallback()

    let fileSpec = FileSpec(
        "./test.txt",
        filename: "test.txt",
        mimeType: "application/octet-stream"
    )
    let attachments = ConfigData.FormItems([
        FormItem(
            "taskOnTest",
            FormItemValue.FileItem(fileSpec)
        )
    ])

    let uploadConfig = Config(
        RAction.Upload,
        "http://xxx",
        title: "taskOnTest",
        mode: Mode.Foreground,
        description: "Sample code for event listening",
        overwrite: false,
        method: "POST",
        data: attachments,
        saveas: "./",
        network: Network.Cellular,
        metered: false,
        roaming: true,
        retry: true,
        redirect: true,
        index: 0,
        begins: 0,
        ends: -1,
        gauge: false,
        precise: false,
        token: "it is a secret"
    )
    let task = create(UiStageContext, uploadConfig)
    task.on(EventCallbackType.Progress, responseCallback)
    task.start()
}

public class ProgressCallback <: Callback1Argument<RProgress> {
    public ProgressCallback() {}

    public open func invoke(err: ?BusinessException, arg: RProgress): Unit {
        Hilog.info(0, "CangjieTest", "ProgressCallback Invoke")
    }
}
```

## Downloading Network Resource Files to Application Directory

Developers can use the download interface of the upload-download module ([ohos.request](../../../../en/application-dev/reference/BasicServicesKit/cj-apis-request-agent.md)) to download network resource files to the application directory. For downloaded files, developers can access them using basic file I/O interfaces ([ohos.file_fs](../../../../en/application-dev/reference/CoreFileKit/cj-apis-file_fs.md)), following the same approach as [Application File Access](../../file-management/cj-app-file-access.md). The download process uses a system service proxy, supporting custom proxy address configuration.

> **Note:**
>
> Currently, network resource files can only be downloaded to the application directory.
>
> To use the upload-download module, refer to [Permission Declaration](../../security/AccessToken/cj-declare-permissions.md): ohos.permission.INTERNET.

The following example demonstrates how to download a network resource file to the application directory:

<!-- compile -->

```cangjie
// pages/xxx.cj
// Download network resource file to application directory
import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.BasicServicesKit.{State as RState, Filter as RFilter, Action as RAction, Progress as RProgress, remove as rRemove}
import std.time.*
import std.collection.*
import std.runtime.*
import std.sync.*

// Download function
func Download(): Unit {
    // Get application file path
    let UiStageContext = Global.abilityContext
    let DefaultSandBoxCache = "/data/storage/el2/base/haps/entry/cache"
    let fileName = "test.txt"
    let filePath = "${DefaultSandBoxCache}/${fileName}"

    // Download URL
    let fileURL = "https://xxx.txt"
    let responseCallback = HttpResponseCallback()

    let config = Config(
        RAction.Download,
        fileURL,
        saveas: fileName,
        headers: HashMap<String, String>([("headers", "http")]),
        metered: false,
        roaming: true,
        description: "download test",
        network: Network.AnyType,
        title: "download test title"
    )
    let task = create(UiStageContext, config)
    task.on(EventCallbackType.Response, responseCallback)

    task.start()
    requestWaitFor(Duration.second * 10) {
        =>
        let stat = FileIo.stat(filePath)
        let size = stat.size
        size > 0
    }
    // Check if file exists
    if (FileIo.access(filePath)) {
        // Delete file
        FileIo.unlink(filePath)
    }
    // End task
    rRemove(task.tid)
}

class HttpResponseCallback <: Callback1Argument<HttpResponse> {
    public HttpResponseCallback() {}
    public open func invoke(err: ?BusinessException, arg: HttpResponse): Unit {
        Hilog.info(0, "CangjieTest", "HttpResponse Invoke")
    }
}

public func requestWaitFor(timeout: Duration, condition: () -> Bool) {
    let monitor = Monitor()
    let conditionIsMet = AtomicBool(false)
    let checkerTimer = Timer.repeatDuring(timeout, Duration.Zero, Duration.millisecond * 500,
        {
            => if (condition()) {
                conditionIsMet.store(true)
                synchronized(monitor) {
                    monitor.notify()
                }
            }
        })
    let cancellerTimer = Timer.once(timeout) {
        => synchronized(monitor) {
            monitor.notify()
        }
    }
    synchronized(monitor) {
        monitor.wait()
    }

    checkerTimer.cancel()
    cancellerTimer.cancel()
}
```