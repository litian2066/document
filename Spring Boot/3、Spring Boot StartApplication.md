# 理解StartApplication

Spring Framework

1. Spring 模式注解

2. Spring 应用上下文

3. Spring 工厂加载机制

4. Spring 应用上下文初始器

5. Spring Environment 抽象

6. Spring 应用时间/监听器

   

Spring Boot

1. SpringApplication

2. SpringApplication Builder API

3. SpringApplication 运行监听器

4. SpringApplication 参数

5. SpringApplication 故障分析

   

## Spring Boot 准备阶段

### SpringApplication

定义：Spring应用引导类，提供便利的自定义行为方法

场景：嵌入式Web应用和非Web应用

运行：SpringApplication#run(String...)

## SpringApplication基本使用

### SpringApplication运行

```java
SpringApplication.run(DevInSpringBootApplication.class, args);
```

`DevInSpringBootApplication.class`是配置元(配置class)，需要`@SpringBootApplication`修饰，因为`@SpringBootApplication`是模式注解，标记是`配置bean`，所以才能进行装配

也不一定当前类作为引导类也行

```java
public class DevInSpringBootApplication {

    public static void main(String[] args) {
				// 需要丢进去的不一定是主类，只要是一个配置类就行了
        SpringApplication.run(ApplicationConfiguration.class, args);
    }

    @SpringBootApplication
    public static class ApplicationConfiguration {

    }
}
```

### 自定义 SpringApplication

````java
public class DevInSpringBootApplication {

    public static void main(String[] args) {

        // SpringApplication.run(ApplicationConfiguration.class, args);
        Set<String> sources = new HashSet<String>();
        sources.add(ApplicationConfiguration.class.getName());

        SpringApplication springApplication = new SpringApplication();
        springApplication.setSources(sources);
        ConfigurableApplicationContext context = springApplication.run(args);

        System.out.println(context);

    }

    @SpringBootApplication
    public static class ApplicationConfiguration {

    }
}
````

这种方式也行

#### 通过 SpringApplication API调整

`流畅的API，这儿就不再演示了`

## 准备阶段

`SpringApplication`类准备的过程会有很多类被初始化，比如推导Web类型，推断引导类....

````java
// 这是SpringApplication的构造方法
/*
	primarySources: 传入配置Bean
*/
public SpringApplication(ResourceLoader resourceLoader, Class... primarySources) {
        this.sources = new LinkedHashSet();
        this.bannerMode = Mode.CONSOLE;
        this.logStartupInfo = true;
        this.addCommandLineProperties = true;
        this.addConversionService = true;
        this.headless = true;
        this.registerShutdownHook = true;
        this.additionalProfiles = new HashSet();
        this.isCustomEnvironment = false;
        this.resourceLoader = resourceLoader;
  			// Java 断言
        Assert.notNull(primarySources, "PrimarySources must not be null");
        this.primarySources = new LinkedHashSet(Arrays.asList(primarySources));
    		// 推断Web类型
        this.webApplicationType = WebApplicationType.deduceFromClasspath();
        // 初始化上下文				             	
        this.setInitializers(
        this.getSpringFactoriesInstances(ApplicationContextInitializer.class));
        // 初始化监听器
        this.setListeners(this.getSpringFactoriesInstances(ApplicationListener.class));
        // 推断引导类    
        this.mainApplicationClass = this.deduceMainApplicationClass();
    }
````



### 配置 Spring Bean 来源

Java 配置 Class 或 XML 上下文配置文件集合，用于 Spring Boot `BeanDefinitionLoader` 读取 ，并且将配置源解析加载为 Spring Bean 定义

