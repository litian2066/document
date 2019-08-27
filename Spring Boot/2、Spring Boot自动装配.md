# Spring Framework手动装配

## Spring 模式注解装配

定义：一种用于声明在应用中扮演“组件”角色的注解。如Spring Framework中的`@Repository`标注在任何类上，用于仓储角色的模式注解。

举例：`@Component(Spring2.5)`、`@Service(Spring2.5)`、`@Configuration(Spring3)`等

装配：`<context:component-scan>（spring2.5）`或`@ComponentScan(Spring3.1)`

`@Component(Spring2.5)`作为一种由Spring容器托管的通用模式注解，任何被`@Component(Spring2.5)`标记的注解均为组件扫描的候选对象。类似地，凡是被`@Component(Spring2.5)`元标注(**meta-annotated**)的注解，如`@Service`，当任何组件标注它时，也被视作组件扫描的候选对象。

### 模式注解举例

| Spring Framework注解 | 场景说明          | 起始版本 |
| -------------------- | ----------------- | -------- |
| `@Repository`        | 数据仓储模式注解  | 2.0      |
| `@Component`         | 通用组件模式注解  | 2.5      |
| `@Service`           | 服务模式注解      | 2.5      |
| `@Controller`        | Web控制器模式注解 | 2.5      |
| `@Configuration`     | 配置类模式注解    | 3.0      |

### 装配方式

#### `<context:component-scan>`方式

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:context="http://www.springframework.org/schema/context"
xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-
context.xsd">
    <!-- 激活注解驱动特性 -->
    <!-- <context:annotation-config /> -->
    <!-- 找寻被 @Component 或者其派生 Annotation 标记的类（Class），将它们注册为 Spring Bean -->
    <!-- 在Spring3的某个版本后两行代码合并为一行了 -->
    <context:component-scan base-package="com.imooc.dive.in.spring.boot" />
    
</beans>
```

####`@ComponentScan`方式

典型的Java Config方式

```java
@ComponentScan(basePackages = "com.imooc.dive.in.spring.boot")
public class SpringConfiguration {
...
}
```

### 自定义模式注解

#### `@Component`派生性

```java
**
 * 一级 {@link Repository @Repository}
 *
 * @author <a href="mailto:mercyblitz@gmail.com">Mercy</a>
 * @since 1.0.0
 */
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Repository
public @interface FirstLevelRepository {
    String value() default "";
}
```

测试

````java
@FirstLevelRepository(value = "myFirstLevelRepository") // bean名称
public class MyFirstLevelRepository {
}
````

```java
@ComponentScan(basePackages = "com.dev.devinspringboot.repository")
public class RepositoryBootstrap {

    public static void main(String[] args) {
        ConfigurableApplicationContext context =
                new SpringApplicationBuilder(RepositoryBootstrap.class)
                    .web(WebApplicationType.NONE)
                    .run(args);
        // myFirstLevelRepository bean是否存在
        MyFirstLevelRepository myFirstLevelRepository =
                context.getBean("myFirstLevelRepository", MyFirstLevelRepository.class);
        System.out.println("myFirstLevelRepository: " + myFirstLevelRepository);
        // 关闭上下文
        context.close();
    }

}
```

```java
myFirstLevelRepository: com.dev.devinspringboot.repository.MyFirstLevelRepository@f381794
```

可以知道：

+ `@Component`
  + `@Repository`
    + `@MyFirstLevelRepository`

#### `@Component`层次性

`@MyFirstLevelRepository`还可以标注到其他注解上

```java
/**
 * 一级 {@link Repository @Repository}
 *
 * @author <a href="mailto:mercyblitz@gmail.com">Mercy</a>
 * @since 1.0.0
 */
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@FirstLevelRepository
public @interface SecondLevelRepository {

