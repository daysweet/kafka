# 说明
用于对照《kafka技术内幕》研究kafka

# 环境
- mac
- java version "1.8.0_171"
- Gradle 5.6.3
- kafka https://github.com/apache/kafka/tree/0.10.0

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
5. 运行单节点zk: bin/zookeeper-server-start.sh config/zookeeper.properties
6. idea中启动项目。

