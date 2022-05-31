# iOS Energy Efficiency And Thermal Problem

## Energy Efficiency

### Energy Essertials

#### Fundamental Concepts

1. CPU. The CPU is a major consumer of energy. It should do so wisely—by doing work only when necessary through batching, scheduling, and prioritizing.
2. Device wake
3. Networking operations. Most iOS apps perform networking operations. When networking occurs, components such as cellular radios and Wi-Fi power up and use energy. By batching and reducing transactions, compressing data, and appropriately handling errors, your app can make significant contributions to energy conservation.
4. Graphics, animations, and video. Every time your app’s content updates on screen, it uses energy to produce those pixels. Animations and videos can be especially taxing. Unexpected and unnecessary content updates also drain power. Your app should avoid updating content when its interface isn’t visible to the user. 
5. Location. Many apps make location requests in order to log a user’s physical activity or provide environment-based alerts. Energy use increases with greater precision and longer location requests. Your app should reduce accuracy and duration of location activity whenever possible. Stop location requests when no longer needed.
6. Motion Continuous unwarranted requests for accelerometer, gyroscope, magnetometer, and other motion data waste energy. Request motion updates only when necessary, and stop updates when data is no longer needed.
7. Bluetooth. High periods of Bluetooth activity can drain the battery of the iOS device and the Bluetooth device. Whenever possible, batch and buffer Bluetooth activity, and reduce polling for data.

#### CPU Usage and Power Draw
provides a rough comparison of varying CPU usage against an idle state.

##### Example of idle vs. CPU power draw
State | Times
---- | ----
Idle | 10x greater power draw over sleep
1% CPU use | 10% greater power draw over idle
10% CPU use | 2x power draw over idle
100% CPU use | 10x power draw over idle

#### Fixed Cost and Dynamic Cost
Tasks your app performs have a dynamic cost—how much energy your app uses by doing actual work. They also have a fixed cost—how much energy is used by bringing the system and various resources up in order for your app to do work, and back down after that work is complete. When lots of sporadic work is occurring, there are dynamic costs and a significant fixed cost too, as resources may never get the chance to reach true idle between the sporadic tasks. This situation results in a lot of energy being used for a relatively small amount of actual work.

