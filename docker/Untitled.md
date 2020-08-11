## docker安装centos

执行如下命令创建一个centos7的容器，会自动从网上下载centos7的镜像。

````
docker run --ip=172.17.0.2 --privileged=true centos:7 /usr/sbin/init
````

–ip表示指定创建容器的IP地址，–privileged=true表示特权模式运行容器，否则在容器内启动mysql服务时会报错。

````
docker pull centos:7
````

```
docker run -it centos:7 /bin/bash
```

进入容器
需要注意的是：docker run 只在第一次创建容器的时候使用，如果重启docker 后可以使用docker start 容器id/容器名来启动一个容器
容器id比较复杂，建议docker rename 容器id 容器别名 取一个自己好记一点的名字

进入容器后先安装一些基础服务

````
curl http://mirrors.aliyun.com/repo/Centos-7.repo > /etc/yum.repos.d/CentOS-Base-7-aliyun.repo
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
````

```
yum makecache
```

```
yum install -y net-tools which openssh-clients openssh-server iproute.x86_64 wget
```

REPOSITORY     TAG         IMAGE ID      CREATED       SIZE

tomcat       latest       94e31e5297d1    3 months ago    507MB

centos       7          5e35e350aded    4 months ago    203MB

## docker安装达梦数据库

````
docker run --privileged -itd --name dm7_centos -p 5236:5236 \
 -v /***/dm7:/data \   # 此处挂载的是iso文件，本地解压之后的文件路径
 -v /***/dmPython:/data/dm_Python \  # 此处挂载的是dmPython.zip本地解压之后的文件路径
 ***/centos:6.20.1833 /usr/sbin/init
````

```
docker run --privileged -itd --name dm7_centos -p 5236:5236 \ -v /***/dm7:/data \   -v /***/dmPython:/data/dm_Python \   ***/centos:6.20.1833 /usr/sbin/init
```

