# hilog  

HiLog is a logging system provided for system frameworks, services, and applications to print logs, record user operations, and track system runtime status. Developers can query relevant log information through the hilog command-line interface.  

## Environment Requirements  

- Complete [environment preparation](./cj-hdc.md#environment-preparation) as per the hdc command-line tool guide.  
- Ensure the device is properly connected and execute `hdc shell`.  

## Command-Line Specifications  

| Short Option | Long Option      | Parameter          | Description |  
| ------------ | ---------------- | ------------------ | ----------- |  
| -h           | --help           | -                  | Help command. |  
| Default      | Default          | -                  | Blocking log read, does not exit. |  
| -x           | --exit           | -                  | Non-blocking log read, exits after reading. |  
| -g           | -                | -                  | Query buffer size. Used with -t to specify a log type (default: app and core). |  
| -G           | --buffer-size    | &lt;size&gt;      | Set buffer size for specified &lt;type&gt;. Used with -t (default: app and core). Units: B/K/M. Range: 64K-16M. |  
| -r           | -                | -                  | Clear buffer logs. Used with -t to specify a type (default: app and core). |  
| <!--DelRow-->-p | --privacy       | &lt;on/off&gt;    | Enable/disable privacy control for system debugging logs. |  
| <!--DelRow--> |                | on                | Enable privacy, display &lt;private&gt;. |  
| <!--DelRow--> |                | off               | Disable privacy, display plaintext. |  
| -k           | -                | &lt;on/off&gt;    | Kernel log read control. |  
|              |                  | on                | Enable kernel log reading. |  
|              |                  | off               | Disable kernel log reading. |  
| -s           | --statistics     | -                  | Query statistics. Requires -t or -D. |  
| -S           | -                | -                  | Clear statistics. Requires -t or -D. |  
| -Q           | -                | &lt;control-type&gt; | Flow control quota switch. |  
|              |                  | pidon             | Enable process flow control. |  
|              |                  | pidoff            | Disable process flow control. |  
|              |                  | domainon          | Enable domain flow control. |  
|              |                  | domainoff         | Disable domain flow control. |  
| -L           | --level          | &lt;level&gt;     | Filter logs by level (e.g., -L D/I/W/E/F). |  
| -t           | --type           | &lt;type&gt;      | Filter logs by type (e.g., -t app/core/init/only_prerelease). `app` for application logs, `core` for system logs, `init` for boot logs, `only_prerelease` for pre-release system logs (irrelevant to app developers). |  
| -D           | --domain         | &lt;domain&gt;    | Filter logs by domain. |  
| -T           | --tag            | &lt;tag&gt;       | Filter logs by tag. |  
| -a           | --head           | &lt;n&gt;         | Display first &lt;n&gt; lines of logs. |  
| -z           | --tail           | &lt;n&gt;         | Display last &lt;n&gt; lines of logs. |  
| -P           | --pid            | &lt;pid&gt;       | Filter logs by process ID. |  
| -e           | --regex          | &lt;expr&gt;      | Print logs matching the regex &lt;expr&gt;. |  
| -f           | --filename       | &lt;filename&gt;  | Set log dump filename. |  
| -l           | --length         | &lt;length&gt;    | Set log dump file size (≥64K). |  
| -n           | --number         | &lt;number&gt;    | Set number of log dump files. |  
| -j           | --jobid          | &lt;jobid&gt;     | Set log dump task ID. |  
| -w           | --write          | &lt;control&gt;   | Log dump task control. |  
|              |                  | query             | Query dump tasks. |  
|              |                  | start             | Start dump task (params: filename, file size, algorithm, rotate count). |  
|              |                  | stop              | Stop dump task. |  
|              |                  | refresh           | Flush buffer logs to dump file. |  
|              |                  | clear             | Delete dumped log files. |  
| -m           | --stream         | &lt;algorithm&gt; | Log dump compression control. |  
|              |                  | none              | No compression. |  
|              |                  | zlib              | Zlib compression (.gz). |  
|              |                  | zstd              | Zstd compression (.zst). |  
| -v           | --format         | &lt;format&gt;    | Log display format. |  
|              |                  | time              | Show local time. |  
|              |                  | color             | Color-coded by level (default: monochrome). |  
|              |                  | epoch             | Show time since 1970. |  
|              |                  | monotonic         | Show time since boot. |  
|              |                  | usec              | Show microsecond precision. |  
|              |                  | nsec              | Show nanosecond precision. |  
|              |                  | year              | Add year to timestamp. |  
|              |                  | zone              | Add timezone to timestamp. |  
|              |                  | wrap              | Omit timestamp prefix for wrapped lines. |  
| -b           | --baselevel      | &lt;loglevel&gt;  | Set minimum log level (D/I/W/E/F). |  

## Common Commands  

### View Help  

```shell  
hilog -h  
```  

**Example:**  

```shell  
$ hilog -h  
Usage:  
-h --help  
Show all help information.  
Show single help information with option:  
query/clear/buffer/stats/persist/private/kmsg/flowcontrol/baselevel/domain/combo  
Querying logs options:  
No option performs a blocking read and keeps printing.  
-x --exit  
   Performs a non-blocking read and exits when all logs in buffer are printed.  
-a <n>, --head=<n>  
   Show n lines logs on head of buffer.  
-z <n>, --tail=<n>  
   Show n lines logs on tail of buffer.  
```  

### Non-Blocking Log Read  

```shell  
hilog -x  
```  

**Example:**  

```shell  
$ hilog -x  
11-15 15:51:02.087  2823  2823 I A01B05/com.ohos.sceneboard/AOD: AodClockFullScreen --> timeTextLineHeight:313.3333333333333 clockMarginTop:99  
11-15 15:51:02.087  2823  2823 I A01B05/com.ohos.sceneboard/AOD: AodClockFullScreen --> timeFontSize:114.48717948717947  
11-15 15:51:02.090  2823  2823 I A01B05/com.ohos.sceneboard/AOD: AodClockFullScreen --> timeTextWidth:202,timeTextHeight:292  
11-15 15:51:02.100  2823  2823 I A01B05/com.ohos.sceneboard/AOD: ComponentUtil --> Component(ComponentId-AodClockNumber) draw complete.  
11-15 15:51:02.110  1197  1197 E C01406/render_service/OHOS::RS: [LoadImgsbyResolution] Can't find resolution (1084 x 2412) in config file  
11-15 15:51:02.127  1197  1197 E C01406/render_service/OHOS::RS: [LoadImgsbyResolution] Can't find resolution (1084 x 2412) in config file  
```  

### Query Buffer Size  

```shell  
hilog -g  
```  

**Example:**  

```shell  
$ hilog -g  
Log type app buffer size is 16.0M  
Log type init buffer size is 16.0M  
Log type core buffer size is 16.0M  
Log type only_prerelease buffer size is 16.0M  
```  

### Modify Buffer Size  

```shell  
hilog -G size  
```  

**Example:**  

```shell  
$ hilog -G 16M  
Set log type app buffer size to 16.0M successfully  
Set log type init buffer size to 16.0M successfully  
Set log type core buffer size to 16.0M successfully  
Set log type only_prerelease buffer size to 16.0M successfully  
```  

### Clear Buffer Logs  

```shell  
hilog -r  
```  

**Example:**  

```shell  
$ hilog -r  
Log type core,app,only_prerelease buffer clear successfully  
```  

### Kernel Log Control  

```shell  
hilog -k on/off  
```  

**Example:**  

```shell  
$ hilog -k on  
Set hilogd storing kmsg log on successfully  
$  
$ hilog -k off  
Set hilogd storing kmsg log off successfully  
```  

### Query Statistics  

```shell  
hilog -s  
```  

**Example:**  

```shell  
$ param set persist.sys.hilog.stats true  
Set parameter persist.sys.hilog.stats true success  
$ reboot  
$ hilog -s  
Log statistic report (Duration: 0h0m32s.564, From: 11-15 16:04:08.628):  
Total lines: 137517, length: 8.0M  
Debug lines: 0(0%), length: 0.0B(0%)  
Info lines: 101795(74%), length: 6.1M(76%)  
Warn lines: 10268(7.5%), length: 719.9K(8.8%)  
Error lines: 25452(19%), length: 1.2M(15%)  
Fatal lines: 2(0.0015%), length: 259.0B(0.0031%)  
------------------------------------------------------------  
Domain Table:  
LOGTYPE- DOMAIN---- TAG----------------------------- MAX_FREQ-- TIME---------------- MAX_TP---- TIME---------------- LINES----- LENGTH---- DROPPED---  
app----- 0xf00----- -------------------------------- 924.00---- 11-15 16:04:25.594-- 111975.00- 11-15 16:04:25.594-- 3386------ 371.5K---- 0---------  
app----- 0x0------- -------------------------------- 285.00---- 11-15 16:04:34.877-- 44242.00-- 11-15 16:04:34.877-- 990------- 129.2K---- 0---------  
```  

**Statistics Explanation:**  

```shell  
MAX_FREQ: Highest log frequency (lines/sec)  
TIME:    Timestamp of occurrence  
MAX_TP:  Highest throughput (bytes/sec)  
LINES:   Total lines in the period  
LENGTH:  Total bytes in the period  
DROPPED: Dropped lines in the period  
```  

### Clear Statistics  

```shell  
hilog -S  
```  

**Example:**  

```shell  
$ hilog -S  
Statistic info clear successfully  
```  

### Process Flow Control  

```shell  
hilog -Q pidon/pidoff  
```  

**Example:**  

```shell  
$ hilog -Q pidon  
Set flow control by process to enabled successfully  
$  
$ hilog -Q pidoff  
Set flow control by process to disabled successfully  
```  

### Domain Flow Control  

```shell  
hilog -Q domainon/domainoff  
```  

**Example:**  

```shell  
$ hilog -Q domainon  
Set flow control by domain to enabled successfully  
$  
$ hilog -Q domainoff  
Set flow control by domain to disabled successfully  
```  

### Filter Logs by Level  

```shell  
hilog -L D/I/W/E/F  
```  

**Example:**  

```shell  
$ hilog -L E  
08-28 09:01:25.730  2678  2678 E A00F00/com.aidataservice/AiDataService_5.10.7.320: DataChangeNotifyManager: notifyDataChange CommonEntity no valid entity to notify  
08-28 09:01:56.058  8560  8560 E A00500/com.ohos.settingsdata/SettingsData: DB not ready request = datashare:///com.ohos.settingsdata/entry/settingsdata/SETTINGSDATA?Proxy=true&key=analysis_service_switch_on , retry after DB startup  
08-28 09:01:56.082  8560  8560 E A00500/com.ohos.settingsdata/SettingsData: decoder failure: /data/migrate/settings_global.xml , error code:-1  
08-28 09:01:56.082  8560  8560 E A00500/com.ohos.settingsdata/SettingsData: clearXml failed:No such file or directory, error code:13900002  
08-28 09:01:56.083  8560  8560 E A00500/com.ohos.settingsdata/SettingsData: readText failed:No such file or directory, error code:13900002  
08-28 09:01:56.371  8586  8586 E A00500/com.ohos.settingsdata/SettingsData: DB not ready request =    datashare:///com.ohos.settingsdata/entry/settingsdata/SETTINGSDATA?Proxy=true&key=photo_network_connection_status , retry after DB startup  
08-28 09:01:56.408  8586  8586 E A00500/com.ohos.settingsdata/SettingsData: decoder failure: /data/migrate/settings_global.xml , error code:-1  
```  

### Filter Logs by Type  

```shell  
hilog -t app  
```  

**Example:**  

```shell  
$ hilog -t app  
11-15 16:04:45.903  5630  5630 I A0A5A5/os.hiviewcare:staticSubscriber/Diagnosis: [DetectionFilter]820001084: switch off  
11-15 16:04:45.905  5630  5630 I A0A5A5/os.hiviewcare:staticSubscriber/Diagnosis: [DetectionFilter]847005050: frequency limit  
11-15 16:04:45.905  5630  5630 I A0A5A5/os.hiviewcare:staticSubscriber/Diagnosis: [SmartNotifyHandler]detections after filter: []  
11-15 16:04:45.905  5630  5630 I A0A5A5/os.hiviewcare:staticSubscriber/Diagnosis: [SmartNotifyHandler]no detections to detect  
11-15 16:04:45.924  5687  5687 I A01B06/common/KG: MetaBalls-SystemTopPanelController --> init charging status = 3  
```  

### Filter Logs by Domain  

```shell  
hilog -D 01B06  
```  

**Example:**  

```shell  
$ hilog -D 01B06  
11-15 16:04:54.981  5687  5687 I A01B06/common/KG: MetaBalls-MetaBallRenderer --> pressTime = 0 appearTime = 1731657885972  
11-15 16:04:54.981  5687  5687 I A01B06/common/KG: MetaBalls-MetaBallRenderer --> backAnimator on finish  
11-15 16:04:54.982  5687  5687 I A01B06/common/KG: MetaBalls-MetaBallRenderer --> setTimeout over 9s and begin animate on finish  
11-15 16:04:55.297  5687  5687 I A01B06/common/KG: MetaBalls-MetaBallRenderer --> chargingTextExitAnimation onFinish  
11-15 16:04:55.494  5687  5687 I A01B06/common/KG: MetaBalls-MetaBallRenderer --> uiExtension session send data success,type: exitAnimationFinish  
```  

### Filter Logs by Tag  

```shell  
hilog -T tag  
```  

**Example:**  

```shell  
$ hilog -T SAMGR  
08-28 09:27:59.581   610 11504 I C01800/samgr/SAMGR: CommonEventCollect save extraData 1661  
08-28 09:27:59.581   610 11504 I C01800/samgr/SAMGR: OnReceiveEvent get action: usual.event.BATTERY_CHANGED code: 0, extraDataId 1661  
08-28 09:27:59.582   610 11504 I C01800/samgr/SAMGR: DoEvent:4 name:usual.event.BATTERY_CHANGED value:0  
08-28 09:27:59.582   610 11504 W C01800/samgr/SAMGR: LoadSa SA:10120 AddDeath fail,cnt:1,callpid:610  
08-28 09:27:59.583   610 11504 I C01800/samgr/SAMGR: LoadSa SA:10120 size:1,count:1  
08-28 09:27:59.601   610 11504 I C01800/samgr/SAMGR: Scheduler SA:10120 loading  
08-28 09:27:59.965 11518 11518 I C01800/media_analysis_service/SAMGR: SA:10120 OpenSo spend 315ms  
08-28 09:27:59.965   610  4064 I C01800### View and Configure Log Persistence Tasks

```shell
hilog -w control
```

> **Note:**
>
> Query current task: hilog -w query  
> Start hilog persistence task with 1000 log files: hilog -w start -n 1000  
> Start kmsglog persistence task with 100 log files: hilog -w start -n 100 -t kmsg  
> Stop current persistence task: hilog -w stop  
> Start kmsglog persistence task with custom rules (compression methods: zlib, zstd, none). Example configuration: filename=kmsglog, size=2M, count=100 files, zlib compression. Command: hilog -w start -t kmsg -f kmsglog -l 2M -n 100 -m zlib  

**Usage Examples:**

```shell
$ hilog -w query
Persist task query failed
No running persistent task [CODE: -63]
$
$ hilog -w start -n 1000
Persist task [jobid:1][fileNum:1000][fileSize:4194304] start successfully
$
$ hilog -w start -n 100 -t kmsg
Persist task [jobid:2][fileNum:100][fileSize:4194304] start successfully
$
$ hilog -w stop
Persist task [jobid:1] stop successfully
Persist task [jobid:2] stop successfully
$
$ hilog -w start -t kmsg -f kmsglog -l 2M -n 100 -m zlib
Persist task [jobid:2][fileNum:100][fileSize:2097152] start successfully
```

### Configure Log Display Format

```shell
hilog -v time/color/epoch/monotonic/usec/nsec/year/zone/wrap
```

**Usage Examples:**

```shell
$ hilog -v time
11-15 16:36:21.027  1134  1723 I C02B01/riladapter_host/HrilExt: [NotifyToBoosterTel-(hril_manager_ext.cpp:440)] RilExt:Notify to booster tel finish
11-15 16:36:21.027  1134  1723 I C02B01/riladapter_host/HrilExt: [NotifyToBoosterNet-(hril_manager_ext.cpp:450)] RilExt: HNOTI_BOOSTER_NET_IND report to booster net
11-15 16:36:21.027  1134  1723 I C02B01/riladapter_host/HrilExt: [NotifyToBoosterNet-(hril_manager_ext.cpp:454)] RilExt: HNOTI_BOOSTER_NET_IND report to booster net finish
11-15 16:36:21.027  1134  1723 I P01FFF/riladapter_host/Rilvendor: CHAN [HandleUnsolicited] HandleUnsolicited done for modem:0, index:0, atResponse:^BOOSTERNTF: 3, 20,"0600100001000004000000000102A4FF0202F6FF"
11-15 16:36:21.802  2809  2831 E C02D06/com.ohos.sceneboard/XCollie: Send kick,foundation to hungtask Successful
11-15 16:36:21.911   882  3016 I C01F0B/telephony/TelephonyVSim: state machine ProcessEvent Id: 125
11-15 16:36:21.911   882  3016 I C01F0B/telephony/TelephonyVSim: StateProcess
$
$ hilog -v nsec
11-15 16:37:09.010658555  1134  1723 I C02B01/riladapter_host/HrilExt: [BoosterRawInd-(hril_booster.cpp:296)] RilExt: BoosterRawInd
11-15 16:37:09.010676263  1134  1723 I C02B01/riladapter_host/HrilExt: [BoosterRawInd-(hril_booster.cpp:328)] check need notify to satellite:indType 6
11-15 16:37:09.010800221  1134  1723 I C02B01/riladapter_host/HrilExt: [NotifyToBoosterTel-(hril_manager_ext.cpp:436)] RilExt: report to telephony ext, requestNum: 4201
11-15 16:37:09.011011680  1134  1723 I C02B01/riladapter_host/HrilExt: [NotifyToBoosterTel-(hril_manager_ext.cpp:440)] RilExt:Notify to booster tel finish
11-15 16:37:09.011064805  1134  1723 I C02B01/riladapter_host/HrilExt: [NotifyToBoosterNet-(hril_manager_ext.cpp:450)] RilExt: HNOTI_BOOSTER_NET_IND report to booster net
11-15 16:37:09.011200742  1134  1723 I C02B01/riladapter_host/HrilExt: [NotifyToBoosterNet-(hril_manager_ext.cpp:454)] RilExt: HNOTI_BOOSTER_NET_IND report to booster net finish
```

### View and Configure Log Levels

```shell
// Default global log level is Info. Query global log level:
param get param get hilog.loggable.global

// Set global log level:
hilog -b D/I/W/E/F

// Set printable log level for [DOMAINID]:
hilog -b D/I/W/E/F -D [DOMAINID]

// Set printable log level for [TAG]:
hilog -b D/I/W/E/F -T [TAG]

// Set persistent global log level (survives reboot):
hilog -b D/I/W/E/F --persist
```

**Usage Examples:**

```shell
$ param get hilog.loggable.global
I

$ hilog -b E
Set global log level to E successfully

$ hilog -b D -D 0x2d00
Set domain 0x2d00 log level to D successfully

$ hilog -b E -T testTag
Set tag testTag log level to E successfully
```

<!--Del-->
### Privacy Toggle

```shell
hilog -p on/off
```

**Usage Examples:**

```shell
# hilog -p on
Set hilog privacy format on successfully
#
# hilog -p off
Set hilog privacy format off successfully
```

<!--DelEnd-->