![](https://developer.apple.com/library/archive/documentation/Performance/Conceptual/EnergyGuide-iOS/Art/2-2_fixed-vs-dynamic-energy-cost_2x.png)

#### Trading Dynamic Cost for Fixed Cost
Your app can avoid sporadic work by batching tasks and performing them less frequently. For example, instead of performing a series of sequential tasks on the same thread, distribute those same tasks simultaneously across multiple threads, as shown in Figure 2-3. Each time the CPU is accessed, memory, caches, buses, and so forth must be powered up. By batching activity, components can be powered up once and used over a shorter period of time.

![](https://developer.apple.com/library/archive/documentation/Performance/Conceptual/EnergyGuide-iOS/Art/2-3_multi-threading-power_2x.png)

### Reduce and Prioritize Work
#### Work Less in the Background

Resolving Runaway Background App Crashes
iOS employs a CPU Monitor that watches background apps for excessive CPU usage and terminates them if they fall outside of certain limits. Most apps performing normal background activity should never encounter this situation. Example of an Excess CPU Usage Crash Log Entry

1. Exception Type: EXC_RESOURCE
2. Exception Subtype: CPU_FATAL
3. Exception Message: (Limit 80%) Observed 89% over 60 seconds

#### Prioritize Work with Quality of Service Classes

Primary QoS classes (shown in order of priority)

QoS Class | Type of work and focus of QoS | Duration of work to be performed
---- | ---- | ----
User-interactive | Work that is interacting with the user, such as operating on the main thread, refreshing the user interface, or performing animations. If the work doesn’t happen quickly, the user interface may appear frozen. Focuses on responsiveness and performance. | Work is virtually instantaneous.
User-initiated | Work that the user has initiated and requires immediate results, such as opening a saved document or performing an action when the user clicks something in the user interface. The work is required in order to continue user interaction. Focuses on responsiveness and performance. | Work is nearly instantaneous, such as a few seconds or less.
Utility | Work that may take some time to complete and doesn’t require an immediate result, such as downloading or importing data. Utility tasks typically have a progress bar that is visible to the user. Focuses on providing a balance between responsiveness, performance, and energy efficiency. | Work takes a few seconds to a few minutes.
Background | Work that operates in the background and isn’t visible to the user, such as indexing, synchronizing, and backups. Focuses on energy efficiency. | Work takes significant time, such as minutes or hours.

#### Minimize Timer Use

1.The High Cost of Timers

* Apps use timers to poll for state changes when they should respond to events instead.
* Other apps use timers as synchronization tools when they should use semaphores or other locks to achieve the greatest efficiency. 
* Some timers are executed without suitable timeouts, causing them to continue firing when they’re no longer needed.

2. Get Event Notifications Without Using Timers
3. If You Must Use a Timer, Employ It Efficiently
4. Specify Suitable Timeouts
5. Invalidate Repeating Timers You No Longer Need
6. Specify a Tolerance for Batching Timers Systemwide

#### Minimize I/O

1. Minimize data writes
2. Avoid accessing memory too frequently
3. Read and write data sequentially whenever possible
4. Read and write larger blocks of data from files whenever possible, keeping in mind that reading too much data at once might cause other problems.
5. For reading or writing significant amounts of data, consider using dispatch_io
6. f your data consists of structured content that is randomly accessed, store it in a database
7. Understand how the system caches file data and know how to optimize the use of those caches

#### React to Low Power Mode on iPhones

Users who wish to prolong their iPhone’s battery life can enable Low Power Mode under Settings > Battery. In Low Power Mode, iOS conserves battery life by enacting certain energy-saving measures. For example, the system may:

* Reduce CPU and GPU performance
* Pause discretionary and background activities, including networking
* Reduce screen brightness
* Reduce the timeout for auto-locking the device
* Disable Mail fetch
* Disable motion effects
* Disable animated wallpapers

Your app can register to receive notifications when the power state (Low Power Mode is enabled or disabled) of the device changes.


### Minimize and Defer Networking

#### Energy and Networking

1. Device Networking Overhead

	Networking hardware, such as cellular and Wi-Fi radios, are powered down by default to conserve battery

	![Example of overhead due to recurring network activity](https://developer.apple.com/library/archive/documentation/Performance/Conceptual/EnergyGuide-iOS/Art/new_chart_2x.png)

2. Networking Variable Effect on Energy

1. Cellular network activity requires significantly more energy than activity over Wi-Fi.
2. Poor or fluctuating signal conditions may result in slower or problematic transactions, which must be retried.
3. Low network throughput (bandwidth) means radios have to stay on longer to perform transactions.
4. Even geographic location and choice of cellular provider can impact energy consumption, as signal conditions and throughput can vary.

#### Minimize Networking

1. Reduce Data Sizes
2. Reduce Media Quality and Size
3. Compress Data
4. Avoid Redundant Transfers
5. Cache Data
6. Use Pausable and Resumable Transactions

#### Handle Errors

Don’t attempt to perform network operations when the network is unavailable.

#### Check Signal Conditions

If network operations fail, use the SCNetworkReachability API to to see whether the host is available.

#### Provide an Escape Route

Don’t wait forever for a response from the server that never comes. Let the user cancel long-running or stalled network operations, and set appropriate timeouts so your app doesn’t keep connections open needlessly.

#### Use Retry Policies

If a transaction fails, try again when the network becomes available.

### Defer Networking

1. Batch Transactions

	* If your app streams video, download the entire file (or a large portion of the file) at once instead of requesting it in small pieces.
	* If your app serves ads, download several at once and show them over a period of time, rather than downloading them as needed.
	* If your app downloads email from a server, download multiple messages at once. Assume that the user will probably read most of them, rather than downloading each one individually as the user selects it.

2. Delay Deferrable Network Operations

	For upload and download activities over HTTP, the NSURLSession API provides the ability to create deferrable background sessions. A background session lets your app send URL requests to the system, which performs them at an optimal time and notifies your app when they are complete

	To use deferrable background sessions:
	
	* Configure Background Session Options
	* Restrict the Background Session to only Wi-Fi
	* Adjust Scheduling Tolerance for the Background Session
	* Create a Background Session Object
	* Add a URL Request to the Background Session
	* Get Notified About Background Session Activity

### Use Graphics, Animations, and Video Efficiently

* Avoid Extraneous Graphics and Animations
* Restrict UI When Playing Full-Screen Video

### Optimize Location and Motion

* Reduce Location Accuracy and Duration
* Reduce the Frequency of Motion Updates

### Monitor Energy Use

#### Measure Energy Impact with Xcode

There’s no better time to diagnose your app’s energy footprint than when you are in the process of developing your app. Xcode includes a number of features that can help.

1. Debugging Gauges
	* Energy impact gauge
	* CPU gauge
	* Disk usage gauge
	* Network usage gauge

#### Measure Energy Impact with Instruments

* Activity Monitor Profiling Template. Use this template to monitor overall CPU, disk I/O, and network usage.
* Core Animation Profiling Template. Use this template to measure graphics performance and CPU usage. Enable the Flash Updated Regions setting of the template’s Core Animation instrument to see each screen update occurring in your app and watch for unnecessary or unexpected updates.
* GPU Driver Profiling Template. Use this template to measure GPU driver statistics and sample active CPU usage.
* Location Energy Instrument. Use this instrument to measure the energy impact and duration of requests to Core Location.
* Metal System Trace Profiling Template. Use this template to measure the performance of iOS Metal applications by tracing information from the application, driver, and GPU layers.
* Network Profiling Template. Use this template to analyze the TCP/IP and UDP/IP connections your app uses.
* Time Profiler Profiling Template. Use this template to perform low-overhead time-based sampling of running processes. Time Profiler watches the running threads in your app and takes samples at regular intervals. A complete backtrace is collected for each sample, allowing you to drill down into a sample to find exactly where in your code large amounts of time are being spent.
* Your Custom Template Here.


## Thermal Problem

### What is a thermal problem

1. As the heat increases, the system decreases heat by reducing the speed of the processors. 
2. If running the app make the device hot or even burning hot then the user will refuse to use the app. 

### How to solve the thermal problem

1. iOS 11 has the thermalState API in ProcessInfo class. 
	
	Thermal state indicates the level of heat generated by logic components as they run apps. Optimize your app’s performance by monitoring the thermal state and reducing system usage as the thermal state increases. 

2. The following items will aspect the thermal problem
	
	* Overhead - represents energy use as a result of bringing up radios and other system resources.
	* High CPU Utilization
	* Network And Bluetooth Activity
	* Location Activity
	* High GPU Utilization
	* Display Utilization

### NSProcessInfo

NSProcessInfo provides the following property and notification to monitor the thermal changes

#### NSProcessInfoThermalState

The API thermalState is available since iOS 11, it's a enum and has four values

* Nominal - The thermal state is within normal limits.
* Fair - Recommendation: Defer non-user-visible activity.
* Serious - System performance may be impacted. Recommendation: reduce application's usage of CPU, GPU and I/O, if possible. Switch to lower quality visual effects, reduce frame rates.
* Critical - System performance is significantly impacted and the system needs to cool down. Recommendation: reduce application's usage of CPU, GPU, and I/O to the minimum level needed to respond to user actions. Consider stopping use of camera and other peripherals if your application is using them.

#### NSProcessInfoThermalStateDidChangeNotification

We can use this notification to monitor the thermal changes.

### Analyze Huajiao app energy utilization

Using iPhone X gets the following Energy Impact gauge

App home page

![](https://github.com/PeterLu7799/documents/blob/master/energy_impact/home_page.png?raw=true)

As compare a sample demo app home page (a view with few UIControls)

![](https://github.com/PeterLu7799/documents/blob/master/energy_impact/other_app.png?raw=true)

App goes live

![](https://github.com/PeterLu7799/documents/blob/master/energy_impact/start_live.png?raw=true)

App goes live after 3 mintues, thermal state is fair

![](https://github.com/PeterLu7799/documents/blob/master/energy_impact/live_fair_3min.png?raw=true)

App goes live after 8 mintues, thermal state is serious

![](https://github.com/PeterLu7799/documents/blob/master/energy_impact/live_serious_8min.png?raw=true)

App's CPU gauge when going live

![](https://github.com/PeterLu7799/documents/blob/master/energy_impact/cpu-normal.png?raw=true)

App started linkmic

![](https://github.com/PeterLu7799/documents/blob/master/energy_impact/linkmic.png?raw=true)

### Analyze Huajiao Goes Live CPU, GPU and I/O Utilization via Instruments

1. CPU utilization

Using Instruments' Time profile to see 

2. GPU utilization

3. I/O utilization 


### How fix the thermal problem

## References

[Energy Efficiency Guide for iOS Apps](https://developer.apple.com/library/archive/documentation/Performance/Conceptual/EnergyGuide-iOS/MinimizeTimerUse.html#//apple_ref/doc/uid/TP40015243-CH41-SW1)、

[Analyzing the Performance of Your Shipping App
](https://developer.apple.com/documentation/xcode/analyzing-the-performance-of-your-shipping-app)

[Instruments Help](https://help.apple.com/instruments/mac/current/)

[Test under adverse device conditions (iOS)
](https://help.apple.com/xcode/mac/current/#/dev308429d42)

[NSProcessInfo](https://developer.apple.com/documentation/foundation/nsprocessinfo?language=objc)

[An overview of the time profiler in Instruments
](https://augmentedcode.io/2021/05/24/an-overview-of-the-time-profiler-in-instruments/)