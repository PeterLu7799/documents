# iOS崩溃问题处理


## iOS有如下两种崩溃
1. 一种是程序运行引起的崩溃，卡死有标准的崩溃日志 
2. 一种内存不足引起的崩溃，没有标准日志有jetsam event report

## 崩溃日志
崩溃日志是解决崩溃的关键所以要先得到崩溃日志，有了日志后我们要符号化日志这样才能开始分析。崩溃日志分以下几个部分

### 头部


	*  exception code
	*  backtraces
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
