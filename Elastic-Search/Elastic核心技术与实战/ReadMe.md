#  Elasticsearch简介及其发展历史

> 本文采用的是Elastic7.1.0的版本

![image-20220508140442913](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140442913.png)

![image-20220508140507009](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140507009.png)

![image-20220508140525890](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140525890.png)

![image-20220508140552354](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140552354.png)

![image-20220508140615228](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140615228.png)

![image-20220508140701759](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140701759.png)

![image-20220508140746669](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140746669.png)

![image-20220508140808332](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140808332.png)

![image-20220508140830627](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140830627.png)

![image-20220508140908338](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140908338.png)

![image-20220508140953989](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508140953989.png)

![image-20220508141011784](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141011784.png)

![image-20220508141029973](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141029973.png)

![image-20220508141056681](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141056681.png)

# Elastic Stack家族成员

## Elastic Stack 生态圈

![image-20220508141329926](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141329926.png)

## Logstash：数据处理管道

![image-20220508141356355](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141356355.png)

## Logstash 特性

![image-20220508141505872](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141505872.png)

## kibana：可视化分析利器

![image-20220508141545112](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141545112.png)

## Kibana 特性

![image-20220508141613183](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141613183.png)

## Elastic的发展

![image-20220508141635322](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141635322.png)

## BEATS - 轻量的数据采集器

![image-20220508141802699](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141802699.png)

## X-Pack： 商业化套件

![image-20220508141900815](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141900815.png)

##  ELK客户及应用场景

![image-20220508141936983](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508141936983.png)

## 日志的重要性

![image-20220508142007597](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508142007597.png)

## 日志管理

![image-20220508142048089](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508142048089.png)

## Elasticsearch 与数据库的集成

![image-20220508142136095](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508142136095.png)

## 指标分析 / 日志分析

![image-20220508142257995](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508142257995.png)

# Elasticsearch的安装与简单配置

## 本地部署 & 水平扩展

![image-20220508142557008](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508142557008.png)

## 安装Java

![image-20220508142609274](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508142609274.png)

## 获取Elasticsearch安装包

> 下载7.1.0版本

+ 下载二进制文件

  https://www.elastic.co/cn/downloads/past-releases/elasticsearch-7-1-0

+ 支持Docker本地运行

+ Helm chart for kubernetes

+ Puppet Module

## Elasticsearch 的文件目录结构

![image-20220508151322164](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508151322164.png)

## JVM 配置

> 生产环境总量不要超过30GB

![image-20220508151633056](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508151633056.png)

## Elastic运行

在elastic解压缩包目录下执行`bin/elasticsearch`

```shell
elasticsearch-7.1.0 bin/elasticsearch
```

## Elastic插件安装

1. 查看本地安装的插件（目前没有安装任何插件）

   **➜** **elasticsearch-7.1.0** bin/elasticsearch-plugin list

   **➜** **elasticsearch-7.1.0** 

2. 安装插件（analysis-icu是国际化的分词插件）

   **➜** **elasticsearch-7.1.0** bin/elasticsearch-plugin install analysis-icu

3. 这下就能看到插件了

   ````shell
   ➜  elasticsearch-7.1.0 bin/elasticsearch-plugin list                
   analysis-icu
   ➜  elasticsearch-7.1.0 
   ````

4. 重新启动后能看到插件装载

   ![image-20220508153255812](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508153255812.png)

5. 访问`http://localhost:9200/_cat/plugins?v`能看到装载的插件

   ![image-20220508153408140](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508153408140.png)

6. Elasticsearch 提供插件的机制对系统进行扩展

   + Discovery Plugin
   + Analysis Plugin
   + Security Plugin
   + Management Plugin
   + Ingest Plugin
   + Mapper Plugin
   + Backup Plugin

## 如何在开发机上运行多个Elasticsearch实例

1. 启动集群节点

   **➜** **elasticsearch-7.1.0** bin/elasticsearch -E node.name=node1 -E cluster.name=geekting -E path.data=data/node1_data -d

   **➜** **elasticsearch-7.1.0** bin/elasticsearch -E node.name=node2 -E cluster.name=geekting -E path.data=data/node2_data -d

   **➜** **elasticsearch-7.1.0** bin/elasticsearch -E node.name=node3 -E cluster.name=geekting -E path.data=data/node3_data -d

2. 通过访问`http://localhost:9200/_cat/nodes`可以查看ES里面运行的节点

   ![image-20220508154451783](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508154451783.png)

3. 停止ES服务

   **➜** **elasticsearch-7.1.0** ps | grep elasticsearch

   **➜** **elasticsearch-7.1.0** kill pid

