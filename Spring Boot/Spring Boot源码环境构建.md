1. 从github上面下载源码
2. 在目录下执行`mvn clean install -DskipTests -Pfast`命令，该命令为跳过test打包，并执行pom文件下`<profile>`标签下id为fast的选项
3. 耐心等待下载完成后，将项目导入idea，新建一个module，添加锁需要的模块引用到 pom文件即可
4. 在源码工程中新建module然后引入对应的依赖。