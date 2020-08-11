## ElasticSearch安装

通过官网下好

### 单实例安装

**Java开发的时候要保证es的版本和jar包的版本一直**

```
tar -vxf elasticsearch-7.6.1-darwin-x86_64.tar.gz 
```

![image-20200427102832848](/Users/litian/Library/Application Support/typora-user-images/image-20200427102832848.png)

#### 熟悉目录

1、bin 执行文件

2、config 配置文件

​	1、log42j：配置文件

​    2、jvm.options java虚拟机相关配置：电脑配置低的要修改内存大小

​	3、elasticsearch.yml配置文件，默认端口号9200，跨域也修改这个文件

3、lib 相关jar包

4、modules 功能模块

5、plugins：插件，比如IK分词器就放这个目录下

6、logs：日志

#### 启动

````
sh ./bin/elasticsearch
````

#### 启动报错处理

> 第一次解决方式（[参考原文](https://www.cnblogs.com/landhu/p/5206136.html)）：

bash 3.0后，shell中加入了新的符号"<<<" 可以获取子任务，把 elasticsearch-env 文件中第116行代码中的 '< <' 改为了 '<<<',改完后执行不再报这个错误，但是错误变成了 : /bin/elasticsearch-env: line 116: syntax error near unexpected token `(' 



> 第二步解决方式（[参考原文](https://blog.csdn.net/su20145104009/article/details/91458006)）：

把 elasticsearch-env 文件中前置行的脚本内容遵循改为：

`````  
set +o posix
`````

执行后成功启动

访问localhost:9200

![image-20200427110149483](/Users/litian/Library/Application Support/typora-user-images/image-20200427110149483.png)





### 插件安装

1、在github搜索elasticsearch-head

2、 下载第一个mobz的压缩包

3、 解压

4、cd进目录执行npm install

5、修改**elasticsearch**配置文件文件处理跨域

```
vim config/elasticsearch.yml
```

在配置的最后面加上

````
http.cors.enabled: true
http.cors.allow-origin: "*"
````

6、启动head插件

````
npm start
````

7、效果

![image-20200427112144045](/Users/litian/Library/Application Support/typora-user-images/image-20200427112144045.png)



### 安装IK分词器

https://github.com/medcl/elasticsearch-analysis-ik/releases

解压放入plugins文件即可