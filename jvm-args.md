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

## -Xmn<n>[g|m|k]
同时设置新生代的初始、最小和最大尺寸，新生代的尺寸设定为这个值。如果期望-XX:NewSize和-XX:MaxNewSize设置成相同的值，这是一个便利的命令行选项。

## -XX:NewRatio=< n >
新生代和老年代的尺寸比，例如n为3，则比率为1:3，即新生代占新生代和老年代总和的1/4。如果java堆扩展或缩减，HotSpot将依据此比率调整新生代和老年代

如果-Xms和-Xmx不同，并且希望新生代和老年代的大小维持特定比率时，这是个便利的命令选项。

## -XX:PermSize=<n>[g|m|k]
永久代的初始和最小尺寸。永久代永远不会小于这个值。

如果-XX:PermSize小于-XX:MaxPermSize,永久代的尺寸会随着应用的需要而扩展或缩减，特别是需要加载类或存储intern String的情况。永久代的扩展或缩减需要FullGC,所以注重延迟或吞吐量的应用程序通常应把-XX:PermSize和-XX:MaxPermSize设置成相同的值。

## -XX:MaxPermSize=<n>[g|m|k]
永久代的最大尺寸，永久代永远不会超过这个值。

如果-XX:MaxPermSize大于-XX:PermSize，永久代的尺寸会随着应用的需要而扩展和缩减，特别是在需要加载类或存储intern String时。永久代的扩展或缩绒需要FullGC,所以注重延迟或吞吐量的应用程序通常应把-XX:MaxPermSize和-XX:PermSize设置成相同的值。

## -XX:SurvivorRatio=< n >
单块Survivor区与Eden区的大小比率，< n >是比率。依据-XX:SurvivorRatio=< n >指定的比率，可以用以下等式计算Survivor区的大小：

		survivor size=-Xmn<n>/(-XX:SurvivorRatio=<n> + 2)
-Xmn< n >是新生代的尺寸，而-XX:SurvivorRatio=< n >是比率值。等式中的+2是因为有两块Survivor区，指定的比率越大，Survivor区的尺寸越小。

在使用CMS收集器或Throughput收集器，并且自适应尺寸调整关闭（-XX:-UseAdaptiveSizePolicy）时，如果你想显示调整Survivor区从而控制对象的老化，那就应该使用-XX:SurvivorRatio=< n >

在使用Throughput收集器，并且自适应尺寸调整开启时，不要使用-XX:SurvivorRatio=< n >。通过-XX:+UseParallelGC或-XX：+UseParallelOldGC选择的Throughput收集器，默认开启自适应尺寸调整。如果想为Throughput收集器的自适应尺寸调整设定初始Survivor比率，则可使用选项-XX:InitialSurvivorRatio=< n >

## -XX:+PrintTenuringDistribution
在日志中输出对象年龄分布

## -XX:+PrintGCApplicationStoppedTime 

在日志中输出程序STW 的暂停时间，输出形式: Total time for which application threads were stopped: 0.0468229 seconds。

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

-XX:+PrintGCCause

-XX:+PrintGCApplicationStoppedTime

-XX:+PrintGCApplicationConcurrentTime

-XX:+HeapDumpOnOutOfMemoryError

-XX:HeapDumpPath=$FLUME_PID_DIR 

-XX:ErrorFile=$FLUME_PID_DIR/java_error_%p.log













前几年在将OS从32 bit升级到64 bit，以及虚拟机的内存调整到8G后，我把应用的Java启动参数重新写了一版，作为目前大部分Java应用的默认启动参数模版，这几年下来，发现在这个标准版的启动参数上还是犯了一些错误的。
 
1. -XX:+DisableExplicitGC
Java在实现RMI Server的时候会通过定时的调System.gc来强制做GC（即使程序里没用到RMI也会被启动），这个动作非常烦人，另外也是为了避免应用代码上显式去调用System.gc导致一些没必要的GC动作产生，所以当时就直接加上了这个参数。
现在来看，这个参数有个挺大的问题是，Direct ByteBuffer所占用的内存以及FileChannel.map所占用的内存当达到了他们的最大阈值时，需要依赖调用System.gc来强制释放下，如果加上了这个启动参数，就意味着这个强制的释放就无效了，这会导致的一个问题是，当old gen还没到达触发full gc/cms gc的条件，而堆外的Direct ByteBuffer/FileChannel.map占用的空间又超过了它们的最大阈值时，就会直接导致OOM，而这种情况下很有可能其实是可以借助显式调用System.gc来释放出足够的空间，不过话说我仍然觉得这是JDK设计上应该改进的一点，不应该在这个时候需要依赖System.gc来管理堆外的空间，大家可以翻下FileChannel.map的代码就会发现那里在等待System.gc执行的结果是写S的等待100ms，事实上很少有full gc/cms gc可以在100ms完成。
 
