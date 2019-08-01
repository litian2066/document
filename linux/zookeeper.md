#  zookeeper

## zookeeper下载、安装以及配置环境变量

文件已然上传至百度网盘：https://pan.baidu.com/s/1ieclT4MN6KFT73d7APqe0w

提取码：f5sh

也可以访问https://archive.apache.org/dist/zookeeper/这个网址下载对应的版本

使用rz命令上传到home文件夹下面

````
[root@zookeeper jdk8]# cd /home
[root@zookeeper home]# rz
rz waiting to receive.
Starting zmodem transfer.  Press Ctrl+C to cancel.
  100%   35808 KB 35808 KB/s 00:00:01       0 Errors
````

解压

````
tar -zxvf zookeeper-3.4.11.tar.gz
````

重命名：

```
mv zookeeper-3.4.11 zookeeper
```

放到``/usr/local/``目录下面（许多软件都放在了这个目录）

```
mv zookeeper /usr/local/
```

配置环境变量

```
vim /etc/profile
```

加上zookeeper配置

```
export JAVA_HOME=/usr/jdk8
export ZOOKEEPER_HOME=/usr/local/zookeeper
export CLASSPATH=.:%JAVA_HOME%/lib/dt.jar:%JAVA_HOME%/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin:$ZOOKEEPER_HOME/bin
```

```

```

## zookeeper主要目录介绍

```
[root@zookeeper home]# cd /usr/local/zookeeper/
[root@zookeeper zookeeper]# ll
total 1596
drwxr-xr-x.  2 502 games     149 Nov  2  2017 bin
-rw-r--r--.  1 502 games   87943 Nov  2  2017 build.xml
drwxr-xr-x.  2 502 games      77 Nov  2  2017 conf
drwxr-xr-x. 10 502 games     130 Nov  2  2017 contrib
drwxr-xr-x.  2 502 games    4096 Nov  2  2017 dist-maven
drwxr-xr-x.  6 502 games    4096 Nov  2  2017 docs
-rw-r--r--.  1 502 games    1709 Nov  2  2017 ivysettings.xml
-rw-r--r--.  1 502 games    8197 Nov  2  2017 ivy.xml
drwxr-xr-x.  4 502 games    4096 Nov  2  2017 lib
-rw-r--r--.  1 502 games   11938 Nov  2  2017 LICENSE.txt
-rw-r--r--.  1 502 games    3132 Nov  2  2017 NOTICE.txt
-rw-r--r--.  1 502 games    1585 Nov  2  2017 README.md
-rw-r--r--.  1 502 games    1770 Nov  2  2017 README_packaging.txt
drwxr-xr-x.  5 502 games      47 Nov  2  2017 recipes
drwxr-xr-x.  8 502 games     211 Nov  2  2017 src
-rw-r--r--.  1 502 games 1478279 Nov  2  2017 zookeeper-3.4.11.jar
-rw-r--r--.  1 502 games     195 Nov  2  2017 zookeeper-3.4.11.jar.asc
-rw-r--r--.  1 502 games      33 Nov  2  2017 zookeeper-3.4.11.jar.md5
-rw-r--r--.  1 502 games      41 Nov  2  2017 zookeeper-3.4.11.jar.sha1
```

bin：主要的一些执行命令，包含windows下执行，咱们这儿是在linux里面可以使用```./xxx.sh xxx```命令执行

```
[root@zookeeper zookeeper]# cd bin/
[root@zookeeper bin]# ll
total 36
-rwxr-xr-x. 1 502 games  232 Nov  2  2017 README.txt
-rwxr-xr-x. 1 502 games 1937 Nov  2  2017 zkCleanup.sh
-rwxr-xr-x. 1 502 games 1056 Nov  2  2017 zkCli.cmd
-rwxr-xr-x. 1 502 games 1534 Nov  2  2017 zkCli.sh
-rwxr-xr-x. 1 502 games 1628 Nov  2  2017 zkEnv.cmd
-rwxr-xr-x. 1 502 games 2696 Nov  2  2017 zkEnv.sh
-rwxr-xr-x. 1 502 games 1089 Nov  2  2017 zkServer.cmd
-rwxr-xr-x. 1 502 games 6773 Nov  2  2017 zkServer.sh
```

conf：存放配置文件，其中我们需要修改``zoo_sample.cfg``

```
[root@zookeeper zookeeper]# cd conf/
[root@zookeeper conf]# ll
total 12
-rw-r--r--. 1 502 games  535 Nov  2  2017 configuration.xsl
-rw-r--r--. 1 502 games 2161 Nov  2  2017 log4j.properties
-rw-r--r--. 1 502 games  922 Nov  2  2017 zoo_sample.cfg
```

contrib：附加的一些功能

```
[root@zookeeper zookeeper]# cd contrib/
[root@zookeeper contrib]# ll
total 0
drwxr-xr-x. 4 502 games  81 Nov  2  2017 fatjar
drwxr-xr-x. 3 502 games  71 Nov  2  2017 loggraph
drwxr-xr-x. 4 502 games  62 Nov  2  2017 rest
drwxr-xr-x. 3 502 games 106 Nov  2  2017 zkfuse
drwxr-xr-x. 4 502 games 208 Nov  2  2017 zkperl
drwxr-xr-x. 3 502 games  78 Nov  2  2017 zkpython
drwxr-xr-x. 4 502 games 119 Nov  2  2017 zktreeutil
drwxr-xr-x. 7 502 games 129 Nov  2  2017 ZooInspector
[root@zookeeper contrib]# 	
```

dist-maven：mvn编译后的目录。包含pom文件，jar包什么的，或者编译后生成的文件。

