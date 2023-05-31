# iOS崩溃问题处理


## iOS有如下两种崩溃
1. 一种是程序运行引起的崩溃，卡死有标准的崩溃日志 
2. 一种内存不足引起的崩溃，没有标准日志有jetsam event report

## 崩溃日志
![](https://docs-assets.developer.apple.com/published/eeb9b57faffdc4950af93d82c9becaa6/examining-the-fields-in-a-crash-report-1~dark@2x.png)
崩溃日志是解决崩溃的关键所以要先得到崩溃日志，有了日志后我们要符号化日志这样才能开始分析。崩溃日志分以下几个部分

### 头部
![](https://github.com/PeterLu7799/documents/blob/master/CrashReport/crash_report_header.png?raw=true)

* Incident Identifier: 报告的唯一标识符。 两份报告有不同的标识符
* CrashReporter Key: 一个匿名的设备标识符。 来自同一台设备的两份报告包含相同的值
* Hardware Model: 设备型号
* Process: 崩溃app的文件名称与app信息属性列表中的CFBundleExecutable值相匹配，括号中的数字是进程ID
* Path: app文件在磁盘上的位置
* Identifier: app的bundleID：CFBundleIdentifier
* Version: app的CFBundleVersion和CFBundleShortVersionString的组合
* Code Type: app的CPU架构
* Role: 崩溃时分配给进程的task_role，不用关心
* Parent Process: 启动崩溃进程的进程的名称和进程ID（在方括号中）
* Coalition: 包含应用程序的进程联盟的名称，不用关心
* Date/Time: 崩溃时间
* Launch Time: app启动时间
* OS Version: iOS版本

### 异常信息

### 调用堆栈


	Jetsam event reports
	
    1. How many type of crashing
    2. Describe crash
    3. Describe deadlock
    4. Describe OOM
    5. single device high crashes

    
    
## APM introduction
    1. first fix the foreground issues

    
## Case Study
    1. Player disable recording by default
    2. Update SDWebImage
    3. Close Qdas crashing report
    4. Fixed danmu stuck 

    
## Tips
    1. New OS will have new crash for example iOS 16
    2. Crashing feedback from user 
    3. ignoring 1 device more crashings


SIGABRT--程序中止命令中止信号
SIGALRM--程序超时信号
SIGFPE--程序浮点异常信号
SIGILL--程序非法指令信号
SIGHUP--程序终端中止信号
SIGINT--程序键盘中断信号
SIGKILL--程序结束接收中止信号
SIGTERM--程序kill中止信号
SIGSTOP--程序键盘中止信号　
SIGSEGV--程序无效内存中止信号
SIGBUS--程序内存字节未对齐中止信号
SIGPIPE--程序Socket发送失败中止信号



https://developer.apple.com/documentation/xcode/addressing-watchdog-terminations