不过鉴于上面的状况，如果应用里有使用到不少Direct ByteBuffer或FileChannel.map的话，建议还是不要开启-XX:+DisableExplicitGC，如果是cms gc的，还是改为加上这个参数-XX:+ExplicitGCInvokesConcurrent，另外如果有RMI Server这种定时GC影响的，再调整下-Dsun.rmi.dgc.client.gcInterval和-Dsun.rmi.dgc.server.gcInterval这两个时间吧，时间单位是ms，也可以设置为Long.MAX_VALUE。
 
2. 缺少-XX:+UseCMSInitiatingOccupancyOnly
由于我们的Java应用的heap基本都是大于4G的，所以都是用的CMS，当时我在写启动参数的时候一直犹豫要不要加上-XX:+UseCMSInitiatingOccupancyOnly这个参数，一犹豫就没加，但事实上后来碰到了不少应用由于JVM自行触发CMS GC的机制导致CMS GC频繁，所以建议用CMS GC的场景下还是加上这个参数更稳妥。
 
 -XX:+UseCMSInitiatingOccupancyOnly CMS GC条件只根据XX:CMSInitiatingOccupancyFraction
 
3. -XX:MaxDirectMemorySize
话说在写启动参数的时候我都压根不知道这参数（要知道Java到底有哪些启动参数可用，以及默认值是多少，最靠谱的方法是在启动参数上加-XX:+PrintFlagsFinal或用jinfo -flags [pid]来查看），后来是由于有一次出现了有应用物理内存被耗光，排查的时候才发现是Direct ByteBuffer这块默认的大小是heap size，所以在有些情况下可能会出现Direct ByteBuffer这里占用了大量的空间，但heap这边又还不到触发Full gc/CMS gc的条件，就会有可能导致物理内存被耗光。
因此对于远程交互比较多的应用，建议还是加上这个参数，合理控制大小，不要让heap size+Direct Memory Size就把物理内存给耗光了。
 
ps: 关于Java常见问题的排查方法，重新专门写了一个PPT，涵盖了以下几种常见的Java问题的排查方法：
1. 类加载问题，例如NoSuchMethodException；
2. 内存问题，例如各种OOM；
3. 应用无响应问题，例如http访问后返回499；
4. CPU利用率问题，例如us耗尽；
5. Java进程退出问题。
6. 






串行收集器： 
DefNew：是使用-XX:+UseSerialGC（新生代，老年代都使用串行回收收集器）。

并行收集器： 
ParNew：是使用-XX:+UseParNewGC（新生代使用并行收集器，老年代使用串行回收收集器）或者-XX:+UseConcMarkSweepGC(新生代使用并行收集器，老年代使用CMS)。

PSYoungGen：是使用-XX:+UseParallelOldGC（新生代，老年代都使用并行回收收集器）或者-XX:+UseParallelGC（新生代使用并行回收收集器，老年代使用串行收集器）

garbage-first heap：是使用-XX:+UseG1GC（G1收集器）



## 吞吐量调优案例

	java -Xmx3800m -Xms3800m -Xmn2g -Xss128k -XX:+UseParallelGC -XX:ParallelGCThreads=20 -XX:+UseParallelOldGc

-XX:+UseParallelOldGC：配置年老代垃圾收集方式为并行收集
-XX:+UseParallelGC 新生代使用并行回收收集器，可以尽可能的减少gc时间
	
	
## 使用CMS收集器注意

因为年老代的并发收集器使用标记、清除算法，所以不会对堆进行压缩。当收集器回收时，他会把相邻的空间进行合并，这样可以分配给较大的对象。但是，当堆空间较小时，运行一段时间以后，就会出现“碎片”，如果并发收集器找不到足够的空间，那么并发收集器将会停止，然后使用传统的标记、清除方式进行回收。如果出现“碎片”，可能需要进行如下配置：

-XX:+UseCMSCompactAtFullCollection：使用并发收集器时，开启对年老代的压缩。  
-XX:CMSFullGCsBeforeCompaction=0：上面配置开启的情况下，这里设置多少次Full GC后，对年老代进行压缩




-XX:+UseParallelGC -XX:+UseConcMarkSweepGC -XX:+UseCMSCompactAtFullCollection -XX:CMSFullGCsBeforeCompaction=3 -Xmx4g -Xms4g -XX:MaxPermSize=256m -Xmn2g -XX:+UseCMSInitiatingOccupancyOnly -XX:CMSInitiatingOccupancyFraction=80 -XX:ParallelGCThreads=4 -XX:ConcGCThreads=2 -Xloggc:/export/Logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCTimeStamps -XX:+PrintGC 




DefNewGeneration是default new generation 
ParNewGeneration是parallel new generation 