## Kibana的安装与界面快速浏览

1. 下载安装包解压到指定目录

   https://www.elastic.co/cn/downloads/past-releases/kibana-7-1-0

2. 在解压目录使用`bin/kibana`启动kibana（elastic需要先启动）

   **➜** **kibana-7.1.0-darwin-x86_64** bin/kibana

3. 访问`localhost:5601`端口查看

   ![image-20220508155720689](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508155720689.png)

4. 这儿推荐一个kibana好用的工具 dev tools，可以在这儿对ES进行命令操作

   ![image-20220508155938800](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508155938800.png)

   

## Kibana Console

![image-20220508160000235](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508160000235.png)

## Kibana Plugins

> 插件只需要给定名字就行，类似Elastic

![image-20220508160035841](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508160036555.png)

# 在Docker容器中运行Elasticsearch Kibana和Cerebro

1. 安装Docker 与 Docker Compose

   访问https://docs.docker.com/desktop/mac/install/

   ![image-20220508161431333](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508161431333.png)

2. 按照官网提示安装docker（选择自己对应的芯片，我这儿是mac，所以傻瓜式安装）

3. 添加加速地址，以下是我的加速地址

   ![image-20220508182521260](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508182521260.png)
   
   ```json
   {
     "builder": {
       "gc": {
         "defaultKeepStorage": "20GB",
         "enabled": true
       }
     },
     "experimental": false,
     "features": {
       "buildkit": true
     },
     "registry-mirrors": [
         "https://gpdm9i3j.mirror.aliyuncs.com"
     ]
}
   ```

4. 安装docker-compose

   mac安装的docker默认携带docker-compose，使用以下命令可以查看是否安装？

   **➜** **~** docker-compose --version

   ```shell
   docker-compose version 1.29.2, build 5becea4c
   ```

5. 编辑docker-compose.yaml文件

   ```yaml
   version: '2.2'
   services:
     cerebro:
       image: lmenezes/cerebro:0.8.3
       container_name: cerebro
       ports:
         - "9000:9000"
       command:
         - -Dhosts.0.host=http://elasticsearch:9200
       networks:
         - es7net
     kibana:
       image: docker.elastic.co/kibana/kibana:7.1.0
       container_name: kibana7
       environment:
         - I18N_LOCALE=zh-CN
         - XPACK_GRAPH_ENABLED=true
         - TIMELION_ENABLED=true
         - XPACK_MONITORING_COLLECTION_ENABLED="true"
         - ELASTICSEARCH_USERNAME=kibana
         - ELASTICSEARCH_PASSWORD=demo_password
       ports:
         - "5601:5601"
       networks:
         - es7net
     elasticsearch:
       image: docker.elastic.co/elasticsearch/elasticsearch:7.1.0
       container_name: es7_01
       environment:
         - cluster.name=test-es
         - node.name=es7_01
         - bootstrap.memory_lock=true
         - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
         - "TZ=Asia/Shanghai"
         - discovery.type=single-node
         - path.data=node0_data
         - xpack.security.enabled=true
         - xpack.security.transport.ssl.enabled=false
       ulimits:
         memlock:
           soft: -1
           hard: -1
       privileged: true
       volumes:
         - /data/es7data1:/usr/share/elasticsearch/data
       ports:
         - 9200:9200
       networks:
         - es7net
   
   networks:
     es7net:
       driver: bridge
   ```

6. 执行命令启动

   在docker-compose.yml 文件所在的目录执行下面命令，后台启动容器。

   ````shell
   docker-compose up --build -d
   ````

7. 错误分析

   ![image-20220508191151486](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508191151486.png)

   命令行启动的时候遇上以上问题，于是我使用mac的docker客户端进行启动，这会儿错误就比较明显

   ![image-20220508191513135](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508191513135.png)

   由于这是我在网上找的配置文件，启动的时候需要在docker里面的resource的share文件配置相应的信息

   ![image-20220509090011136](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220509090011136.png)

   但是以上文件是单机模式，需要进入到容器内部设置密码才能访问，于是这儿采用非密码集群的方式启动