+ 数量：一个或多个以上

  ```java
  SpringApplication.run(StartApplication.class, args);
  ```

  

  ```java
  /**
  	在SpringApplication的构造函数里面可以看见会加载不止一个class
  **/
  public SpringApplication(Class... primarySources) {
      this((ResourceLoader)null, primarySources);
  }
  ```

  再来看看`BeanDefinitionLoader `的构造器

  ````java
  // bean定义的注册器
  BeanDefinitionLoader(BeanDefinitionRegistry registry, Object... sources) {
      Assert.notNull(registry, "Registry must not be null");
      Assert.notEmpty(sources, "Sources must not be empty");
      this.sources = sources;
      // 注册注解
      this.annotatedReader = new AnnotatedBeanDefinitionReader(registry);
      // 注册XML
      this.xmlReader = new XmlBeanDefinitionReader(registry);
      if (this.isGroovyPresent()) {
          this.groovyReader = new GroovyBeanDefinitionReader(registry);
      }
  
      this.scanner = new ClassPathBeanDefinitionScanner(registry);
      this.scanner.addExcludeFilter(new BeanDefinitionLoader.ClassExcludeFilter(sources));
  }
  ````

  `显而易见，这儿的BeanDefinitionLoader可以支持Java配置的class或者xml上下文的配置文件`

#### Java 配置 Class

用于 Spring 注解驱动中 Java 配置类，大多数情况是 Spring 模式注解所标注的类，如`@Configuration` 

上文有演示过

#### XML 上下文配置文件

用于 Spring 传统配置驱动中的 XML 文件。这儿略过

### 推断 Web 应用类型 

根据当前应用 ClassPath 中是否存在相关实现类来推断 Web 应用的类型，包括:

+ Web Reactive: ` WebApplicationType.REACTIVE `
+ Web Servlet： WebApplicationType.SERVLET 
+ 非 Web： WebApplicationType.NONE

参考方法： org.springframework.boot.SpringApplication#deduceWebApplicationType

````java
private WebApplicationType deduceWebApplicationType() {
    // DispatcherHandler存在 DispatcherServlet/ResourceConfig 不存在 
    if (ClassUtils.isPresent("org.springframework.web.reactive.DispatcherHandler", (ClassLoader)null) && !ClassUtils.isPresent("org.springframework.web.servlet.DispatcherServlet", (ClassLoader)null) && !ClassUtils.isPresent("org.glassfish.jersey.server.ResourceConfig", (ClassLoader)null)) {
        return WebApplicationType.REACTIVE;
    } else {
        String[] var1 = WEB_ENVIRONMENT_CLASSES;
        int var2 = var1.length;

        for(int var3 = 0; var3 < var2; ++var3) {
            String className = var1[var3];
            if (!ClassUtils.isPresent(className, (ClassLoader)null)) {
                return WebApplicationType.NONE;
            }
        }
	   // 显然默认是Servlet的Web
        return WebApplicationType.SERVLET;
    }
}
````

```java
// 也可以自定义设置
springApplication.setWebApplicationType(WebApplicationType.NONE);
```

`````
如果仅存在 Reactive 的包，则为WebApplicationType.REACTIVE类型；
如果 Servlet 和 Reactive的包都不存在，则为WebApplicationType.NONE类型；
其他情况都为WebApplicationType.SERVLET类型。
`````



### 推断引导类（Main Class）

根据 Main 线程执行堆栈判断实际的引导类

其将调用栈中`main`方法所在的类作为引导类。

参考方法： `org.springframework.boot.SpringApplication#deduceMainApplicationClass`

```java
private Class<?> deduceMainApplicationClass() {
    try {
        StackTraceElement[] stackTrace = (new RuntimeException()).getStackTrace();
        StackTraceElement[] var2 = stackTrace;
        int var3 = stackTrace.length;

        for(int var4 = 0; var4 < var3; ++var4) {
            StackTraceElement stackTraceElement = var2[var4];
            if ("main".equals(stackTraceElement.getMethodName())) {
                return Class.forName(stackTraceElement.getClassName());
            }
        }
    } catch (ClassNotFoundException var6) {
    }

    return null;
}
```

