# Kafka连接超时:org.apache.kafka.common.errors.TimeoutException:Expiring 1 resord(s)...

背景概述：在EC2上部署了向Kafka生产数据的服务，运行一段时间后报错org.apache.kafka.common.errors.TimeoutException:Expiring 1 resord(s)...

![报错信息](D:\Onebox\笔记\图片\Kafka连接超时.png)

该报错导致数据入湖和入MySQL产生了巨大的延迟。

## 1. 检查Kafka连接数

```
netstat -an|grep 9092|wc -l
```

在服务器使用该命令打印出Kafka的连接数。其中9092是自己的Kafka连接串的端口号。如果连接数过大，则无法再和Kafka建立新的连接。具体连接数的上限需要咨询Kafka的管理人员。

## 2. 解决问题

如果Kafka的连接数过大，问题可能是程序在运行过程中建立了太多的Kafka连接，应该修改程序中Kafka生产者的代码。确保为单例且线程安全。

```java
    // volatile保证线程安全，不然流水线可能报错
	private static volatile KafkaProducer<String, byte[]> kafkaProducer = null;

    private static final Object LOCK = new Object();

    private KafkaProcedure() {
    }

    /**
     * get producer
     *
     * @return get producer
     */
    public static synchronized KafkaProducer<String, byte[]> getProducer() {
        if (kafkaProducer == null) {
            synchronized (LOCK) {
                if (kafkaProducer == null) {
                    Map<String, Object> configs = new HashMap<>();
                    configs.put("bootstrap.servers", BOOTSTRAP_SERVERS);
                    configs.put("key.serializer", StringSerializer.class.getCanonicalName());
                    configs.put("value.serializer", ByteArraySerializer.class.getCanonicalName());
                    configs.put("acks", "1"); // 0:不需要等待确认; 1:只需要leader确认; all: 所有节点确认
                    configs.put("batch.size", BATCH_SIZE); // 批处理大小
                    configs.put("request.timeout.ms", REQUEST_TIMEOUT_MS);
                    configs.put("max.request.size", MAX_REQUEST_SIZE); // 设置消息体大小，华为云kafka 生产消息大小默认为1M，最大支持10M
                    kafkaProducer = new KafkaProducer<>(configs);
                }
            }
        }
        return kafkaProducer;
    }
```