    String value() default "";

}
```

`@Component`

- `@Repository`

  - `@MyFirstLevelRepository`

    ​	`@SecondLevelRepository`

所以我们可以发现`@SpringBootApplication`也是模式注解

```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration // 模式注解
@EnableAutoConfiguration
@ComponentScan(
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
public @interface SpringBootApplication {
}    
```

```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Configuration
public @interface SpringBootConfiguration {
}
```

## Spring @Enable 模块装配

Spring Framework 3.1 开始支持”@Enable 模块驱动“。所谓“模块”是指具备相同领域的功能组件集合， 组合所形成一个独立的单元。比如 Web MVC 模块、AspectJ代理模块、Caching（缓存）模块、JMX（Java 管 理扩展）模块、Async（异步处理）模块等。

实现方式：注解方式、编程方式

### `@Enable` 注解模块举例

| 框架实现         | @Enable 注解模块               | 激活模块            |
| ---------------- | ------------------------------ | ------------------- |
| Spring Framework | @EnableWebMvc                  | Web MVC 模块        |
|                  | @EnableTransactionManagement   | 事务管理模块        |
|                  | @EnableCaching                 | Caching 模块        |
|                  | @EnableMBeanExport             | JMX 模块            |
|                  | @EnableAsync                   | 异步处理模块        |
|                  | @EnableWebFlux                 | Web Flux 模块       |
|                  | @EnableAspectJAutoProxy        | AspectJ 代理模块    |
|                  |                                |                     |
| Spring Boot      | @EnableAutoConfiguration       | 自动装配模块        |
|                  | @EnableManagementContext       | Actuator 管理模块   |
|                  | @EnableConfigurationProperties | 配置属性绑定模块    |
|                  | @EnableOAuth2Sso               | OAuth2 单点登录模块 |
|                  |                                |                     |
| Spring Cloud     | @EnableEurekaServer            | Eureka服务器模块    |
|                  | @EnableConfigServer            | 配置服务器模块      |
|                  | @EnableFeignClients            | Feign客户端模块     |
|                  | @EnableZuulProxy               | 服务网关 Zuul 模块  |
|                  | @EnableCircuitBreaker          | 服务熔断模块        |

### 实现方式

#### 1、注解驱动方式

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@Documented
@Import(DelegatingWebMvcConfiguration.class)
public @interface EnableWebMvc {
}
```

```java
@Configuration
public class DelegatingWebMvcConfiguration extends
WebMvcConfigurationSupport {
...
}
```

#### 1.1、自定义注解驱动方式

````java
// 自定义注解
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@Documented
@Import(HelloWorldConfiguration.class) // 导入自定义配置类
public @interface EnableHelloWorld {

}
````

````java
// 自定义配置类
@Configuration
public class HelloWorldConfiguration {

    // 方法名即是bean名称
    @Bean
    public String helloWorld() {
        return "Hello World";
    }
}
````

```java
@EnableHelloWorld
public class EnableHelloWorldBootstrap {

    public static void main(String[] args) {
        ConfigurableApplicationContext context =
                new SpringApplicationBuilder(EnableHelloWorldBootstrap.class)
                    .web(WebApplicationType.NONE)
                    .run(args);
        String helloWorld =
                (String) context.getBean("helloWorld");
        System.out.println("bean " + helloWorld);
        context.close();
    }

}
```

```java
bean Hello World
```

#### 2、接口编程方式

```java
/**
	激活缓存
**/
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Import(CachingConfigurationSelector.class)
public @interface EnableCaching {
...
}
```

`````java
public class CachingConfigurationSelector extends AdviceModeImportSelector<EnableCaching> {
    /**
    * {@inheritDoc}
    * @return {@link ProxyCachingConfiguration} or {@code
    AspectJCacheConfiguration} for
    * {@code PROXY} and {@code ASPECTJ} values of {@link
    EnableCaching#mode()}, respectively
    */
    public String[] selectImports(AdviceMode adviceMode) {
        switch (adviceMode) {
            case PROXY:
                return new String[] {
                    AutoProxyRegistrar.class.getName(),ProxyCachingConfiguration.class.getName() };
            case ASPECTJ:
                return new String[] {
                    AnnotationConfigUtils.CACHE_ASPECT_CONFIGURATION_CLASS_NAME };
            default:
                return null;
     }
}
`````

#### 2.1、自定义接口编程方式

```java
/**
 * 增加 HelloWorld Selector
 */
public class HelloWorldImportSelector implements ImportSelector {
    @Override
    public String[] selectImports(AnnotationMetadata annotationMetadata) {
        return new String[] {HelloWorldConfiguration.class.getName()};
    }
}
```

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@Documented
// @Import(HelloWorldConfiguration.class)
@Import(HelloWorldImportSelector.class) // 注解导入Seletor类
public @interface EnableHelloWorld {

}
```

`HelloWorldImportSelector` -> `HelloWorldConfiguration` -> `HelloWorldBean`

`依旧用上面的类测试， 结果没有差别，接口编程的方式只是中间需要通过一个实现了ImportSelector的类来实现配置bean，这个方法比注解驱动的方式好，给了我们更多的空间去控制bean的配置注入`



## Spring 条件装配

从 Spring Framework 3.1 开始，允许在 Bean 装配时增加前置条件判断

### 条件注解举例

| Spring 注解    | 场景说明       | 起始版本 |
| -------------- | -------------- | -------- |
| `@Profile`     | 配置化条件装配 | 3.1      |
| `@Conditional` | 编程条件装配   | 4.0      |

### 实现方式

#### 配置方式 - `@Profile`

略.....

#### 编程方式 - `@Conditional`

````java
@Target({ ElementType.TYPE, ElementType.METHOD })
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Conditional(OnClassCondition.class)
public @interface ConditionalOnClass {
/**
* The classes that must be present. Since this annotation is parsed by loading class
* bytecode, it is safe to specify classes here that may ultimately not be on the
* classpath, only if this annotation is directly on the affected component and
* <b>not</b> if this annotation is used as a composed, meta-annotation. In order to
* use this annotation as a meta-annotation, only use the {@link #name} attribute.
* @return the classes that must be present
*/
Class<?>[] value() default {};
/**
* The classes names that must be present.
自定义条件装配
基于配置方式实现 - @Profile
计算服务，多整数求和 sum
@Profile("Java7") : for 循环
@Profile("Java8") : Lambda
基于编程方式实现 - @ConditionalOnSystemProperty
Spring Boot 自动装配
在 Spring Boot 场景下，基于约定大于配置的原则，实现 Spring 组件自动装配的目的。其中使用了
底层装配技术
Spring 模式注解装配
Spring @Enable 模块装配
Spring 条件装配装配
Spring 工厂加载机制
实现类： SpringFactoriesLoader
配置资源： META-INF/spring.factories
自动装配举例
参考 META-INF/spring.factories
* @return the class names that must be present.
*/
String[] name() default {};
}
````

### 自定义条件装配

#### 基于配置方式实现 - `@Profile`

计算服务，多整数求和 Sum

`@Profile("java7"):`for循环

`@Profile("java7"):`Labmda

```java
public interface CalculateService {

    // sum求和
    public Integer sum(Integer... values);
}
```

````java
/**
 * Java 7 for 循环实现 {@link CalculateService}
 * profile是java7的才被激活
 */
@Profile("java7")
@Service
public class Java7CalculateService implements CalculateService {

    @Override
    public Integer sum(Integer... values) {
        System.out.println("Java 7 for 循环实现");
        int sum = 0;
        for (int i = 0; i < values.length; i++) {
            sum += values[i];
        }
        return sum;
    }
}
````

```java
/**
 * Java 8 lambda 循环实现 {@link CalculateService}
 * profile是java7的才被激活
 */
@Profile("java8")
@Service
public class Java8CalculateService implements CalculateService {

    @Override
    public Integer sum(Integer... values) {
        System.out.println("Java 8 lambda 实现");
        int sum = Stream.of(values).reduce(0, Integer::sum);
        return sum;
    }
}
```

```java
/**
 * {@link CalculateService} 引导类
 */
@SpringBootApplication(scanBasePackages = "com.dev.devinspringboot.service")
public class CalculateServiceBootstrap {

    public static void main(String[] args) {
        ConfigurableApplicationContext context =
                new SpringApplicationBuilder(CalculateServiceBootstrap.class)
                .web(WebApplicationType.NONE)
                        .profiles("java8")
                .run(args);
        CalculateService service =
                context.getBean(CalculateService.class);
        Integer sum = service.sum(1, 2, 3, 4, 5, 6, 7, 8);
        System.out.println("sum: " + sum);
    }
}
```

```java
Java 8 lambda 实现
sum: 36
```

#### 基于编程方式实现 - @ConditionalOnSystemProperty

@Profile 在 Spring 4 之后发生了变化采用了`@Conditional(ProfileCondition.class)`方式来实现的,查看底层代码

```java
@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Conditional({ProfileCondition.class})
public @interface Profile {
    String[] value();
}
```

```java
class ProfileCondition implements Condition {
    ProfileCondition() {
    }
	// 上下文，元数据注解
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        MultiValueMap<String, Object> attrs = metadata.getAllAnnotationAttributes(Profile.class.getName());
        if (attrs != null) {
            Iterator var4 = ((List)attrs.get("value")).iterator();

            Object value;
            do {
                if (!var4.hasNext()) {
                    return false;
                }

                value = var4.next();
            } while(!context.getEnvironment().acceptsProfiles(Profiles.of((String[])((String[])value))));

            return true;
        } else {
            return true;
        }
    }
}
```

实现的接口`Condition`

```java
@FunctionalInterfacepublic interface Condition {
    /**
    	是否匹配
    **/
    boolean matches(ConditionContext var1, AnnotatedTypeMetadata var2);
}
```

于是也可以通过`@Conditional`实现一个类似的实现，下面列举了一些例子，稍后将会自定义例子来实现

```java
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE, ElementType.METHOD})
@Documented
@Conditional({OnPropertyCondition.class})
public @interface ConditionalOnProperty {
    String[] value() default {};

