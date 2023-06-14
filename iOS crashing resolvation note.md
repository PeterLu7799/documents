# iOS崩溃讲解


## iOS崩溃种类
1. 一种是程序运行引起的崩溃，卡死有标准的崩溃日志 
2. 一种内存不足引起的崩溃，没有标准日志有jetsam event report

### 崩溃日志
![](https://github.com/PeterLu7799/documents/blob/master/CrashReport/crash_overall.png?raw=true)
崩溃日志是解决崩溃的关键所以要先得到崩溃日志，有了日志后我们要符号化日志这样才能开始分析。崩溃日志分以下几个部分

#### 头部
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

#### 异常信息
![](https://github.com/PeterLu7799/documents/blob/master/CrashReport/crash_exception.png?raw=true)

* Exception Type：终止进程的Mach异常的名称以及括号中相应的 BSD 终止信号的名称
* Exception Codes：一个或多个64位十六进制数的有关异常的处理器特定信息，可以忽略此字段，操作系统在其他字段中将信息显示为可读的信息
* Exception Subtype：可读的异常代码
* Exception Message：可读的信息。
* Exception Note：不特定于一种异常类型的附加信息，可包含如下字段
	* EXC_CORPSE_NOTIFY，崩溃并非源自硬件陷阱，因为进程已被操作系统显式终止或调用了 abort() 的进程
	* SIMULATED（不是崩溃）进程没有崩溃，但操作系统可能随后请求终止进程
	* NON-FATAL CONDITION（不是崩溃）则进程不会终止，创建崩溃报告的问题不是致命的
* Termination Reason：操作系统终止进程时指定的退出原因，可以在此字段中找到的信息包括有关无效代码签名、缺少依赖库或访问没有目的字符串的隐私敏感信息的消息
* Triggered by Thread or Crashed Thread：引发崩溃的线程

##### 异常类型
* EXC_BREAKPOINT (SIGTRAP)：断点调试时异常退出引起的崩溃，Swift的崩溃也会用这个异常类型
* EXC_BAD_ACCESS. 访问无效或是非法的内存地址引起的崩溃
* EXC_CRASH (SIGABRT). 收到了SIGABRT信号引起崩溃，主要是调用了abort()函数，一些OC或是C++的语言异常会调用这个函数，当然还有一些别的情况。
* EXC_CRASH (SIGKILL) 操作系统结束了app，崩溃日志的异常信息栏中包含原因和异常号。
* EXC_CRASH (SIGQUIT). 一个进程让另一个退出，比如主app在扩展响应时间长时让其退出。
* EXC_GUARD. app违反了受保护资源的访问限制，多出现在文件访问上。
* EXC_RESOURCE. app超出了资源的使用限制
* EXC_ARITHMETIC. 崩溃线程进行了非法的算数运算，比如除0

更多介绍参考苹果文档：

[Understanding the exception types in a crash report](https://developer.apple.com/documentation/xcode/understanding-the-exception-types-in-a-crash-report#EXCBREAKPOINT-SIGTRAP-and-EXCBADINSTRUCTION-SIGILL)

##### 异常信号
* SIGABRT--程序中止命令中止信号
* SIGALRM--程序超时信号
* SIGFPE--程序浮点异常信号
* SIGILL--程序非法指令信号
* SIGHUP--程序终端中止信号
* SIGINT--程序键盘中断信号
* SIGKILL--程序结束接收中止信号
* SIGTERM--程序kill中止信号
* SIGSTOP--程序键盘中止信号　
* SIGSEGV--程序无效内存中止信号
* SIGBUS--程序内存字节未对齐中止信号
* SIGPIPE--程序Socket发送失败中止信号

#### 诊断信息
诊断信息很有用一定要注意分析理解，但是不是所有的崩溃都有诊断信息。下面是一些诊断信息的例子，

* Dispatch的queue使用不当引起的崩溃
![](https://github.com/PeterLu7799/documents/blob/master/CrashReport/crash_diagnostic1.png?raw=true)

* 线程卡顿Watchdog发起的崩溃
![](https://github.com/PeterLu7799/documents/blob/master/CrashReport/crash_diagnostic2.png?raw=true)
[Addressing watchdog terminations](https://developer.apple.com/documentation/xcode/addressing-watchdog-terminations)
* 内存访问引起的崩溃包含VM的使用信息
![](https://github.com/PeterLu7799/documents/blob/master/CrashReport/crash_diagnostic3.png?raw=true)

[Investigating memory access crashes](https://developer.apple.com/documentation/xcode/investigating-memory-access-crashes)

#### 调用堆栈
列出app崩溃时所有运行线程的调用栈。在出现语言异常时还会有Last Exception的调用栈。

![](https://github.com/PeterLu7799/documents/blob/master/CrashReport/crash_backtrace.png?raw=true)



注意几点
1. 调用栈执行顺序是从上到下


###	OOM日志（Jetsam event reports）
	
    

## 火山引擎APM介绍
### 火山崩溃分几类
1. 崩溃
2. 卡死
3. OOM

### 崩溃过滤怎么用好
1. 看最新版本的崩溃
2. 修复前台的崩溃

    
## 花椒案例

### 花椒降低崩溃的几个里程碑
1. Player disable recording by default
2. Update SDWebImage
3. Close Qdas crashing report
4. Fixed danmu stuck 
5. added memory capablities

    
### Tips
1. New OS will have new crash for example iOS 16
2. Crashing feedback from user 
3. ignoring 1 device more crashings
4. 少用线程






https://developer.apple.com/documentation/xcode/addressing-watchdog-terminations