### 加载应用上下文初始器 `（ ApplicationContextInitializer ）`

利用 Spring 工厂加载机制，实例化 ApplicationContextInitializer 实现类，并排序对象集合。

+ 实现

  ````java
  private <T> Collection<T> getSpringFactoriesInstances(Class<T> type) {
      return this.getSpringFactoriesInstances(type, new Class[0]);
  }
  
  private <T> Collection<T> getSpringFactoriesInstances(Class<T> type, Class<?>[] parameterTypes, Object... args) {
      ClassLoader classLoader = this.getClassLoader();
      Set<String> names = new LinkedHashSet(SpringFactoriesLoader.loadFactoryNames(type, classLoader));
      List<T> instances = this.createSpringFactoriesInstances(type, parameterTypes, classLoader, args, names);
      AnnotationAwareOrderComparator.sort(instances);
      return instances;
  }
  
  private <T> List<T> createSpringFactoriesInstances(Class<T> type, Class<?>[] parameterTypes, ClassLoader classLoader, Object[] args, Set<String> names) {
      List<T> instances = new ArrayList(names.size());
      Iterator var7 = names.iterator();
  
      while(var7.hasNext()) {
          String name = (String)var7.next();
  
          try {
              Class<?> instanceClass = ClassUtils.forName(name, classLoader);
              Assert.isAssignable(type, instanceClass);
              Constructor<?> constructor = instanceClass.getDeclaredConstructor(parameterTypes);
              T instance = BeanUtils.instantiateClass(constructor, args);
              instances.add(instance);
          } catch (Throwable var12) {
              throw new IllegalArgumentException("Cannot instantiate " + type + " : " + name, var12);
          }
      }
  
      return instances;
  }
  ````

  主要方法应该是如下

  ```java
  private static Map<String, List<String>> loadSpringFactories(@Nullable ClassLoader classLoader) {
      MultiValueMap<String, String> result = (MultiValueMap)cache.get(classLoader);
      if (result != null) {
          return result;
      } else {
          try {
              Enumeration<URL> urls = classLoader != null ? classLoader.getResources("META-INF/spring.factories") : ClassLoader.getSystemResources("META-INF/spring.factories");
              LinkedMultiValueMap result = new LinkedMultiValueMap();
  
              while(urls.hasMoreElements()) {
                  URL url = (URL)urls.nextElement();
                  UrlResource resource = new UrlResource(url);
                  Properties properties = PropertiesLoaderUtils.loadProperties(resource);
                  Iterator var6 = properties.entrySet().iterator();
  
                  while(var6.hasNext()) {
                      Entry<?, ?> entry = (Entry)var6.next();
                      String factoryClassName = ((String)entry.getKey()).trim();
                      String[] var9 = StringUtils.commaDelimitedListToStringArray((String)entry.getValue());
                      int var10 = var9.length;
  
                      for(int var11 = 0; var11 < var10; ++var11) {
                          String factoryName = var9[var11];
                          result.add(factoryClassName, factoryName.trim());
                      }
                  }
              }
  
              cache.put(classLoader, result);
              return result;
          } catch (IOException var13) {
              throw new IllegalArgumentException("Unable to load factories from location [META-INF/spring.factories]", var13);
          }
      }
  }
  ```

  

+ 技术

  实现类： org.springframework.core.io.support.SpringFactoriesLoader 

  配置资源： META-INF/spring.factories 

  排序： AnnotationAwareOrderComparator#sort

  `排序不是Order接口或者Ordered接口而是如下`

  ```java
  public class AnnotationAwareOrderComparator extends OrderComparator {
      public static void sort(List<?> list) {
          if (list.size() > 1) {
              list.sort(INSTANCE);
          }
  
      }
  }    
  ```

  ````java
  public class OrderComparator implements Comparator<Object> {
  }
  ````

  `通过实现比较器来实现排序`

  

#### 网上资料