```
[root@zookeeper zookeeper]# cd dist-maven/
[root@zookeeper dist-maven]# ll
total 2608
-rw-r--r--. 1 502 games 887737 Nov  2  2017 zookeeper-3.4.11.jar
-rw-r--r--. 1 502 games    195 Nov  2  2017 zookeeper-3.4.11.jar.asc
-rw-r--r--. 1 502 games     33 Nov  2  2017 zookeeper-3.4.11.jar.md5
-rw-r--r--. 1 502 games     41 Nov  2  2017 zookeeper-3.4.11.jar.sha1
-rw-r--r--. 1 502 games 413360 Nov  2  2017 zookeeper-3.4.11-javadoc.jar
-rw-r--r--. 1 502 games    195 Nov  2  2017 zookeeper-3.4.11-javadoc.jar.asc
-rw-r--r--. 1 502 games     33 Nov  2  2017 zookeeper-3.4.11-javadoc.jar.md5
-rw-r--r--. 1 502 games     41 Nov  2  2017 zookeeper-3.4.11-javadoc.jar.sha1
-rw-r--r--. 1 502 games  11829 Nov  2  2017 zookeeper-3.4.11.pom
-rw-r--r--. 1 502 games    195 Nov  2  2017 zookeeper-3.4.11.pom.asc
-rw-r--r--. 1 502 games     33 Nov  2  2017 zookeeper-3.4.11.pom.md5
-rw-r--r--. 1 502 games     41 Nov  2  2017 zookeeper-3.4.11.pom.sha1
-rw-r--r--. 1 502 games 598115 Nov  2  2017 zookeeper-3.4.11-sources.jar
-rw-r--r--. 1 502 games    195 Nov  2  2017 zookeeper-3.4.11-sources.jar.asc
-rw-r--r--. 1 502 games     33 Nov  2  2017 zookeeper-3.4.11-sources.jar.md5
-rw-r--r--. 1 502 games     41 Nov  2  2017 zookeeper-3.4.11-sources.jar.sha1
-rw-r--r--. 1 502 games 689833 Nov  2  2017 zookeeper-3.4.11-tests.jar
-rw-r--r--. 1 502 games    195 Nov  2  2017 zookeeper-3.4.11-tests.jar.asc
-rw-r--r--. 1 502 games     33 Nov  2  2017 zookeeper-3.4.11-tests.jar.md5
-rw-r--r--. 1 502 games     41 Nov  2  2017 zookeeper-3.4.11-tests.jar.sha1
```

docs： 文档

lib： 需要依赖的jar包（开发Java客户端会用到，但一般用``curator``客户端来开发）

recipes： 案例demo代码

src：源码

## zookeeper配置文件介绍以及运行

### zoo.cfg配置

![](./img/66.png)

![](./img/67.png)

将```conf/```目录下的```zoo_sample.cfg```文件拷贝为```zoo.cfg```,，查看文件。

```
# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just
# example sakes.
dataDir=/tmp/zookeeper
# the port at which the clients will connect
clientPort=2181
# the maximum number of client connections.
# increase this if you need to handle more clients
#maxClientCnxns=60
#
# Be sure to read the maintenance section of the
# administrator guide before turning on autopurge.
#
# http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
#
# The number of snapshots to retain in dataDir
#autopurge.snapRetainCount=3
# Purge task interval in hours
# Set to "0" to disable auto purge feature
#autopurge.purgeInterval=1
```

介绍：



修改dataDir配置：

```
dataDir=/usr/local/zookeeper/dataDir
dataLogDir=/usr/local/zookeeper/dataLogDir
```

没有的文件夹需另行创建。

### 启动zookeeper

进入bin目录使用``./zkServer.sh start``启动

```
[root@zookeeper zookeeper]# cd bin/
[root@zookeeper bin]# ./zkServer.sh start
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED
```

使用status命令查看当当前运行状态

```
[root@zookeeper bin]# ./zkServer.sh status
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/bin/../conf/zoo.cfg
Mode: standalone
```

```mode: 是当前启动的模式，standalone：单机启动，集群启动会有master以及follower```。

关闭zookeeper：

```
[root@zookeeper bin]# ./zkServer.sh stop
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/bin/../conf/zoo.cfg
Stopping zookeeper ... STOPPED
```

重启为```./zkServer.sh restart```

**连接zookeeper客户端**

```
[root@zookeeper bin]# ./zkCli.sh -server localhost:2181
```

## zookeeper基本数据模型

![](./img/68.png)



![](./img/69.png)![](./img/70.png)

![](./img/71.png)

![](./img/72.png)

## zookeeper作用体现

1. **master节点选举**，主节点挂了之后，从节点就会接受工作，并且保证这个节点是唯一的，这也是所谓首脑模式，从而保证我们的集群是高可用的。
2. **统一配置文件管理**，即只需要部署一台服务器，则可以把相同的配置文件同步更新到其他所有服务器，此操作在云计算中用的特别多（假设修改了redis统一配置）。
3. **发布与订阅**，类似消息队列MQ（amq，rmq），dubbo发布者把数据存在znode上，订阅者会读取这个数据。**watcher机制**
4. **提供分布式锁**，分布式环境中不同进程之间争夺资源，类似于多线程中的锁。
5. **集群管理，保证数据的强一致性。**

## zookeeper命令

