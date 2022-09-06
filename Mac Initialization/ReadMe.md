# Maven配置

1. 访问官网

   https://maven.apache.org/

2. 下载文件

   ![image-20220508110047890](/Users/litian/Documents/lian2077/documents/documents/Mac Initialization/images/image-20220508110047890.png)

3. 解压到对应的目录，并配置对应的本地仓库地址

   + 修改解压后conf文件夹里面的setting文件

     ![image-20220508110448531](/Users/litian/Documents/lian2077/documents/documents/Mac Initialization/images/image-20220508110448531.png)

   + 在`mirrors`标签里面添加阿里云镜像

     ```xml
     <mirror>
       <id>alimaven</id>
       <mirrorOf>central</mirrorOf>
       <name>aliyun maven</name>
       <url>http://maven.aliyun.com/nexus/content/groups/public</url>
     </mirror>
     ```

     ![image-20220508110634102](/Users/litian/Documents/lian2077/documents/documents/Mac Initialization/images/image-20220508110634102.png)

4. 修改mac配置文件，添加maven支持

   1. 终端里面输入`vim ~/.bash_profile`

   2. 添加以下配置（maven安装目录为你的本地目录），保存后退出

      ```
      MAVEN_HOME=/Users/litian/Documents/lian/applications/apache-maven-3.8.5
      
      PATH=$MAVEN_HOME/bin:$PATH
      
      export MAVEN_HOME
      
      export PATH
      ```

      在终端里面输入`source .bash_profile`刷新配置文件

   3. 输入`mvn -v`命令查看是否配置成功

      ````shell
      ➜  ~ source .bash_profile
      ➜  ~ mvn -v
      Apache Maven 3.8.5 (3599d3414f046de2324203b78ddcf9b5e4388aa0)
      Maven home: /Users/litian/Documents/lian/applications/apache-maven-3.8.5
      Java version: 1.8.0_181, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/jdk1.8.0_181.jdk/Contents/Home/jre
      Default locale: zh_CN, platform encoding: UTF-8
      OS name: "mac os x", version: "10.15.7", arch: "x86_64", family: "mac"
      ````

      