````java
1. 通过SpringFactoriesLoader.loadFactoryNames(type, classLoader)方法，在 META-INF/spring.factories 文件下查找ApplicationContextInitializer类型对应的资源名称。
2. 实例化上面的资源信息（初始化器）。
对初始化器根据Ordered接口或者@Order注解进行排序。

同理，初始化listeners监听器也是类似的，这里不再赘诉。
````

#### 自定义上下文初始化

````java
// 这里不想写代码
// 1.创建两个类
@Order(Ordered.HIGHEST_P....)
public class HelloWorldApplicationContextInitillizer<C extends ConfigurableApplicationContext> implements ApplicationContextInitializer<C> {
    @Override
    public void initalize(C applicaitonContext) {
        sout(applicaitonContext.getId())
    }
}

public class AfterHell..... implements ApplicationContextInitializer, Order {
    @Override
    public void initalize(ConfigurableApplicationContext conetxt) {
     sout(conetxt.getId())   
    }
    // 排序的方法，区别于注解
    @Override
    public int getOrder() {
    	return Ordered.LOWEST_..
    }
}
// 2.两个类配置进spring.factories里面，在resources目录下新建META-INF目录新建这个文件
org...............ApplicationContextInitializer =\
XXXXXX,\
xxxxx
// 3.启动引导类就可以了
````

### 加载应用事件监听器（ ApplicationListener ）

利用 Spring 工厂加载机制，实例化 ApplicationListener 实现类，并排序对象集合

```java
this.setListeners(this.getSpringFactoriesInstances(ApplicationListener.class));
```

````java
@FunctionalInterface
public interface ApplicationListener<E extends ApplicationEvent> extends EventListener {
    void onApplicationEvent(E var1);
}

````

同样也是读取spring.factories来监听

这儿监听的是Spring boot的事件，Spring boot事件是基于Spring 的事件的

####  Spring 事件

Spring 的事件是基于一个`EventObject`的类，是所有事件的源

举个例子

````java
public abstract class ApplicationEvent extends EventObject {
    private static final long serialVersionUID = 7099057708183571937L;
    private final long timestamp = System.currentTimeMillis();

    public ApplicationEvent(Object source) {
        super(source);
    }

    public final long getTimestamp() {
        return this.timestamp;
    }
}
````

自定义

监听上下文刷新事件

````java
@Order(Ordered.HIGHEST_PRECEDENCE)
public class HelloWorldApplicationListener implements ApplicationListener<ContextRefreshedEvent> {

    @Override
    public void onApplicationEvent(ContextRefreshedEvent event) {
        System.out.println("HelloWorld : " + event.getApplicationContext().getId());
    }
}

@Order(Ordered.LOWEST_PRECEDENCE)
public class AfterHelloWorldApplicationListener implements ApplicationListener<ContextRefreshedEvent> {

    @Override
    public void onApplicationEvent(ContextRefreshedEvent event) {
        System.out.println("AfterHelloWorld : " + event.getApplicationContext().getId());
    }
}
````

```pro
# Application Listeners
org.springframework.context.ApplicationListener=\
  com.dev.devinspringboot.listener.HelloWorldApplicationListener,\
  com.dev.devinspringboot.listener.AfterHelloWorldApplicationListener
```

`启动测试`

```java
HelloWorld : application
AfterHelloWorld : application
```

## 运行阶段

````java
SpringApplication 运行阶段属于核心过程，完全围绕 run(String...) 方法展开。该过程结合初始化阶段完成的状态，进一步完善运行时所需要准备的资源，随后启动 Spring 应用上下文。在此期间伴随着 Spring Boot 和 Spring 事件的触发，形成完整的 SpringApplication 生命周期。因此，下面将围绕以下三个子议题进行讨论。

SpringApplication 准备阶段
ApplicationContext 启动阶段
ApplicationContext 启动后阶段

作者：habit_learning
链接：https://www.jianshu.com/p/c2789f1548ab
来源：简书
简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。
````

