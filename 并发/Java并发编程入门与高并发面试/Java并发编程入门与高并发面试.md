# 4、安全发布对象

### 1、发布与逸出

发布对象：使一个对象能够被当前范围之外的代码所使用

对象逸出：一种的错误的发布。当一个对象还么有构造完成时，就使它被其他线程所见

日常开发中经常要发布对象，下面演示发布对象

```java
public class UnsafePublish {

    private String[] states = {"a", "b", "c"};

    public String[] getStates() {
        return states;
    }

    public static void main(String[] args) {
        UnsafePublish unsafePublish =
                new UnsafePublish();
        System.out.println(Arrays.toString(unsafePublish.getStates()));

        unsafePublish.getStates()[0] = "d";
        System.out.println(Arrays.toString(unsafePublish.getStates()));
    }

}
```

```txt
分析：
以上发布对象是不安全的，通过getStates得到私有域的states数组的引用，就可以在其他任何线程里面修改数组的值，如果想在任何线程里使用数据的引用的时候，数据不一定是正确的。
```

逸出

```java
public class Escape {

    private int thisCanBeEscape = 0;

    public Escape() {
        new InnerClass();
    }
    // 内部类
    private class InnerClass {

        public InnerClass() {
            System.out.println(Escape.this.thisCanBeEscape);
        }
    }

    public static void main(String[] args) {
        new Escape();
    }
}
```

```txt
0


分析：内部类的实例里面包含了对封装实例的隐含和引用，这样在对象没有被正确构造之前就会被发布，导致this引用在构造期间逸出的错误，在构造期间启动一个线程，新线程在构造之前就可以看到this
在对象未完成构造之前不能被发布
```

### 2、四种方法

1. 在静态初始化函数中初始化一个对象引用
2. 将对象的引用保存到volatile类型域或者AtomicReference对象中
3. 将对象的引用保存到某个正确构造对象的final类型域中
4. 将对象的引用保存到一个由锁保护的域中

### 3、单例模式

下面通过单例的方式来验证`安全发布对象`

#### 1、懒汉模式

```java
/**
 * 懒汉模式
 * 在第一次调用的时候才创建
 */
public class SingletonExample1 {
    // 私有构造函数
    private SingletonExample1(){}
    // 单例对象
    private static SingletonExample1 instance = null;
    // 静态的工厂方法
    public static SingletonExample1 getInstance() {
        if (instance == null) {
            instance = new SingletonExample1();
        }
        return instance;
    }
}
```

```java
以上的单例模式是线程不安全的，显而易见
```

#### 2、饿汉模式

```java
/**
 * 饿汉模式
 * 在类加载的时候创建
 */
public class SingletonExample2 {
    // 私有构造函数
    private SingletonExample2(){}
    // 单例对象
    private static SingletonExample2 instance = new SingletonExample2();
    // 静态的工厂方法
    public static SingletonExample2 getInstance() {
        return instance;
    }
}
```

`饿汉模式是线程安全的，因为Java类加载的时候是天然线程安全的，但是如果构造方法中存在过多的处理，会导致类加载很慢，引起性能问题，如果加载后没有调用会造成资源的浪费`

`也可以通过静态代码块初始化对象`

```java
static {
    instance = new SingletonExample2();
}
```

那么懒汉模式也可以线程安全么？

增加`synchronized`关键字

```java
public static synchronized SingletonExample1 getInstance() {
    if (instance == null) {
        instance = new SingletonExample1();
    }
    return instance;
}
```

```java
线程安全，但是这种写法并不推荐，加了关键字通过同一时刻只能允许一个线程创建对象，但是会造成性能的开销
```

#### 3、双重检查锁定

那么将`synchronized`下沉到类中，双重检查锁定

```java
public static synchronized SingletonExample1 getInstance() {
    if (instance == null) {
        synchronized (SingletonExample1.class) { // 同步锁
            if (instance == null) {
                instance = new SingletonExample1();
            }
        }
    }
    return instance;
}
```

