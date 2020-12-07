### 优化Tomcat的server.xml参数：   
在tomcat配置文件server.xml中的<Connector ... />配置中，和连接数相关的参数有：   
minProcessors：最小空闲连接线程数，用于提高系统处理性能，默认值为10   
maxProcessors：最大连接线程数，即：并发处理的最大请求数，默认值为75   
acceptCount：允许的最大连接数，应大于等于maxProcessors，默认值为100   
enableLookups：是否反查域名，取值为：true或false。为了提高处理能力，应设置为false   
connectionTimeout：网络连接超时，单位：毫秒。设置为0表示永不超时，这样设置有隐患的。通常可设置为30000毫秒。  
其中和最大连接数相关的参数为maxProcessors和acceptCount。如果要加大并发连接数，应同时加大这两个参数。   


    <Connector executor="tomcatThreadPool"
     
        port="8080" protocol="HTTP/1.1"
     
        maxThreads="2048"     connectionTimeout="20000"
     
    minProcessors="50" maxProcessors="2048" maxSpareThreads="100"
     
    enableLookups="false" acceptCount="2048"
     
    compression="on" compressionMinSize="2048"
     
    redirectPort="8443"  URIEncoding="GBK"/>



### 增加Tomcat使用内存：
vi catalina.sh   
修改TOMCAT_HOME/bin/catalina.sh   
在"echo "Using CATALINA_BASE:   $CATALINA_BASE""上面加入以下行：    
JAVA_OPTS='-Xms1024m -Xmx1024m -XX:PermSize=256M -XX:MaxNewSize=256m -XX:MaxPermSize=256m '   
可以根据应用的不同，调整JVM的参数设置，此话题另有专题介绍。   
另建议：将相同的第三方jar文件移置到tomcat/shared/lib目录下，这样可以达到减少jar 文档重复占用内存的目的。   