1. ```ls```与```ls2```命令

   **ls**：查看指定的文件目录信息。

   **ls2**：查看指定的文件目录信息并且显示节点的状态信息。

   ```
   [zk: localhost:2181(CONNECTED) 0] ls /
   [zookeeper] # 根节点  
   [zk: localhost:2181(CONNECTED) 1] ls2 /
   [zookeeper]
   cZxid = 0x0
   ctime = Thu Jan 01 08:00:00 CST 1970
   mZxid = 0x0
   mtime = Thu Jan 01 08:00:00 CST 1970
   pZxid = 0x0
   cversion = -1
   dataVersion = 0
   aclVersion = 0
   ephemeralOwner = 0x0
   dataLength = 0
   numChildren = 1
   [zk: localhost:2181(CONNECTED) 2] 
   ```

2. ```get```与```stat```命令

   ```get```：取出节点的数据信息以及状态信息。

   ```stat```：取出节点的状态信息。

   ```
   [zk: localhost:2181(CONNECTED) 12] stat /         
   cZxid = 0x0
   ctime = Thu Jan 01 08:00:00 CST 1970
   mZxid = 0x0
   mtime = Thu Jan 01 08:00:00 CST 1970
   pZxid = 0x0
   cversion = -1
   dataVersion = 0
   aclVersion = 0
   ephemeralOwner = 0x0
   dataLength = 0
   numChildren = 1
   [zk: localhost:2181(CONNECTED) 0] get /
   
   cZxid = 0x0  #zookeeper为节点分配的id
   ctime = Thu Jan 01 08:00:00 CST 1970 #创建的时间
   mZxid = 0x0 ##修改的id
   mtime = Thu Jan 01 08:00:00 CST 1970 #修改的时间
   pZxid = 0x0 #子节点的id
   cversion = -1 #子节点的version
   dataVersion = 0 #当前节点的数据版本号，修改后会自动加一
   aclVersion = 0 # 权限的version 更改会加一
   ephemeralOwner = 0x0
   dataLength = 0 #数据长度
   numChildren = 1 #子节点个数       
   ```

3. session的基本原理

   客户端与服务端之间的连接存在会话

   每个会话都会可以设置一个超时时间

   心跳结束，session则过期

   session过期，则临时节点znode会被抛弃

   心跳机制：客户端向服务端的ping包请求

4. ```create```命令

   ```
   create [-s]  [-e]  path  data   acl
   创建节点 [顺序节点]	[临时节点] 节点名字   数据	权限
   ```

   ````
   [zk: localhost:2181(CONNECTED) 24] create /immoc imooc-data
   Created /immoc
   [zk: localhost:2181(CONNECTED) 27] get /immoc
   imooc-data
   cZxid = 0x4
   ctime = Wed Jul 31 14:28:24 CST 2019
   mZxid = 0x4
   mtime = Wed Jul 31 14:28:24 CST 2019
   pZxid = 0x4
   cversion = 0
   dataVersion = 0
   aclVersion = 0
   ephemeralOwner = 0x0
   dataLength = 10
   numChildren = 0
   ````

   

5. ``set``命令

   `````
   set path data [version]
   修改节点的值，version是版本号，如果加上就必须和修改的节点的dataVersion一模一样
   `````

6. ``delete``命令

   ```Java
   delete path [version]
   删除节点，如果加上version 只能删除对应dataVersion的节点
   ```

   

   

## watcher机制

1. 针对每个节点的操作，都会有一个监督者 -> watcher

2. 当监控的某个对象（znode）发生了变化，则触发watcher事件

3. zk中的watcher是一次性的，触发后立即销毁

4. 父节点，子节点增删改都能触发其watcher

5. 针对不同类型的操作，触发的watcher事件也不同

   1. （子）节点创建事件
   2. （子）节点删除事件
   3. （子）节点数据变化事件

   

### watcher事件类型一

创建父节点触发：```NodeCreated```

使用如下命令都可以为节点创建watcher

```
stat path [watch] 
ls path [watch]
ls2 path [watch]
get path [watch]
```



```

[zk: localhost:2181(CONNECTED) 79] stat /imooc watch
Node does not exist: /imooc
[zk: localhost:2181(CONNECTED) 82] create /imooc 123

WATCHER::

WatchedEvent state:SyncConnected type:NodeCreated path:/imooc
Created /imooc
[zk: localhost:2181(CONNECTED) 83] 
```

修改父节点数据触发：```NodeDataChanged```

```
[zk: localhost:2181(CONNECTED) 95] get /imooc watch
222
cZxid = 0x13
ctime = Wed Jul 31 16:00:22 CST 2019
mZxid = 0x14
mtime = Wed Jul 31 16:03:06 CST 2019
pZxid = 0x13
cversion = 0
dataVersion = 1
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 3
numChildren = 0
[zk: localhost:2181(CONNECTED) 96] set /imooc 112

WATCHER::

WatchedEvent state:SyncConnected type:NodeDataChanged path:/imooc
cZxid = 0x13
ctime = Wed Jul 31 16:00:22 CST 2019
mZxid = 0x15
mtime = Wed Jul 31 16:03:46 CST 2019
pZxid = 0x13
cversion = 0
dataVersion = 2
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 3
numChildren = 0
```



删除父节点：```NodeDeleted```

```
[zk: localhost:2181(CONNECTED) 49] create /imook 11
Created /imook
[zk: localhost:2181(CONNECTED) 50] stat /imook watch
cZxid = 0x9
ctime = Wed Jul 31 15:51:48 CST 2019
mZxid = 0x9
mtime = Wed Jul 31 15:51:48 CST 2019
pZxid = 0x9
cversion = 0
dataVersion = 0
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 2
numChildren = 0
[zk: localhost:2181(CONNECTED) 51] delete /imook

WATCHER::

WatchedEvent state:SyncConnected type:NodeDeleted path:/imook
```

### watcher事件类型二

ls为父节点设置watcher，创建子节点触发：```NodeChildrenChanged```

