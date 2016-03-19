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

如果Java堆超过了32位HotSpot VM的限制，但又不想牺牲性能，可以使用该选项。



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


