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