    String prefix() default "";

    String[] name() default {};

    String havingValue() default "";

    boolean matchIfMissing() default false;
}

```

````java
/***
 	里面略掉了很多代码
 	这儿的order是一个排序的注解后面会有讲解
 	SpringBootCondition其实实现了Condition的接口
***/
@Order(-2147483608)
class OnPropertyCondition extends SpringBootCondition {
}    
````

````java
/***
	删掉了一些方法，由下显而易见，通过重写matches方法来进行条件过滤
***/
public abstract class SpringBootCondition implements Condition {
    private final Log logger = LogFactory.getLog(this.getClass());

    public SpringBootCondition() {
    }

    public final boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        String classOrMethodName = getClassOrMethodName(metadata);

        try {
            ConditionOutcome outcome = this.getMatchOutcome(context, metadata);
            this.logOutcome(classOrMethodName, outcome);
            this.recordEvaluation(context, classOrMethodName, outcome);
            return outcome.isMatch();
        } catch (NoClassDefFoundError var5) {
            throw new IllegalStateException("Could not evaluate condition on " + classOrMethodName + " due to " + var5.getMessage() + " not found. Make sure your own configuration does not rely on that class. This can also happen if you are @ComponentScanning a springframework package (e.g. if you put a @ComponentScan in the default package by mistake)", var5);
        } catch (RuntimeException var6) {
            throw new IllegalStateException("Error processing condition on " + this.getName(metadata), var6);
        }
    }

    
}
````

#### 自定义`@ConditionalOnSystemProperty`

##### 1、自定义`@Conditional`注解，引入条件类

````java
/**
 * Java 系统属性条件判断
 */
@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Conditional(OnSystemPropertyCondition.class)
public @interface ConditonOnSystemProperty {

    /**
     * Java系统属性名称
     * @return
     */
    String name();

    /**
     * Java系统属性值
     * @return
     */
    String value();

}
````

##### 2、创建条件类

````java
/**
 * 系统属性条件判断
 */
public class OnSystemPropertyCondition implements Condition {

    @Override
    public boolean matches(ConditionContext conditionContext, AnnotatedTypeMetadata annotatedTypeMetadata) {

        Map<String, Object> attributes =
                annotatedTypeMetadata.getAnnotationAttributes(ConditonOnSystemProperty.class.getName());
        // 类型安全的一个写法、String.valueof
        String propertyName = String.valueOf(attributes.get("name"));

        String propertyValue = String.valueOf(attributes.get("value"));
	   
        String javaPropertyValue = System.getProperty(propertyName);
		// 这儿只是把电脑的名字拿出来和注解里面定义的进行比较，如果返回false 就会报错，如果true就能拿到Bean
        return javaPropertyValue.equals(propertyValue);
    }
}
````

```java
/**
 * 系统条件属性引导类
 */