8. 正确的Elastic相关的docker-compose文件

   ````yaml
   version: '2.2'
   services:
     cerebro:
       image: lmenezes/cerebro:0.8.3
       container_name: cerebro
       ports:
         - "9000:9000"
       command:
         - -Dhosts.0.host=http://elasticsearch:9200
       networks:
         - es7net
     kibana:
       image: docker.elastic.co/kibana/kibana:7.1.0
       container_name: kibana7
       environment:
         - I18N_LOCALE=zh-CN
         - XPACK_GRAPH_ENABLED=true
         - TIMELION_ENABLED=true
         - XPACK_MONITORING_COLLECTION_ENABLED="true"
       ports:
         - "5601:5601"
       networks:
         - es7net
     elasticsearch:
       image: docker.elastic.co/elasticsearch/elasticsearch:7.1.0
       container_name: es7_01
       environment:
         - cluster.name=geektime
         - node.name=es7_01
         - bootstrap.memory_lock=true
         - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
         - discovery.seed_hosts=es7_01,es7_02
         - cluster.initial_master_nodes=es7_01,es7_02
       ulimits:
         memlock:
           soft: -1
           hard: -1
       volumes:
         - es7data1:/usr/share/elasticsearch/data
       ports:
         - 9200:9200
       networks:
         - es7net
     elasticsearch2:
       image: docker.elastic.co/elasticsearch/elasticsearch:7.1.0
       container_name: es7_02
       environment:
         - cluster.name=geektime
         - node.name=es7_02
         - bootstrap.memory_lock=true
         - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
         - discovery.seed_hosts=es7_01,es7_02
         - cluster.initial_master_nodes=es7_01,es7_02
       ulimits:
         memlock:
           soft: -1
           hard: -1
       volumes:
         - es7data2:/usr/share/elasticsearch/data
       networks:
         - es7net
   
   
   volumes:
     es7data1:
       driver: local
     es7data2:
       driver: local
   
   networks:
     es7net:
       driver: bridge
   ````