```java
双重同步锁单例模式，但是依旧不是线程安全的
instance = new SingletonExample1();
// 1.memory = allocate() 分配对象的内存空间
// 2.ctorInstance() 初始化对象
// 3.instance = memory 设置instance指向刚分配的内存
但是在多线程会发生指令重拍，2,3操作重排后，会存在对象还没有初始化就返回回去了
```

那么有什么方法呢

```java
private volatile static SingletonExample3 instance = null;
```

```java
volatile + 双重检测机制 来禁止指令重排序
```

对于单例模式还有其他方法么？

#### 4、枚举

```java
public class SingletonExample4 {
    
    private SingletonExample4(){}
    
    private volatile static SingletonExample4 instance = null;
    
    public static synchronized SingletonExample4 getInstance() {
        return Singleton.INSTANCE.getInstance();
    }

    private enum Singleton {
        INSTANCE;
        
        private SingletonExample4 singleton;
        // JVM保证这个方法只调用一次
        Singleton() {
            singleton = new SingletonExample4();
        }
        
        public SingletonExample4 getInstance() {
            return singleton;
        }
    }
}
```

`使用枚举方法是天然的线程安全，同时又是延迟加载`

#### 5、静态内部类

相比于懒汉以及饿汉模式，静态内部类模式（一般也被称为 Holder）是许多人推荐的一种单例的实现方式，因为相比懒汉模式，它用更少的代码量达到了延迟加载的目的。

顾名思义，这种模式使用了一个私有的静态内部类，来存储外部类的单例，这种静态内部类，一般称为 Holder。

而利用静态内部类的特性，外部类的 getinstance() 方法，可以直接指向 Holder 持有的对象。

```java
public class SingletonExample5 {

    private SingletonExample5(){}

    private volatile static SingletonExample5 instance = null;

    public static synchronized SingletonExample5 getInstance() {
        return SingtonHolder.instance;
    }
    // 静态内部类
    private static class SingtonHolder {
        private static SingletonExample5 instance = new SingletonExample5();
    }
}
```

`分析：在调用的时候才去初始化静态内部类，因为Java类的加载是一个天然的线程安全的过程，所以这个intance对象是线程安全的`

#### 6、单例模式的破坏

##### 1、序列化和反序列化

```java
public class SingletonExample2 implements Serializable {

    private SingletonExample2(){}

    private static SingletonExample2 instance = new SingletonExample2();

    public static SingletonExample2 getInstance() {
        return instance;
    }

    public static void main(String[] args) throws IOException, ClassNotFoundException {
        SingletonExample2 instance =
                SingletonExample2.getInstance();
        ObjectOutputStream oos =
                new ObjectOutputStream(new FileOutputStream("E:\\ceshi.txt"));
        oos.writeObject(instance);

        File file = new File("E:\\ceshi.txt");
        ObjectInputStream ois =
                new ObjectInputStream(new FileInputStream(file));
        SingletonExample2 newInstance = (SingletonExample2) ois.readObject();

        System.out.println(instance == newInstance);
    }
}
```

```java
false
```

解决方法：

在代码中加入一个方法

```java
public Object readResolve() {
   return instance;
}
```

为什么会这样？让我们查看源码

```java
oos.writeObject(instance);
```

```java
Object obj = readObject0(false);
```

```java
case TC_OBJECT:
	return checkResolve(readOrdinaryObject(unshared));
```

```java
try {
    obj = desc.isInstantiable() ? desc.newInstance() : null;
} catch (Exception ex) {
    throw (IOException) new InvalidClassException(
        desc.forClass().getName(),
        "unable to create instance").initCause(ex);
}
```