```
[zk: localhost:2181(CONNECTED) 123] ls /           
[zookeeper, imooc]
[zk: localhost:2181(CONNECTED) 124] ls /imooc watch
[]
[zk: localhost:2181(CONNECTED) 125] create /imooc/abc 55

WATCHER::

WatchedEvent state:SyncConnected type:NodeChildrenChanged path:/imooc
Created /imooc/abc
```

ls为父节点设置watcher，删除子节点触发：```NodeChildrenChanged```

```
[zk: localhost:2181(CONNECTED) 133] ls /imooc watch   
[abc]
[zk: localhost:2181(CONNECTED) 134] delete /imooc/abc

WATCHER::

WatchedEvent state:SyncConnected type:NodeChildrenChanged path:/imooc
```

ls为父节点设置watcher，修改子节点不触发事件

只有将子节点当作一个父节点添加watcher事件，才能触发事件。

### watcher使用场景

统一资源配置

## ACL权限控制

针对节点可以设置向光读写等权限，目的为了保障数据安全性。

权限permission可以指定不同的权限范围以及角色

### ACL命令行

getAcl： 获取某个节点的acl权限信息

setAcl：设置某个节点的acl权限信息

addauth：输入认证授权信息，注册时输入明文密码（登录） 但是在zk的系统里，密码是以加密的形式存在的。

```
[zk: localhost:2181(CONNECTED) 142] getAcl /imooc/abc
'world,'anyone
: cdrwa
```

### ACL的构成一

zk的acl通过[scheme:id:permissions]来构成权限列表

scheme：代表采用的某种权限机制

id：代表允许访问的用户

permissions：权限组合字符串

### ACL的构成二

world：world下只有一个id，即只有一个用户，也就是anyone，那么组合的写法就是world:anyone:[permissions]

auth：代表认证登录，需要注册用户有权限就可以，形式为auth:user:password:[permissions]

digest：需要对密码加密才能访问，组合形式为digest:username:BASE64(SHA1(password)):[permissions]

 简而言之，auth与digest的区别就是，前者明文，后者密文。```setAcl /patch auth:lee:cdrwa``` 与 ```setAcl /path digest:username:BASE64(SHA1(password))cdrwa```是等价的，在通过addauth digest lee:lee后都能操作指定节点的权限。

ip：当设置为ip指定的ip地址，此时限制ip进行访问，比如ip:192.168.1.1:[permissions]

super：代表超级管理员，拥有所有的权限

### ACL的构成三

权限字符串缩写crdwa

1. create：创建子节点

2. read：获取节点、子节点

3. write：设置节点数据

4. delete：删除子节点

5. admin：设置权限

   

### ACL命令行学习一

```world:anyone:cdrwa```

```'world,'anyone
[zk: localhost:2181(CONNECTED) 12] setAcl /imooc/abc world:anyone:crwa 
cZxid = 0x18
ctime = Wed Jul 31 17:22:11 CST 2019
mZxid = 0x18
mtime = Wed Jul 31 17:22:11 CST 2019
pZxid = 0x18
cversion = 0
dataVersion = 0
aclVersion = 1
ephemeralOwner = 0x0
dataLength = 3
numChildren = 0
```

```
[zk: localhost:2181(CONNECTED) 12] getAcl /imooc/abc
'world,'anyone
: crwa
```

```
[zk: localhost:218[zk: localhost:2181(CONNECTED) 22] create /imooc/abc/xyz 1231
Created /imooc/abc/xyz
[zk: localhost:2181(CONNECTED) 23] delete /imooc/abc/xyz
Authentication is not valid : /imooc/abc/xyz
```

```auth```

使用auth设置权限需要添加权限用户

```
[zk: localhost:2181(CONNECTED) 31] ls /             
[names, zookeeper, imooc]
[zk: localhost:2181(CONNECTED) 32] create /names/imooc imooc
Created /names/imooc
[zk: localhost:2181(CONNECTED) 33] getAcl /names/imooc
'world,'anyone
: cdrwa
[zk: localhost:2181(CONNECTED) 34] setAcl /names/imooc auth:imooc:imooc:cdrwa
Acl is not valid : /names/imooc
[zk: localhost:2181(CONNECTED) 35] addauth digest imooc:imooc
[zk: localhost:2181(CONNECTED) 36] setAcl /names/imooc auth:imooc:imooc:cdrwa
cZxid = 0x22
ctime = Wed Jul 31 17:50:28 CST 2019
mZxid = 0x22
mtime = Wed Jul 31 17:50:28 CST 2019
pZxid = 0x22
cversion = 0
dataVersion = 0
aclVersion = 1
ephemeralOwner = 0x0
dataLength = 5
numChildren = 0
[zk: localhost:2181(CONNECTED) 37] 
```

```
[zk: localhost:2181(CONNECTED) 59] getAcl /names/imooc                
'digest,'imooc:XwEDaL3J0JQGkRQzM0DpO6zMzZs=
: cdrwa
```

只要使用了auth：设置权限以后设置的都是第一个设置的，命令可以省略的改为

```
 setAcl /names/imooc auth::cdrwa
```

```digest```

```
[zk: localhost:2181(CONNECTED) 62] create /names/test ttt
Created /names/test
[zk: localhost:2181(CONNECTED) 63] getAcl /names/test
'world,'anyone
: cdrwa
[zk: localhost:2181(CONNECTED) 64] 
[zk: localhost:2181(CONNECTED) 64] setAcl /names/test digest:imooc:XwEDaL3J0JQGkRQzM0DpO6zMzZs=:cdrwa
cZxid = 0x25
ctime = Wed Jul 31 17:56:31 CST 2019
mZxid = 0x25
mtime = Wed Jul 31 17:56:31 CST 2019
pZxid = 0x25
cversion = 0
dataVersion = 0
aclVersion = 1
ephemeralOwner = 0x0
dataLength = 3
numChildren = 0
[zk: localhost:2181(CONNECTED) 65] getAcl /names/test
'digest,'imooc:XwEDaL3J0JQGkRQzM0DpO6zMzZs=
: cdrwa
[zk: localhost:2181(CONNECTED) 66] 

```