public class SystemPropertyConditionalBootstrap {

    @Bean
    @ConditonOnSystemProperty(name = "user.name", value = "Administrator")
    public String helloWorld() {
        return "Hello World 小马哥";
    }


    public static void main(String[] args) {
        ConfigurableApplicationContext context =
                new SpringApplicationBuilder(SystemPropertyConditionalBootstrap.class)
                .web(WebApplicationType.NONE)
                .run(args);

        String helloWorld = context.getBean("helloWorld", String.class);
        System.out.println(helloWorld);
        context.close();
    }

}
```

报错的时候：

````java
Exception in thread "main" org.springframework.beans.factory.NoSuchBeanDefinitionException: No bean named 'helloWorld' available
````

成功匹配的时候：

```java
Hello World 小马哥
```

`条件判断里面这儿处理的比较简单，实际上可以很复杂`

## Spring Boot 自动装配

在 Spring Boot 场景下，基于约定大于配置的原则，实现 Spring 组件自动装配的目的。其中使用了

````java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
public @interface SpringBootApplication {
}    
````



### 底层装配技术

#### Spring 模式注解装配

#### Spring @Enable 模块装配

#### Spring @Enable 模块装配

#### Spring 工厂加载机制

#####  实现类：`SpringFactoriesLoader`

##### 配置资源：`META-INF/spring.factories`

```java
public final class SpringFactoriesLoader {
    public static final String FACTORIES_RESOURCE_LOCATION = "META-INF/spring.factories";
    private static final Log logger = LogFactory.getLog(SpringFactoriesLoader.class);
    private static final Map<ClassLoader, MultiValueMap<String, String>> cache = new ConcurrentReferenceHashMap();

