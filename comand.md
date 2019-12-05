- 创建topic
bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --create --topic multipart-replicated-topic --partitions 3  --replication-factor 3

- 查看kafka topic列表，使用--list参数
bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --list

- 查看kafka特定topic的详情，使用--topic与--describe参数
bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic  multipart-replicated-topic --describe

展示当前消费者群组：
./kafka-consumer-groups.sh --new-consumer --bootstrap-server 127.0.0.1:9092 --list

展示当前消费者群组偏移量：
./kafka-consumer-groups.sh --new-consumer --bootstrap-server 127.0.0.1:9092 --describe --group group-MultipartConsumer


- 查询topic的每个Partition 的生产消息的最大偏移位置
bin/kafka-run-class.sh kafka.tools.GetOffsetShell --broker-list 127.0.0.1:9092 --topic multipart-replicated-topic --time -1

- 查询某消费者组下某个topic的每个Partition 的消费者当前提交便偏移位置：
bin/kafka-run-class.sh kafka.tools.ConsumerOffsetChecker --group group-MultipartConsumer --topic multipart-replicated-topic --zookeeper 127.0.0.1:2181

- 连接zk：
bin/zookeeper-shell.sh 127.0.0.1:2181

- 读取消息：
bin/kafka-console-consumer.sh  --zookeeper 127.0.0.1:2181  --topic daysweet_test01 --from-beginning


- 重置offset：
bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group group-DemoConsumer --reset-offsets --topic  my-replicated-topic --to-offset 100 --execute
