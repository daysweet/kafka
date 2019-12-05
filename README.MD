# 说明
用于对照《kafka权威指南》、《kafka技术内幕》研究kafka。

# 环境
- mac
- java version "1.8.0_171"
- Gradle 5.6.3
- kafka源码： https://github.com/apache/kafka/tree/0.10.0
- kafka二进制压缩包：http://kafka.apache.org/downloads

# 运行zk:
解压kafka二进制压缩包，执行zk: bin/zookeeper-server-start.sh config/zookeeper.properties

# 本地idea跑起来
1. 参考 KAFKA-7706，编辑 build.gradle 文件，修改 org.scoverage:gradle-scoverage 版本由 2.3.0 为 2.5.0
2. 编译，在项目目录下执行 gradle 
3. idea 导入项目。
4. 新建运行配置
```
Main Class：kafka.Kafka
VM options：-Dlog4j.configuration=file:config/log4j.properties -Dkafka.logs.dir=logs
Program Arguments：config/server.properties
Use classpath of module：core_main
```
5. idea中启动项目。

# 用二进制压缩包跑集群
参见二进制压缩包中的site-docs目录下的quickstart.html文档。

# 编写消费者和生产者
参照源码项目下的examples目录。
pom只需要添加
``` 
<dependency>
	<groupId>org.apache.kafka</groupId>
	<artifactId>kafka_2.10</artifactId>
	<version>0.10.0.0</version>
</dependency>
```