    private SpringFactoriesLoader() {
    }
	
    // 主要方法
    // 装载
    public static <T> List<T> loadFactories(Class<T> factoryClass, @Nullable ClassLoader classLoader) {
        Assert.notNull(factoryClass, "'factoryClass' must not be null");
        ClassLoader classLoaderToUse = classLoader;
        if (classLoader == null) {
            classLoaderToUse = SpringFactoriesLoader.class.getClassLoader();
        }

        List<String> factoryNames = loadFactoryNames(factoryClass, classLoaderToUse);
        if (logger.isTraceEnabled()) {
            logger.trace("Loaded [" + factoryClass.getName() + "] names: " + factoryNames);
        }

        List<T> result = new ArrayList(factoryNames.size());
        Iterator var5 = factoryNames.iterator();

        while(var5.hasNext()) {
            String factoryName = (String)var5.next();
            result.add(instantiateFactory(factoryName, factoryClass, classLoaderToUse));
        }

        AnnotationAwareOrderComparator.sort(result);
        return result;
    }

    public static List<String> loadFactoryNames(Class<?> factoryClass, @Nullable ClassLoader classLoader) {
        String factoryClassName = factoryClass.getName();
        return (List)loadSpringFactories(classLoader).getOrDefault(factoryClassName, Collections.emptyList());
    }

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

