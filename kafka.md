![image-20200225092514108](/Users/litian/Library/Application Support/typora-user-images/image-20200225092514108.png)

因为卡夫卡有发布订阅的功能，很多人便认为它是一中消息中间件，其实消息中间件只是它40%的功能

Topic：把数据归类

partion：分区，在topic之下，数据都存在分区里面，可以体现在磁盘里面z

![image-20200225093141704](/Users/litian/Library/Application Support/typora-user-images/image-20200225093141704.png)

一个消费者可以消费一个topic里面所有分区的数据，但是一个分区只能对应一个消费者，不能有2个消费者消费同一个分区

![image-20200225093247608](/Users/litian/Library/Application Support/typora-user-images/image-20200225093247608.png)

数据怎么判断被消费了，这就涉及到了偏移量了，其实偏移量其实就是一个Long型的数字，如果重新读取数据，可以重置偏移量。**用过的消息默认不会消除，因为设计之初就不是消息队列，是数据存储方面的。默认存储在磁盘当中。**

打包方式生产消息，卡夫卡为了性能可以把消息缓存到本地，然后打包一次性发给broker，还可以把消息进行压缩，减少网络的损耗，

## 优点

+ 基于磁盘的数据存储

  数据可靠性比较高，不同于rabbitmq，因为rabbitmq也是能将数据存储到磁盘里面，**卡夫卡是把数据存储在磁盘里面还能保持这么高的性能，所以很厉害。**

+ 高伸缩性

  无论有多少生产者和消费者接进来，也不会对性能有多大的影响。对于集群，新增集群不会对之前的有多大的影响，因为设计之初就是考虑到了集群方面的东西，搭建集群只需要修改两个参数就好了。

+ 高性能

## 应用场景

+ 收集指标和日志

  统计信息和日志刷新频率非常快，而且数据非常大，足见卡夫卡性能

+ 提交日志

  操作日志，大型互联网在处于比较关键的时刻要考虑，比如容灾，如果湖南机房发生了灾难，那么武汉机房就会顶上来，因为湖南机房会将操作日志上传到卡夫卡，而武汉机房会去消费日志，同步到本地数据库

+ 流处理

## 缺点

+ 运维难度大

+ 偶尔有数据混乱的情况

  对于磁盘是卡夫卡不能控制的，比如刚好磁盘坏了，硬件问题是不能控制的。

+ 对zk强依赖

+ 多副本模式下对带宽有一定的要求

main方法args，启动程序需要传递参数，类似命令行启动传递后面参数，空格隔开，所以这儿是个数组

## 基本管理操作命令

![image-20200225141153062](/Users/litian/Library/Application Support/typora-user-images/image-20200225141153062.png)

文件占用导致topic起不来，只能把日志目录里面的文件删掉，只是windows会有的问题

![image-20200225165429804](/Users/litian/Library/Application Support/typora-user-images/image-20200225165429804.png)

1. 获取指定topic所有分区下面所有的消息不管是否被消费
2. 指定分区，指定offset的所有数据



在不换groupid的情况下重置offset

![image-20200225170758365](/Users/litian/Library/Application Support/typora-user-images/image-20200225170758365.png)

**全量获取**：在不换groupid的情况下获取指定topic下所有分区下的所有的消息

判断是否获取所有的消息，提前进行判断

```
/**
 * 在kafka来说这个方法叫优雅退出消费者，当我们不需要某个消费者消费某个topic的时候可以直接退出程序
 * 用这个方法kafka知道你退出了，kafka就会准备下一次分区再均衡，同时会最后帮你提交一次偏移量
 * kafka默认和消费者有心跳机制来判断是否再均衡
 */
// consumer.close();
```

![image-20200226155355989](/Users/litian/Library/Application Support/typora-user-images/image-20200226155355989.png)