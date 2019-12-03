1. 在调试消费者时，如果超过一定时间，commit偏移量会报错：
```
@Component
public class KafkaConsumer {

    @KafkaListener(groupId="${kafka.group.id}",topics = "${kafka.topic.order}", containerFactory = "kafkaListenerContainerFactory")
    public void consume(@Payload String message) {
        GsonBuilder builder = new GsonBuilder();
        builder.setPrettyPrinting();
        builder.setDateFormat("yyyy-MM-dd HH:mm:ss");
        Gson gson = builder.create();
        OrderBasic orderBasic = gson.fromJson(message, new TypeToken<OrderBasic>() {
        }.getType());
        String json = gson.toJson(orderBasic);
        System.out.println("\n接受并消费消息\n" + json);
    }
}
```
```
org.apache.kafka.clients.consumer.CommitFailedException: Commit cannot be completed since the group has already rebalanced and assigned the partitions to another member. This means that the time between subsequent calls to poll() was longer than the configured max.poll.interval.ms, which typically implies that the poll loop is spending too much time message processing. You can address this either by increasing max.poll.interval.ms or by reducing the maximum size of batches returned in poll() with max.poll.records.
	at org.apache.kafka.clients.consumer.internals.ConsumerCoordinator.sendOffsetCommitRequest(ConsumerCoordinator.java:820) ~[kafka-clients-2.3.1.jar:na]
	at org.apache.kafka.clients.consumer.internals.ConsumerCoordinator.commitOffsetsSync(ConsumerCoordinator.java:692) ~[kafka-clients-2.3.1.jar:na]
	at org.apache.kafka.clients.consumer.KafkaConsumer.commitSync(KafkaConsumer.java:1454) ~[kafka-clients-2.3.1.jar:na]
	at org.springframework.kafka.listener.KafkaMessageListenerContainer$ListenerConsumer.commitIfNecessary(KafkaMessageListenerContainer.java:1938) ~[spring-kafka-2.3.3.RELEASE.jar:2.3.3.RELEASE]
	at org.springframework.kafka.listener.KafkaMessageListenerContainer$ListenerConsumer.processCommits(KafkaMessageListenerContainer.java:1761) ~[spring-kafka-2.3.3.RELEASE.jar:2.3.3.RELEASE]
	at org.springframework.kafka.listener.KafkaMessageListenerContainer$ListenerConsumer.pollAndInvoke(KafkaMessageListenerContainer.java:930) ~[spring-kafka-2.3.3.RELEASE.jar:2.3.3.RELEASE]
	at org.springframework.kafka.listener.KafkaMessageListenerContainer$ListenerConsumer.run(KafkaMessageListenerContainer.java:890) ~[spring-kafka-2.3.3.RELEASE.jar:2.3.3.RELEASE]
	at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511) [na:1.8.0_171]
	at java.util.concurrent.FutureTask.run$$$capture(FutureTask.java:266) [na:1.8.0_171]
	at java.util.concurrent.FutureTask.run(FutureTask.java) [na:1.8.0_171]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_171]

```