```ip```

```
setAcl /names/ip ip:192.168.1.1:cdrwa
```

### ACL命令行学习二

1. 修改zkServer.sh 增加super管理员

2. 重启zkServer.sh

### ACL的常用使用场景

开发/测试环境分离，开发者无线操作测试库的节点，只能看

生产环境上控制指定ip的服务可以访问相关节点，防止混乱

## 选举模式和ZooKeeper的集群安装

### zookeeper集群搭建

zk集群，主从节点，心跳机制（选举模式）

当一个节点挂掉后，两个slave节点竞争，其中一个节点竞争为master，挂掉的节点重新加入集群是以slave的形式添加进去的。

![](./img/73.png)

### zookeeper集群搭建注意点

配置数据文件 myid 1/2/3 对应 server.1/2/3

通过 ./zkCli.sh -server [ip]:[port] 检测集群是否配置成功

### 伪分布式集群搭建

拷贝zookeeper

```
[root@zookeeper local]# cp zookeeper/ zookeeper02 -rf
[root@zookeeper local]# cp zookeeper zookeeper03 -rf
[root@zookeeper local]# ll
total 12
drwxr-xr-x.  2 root root     6 Apr 11  2018 bin
drwxr-xr-x.  2 root root     6 Apr 11  2018 etc
drwxr-xr-x.  2 root root     6 Apr 11  2018 games
drwxr-xr-x.  2 root root     6 Apr 11  2018 include
drwxr-xr-x.  2 root root     6 Apr 11  2018 lib
drwxr-xr-x.  2 root root     6 Apr 11  2018 lib64
drwxr-xr-x.  2 root root     6 Apr 11  2018 libexec
drwxr-xr-x.  2 root root     6 Apr 11  2018 sbin
drwxr-xr-x.  5 root root    49 Jul 30 17:27 share
drwxr-xr-x.  2 root root     6 Apr 11  2018 src
drwxr-xr-x. 12  502 games 4096 Jul 31 11:26 zookeeper
drwxr-xr-x. 12 root root  4096 Jul 31 18:41 zookeeper02
drwxr-xr-x. 12 root root  4096 Jul 31 18:41 zookeeper03
```

在``conf/``下的``zoo.cfg``文件添加配置，因为是单机部署所以要**修改端口号**，但是对应的日志文件夹什么的目录需要修改。

```
						 数据同步的端口号：选举模式通过的端口号 	
server.1=192.168.119.128:2888:3888 # 这台是master
server.2=192.168.119.128:2889:3889
server.3=192.168.119.128:2888:3890
```

在zookeeper目录dataDir目录下面创建一个```myid```文件，并添加对应的内容：1/2/3

###　真实环境下搭建集群

需要注意：环境变量的配置，ip配置不同，**端口号可以相同**

和伪分布式集群有所不同的是：端口号不用修改，但是数据同步和选举的端口号都要保持一致，myid也需要有，内容如上。

```
server.1=192.168.119.128:2888:3888 # 这台是master
server.2=192.168.119.129:2888:3888
server.3=192.168.119.130:2888:3888
```

启动成功后可以通过命令查看启动模式，这是就会有```leader```，``follower``两种显示了

## Apache curator 客户端

比较常用的zk客户端

### zk原生api的不足之处

+ 超时重连，不支持自动，需要手动操作。

+ Watch注册一次后会失效。

+ zk不支持递归创建节点

  

### Apache curator

+ Apache的开源项目

+ 解决watcher的注册一次就失效

+ Api更加简单易用

+ 提供更多解决方案并且实现简单：比如　分布式锁

+ 提供常用的Zookeeper工具类

+ 编程风格比较爽（比如建造者模式的builder）

  

### curator客户端的使用

#### 会话的连接与关闭

添加依赖

```
<!--加入zookeeper-->
<dependency>
    <groupId>org.apache.zookeeper</groupId>
    <artifactId>zookeeper</artifactId>
    <version>3.4.11</version>
</dependency>

<!-- 加入curator客户端 -->
<dependency>
    <groupId>org.apache.curator</groupId>
    <artifactId>curator-framework</artifactId>
    <version>4.0.0</version>
</dependency>

<dependency>
    <groupId>org.apache.curator</groupId>
    <artifactId>curator-recipes</artifactId>
    <version>4.0.0</version>
</dependency>
```

创建curator操作类：