9. 访问*cerebro*[http://localhost:9000/#/connect]

   ![image-20220509143650440](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220509143650440.png)

10. 选择已经知道的ES集群，自动连接，下图包含了ES的集群信息以及节点和索引大小之类的信息，关于详细使用，在之后的地方会提及（集群的名字不同是因为我后来用了下7.8.1的版本来测试，为了防止docker container名称相同导致的启动失败，所以改了个名字）

    ![image-20220509143743707](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220509143743707.png)

# Logstash安装与导入数据

1. 下载安装logstash，需要和ES版本保持一致，我这儿下载的是ZIP版本

   https://www.elastic.co/cn/downloads/past-releases/logstash-7-1-0

   ![image-20220508171616661](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508171616661.png)

2. 解压，然后去[Movielens][https://grouplens.org/datasets/movielens/]下载数据集，我这儿下载的最小的那个

   ![image-20220508171657832](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508171657832.png)

3. 在bin目录里面编写logstash.conf，内容如下

   > input里面指定对应的数据集路径

   ```conf
   input {
     file {
       path => "/Users/litian/Documents/lian/applications/elastic Statck7.1.0/movielens/ml-latest-small/movies.csv"
       start_position => "beginning"
       sincedb_path => "/dev/null"
     }
   }
   filter {
     csv {
       separator => ","
       columns => ["id","content","genre"]
     }
   
     mutate {
       split => { "genre" => "|" }
       remove_field => ["path", "host","@timestamp","message"]
     }
   
     mutate {
   
       split => ["content", "("]
       add_field => { "title" => "%{[content][0]}"}
       add_field => { "year" => "%{[content][1]}"}
     }
   
     mutate {
       convert => {
         "year" => "integer"
       }
       strip => ["title"]
       remove_field => ["path", "host","@timestamp","message","content"]
     }
   
   }
   output {
      elasticsearch {
        hosts => "http://localhost:9200"
        index => "movies"
        document_id => "%{id}"
      }
     stdout {}
   }
   ```

   

4. 执行命令，将电影数据导入到ES里面（我这儿是在bin目录里面执行的，需要sudo命令）

   **➜** **bin** sudo ./logstash -f logstash.conf 

5. 在kibana的console里面执行`GET _cat/indices`查看所有索引，能看到最新添加的电影索引，也可以在终端中执行`curl localhost:9200/_cat/indices`，也能获得同样的效果

   ![image-20220508173602747](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508173602747.png)

# Elasticsearch基本概念

## 文档（Document）

![image-20220508173923361](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508173923361.png)

## JSON文档

![image-20220508174029507](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508174029507.png)

## 文档的元数据

![image-20220508174119092](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508174119092.png)

## 索引

![image-20220508174212323](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508174212323.png)

## 索引的不同语意

![image-20220508174308548](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508174308548.png)

## TYPE

![image-20220508174344288](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508174344288.png)

## 抽象与类比

![image-20220508174359266](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508174359266.png)

## REST API - 很容易被各种语言调用

![image-20220508174511675](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508174511675.png)

## 一些基本的API

在Kibana里面提供一个管理功能，里面有索引管理

![image-20220508174727859](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508174727859.png)

点击的时候还可以看到setting、mapping之类的信息

![image-20220508174841045](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508174841045.png)

接下来使用dev tools来执行一些基本命令

1. 查看索引相关信息`GET movies`

   ![image-20220508175105772](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508175105772.png)

   

2. 查看indices，支持通配符：`GET /_cat/indices/.kibana*?v&s=index`

   ![image-20220508175256027](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508175256027.png)

3. 查看每个索引使用的内存`GET /_cat/indices?v&h=i,tm&s=tm:desc`

   ![image-20220508175512954](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508175512954.png)

## 分布式系统的可用性和扩展性

![image-20220508175808818](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508175808818.png)

## 分布式特性

![image-20220508175913059](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508175913059.png)

## 节点

![image-20220508180022120](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508180022120.png)

## Master-eligible nodes 和 Master Node

![image-20220508180215008](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508180215008.png)

## Data Node & Coordinating Node

![image-20220508180248105](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508180248105.png)

## 其他的节点类型

![image-20220508180434007](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508180434007.png)

## 配置节点类型

> 在Elastic的yaml配置文件中指定节点的角色

![image-20220508180556929](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508180556929.png)

## 分片（Primary Shard & Replica Shard）

![image-20220508180722699](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508180722699.png)

下图里面主分片为3，副本分片为1，正好就3个节点，所以一个节点一个主分片，然后每个主分片一个副本分片

![image-20220508181211804](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508181211804.png)



## 分片的设定

![image-20220508181434645](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508181434645.png)

## 查看集群的健康状况

![image-20220508181642019](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220508181642019.png)

## 一些常用的命令

> 在mac的环境下 将光标放到命令行，按住command + / 即可跳转到官方文档信息，亲测可用

![image-20220510092744440](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510092744440.png)

## 使用Cerebro查看集群信息

> 访问localhost:9000查看
>
> 集群默认设置的是1个主分片、1个副本，所以下图中均摊在两个节点上

![image-20220510093428543](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510093428543.png)

接下来尝试停掉某个节点再来查看集群的信息，使用docker命令

````shell
➜  ~ docker ps
CONTAINER ID   IMAGE                                                 COMMAND                  CREATED        STATUS          PORTS                              NAMES
55da2f831b21   docker.elastic.co/elasticsearch/elasticsearch:7.1.0   "/usr/local/bin/dock…"   25 hours ago   Up 27 minutes   0.0.0.0:9200->9200/tcp, 9300/tcp   es7_01
4974d141b30f   docker.elastic.co/elasticsearch/elasticsearch:7.1.0   "/usr/local/bin/dock…"   25 hours ago   Up 27 minutes   9200/tcp, 9300/tcp                 es7_02
dd464d85a9b8   docker.elastic.co/kibana/kibana:7.1.0                 "/usr/local/bin/kiba…"   25 hours ago   Up 27 minutes   0.0.0.0:5601->5601/tcp             kibana7
df1e8c8260c2   lmenezes/cerebro:0.8.3                                "/opt/cerebro/bin/ce…"   25 hours ago   Up 27 minutes   0.0.0.0:9000->9000/tcp             cerebro
````

```
➜  ~ docker stop 55da2f831b21
```

无论我停掉那个节点，都无法再继续使用kibana或者cerebro，不知道我的设置是否哪儿出错，竟然不能保证集群的可用性，理论上来说，集群健康度应该是黄色才对，还能访问

# 文档的CURD与批量操作

## Create 一个文档

![image-20220510094942055](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510094942055.png)

## Get 一个文档

![image-20220510095141514](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510095141514.png)

## Index 一个文档

![image-20220510095313692](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510095313692.png)

## Update 文档

> update会新增没有的字段与数据

![image-20220510095429903](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510095429903.png)

##  Bulk API

![image-20220510100100862](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510100100862.png)

```
POST _bulk
{"index": {"_index": "test", "_id": "1"}}
{"field": "value1"}
{"delete": {"_index":"test", "_id": "2"}}
{"create": { "_index": "test2", "_id": "3"}}
{"field1": "value3"}
{"udpate": {"_id": "1", "_index": "test"}}
{"doc": {"field2": "value2"}}
```

## 批量读取 - mget

![image-20220510100410692](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510100410692.png)

```
GET _mget
{
  "docs": [
    {
      "_index": "test",
      "_id": 1
    },
    {
      "_index": "test",
      "_id": 2
    }
  ]
}
```

## 批量查询 - msearch

![image-20220510100528474](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510100528474.png)

## 常见错误返回

![image-20220510100850808](/Users/litian/Documents/lian2077/documents/documents/Elastic-Search/Elastic核心技术与实战/images/image-20220510100850808.png)