```java
/**
     * Returns true if represented class is serializable/externalizable and can
     * be instantiated by the serialization runtime--i.e., if it is
     * externalizable and defines a public no-arg constructor, or if it is
     * non-externalizable and its first non-serializable superclass defines an
     * accessible no-arg constructor.  Otherwise, returns false.
     */
// 简单来说就是类被序列化后，会返回true
boolean isInstantiable() {
    requireInitialized();
    return (cons != null);
}
```

```java
所以在上一步就会desc.newInstance() 返回 不着急还有下面代码
```

```java
if (obj != null &&
            handles.lookupException(passHandle) == null &&
            desc.hasReadResolveMethod())
        {
            Object rep = desc.invokeReadResolve(obj);
            if (unshared && rep.getClass().isArray()) {
                rep = cloneArray(rep);
            }
            if (rep != obj) {
                // Filter the replacement object
                if (rep != null) {
                    if (rep.getClass().isArray()) {
                        filterCheck(rep.getClass(), Array.getLength(rep));
                    } else {
                        filterCheck(rep.getClass(), -1);
                    }
                }
                handles.setObject(passHandle, obj = rep);
            }
        }
```

```java
看判断条件如果desc.hasReadResolveMethod()为true 就会执行这个方法，所以会在原来的类里面添加readResolve（）方法
```

##### 2、反射破坏

```java
SingletonExample2 instance = SingletonExample2.getInstance();
Class clazz = SingletonExample2.class;
Constructor constructor = clazz.getDeclaredConstructor();
constructor.setAccessible(true); // 获取private权限
SingletonExample2 newInstance = (SingletonExample2) constructor.newInstance();
System.out.println(instance == newInstance);
```

```java
false
```

解决方法：

在构造函数加入判断

```java
private SingletonExample2() {
    if (instance != null) {
        throw new RuntimeException("单例类禁止反射调用");
    }
}
```

```java
Exception in thread "main" java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at com.dev.devinspringboot.concurrency.singleton.SingletonExample2.main(SingletonExample2.java:46)
Caused by: java.lang.RuntimeException: 单例类禁止反射调用
	at com.dev.devinspringboot.concurrency.singleton.SingletonExample2.<init>(SingletonExample2.java:15)
	... 5 more
```

`在使用反射的时候newInstance的时候一定会调用构造方法，所以加上判断就好了，那么还有那种单例方法能使用呢`

静态内部类方式：

```java
public class SingletonExample5 {

    private SingletonExample5(){}

    private volatile static SingletonExample5 instance = null;

    public static synchronized SingletonExample5 getInstance() {
        return SingtonHolder.instance;
    }
    // 静态内部类
    private static class SingtonHolder {
        private static SingletonExample5 instance = new SingletonExample5();
    }

    public static void main(String[] args) throws Exception {
        SingletonExample5 instance =
                SingletonExample5.getInstance();
        Class clazz = SingletonExample5.class;
        Constructor constructor = clazz.getDeclaredConstructor();
        constructor.setAccessible(true); // 获取private权限
        SingletonExample5 newInstance = (SingletonExample5) constructor.newInstance();
        System.out.println(instance == newInstance);
    }
}
```

```java
false
```

照例在构造方法加入判断

```java
private SingletonExample5() {
    if (SingtonHolder.instance != null) {
        throw new RuntimeException("单例类禁止反射调用");
    }
}
```

```java
Caused by: java.lang.RuntimeException: 单例类禁止反射调用
```

使用懒汉模式测试

```java
public class SingletonExample1 {
    // 私有构造函数
    private SingletonExample1(){
        if (instance != null) {
            throw new RuntimeException("单例模式禁止调用反射");
        }
    }
    // 单例对象
    private static SingletonExample1 instance = null;
    // 静态的工厂方法
    public static synchronized SingletonExample1 getInstance() {
        if (instance == null) {
            instance = new SingletonExample1();
        }
        return instance;
    }

    public static void main(String[] args) throws NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
        SingletonExample1 instance =
                SingletonExample1.getInstance();
        Class clazz = SingletonExample1.class;
        Constructor constructor = clazz.getDeclaredConstructor();
        constructor.setAccessible(true); // 获取private权限
        SingletonExample1 newInstance = (SingletonExample1) constructor.newInstance();
        System.out.println(instance == newInstance);
    }
}
```

