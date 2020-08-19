## 准备环境并部署Activiti6.0

### 准备物料

+ Activiti软件包activiti-6.0.0.zip

   https://github.com/Activiti/Activiti/releases/download/activiti-6.0.0/activiti-6.0.0.zip

+ Java环境1.8

+ Servlet容器tomcat8

### 部署流程

1. 解压缩下载好的Activiti压缩包，将war目录下的app和admin两个war包放进tomcat里面并启动
2. 启动命令：`sh startup.sh`
3. 查看启动日志：`tail -200f ${tomcat-homt}/logs/catalina.out`
4. 访问程序：`open http://localhost:8080/activiti-app`
5. 页面输入用户名：`admin`，  密码：`test`即可查看

### 流程体验

## Activiti6.0源码初探

### Activiti6.0源码概述

1. Clone 代码
2. 创建本地分支：`git checkout -b activiti-study activiti-6.0.0`
3. 编译：`mvn clean test-compile`
4. 导入idea



## Activiti6.0引擎配置

### 流程引擎配置类的作用

+ 查找并解析xml配置文件activiti.cfg.xml
+ 提供多个静态方法创建配置对象
+ 实现了几个基于不用场景的子类，配置方式灵活

![image-20200302104147936](/Users/litian/Library/Application Support/typora-user-images/image-20200302104147936.png)

![image-20200302104231929](/Users/litian/Library/Application Support/typora-user-images/image-20200302104231929.png)

![image-20200302104357630](/Users/litian/Library/Application Support/typora-user-images/image-20200302104357630.png)

+ ProcessEngineCinfiguration

  + ProcessEngineConfigurationImpl

    虽以impl结尾但不是实现，而是抽象类，这个类里面配置了ProcessEngineCinfiguration大多的80%的属性配置，还有一些get/set方法

  + StandaloneProcessEngineCinfiguration

    如果说要独立部署引擎，我们可以用它根据new 的方法创建对象，然后再去set具体的配置属性

  + SpringProcessEngineCinfiguration

    基于Spring的集成完成了spring对它的功能的扩展，比如数据源配置的扩展，自动加载

    + 开启工作流接口
    + 获取历史流程记录
    + 获取工作流的流程图接口
    + 任务提交审核的接口
    + 驳回接口

![image-20200303135700457](/Users/litian/Library/Application Support/typora-user-images/image-20200303135700457.png)

![image-20200303135755452](/Users/litian/Library/Application Support/typora-user-images/image-20200303135755452.png)

![image-20200303135809804](/Users/litian/Library/Application Support/typora-user-images/image-20200303135809804.png)

```
/**
 * 分页Post请求示例
 * @param departmentDTO
 * @param currentPage
 * @param pageSize
 * @return 分页<数据实体>
 */
@ApiOperation(value = "分页Post请求示例", notes = "传递整个条件Dto以及分页信息，Post请求查询分页列表")
@CrossOrigin
@ApiImplicitParams({
        @ApiImplicitParam( name = "currentPage", value = "查询的页数", required = true, dataType = "Integer"),
        @ApiImplicitParam( name = "pageSize", value = "每页查询的数量", required = true, dataType = "Integer"),
        @ApiImplicitParam( name = "departmentDTO", value = "查询的条件dto", required = false, dataType = "DepartmentDTO")
})
@PostMapping("/findPaginationPage/{currentPage}/{pageSize}")
JsonResponse<Page<DepartmentDTO>> findPaginationPage(@RequestBody DepartmentDTO departmentDTO,
                                                     @PathVariable Integer currentPage,
                                                     @PathVariable Integer pageSize);
```

![image-20200303144457905](/Users/litian/Library/Application Support/typora-user-images/image-20200303144457905.png)

![image-20200303144615334](/Users/litian/Library/Application Support/typora-user-images/image-20200303144615334.png)

![image-20200303152232286](/Users/litian/Library/Application Support/typora-user-images/image-20200303152232286.png)

提交之后添加监听

![image-20200303210223991](/Users/litian/Library/Application Support/typora-user-images/image-20200303210223991.png)

![image-20200303210430773](/Users/litian/Library/Application Support/typora-user-images/image-20200303210430773.png)

![image-20200303210644441](/Users/litian/Library/Application Support/typora-user-images/image-20200303210644441.png)