```java
import org.apache.curator.RetryPolicy;
import org.apache.curator.framework.CuratorFramework;
import org.apache.curator.framework.CuratorFrameworkFactory;
import org.apache.curator.retry.*;

public class CuratorOperator {

    public CuratorFramework client = null;
    // 集群的地址使用逗号分割就好了
    public static final String zkServerPath = "192.168.119.128:2181";

    /**
     * 实例化zk客户端
     */
    public CuratorOperator() {

        // 重试的机制或者策略
        /**
         * 同步创建zk示例，原生api是异步的
         * curator链接zookeeper的策略：ExponentialBackoffRetry
         * baseSleepTimeMs: 初始化sleep的时间 两次重试的间隔时间
         * maxRetries: 最大重试次数 超时重试次数
         * maxSleepMs: 最大重试时间 超时重试最大间隔时间
         */
        //RetryPolicy retryPolicy
        //        = new ExponentialBackoffRetry(1000, 5);

        /**
         * curator链接zookeeper的策略：RetryNTimes（可以重试N次）
         * n: 重试的次数
         * sleepMsBetweenRetries: 每次重试间隔的时间
         */
        RetryPolicy retryPolicy = new RetryNTimes(3, 5000);

        /**
         * 重试一次
         * curator链接zookeeper的策略：RetryOneTime
         * sleepMsBetweenRetry: 每次重试间隔的时间
         */

        RetryPolicy retryPolicy2 = new RetryOneTime(3000);

        /**
         * 永远重试，不推荐使用
         */
        RetryPolicy retryPolicy3 = new RetryForever(5000);

        /**
         * curator链接zookeeper的策略：RetryUntilElapsed
         * maxElasedTimeMs: 最大重试时间
         * sleepMsBetweenRetries: 每次重试间隔
         * 重试时间冲啊过maxElasedTimeMs后，就不再重试
         */
        RetryPolicy retryPolicy4 = new RetryUntilElapsed(2000, 3000);

        // 启动
        client = CuratorFrameworkFactory.builder()
                .connectString(zkServerPath)
                .sessionTimeoutMs(10000).retryPolicy(retryPolicy)
                // .namespace("curator") // 命名空间
                .build();
        client.start();
    }

    /**
     * 关闭zk客户端连接
     */
    public void closeZKClient() {
        if (client != null) {
            this.client.close();
        }
    }
}
```

测试：

```
public static void main(String[] args) throws InterruptedException {
        CuratorOperator cto = new CuratorOperator();
        boolean isZkCuratorStarted = cto.client.isStarted();
        System.out.println("当前客户端的状态：" + (isZkCuratorStarted ? "连接中" : "已关闭"));

        Thread.sleep(3000);

        cto.closeZKClient();

        boolean isZkCuratorStarted2 = cto.client.isStarted();
        System.out.println("当前客户端的状态：" + (isZkCuratorStarted2 ? "连接中" : "已关闭"));
    }
```

```java
11:20:27.477 [main] INFO org.apache.zookeeper.ZooKeeper - Initiating client connection, connectString=192.168.119.131:2181,192.168.119.131:2182,192.168.119.131:2183 sessionTimeout=10000 watcher=org.apache.curator.ConnectionState@68837a77
11:20:27.479 [main] DEBUG org.apache.zookeeper.ClientCnxn - zookeeper.disableAutoWatchReset is false
11:20:28.079 [main-SendThread(192.168.119.131:2182)] INFO org.apache.zookeeper.ClientCnxn - Opening socket connection to server 192.168.119.131/192.168.119.131:2182. Will not attempt to authenticate using SASL (unknown error)
11:20:28.081 [main-SendThread(192.168.119.131:2182)] INFO org.apache.zookeeper.ClientCnxn - Socket connection established to 192.168.119.131/192.168.119.131:2182, initiating session
11:20:28.082 [main] INFO org.apache.curator.framework.imps.CuratorFrameworkImpl - Default schema
当前客户端的状态：连接中
11:20:28.083 [main-SendThread(192.168.119.131:2182)] DEBUG org.apache.zookeeper.ClientCnxn - Session establishment request sent on 192.168.119.131/192.168.119.131:2182
11:20:28.097 [main-SendThread(192.168.119.131:2182)] INFO org.apache.zookeeper.ClientCnxn - Session establishment complete on server 192.168.119.131/192.168.119.131:2182, sessionid = 0x200000c0a940000, negotiated timeout = 10000
11:20:28.099 [main-EventThread] DEBUG org.apache.curator.ConnectionState - Negotiated session timeout: 10000
11:20:28.104 [main-EventThread] INFO org.apache.curator.framework.state.ConnectionStateManager - State change: CONNECTED
11:20:31.083 [main] DEBUG org.apache.curator.framework.imps.CuratorFrameworkImpl - Closing
11:20:31.084 [Curator-Framework-0] INFO org.apache.curator.framework.imps.CuratorFrameworkImpl - backgroundOperationsLoop exiting
11:20:31.084 [main] DEBUG org.apache.curator.CuratorZookeeperClient - Closing
11:20:31.084 [main] DEBUG org.apache.curator.ConnectionState - Closing
11:20:31.085 [main] DEBUG org.apache.zookeeper.ZooKeeper - Closing session: 0x200000c0a940000
11:20:31.085 [main] DEBUG org.apache.zookeeper.ClientCnxn - Closing client for session: 0x200000c0a940000
11:20:31.096 [main-SendThread(192.168.119.131:2182)] DEBUG org.apache.zookeeper.ClientCnxn - Reading reply sessionid:0x200000c0a940000, packet:: clientPath:null serverPath:null finished:false header:: 1,-11  replyHeader:: 1,8589934595,0  request:: null response:: null
11:20:31.096 [main] DEBUG org.apache.zookeeper.ClientCnxn - Disconnecting client for session: 0x200000c0a940000
11:20:31.096 [main-SendThread(192.168.119.131:2182)] DEBUG org.apache.zookeeper.ClientCnxn - An exception was thrown while closing send thread for session 0x200000c0a940000 : Unable to read additional data from server sessionid 0x200000c0a940000, likely server has closed socket
11:20:31.096 [main] INFO org.apache.zookeeper.ZooKeeper - Session: 0x200000c0a940000 closed
当前客户端的状态：已关闭
```

#### 节点的增删改

增加```namespace```,类似于工作站