```java
Caused by: java.lang.RuntimeException: 单例模式禁止调用反射
```

`如果调换反射的懒加载的顺序呢`

```java
Class clazz = SingletonExample1.class;
Constructor constructor = clazz.getDeclaredConstructor();
constructor.setAccessible(true); // 获取private权限
SingletonExample1 newInstance = (SingletonExample1) constructor.newInstance();
SingletonExample1 instance =
    SingletonExample1.getInstance();
System.out.println(instance == newInstance);
```

```java
false
```

`先由反射生成对象，然后再由懒加载方式生成对象就不会跑错，怎么会这样？结论是懒加载的模式反射调用是可以的，无法避免的，如果加入一个变量来控制呢？`

```java
private static boolean flag = true;
// 私有构造函数
private SingletonExample1(){
    if (flag) {
        flag = false;
    } else {
        throw new RuntimeException("单例模式禁止调用反射");
    }
}
```

`这样的话虽然可以避免反射攻击，但是反射也可以操作flag变量，所以还是不行的，比如`

```java
Class clazz = SingletonExample1.class;
Constructor constructor = clazz.getDeclaredConstructor();
constructor.setAccessible(true); // 获取private权限
SingletonExample1 newInstance = (SingletonExample1) constructor.newInstance();
// 反射修改私有变量的值
Field flag = newInstance.getClass().getDeclaredField("flag");
flag.setAccessible(true);
flag.set(newInstance, true);
SingletonExample1 instance =
    SingletonExample1.getInstance();
System.out.println(instance == newInstance);
```

`结果证明使用上面枚举的方式和静态内部类的方式，无论是先反射再实例或者先实例化再反射都是可以避免反射对单例的破坏的`

# 5、线程安全策略详解

## 1、不可变对象

不可变对象需要满足的条件

1. 对象创建以后其状态就不能修改
2. 对象所有域都是final类型
3. 对象是正确创建的（在对象创建期间，this引用没有逸出）

### final 关键字：类、方法、变量

+ 修饰类：不能被继承
+ 修饰方法：
  1. 锁定方法不能被继承类修改
  2. 效率
  3. `一个类的private方法会被隐式的修饰为final方法`
+ 修饰变量：基本数据类型变量、引用类型变量

```java
public class ImmutableExample {

    private final static Integer a = 1;
    private final static String b = "2";
    private final static Map<Integer, Integer> map
            = Maps.newHashMap();

    static {
        map.put(1, 2);
        map.put(3, 4);
        map.put(5, 6);
    }

    public static void main(String[] args) {
        // 引用类型修改
        // 不能再重新 map = new HashMap<>(); 但是可以修改值
        map.put(1, 3);
        System.out.println(map.get(1)); // 3
    }

    private void test(final int a) {
        // a = 1; 不能修改基本数据类型
    }
}
```

`final引用类型虽然不能再指定其他对象，但是可以修改里面的值，那么怎么解决这个问题呢？`

````
Collections.unmodifiableXXX:Collection、List、Set、Map
Guava: ImmutableXXX: Collection.....
````

````java
public class ImmutableExample2 {

    private static Map<Integer, Integer> map = Maps.newHashMap();

    static {
        map.put(1, 2);
        map.put(3, 5);
        map.put(4, 6);
        map = Collections.unmodifiableMap(map);
    }

    public static void main(String[] args) {
        map.put(1, 3);
        System.out.println(map.get(1));
    }
}
````

````java
Exception in thread "main" java.lang.UnsupportedOperationException
````

`unmodifiableMap`

