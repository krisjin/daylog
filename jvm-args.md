# Hotspot vm选项

**-XX:<+|->特证名称** 的Hotspot选项，表示开启或关闭某项特性或属性， +代表开启，-代表关闭   
**-XX:特征名称=<n>**  的选项表示需要带有数字，n即数字。一些控制属性大小值的数字后面还可以接后缀k、m、g,表示KB、MB、GB，其它带数字的选项则表示比率或百分比。


## -client
表示HotSpot VM把应用当成客户端类程序来优化。目前来说，该选项使HotSpot VM将运行时环境设置为 client JVM。 该选项应该在应用启动时使用，对这类应用程序而言，**内存占用是最重要的性能标准，远比吞吐量重要**。

## -server
表示HotSpot VM把应用程序当成服务器类来优化。该选项使HotSpot VM将运行时环境设置成 server JVM 。该选项适用于高吞吐量比启动时间和内存占用更重要的应用程序。

## -d64
加载64位的HotSpot VM,而不是默认的32位的HotSpot。64位的HotSpot可以设置更大的堆内存。-Xms和-Xmx小于32G时，该选项要与-XX:+UseComressedOops联合使用。Java6 Update23之后的HotSpot默认开启-XX:UseCompressedOops。

## -XX:UseCompressedOops
**开启压缩指针特性。** oops(Ordinary Object Pointer)是指普通对象指针，HotSpot VM内部以它来引用Java对象。   
     
Java引用的长度从32位增长到64位，这给64位JVM带来了性能的损失。长度的增加使得缓存行容纳的oops 变少了，CPU高速缓存的效率也因此降低。64位JVM上CPU高速缓存效率的降低常常导致64位JVM的性能比32位JVM降低8%-20%。  

开启-XX:UseCompressedOops,使得64位JVM不但有更大的堆，而且还有32位JVM的性能。有些Java应用在64位HotSpot VM上开启压缩指针后，性能比32位HotSpot更好。压缩指针之所以可以改善性能，是因为它可以将64位指针转换为相对于java堆基地址的32位偏移。   

如果Java堆超过了32位HotSpot VM的限制，但又不想牺牲性能，可以使用该选项。如果Java堆上限不超过32GB(-Xmx32g)时，应该使用该选项，不过上限大约为26GB(-Xmx26g)是的性能最好。

## -Xms<n>[g|m|k]
Java堆的初始和最小尺寸是新生代和老年代的总和。<n>是尺寸大小，【g|m|k】表示尺寸的单位GB、MB或KB。Java堆永远不会小-Xms设定的值。

如果-Xms小于-Xmx,Java堆的大小会依据应用的需要而扩展或缩减。Java堆的扩展或缩减需要FullGC,所以注重延迟或吞吐量的应用程序通常应把-Xms和-Xmx设置成相同的值。

## -Xmx<n>[g|m|k]
Java堆的最大尺寸是新生代和老年代的总和，Java堆永远不会超过-Xmx设定的值。如果-Xmx大于-Xms,Java堆的大小会依据应用的需要而扩展或缩减。Java堆的扩展或缩减需要FullGC,所以注重延迟或吞吐量的应用程序通常应把-Xmx和-Xms设置成相同的值。

## -XX:NewSize=<n>[g|m|k]
新生代的初始和最小尺寸，新生代大小永远不会小于这个值。  

如果-XX:NewSize小于 -XX:MaxNewSize,新生代的大小会依据应用的需要而扩展或缩减。新生代的扩展或缩减需要FullGC,所以注重延迟或吞吐量的应用程序通常把-XX:NewSize 和 -XX:MaxNewSize设置成相同的值。

## -XX:MaxNewSize=<n>[g|m|k]
新生的最大尺寸，新生代永远不会超过这个值。

如果-XX:MaxNewSize大于-XX:NewSize,新生代的大小会依据应用的需要而扩展或缩减，新生代的扩展或缩减需要FullGC,所以注重延迟或吞吐量的应用程序通常把-XX:MaxNewSize 和-XX:NewSize设置成相同的值。

## -Xmn<>[g|m|k]
同时设置新生代的初始、最小和最大尺寸，新生代的尺寸设定为这个值。如果期望-XX:NewSize和-XX:MaxNewSize设置成相同的值，这是一个便利的命令行选项。


## JVM虚拟机参数

### 堆大小设置
1. -Xms1024m  初始堆大小
2. -Xmx1024m  最大堆大小

### 永久代设置
1. -XX:PermSize  设置永久代初始大小
2. -XX:MaxPermSize  设置永久代最大大小
 
### 新生代设置
1. -XX:SurvivorRatio：新生代中Eden区域与Survivor区域的容量比值，默认值为8。两个Survivor区与一个Eden区的比值为2:8,一个Survivor区占整个年轻代的1/10。
2. -Xmn 新生代的内存空间大小，注意：此处的大小是（eden+ 2 survivor space)
3. -Xss 栈内存大小

### GC收集设置
1. -XX:+PrintGCDetails 详细GC变化
2. -XX:+PrintGCTimeStamps  了解垃圾收集发生的时间，自JVM启动以后以秒计算 
3. -XX:+UseConcMarkSweepGC  CMS垃圾收集器

### 内存溢出错误时输出堆栈文件，内存映像文件
1. -XX:+HeapDumpOnOutOfMemoryError


-XX:NewRatio=1 

-XX:+UseParallelGC

-XX:ParallelGCThreads=8

-XX:+UseAdaptiveSizePolicy

-Xloggc:$FLUME_PID_DIR/gc.log


-XX:+PrintGC 

-XX:+PrintGCDetails

-XX:+PrintGCTimeStamps

-XX:+PrintGCApplicationStoppedTime

-XX:+PrintGCApplicationConcurrentTime

-XX:+HeapDumpOnOutOfMemoryError

-XX:HeapDumpPath=$FLUME_PID_DIR 

-XX:ErrorFile=$FLUME_PID_DIR/java_error_%p.log