```java
client = CuratorFrameworkFactory.builder()
                .connectString(zkServerPath)
                .sessionTimeoutMs(10000).retryPolicy(retryPolicy)
                .namespace("curator") // 命名空间
                .build();
        client.start();
```

**创建节点：**

```java
// 创建节点
String nodePath = "/super/imooc";
byte[] data = "superme".getBytes();
cto.client.create().creatingParentsIfNeeded() // 如果需要创建父节点
    .withMode(CreateMode.PERSISTENT) // 创建的模式：持久化节点，临时节点、持久化顺序节点、持久化临时节点
    /**
      *     PERSISTENT(0, false, false),
      *     PERSISTENT_SEQUENTIAL(2, false, true),
      *     EPHEMERAL(1, true, false),
      *     EPHEMERAL_SEQUENTIAL(3, true, true);
      */
    .withACL(ZooDefs.Ids.OPEN_ACL_UNSAFE) // 所有权限
    .forPath(nodePath, data);
```

查看了下确实有节点创建，因为是集群查看了其他两台也是创建了的：

```
[zk: localhost:2181(CONNECTED) 0] ls /
[curator, zookeeper, new-data]
[zk: localhost:2181(CONNECTED) 1] get /curator/super/imooc
superme
cZxid = 0x200000008
ctime = Thu Aug 01 11:41:14 CST 2019
mZxid = 0x200000008
mtime = Thu Aug 01 11:41:14 CST 2019
pZxid = 0x200000008
cversion = 0
dataVersion = 0
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 7
numChildren = 0
[zk: localhost:2181(CONNECTED) 2] 
```

**修改节点**

```java
// 更新节点数据
String nodePath = "/super/imooc";
byte[] newData = "batman".getBytes();
cto.client.setData()
    .withVersion(0) // 数据版本号必须一致，这儿也可以不加，加了是为了保持一个乐观锁
    .forPath(nodePath, newData);  
```

```\
[zk: localhost:2181(CONNECTED) 1] get /curator/super/imooc
batman
cZxid = 0x200000008
ctime = Thu Aug 01 11:41:14 CST 2019
mZxid = 0x20000000e
mtime = Thu Aug 01 11:51:33 CST 2019
pZxid = 0x200000008
cversion = 0
dataVersion = 1
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 6
numChildren = 0
```

**删除节点**

```java
// 删除节点
cto.client.delete()
    // 两个方法可加可不加
    .guaranteed() // 如果删除失败，那么在后端还是继续会删除，直到成功。 万一出现网络抖动。
    .deletingChildrenIfNeeded() // 如果有子节点也一并删掉
    .withVersion(1)
    .forPath(nodePath);
```

```
[zk: localhost:2181(CONNECTED) 17] ls /curator/super
[]
```

**查询节点**

读取节点数据：

```java
// 读取节点 stat还可以取到很多节点的信息
Stat stat = new Stat();
byte[] data = cto.client.getData().storingStatIn(stat).forPath(nodePath);
System.out.println("节点：" + nodePath + "的数据为" + new String(data));
System.out.println("节点的版本号：" + stat.getVersion());
```

```
节点：/super/imooc的数据为superme
节点的版本号：0
```

查询子节点：

```java
// 查询子节点
List<String> childNodes = cto.client.getChildren().forPath(nodePath);
for (int i = 0; i < childNodes.size(); i++) {
    System.out.println(childNodes.get(i));
}
```

创建了子节点就会打印出来

```
a
b
c
```

判断节点是否为空，如果不存在则为空

```jva
Stat statExist = cto.client.checkExists().forPath(nodePath);
System.out.println(statExist);

打印结果：比如版本号，时间戳之类的 toString后的结果
8589934612,8589934612,1564632179751,1564632179751,0,3,0,0,7,3,8589934620
```

#### wach与acl的相关操作

创建自定义的watcher类

```java
public class MyCuratorWatcher implements CuratorWatcher {
    @Override
    public void process(WatchedEvent event) throws Exception {
        System.out.println("触发watcher, 节点路径：" + event.getPath());
    }
}
```

还有另一种：

```java
public class MyWatcher implements Watcher {
    @Override
    public void process(WatchedEvent event) {
        System.out.println("触发watcher, 节点路径：" + event.getPath());
    }
}
```

添加：

```java
// watcher　事件　当使用usingWatcher的时候，监听只会触发一次，监听完后就会销毁
cto.client.getData().usingWatcher(new MyCuratorWatcher()).forPath(nodePath);
// 这是原生的wacher
// cto.client.getData().usingWatcher(new MyWatcher()).forPath(nodePath);
```

```java
触发watcher, 节点路径：/super/imooc
```

另外一种方式，只需要注册一次，就可以监听多次

```java
// 监听缓存， nodeCache：监听数据节点的变更，会触发事件
final NodeCache nodeCache = new NodeCache(cto.client, nodePath);
// buildInitial: 初始化的时候获取node的值并且缓存
nodeCache.start(true);
if (nodeCache.getCurrentData() != null) {
    System.out.println("节点初始化数据为：" + new String(nodeCache.getCurrentData().getData()));
} else {
    System.out.println("节点初始化数据为空");
}
```

```
节点初始化数据为：1212
```

添加额外监听器：

```java
nodeCache.getListenable().addListener(new NodeCacheListener() {
            // 当数据发生变化
            @Override
            public void nodeChanged() throws Exception {
                String data =  new String(nodeCache.getCurrentData().getData());
                System.out.println("节点路径：" + nodeCache.getCurrentData().getPath() + "数据:" + data);
            }
        });
```

也可以使用lamda表达式

````java
nodeCache.getListenable().addListener(() -> {
            String data =  new String(nodeCache.getCurrentData().getData());
            System.out.println("节点路径：" + nodeCache.getCurrentData().getPath() + "数据:" + data);
        });