    private static <T> T instantiateFactory(String instanceClassName, Class<T> factoryClass, ClassLoader classLoader) {
        try {
            Class<?> instanceClass = ClassUtils.forName(instanceClassName, classLoader);
            if (!factoryClass.isAssignableFrom(instanceClass)) {
                throw new IllegalArgumentException("Class [" + instanceClassName + "] is not assignable to [" + factoryClass.getName() + "]");
            } else {
                return ReflectionUtils.accessibleConstructor(instanceClass, new Class[0]).newInstance();
            }
        } catch (Throwable var4) {
            throw new IllegalArgumentException("Unable to instantiate factory class: " + factoryClass.getName(), var4);
        }
    }
}
```



### 自动装配举例

参考`META-INF/spring.factories`

### 实现方法

1. 激活自动装配 - @EnableAutoConfiguration
2. 实现自动装配 - XXXAutoConfiguration
3. 配置自动装配实现 - META-INF/spring.factories

### 自定义

#### 1、第一步创建引导类，开启自动装配

````java
/**
 * 自动装配引导类
 */
@EnableAutoConfiguration
public class EnableConfigurationBootstrap {

    public static void main(String[] args) {
        ConfigurableApplicationContext context = new SpringApplicationBuilder(EnableConfigurationBootstrap.class)
                .web(WebApplicationType.NONE)
                .run(args);

        context.close();
    }

}
````

#### 2、结合之前的三种模式，创建`HelloWorldAutoConfiguration`

````java
/**
 * Hello World 自动装配类
 */
@Configuration // Spring模式注解
@EnableHelloWorld // Spring @Enable模块装配
@ConditonOnSystemProperty(name = "user.name", value = "Administrator") // 条件装配
public class HelloWorldAutoConfiguration {


}
````

##### 3、在`resources`目录下创建`META-INF\spring.factories`

````properties
# 自动装配
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.dev.devinspringboot.condition.HelloWorldAutoConfiguration
````

#### 4、启动测试

````java
@EnableAutoConfiguration
public class EnableConfigurationBootstrap {

    public static void main(String[] args) {
        ConfigurableApplicationContext context = new SpringApplicationBuilder(EnableConfigurationBootstrap.class)
                .web(WebApplicationType.NONE)
                .run(args);

        String helloWorld = context.getBean("helloWorld", String.class);
        System.out.println(helloWorld);

        context.close();
    }

}
````

`总结：Spring Boot自动装配简单来说就是将Spring模式注解，@Enable模块注解以及条件装配@Conditional配合它自己的工厂加载机制SpringFactoriesLoader来实现bean的自动装配`

`HelloWorldAutoConfiguration`

+ 条件判断：`user.name = "Administrator"`
+ 模式注解：`@Configuration`
+ `@Enable`模块：`@EnableHelloWorld` -> `HelloWorldImportSelector` -> `HelloWorldConfiguration` -> `HelloWorld`

## 网上分析内容

### @EnableAutoConfiguration注解

Spring Boot中引入了自动配置，让开发者利用起来更加的简便、快捷。比如内嵌的tomcat端口默认配置是8080，这些都属于Spring Boot自动配置的范畴，当然其自动配置相当多。

springboot框架的神奇之处在于@EnableAutoConfiguration注释，此注释自动载入应用程序所需的所有Bean——这依赖于Spring Boot在类路径中的查找。

#### 1、@EnableAutoConfiguration注解

````java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {

    String ENABLED_OVERRIDE_PROPERTY = "spring.boot.enableautoconfiguration";

    Class<?>[] exclude() default {};

    
    String[] excludeName() default {};

}
````

很显然能看出有一特殊的注解@Import，@Import(AutoConfigurationImportSelector.class)

#### 2.AutoConfigurationImportSelector

````java
@Override
public String[] selectImports(AnnotationMetadata annotationMetadata) {
    if (!isEnabled(annotationMetadata)) {
        return NO_IMPORTS;
    }
    try {
        AutoConfigurationMetadata autoConfigurationMetadata = AutoConfigurationMetadataLoader
            .loadMetadata(this.beanClassLoader);
        AnnotationAttributes attributes = getAttributes(annotationMetadata);
        List<String> configurations = getCandidateConfigurations(annotationMetadata,
                                                                 attributes);
        configurations = removeDuplicates(configurations);
        configurations = sort(configurations, autoConfigurationMetadata);
        Set<String> exclusions = getExclusions(annotationMetadata, attributes);
        checkExcludedClasses(configurations, exclusions);
        configurations.removeAll(exclusions);
        configurations = filter(configurations, autoConfigurationMetadata);
        fireAutoConfigurationImportEvents(configurations, exclusions);
        return configurations.toArray(new String[configurations.size()]);
    }
    catch (IOException ex) {
        throw new IllegalStateException(ex);
    }
}
````

看如下代码，获取类路径下spring.factories下key为EnableAutoConfiguration全限定名对应值

`List<String> configurations = getCandidateConfigurations(annotationMetadata,
attributes);`

```java

