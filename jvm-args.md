## JVM虚拟机参数
1. -Xms1024m 初始堆大小
2. -Xmx1024m 最大堆大小
3. -XX:PermSize 设置永久代初始大小
4. -XX:MaxPermSize 设置永久代最大大小
3. -Xmn 新生代的内存空间大小，注意：此处的大小是（eden+ 2 survivor space)
4. -XX:+PrintGCDetails 详细GC变化
5. -XX:+PrintGCTimeStamps  了解垃圾收集发生的时间，自JVM启动以后以秒计算 