````

删除节点后这个会报错 因为节点不存在 取不出数据， ``nodeCache.getCurrentData().getData()``。增加这个监听器后，节点的数据操作都会被监听到。

**监听子节点**

```java
//        为子节点添加watcher
        // PathChildrenCache: 监听数据节点的增删改，会触发事件
        String childNodePathCache = nodePath;
        // cacheData: 设置缓存节点的数据状态
        PathChildrenCache pathChildrenCache
                = new PathChildrenCache(cto.client, childNodePathCache, true/*cacheData: 设置缓存节点的数据状态*/);
        /**
         * startMode: 初始化方式
         * POST_INITIALIZED_EVENT: 异步初始化，初始化后之后会触发事件
         * NORMAL： 异步初始化，初始化后获取不到数据
         * BUILD_INITIAL_CACHE：同步初始化，初始化后可以获取子节点的数据
         */
        pathChildrenCache.start(PathChildrenCache.StartMode.POST_INITIALIZED_EVENT);

        // 获取子节点的数据，只有设置了BUILD_INITIAL_CACHE模式的才能获取到
        List<ChildData> currentData = pathChildrenCache.getCurrentData();
        System.out.println("当前数据节点的子节点数据列表");
        for (int i = 0; i < currentData.size(); i++) {
            ChildData cd = currentData.get(i);
            String childData = new String(cd.getData());
            System.out.println(childData);
        }
        // 添加监听器
//        pathChildrenCache.getListenable().addListener(new PathChildrenCacheListener() {
//            @Override
//            public void childEvent(CuratorFramework curatorFramework, PathChildrenCacheEvent pathChildrenCacheEvent) throws Exception {
//
//            }
//        });
        // 使用lamda表达式
        pathChildrenCache.getListenable().addListener((curatorFramework, event) -> {
            if (event.getType().equals(PathChildrenCacheEvent.Type.INITIALIZED)) {
                // startmode是POST_INITIALIZED_EVENT会触发这个事件
                System.out.println("子节点初始化ok");
            } else if (event.getType().equals(PathChildrenCacheEvent.Type.CHILD_ADDED)) {
                System.out.println("添加子节点路径：" + event.getData().getPath());
                System.out.println("子节点数据：" + new String(event.getData().getData()));
            } else if (event.getType().equals(PathChildrenCacheEvent.Type.CHILD_REMOVED)) {
                System.out.println("删除子节点：" + event.getData().getPath());
            } else if (event.getType().equals(PathChildrenCacheEvent.Type.CHILD_UPDATED)) {
                System.out.println("修改子节点路径：" + event.getData().getPath());
                System.out.println("修改子节点数据：" + new String(event.getData().getData()));
            }
        });
```

#### Watcher统一配置

运维修改某一个节点，可以同步到其他节点上面

#### 权限操作

````java
public class CuratorOperatorAcl {

    public CuratorFramework client = null;
    // 集群的地址使用逗号分割就好了
    public static final String zkServerPath = "192.168.119.132:2181,192.168.119.132:2182,192.168.119.132:2183";

    /**
     * 实例化zk客户端
     */
    public CuratorOperatorAcl() {

        RetryPolicy retryPolicy = new RetryNTimes(3, 5000);

        // 启动 加入用户的登录，不再匿名
        client = CuratorFrameworkFactory.builder().authorization("digest", "immoc1:123456".getBytes())
                .connectString(zkServerPath)
                .sessionTimeoutMs(10000).retryPolicy(retryPolicy)
                .namespace("curator") // 命名空间
                .build();
        client.start();
    }

    /**
     * 关闭zk客户端连接
     */
    public void closeZKClient() {
        if (client != null) {
            this.client.close();
        }
    }

    private static String getDigestUserPwd(String id) {
        String digest = "";
        try {
            digest = DigestAuthenticationProvider.generateDigest(id);
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
        }
        return digest;
    }

    public static void main(String[] args) throws Exception {
        CuratorOperatorAcl cto = new CuratorOperatorAcl();
        boolean isZkCuratorStarted = cto.client.isStarted();
        System.out.println("当前客户端的状态：" + (isZkCuratorStarted ? "连接中" : "已关闭"));

        String nodePath = "/acl/father/child";

        List<ACL> acls = new ArrayList<ACL>();

        Id imooc1 = new Id("digest", getDigestUserPwd("imooc1:123456"));
        Id imooc2 = new Id("digest", getDigestUserPwd("imooc2:123456"));
        acls.add(new ACL(ZooDefs.Perms.ALL, imooc1));
        acls.add(new ACL(ZooDefs.Perms.READ, imooc2));
        acls.add(new ACL(ZooDefs.Perms.DELETE | ZooDefs.Perms.CREATE, imooc2));

        // 创建节点
        byte[] bytes = "spiderman".getBytes();
        cto.client.create().creatingParentsIfNeeded()
                .withMode(CreateMode.PERSISTENT)
                // 如果添加了true那么权限就会影响父节点，简单说就是父节点也会有相应的权限
                // 这儿创建就是一边创建一边赋予权限，因为是匿名登录会报错，因为没有权限，需要登录
                .withACL(acls, true)
                .forPath(nodePath, bytes);
		
        // 设置权限
        cto.client.setACL().withACL(acls).forPath("/curatorNode");
        
        Thread.sleep(10000000);

        cto.closeZKClient();

        boolean isZkCuratorStarted2 = cto.client.isStarted();
        System.out.println("当前客户端的状态：" + (isZkCuratorStarted2 ? "连接中" : "已关闭"));
    }
}
````



