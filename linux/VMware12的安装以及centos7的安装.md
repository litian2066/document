## VMware12的安装以及centos7的安装

### VMware12的安装

文件上传到了百度网盘：https://pan.baidu.com/s/13wBkPhWNvwq7SmyTt2Afug 提取码：fz6m





![1](./img/1.png)



![2](./img/2.png)



![3](./img/3.png)



![4](./img/4.png)



![5](./img/5.png)

### VMware安装Centos7

这儿安装的是[CentOS-7-x86_64-DVD-1804.iso](http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1804.iso)

已经上传到了百度云盘：https://pan.baidu.com/s/1wZ2k1wH8hz-MBYws9flQQQ   提取码：zt89

![6](./img/6.png)

![7](./img/7.png)

![8](./img/8.png)

![9](./img/9.png)

![10](./img/10.png)

![11](./img/11.png)

![12](./img/12.png)

![13](./img/13.png)

![14](./img/14.png)

![15](./img/15.png)

![16](./img/16.png)

![17](./img/17.png)

![18](./img/18.png)

![19](./img/19.png)

![20](./img/20.png)

![21](./img/21.png)

![22](./img/22.png)

![23](./img/23.png)

![24](./img/24.png)

![25](./img/25.png)

![26](./img/26.png)

![27](./img/27.png)

![28](./img/28.png)

![29](./img/29.png)

![30](./img/30.png)

![31](./img/31.png)

![32](./img/32.png)

![33](./img/33.png)

![34](./img/34.png)

![35](./img/35.png)

![36](./img/36.png)

![37](./img/37.png)



![38](./img/38.png)

等待进度条后重启，重启后会有如下操作：

![](./img/39.png)



![](./img/40.png)

成功启动后输入root的用户名和密码登录，接着会有一系列的选项，**其中有隐私的选项记得打开**，这样就会有服务，可以访问互联网。

**关闭防火墙**

```
systemctl stop firewalld # 临时关闭防火墙
systemctl disable firewalld # 禁止开机启动
```

**重启服务**

```yiyiyial
service network restart
```

**配置网络工作**

在/etc/sysconfig/network文件里增加如下配置

```
vi /etc/sysconfig/network
修改：
NETWORKING=yes # 网络是否工作，此处一定不能为no
```

以下配置这次并没有用到，仅供参考。

**配置ip地址等信息**

```
vi   /etc/sysconfig/network-scripts/ifcfg-ens33
```

修改如下：

```
TYPE="Ethernet"   # 网络类型为以太网
BOOTPROTO="static"  # 手动分配ip
NAME="ens33"  # 网卡设备名，设备名一定要跟文件名一致
DEVICE="ens33"  # 网卡设备名，设备名一定要跟文件名一致
ONBOOT="yes"  # 该网卡是否随网络服务启动
IPADDR="192.168.220.101"  # 该网卡ip地址就是你要配置的固定IP，如果你要用xshell等工具连接，220这个网段最好和你自己的电脑网段一致，否则有可能用xshell连接失败
GATEWAY="192.168.220.2"   # 网关
NETMASK="255.255.255.0"   # 子网掩码
DNS1="8.8.8.8"    # DNS，8.8.8.8为Google提供的免费DNS服务器的IP地址
```

**配置公共DNS服务(可选)**

在/etc/resolv.conf文件里增加如下配置

```
nameserver 8.8.8.8
```

**关机命令**

```
poweroff
```



### 使用vmware的克隆功能

右键点击虚拟机，选择“管理”、“克隆

![](./img/62.png)



![](./img/63.png)



![](./img/64.png)



![](./img/65.png)

修改主机名：

````
hostnamectl set-hostname   xxxx(你要的主机名字)
````



这儿加上一些配置的修改，我这儿没有使用到，比如修改ip地址：

 修改hosts文件，将名字和IP建立联系

输入命令“vi /etc/hosts”后，在配置文件中加入

```
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
192.168.220.103（你锁修改的主机IP）   xxxxxxxx(你要的主机名字)
```

重启:reboot 



修改配置文件**/etc/sysconfig/network-scripts/ifcfg-ens33中的IPADDR**

````
IPADDR="192.168.220.102"
````



### 使用secureCRT连接linux

secureCRT以及其注册机已经上传百度云：https://pan.baidu.com/s/12ctaGvcFewkk3uFWFo2p7Q 提取码：dfnf

#### 安装secureCRT

![](./img/41.png)



![](./img/42.png)



![](./img/43.png)



![](./img/44.png)



![](./img/45.png)



![](./img/46.png)

#### 激活secureCRT

打开注册机

![](./img/47.png)

![](./img/49.png)

![](./img/50.png)

![](./img/51.png)

![](./img/52.png)

![](./img/53.png)

![](./img/54.png)

![](./img/55.png)

![](./img/56.png)

![](./img/57.png)

![](./img/58.png)

![](./img/59.png)

![](./img/60.png)

![](./img/61.png)

### 安装JDK

1. 安装rz命令

   rz命令是可以上传本地文件的命令，因为网络配置OK就可以直接yum安装：yum install lrzsz

2.  安装jdk

   1. 下载linux的jdk1.8.tar， 上传至服务器

      文件已经上传到百度云，地址：https://pan.baidu.com/s/1NuNtx-1JXKXvYQN5un_W_A

      提取码：mehn

      使用rz命令上传到linux服务器

      ```
      rz
      rz waiting to receive.
      Starting zmodem transfer.  Press Ctrl+C to cancel.
        100%  155292 KB 25882 KB/s 00:00:06       0 Errors
      ```

   2. 解压缩jdk，配置jdk

      ```
      tar -zxvf jdk-8u11-linux-x64.tar.gz
      ```

      解压完成后，重新命名：

      ```
      mv jdk1.8.0_11/ jdk8
      ```

      移动文件夹到/usr/

      ```
      mv jdk8 /usr/
      ```

      cd到对应的jdk8目录，执行```pwd```命令，然后复制jdk路径

      配置环境

      ````
      vim /etc/profile
      ````

      如果修改文件错误，可以强制退出

      ````
      :q!
      ````

      在````export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL```下面添加配置

      ```
      export JAVA_HOME=/usr/jdk8 #jdk安装目录
      export CLASSPATH=.:%JAVA_HOME%/lib/dt.jar:%JAVA_HOME%/lib/tools.jar
      export PATH=$PATH:$JAVA_HOME/bin
      ```

      

   3. 测试： java -version 显示版本号

      ```
      [root@zookeeper jdk8]# java -version
      openjdk version "1.8.0_161"
      OpenJDK Runtime Environment (build 1.8.0_161-b14)
      OpenJDK 64-Bit Server VM (build 25.161-b14, mixed mode)
      ```

      如果没有显示java版本信息可以使用```source```命令刷新配置文件

      ```
      source /etc/profile
      ```

      