protected List<String> getCandidateConfigurations(AnnotationMetadata metadata,
            AnnotationAttributes attributes) {
        List<String> configurations = SpringFactoriesLoader.loadFactoryNames(
                getSpringFactoriesLoaderFactoryClass(), getBeanClassLoader());
        Assert.notEmpty(configurations,
                "No auto configuration classes found in META-INF/spring.factories. If you "
                        + "are using a custom packaging, make sure that file is correct.");
        return configurations;
    }

    protected Class<?> getSpringFactoriesLoaderFactoryClass() {
        return EnableAutoConfiguration.class;
    }
复制代码
```

`getCandidateConfigurations`会到classpath下的读取META-INF/spring.factories文件的配置，并返回一个字符串数组。

#### 3、总结

总结,@EnableAutoConfiguration 作用
从classpath中搜索所有META-INF/spring.factories配置文件然后，将其中org.springframework.boot.autoconfigure.EnableAutoConfiguration key对应的配置项加载到spring容器
只有spring.boot.enableautoconfiguration为true（默认为true）的时候，才启用自动配置
@EnableAutoConfiguration还可以进行排除，排除方式有2中，一是根据class来排除（exclude），二是根据class name（excludeName）来排除
其内部实现的关键点有
1）ImportSelector 该接口的方法的返回值都会被纳入到spring容器管理中
2）SpringFactoriesLoader 该类可以从classpath中搜索所有META-INF/spring.factories配置文件，并读取配置

### springBoot @Enable* 注解的使用

#### **1、为什么使用@SpringBootApplication注解，即可做到自动配置？**

答：@SpringBootApplication，内部起作用的注解其实有3个。@EnableAutoConfiguration，@ComponentScan，@Configuration。这篇文章主要是讲解@EnableXX注解

#### **2、为什么使用了@EnableAutoConfiguration。当使用了@ConfigurationProperties时，即可自动导入.yml 或者.properties里面的配置项？**

答：在`@EnableAutoConfiguration`内部，使用了`@Import`注解。导入`AutoConfigurationImportSelector`帮助springBoot将符合条件的`Configuration`加载到IOC容器中。但是内部其实使用了`SpringFactoriesLoader`来完成。类似与`java SPI`的功能

即从/META-INF/spring.factories加载配置

`````java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@AutoConfigurationPackage
@Import({AutoConfigurationImportSelector.class})
public @interface EnableAutoConfiguration 
`````

可以看到@Import中，其实是导入了一个AutoConfigurationImportSelector的类。最关键的是，该类实现了接口ImportSelector

````java
public interface ImportSelector {
 /**
  * Select and return the names of which class(es) should be imported based on
  * the {@link AnnotationMetadata} of the importing @{@link Configuration} class.
  */
 String[] selectImports(AnnotationMetadata importingClassMetadata);
 
}
````

这是ImportSelector的描述，大概意思就是，该方法返回的Bean 会自动的被注入，被Spring所管理。

接着来看 AutoConfigurationImportSelector中 selectImports 的实现

````java
public String[] selectImports(AnnotationMetadata annotationMetadata) {
  if(!this.isEnabled(annotationMetadata)) {
   return NO_IMPORTS;
  } else {
   AutoConfigurationMetadata autoConfigurationMetadata = AutoConfigurationMetadataLoader.loadMetadata(this.beanClassLoader);
   AnnotationAttributes attributes = this.getAttributes(annotationMetadata);
   List<String> configurations = this.getCandidateConfigurations(annotationMetadata, attributes);
   configurations = this.removeDuplicates(configurations);
   Set<String> exclusions = this.getExclusions(annotationMetadata, attributes);
   this.checkExcludedClasses(configurations, exclusions);
   configurations.removeAll(exclusions);
   configurations = this.filter(configurations, autoConfigurationMetadata);
   this.fireAutoConfigurationImportEvents(configurations, exclusions);
   return StringUtils.toStringArray(configurations);
  }
 }
````

在@Import中，可以看到 有个链接指向了`ImportBeanDefinitionRegistrar`。这同样是一个接口，作用跟 `ImportSelector` 一样。

````java
public interface ImportBeanDefinitionRegistrar {
 public void registerBeanDefinitions(
   AnnotationMetadata importingClassMetadata, BeanDefinitionRegistry registry);
 
}
````

`在registerBeanDefinitions方法中，可以用BeanDefinitionRegistry 注入我们想要注入的Bean。`