````java
public V put(K key, V value) {
    throw new UnsupportedOperationException();
}
public V remove(Object key) {
    throw new UnsupportedOperationException();
}
public void putAll(Map<? extends K, ? extends V> m) {
    throw new UnsupportedOperationException();
}
public void clear() {
    throw new UnsupportedOperationException();
}
````

`将数据拷贝到一个UnmodifiableMap里面，然后将更新的方法作为异常抛出`

演示Guava里面的类

````java
public class ImmutableExample3 {
   // of的方法可以无限制加进去，加到12扩容
   private final static ImmutableList list
           = ImmutableList.of(1, 2, 3);

   private final static ImmutableSet set
           = ImmutableSet.copyOf(list);

   private final static ImmutableMap<Integer, Integer> map
           = ImmutableMap.of(1, 2, 3, 4);

   private final static ImmutableMap<Integer, Integer> buildMap
           = ImmutableMap.<Integer, Integer>builder()
                .put(1, 2).put(3, 4).build();

    public static void main(String[] args) {
        // 这三个方法显示的表示不能进行这样的操作，虽然编译没有报错，但是运行的时候会报错
        list.add(4);
        set.add(4);
        map.put(1, 3);
    }
}
````

````java
Exception in thread "main" java.lang.UnsupportedOperationException
````

`只要对象不可变，那么就能躲避并发数据不安全的问题`

## 2、线程封闭

把对象封装到一个线程里面，这样就不会有线程不安全的问题了

具体实现方法：

+ Ad-hoc 线程封闭：程序控制实现，最糟糕，忽略

+ 堆栈封闭：局部变量，无并发问题。`平时接触最多，局部变量不被多个线程共享，不会有并发问题`

+ ThreadLocal 线程封闭：特别好的封闭方法

  每个线程里面都有一个ThreadLocal，它是一个map

  可以通过`Filter`在访问的时候将用户信息存入threadLocal、以及使用interceptor将用户的登录信息从threadLocal删除，`如果不这么处理也可以，但是会将我们的request传入service，或者什么util包里面，代码很难看`

  

## 3、线程不安全类与写法

+ StringBuilder -> StringBuffer

  线程不安全 -> 线程安全

  ````java
  没有什么区别，只是StringBuilder加了同步关键字，在最新的JVM里面如果在多少次的操作以内，这个两个类的性能一模一样，因为JVM作了优化，但是超过这个次数，明显StringBuffer性能更好。
  ````

  

+ SimpleDateFormat -> JodaTime

  `多线程情况下调用SimpleDateFormat 的parse()方法会报错，只有通过堆栈封闭的方式局部使用即可`

  ```java
  // JodaTime使用
  private static DateTimeFormatter formater = 
      DateTimeFormat.forPattern("yyyy-MM-dd");
  Datatime.parse("20180208", formater).toDate();
  ```

  

# 6、同步容器

ArrayList（不安全） -> Vector/Stack（线程安全）

HashMap (不安全)  ->  HashTable (线程安全)

`可以使用Collections的静态方法来创建线程安全的容器`

````java
public class CollectionsExample1 {

    public static int theadTotal = 5000;

    public static int clientTotal = 200;

    private static List<Integer> list =
            Collections.synchronizedList(Lists.<Integer>newArrayList());

    public static void main(String[] args) {
        ExecutorService executorService
                = Executors.newCachedThreadPool();
        CountDownLatch countDownLatch = new CountDownLatch(theadTotal);
        Semaphore semaphore = new Semaphore(clientTotal);
        for (int i = 0; i < theadTotal; i++) {
            final int count = i;
            executorService.execute(() -> {
                try {
                    semaphore.acquire();
                    update(count);
                    semaphore.release();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                countDownLatch.countDown();
            });
        }
        try {
            countDownLatch.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(list.size());
        executorService.shutdown();
    }

    private static void update(int count) {
        list.add(count);
    }
}
````

