- 创建topic
bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --create --topic daysweet_test01 --partitions 3  --replication-factor 1

- 查看kafka topic列表，使用--list参数
bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --list

- 查看kafka特定topic的详情，使用--topic与--describe参数
bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic daysweet_test01 --describe

- 旧版kafka查看consumer group列表，使用--list参数
bin/kafka-consumer-groups.sh --zookeeper 127.0.0.1:2181 --list

- 旧版查看特定consumer group 详情，使用--group与--describe参数
bin/kafka-consumer-groups.sh --zookeeper 127.0.0.1:2181 --group console-consumer-14009 --describe

- 查询topic的每个Partition 的生产消息的最大偏移位置
bin/kafka-run-class.sh kafka.tools.GetOffsetShell --broker-list 127.0.0.1:9092 --topic daysweet_test01  --time -1

- 查询某消费者组下某个topic的每个Partition 的消费者当前提交便偏移位置：
bin/kafka-run-class.sh kafka.tools.ConsumerOffsetChecker --group group_daysweet_test01 --topic daysweet_test01 --zookeeper 127.0.0.1:2181

- 连接zk：
bin/zookeeper-shell.sh 127.0.0.1:2181

- 读取消息：
bin/kafka-console-consumer.sh  --zookeeper 127.0.0.1:2181  --topic daysweet_test01 --from-beginning
