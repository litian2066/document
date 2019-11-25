姓名： 李天 

电话： 13718725513

邮箱： litian2066@163.com

是否外包： 否

wifi密码：gsww2402

gitlab 账号密码：litian            UzU!709Ey







1. **【强制】**POJO 类中布尔类型的变量，都不要加 is，否则部 分框架解析会引起序列化错误。

   + 反例：定义为基本数据类型 Boolean isDeleted;的属性，它的方法也是 isDeleted()，RPC 框架在反向解析的时候，“以为”对 应的属性名称是deleted，导致属性获取不到，进而抛出异常。 

     

     

2. 【强制】包名统一使用小写，点分隔符之间有且仅有一个自 然语义的英语单词。包名统一使用单数形式，但是类名如果有复 数含义，类名可以使用复数形式。 



3. 【推荐】接口类中的方法和属性不要加任何修饰符号 (public 也不要加)，保持代码的简洁性，并加上有效的 Javadoc 注释。尽量不要在接口里定义变量，如果一定要定义变 量，肯定是与接口方法相关，并且是整个应用的基础常量。 

   + 正例：接口方法签名：`void f()`；接口基础常量表示：`String COMPANY = "gsww";` 

   + 反例：接口方法定义：`public abstract void f()` 

4. 接口和实现类的命名有两套规则: 

   1. **【强制**】对于 Service 和 DAO 类，基于SOA的理念，暴露出来的服务一定是接口，内部的实现类用Impl 的后缀与接口区别。 

      + 正例：`CacheServiceImpl` 实现 `CacheService`接口。 

   2. **【推荐】** 如果是形容能力的接口名称，取对应的形容词做 接口名(通常是`–able`的形式)。

      正例：`AbstractTranslator`实现`Translatable`。

   说明：JDK8 中接口允许有默认实现，那么这个 default 方法， 是对所有实现类都有价值的默认实现。

5.  **【强制】**long 或者 Long 初始赋值时，使用大写的L，不能是小写的l，小写容易跟数字 1 混淆，造成误解。
    说明:Long a = 2l; 写的是数字的 21，还是 Long 型的 2? 

6. **【推荐】**不要使用一个常量类维护所有常量，按常量功能进行归类，分开维护。 

   + 说明：大而全的常量类，非得使用查找功能才能定位到修改的常量，不利于理解和维护。
   + 正例：缓存相关常量放在类 CacheConsts 下;系统配置相关常 量放在类 ConfigConsts 下。

7. **【强制】**单行字符数限制不超过 120 个，超出需要换行。换行时遵循如下原则：

   1. 第二行相对第一行缩进 4 个空格，从第三行开始，不再 继续缩进，参考示例。
   2. 运算符与下文一起换行。
   3. 方法调用的点符号与下文一起换行。
   4. 方法调用时，多个参数，需要换行时，在逗号后进行。
   5. 在括号前不要换行，见反例。

   + 正例：`StringBuffer sb = new StringBuffer();`

   ````java
   StringBuffer sb = new StringBuffer();
   // 超过 120 个字符的情况下，换行缩进 4 个空格，点号 和方法名称一起换行 
   sb.append("zi")
     .append("xin")
     .append("huang")...
   ````

   

   + 反例：

     ````java
     StringBuffer sb = new StringBuffer();
      // 超过 120 个字符的情况下，不要在括号前换行 
     
     sb.append("zi").append("xin")...append.("huang"); // 参数很多的方法调用可能超过 120 个字符，不要在逗 号前换行 method(args1, args2, args3, ... , argsX); 
     ````

     

8. **【强制】**所有的覆写方法，必须加@Override 注解。 

9. **【强制】**相同参数类型，相同业务含义，才可以使用Java的可变参数，避免使用 Object。 

   说明：可变参数必须放置在参数列表的最后(提倡同学们尽量不 第17页，共 76页 

   用可变参数编程)。
    **正例：**`public User getUsers(String type, Integer... ids) {...} `

10. **【强制】**外部正在调用或者二方库依赖的接口，不允许修改方法签名，避免对接口调用方产生影响。接口过时必须加`@Deprecated`注解，并清晰地说明采用的新接口或者新服务是什么。

11. **【强制】**不能使用过时的类或方法。

    说明：`java.net.URLDecoder`中的方法`decode(String encodeStr)`这个方法已经过时，应该使用双参数 `decode(String source, String encode)`。接口提供方既然明确是过时接口，那么有义务同时提供新的接口;作为调用方来说， 有义务去考证过时方法的新实现是什么。

12. **【强制】**Object 的 equals 方法容易抛空指针异常，应使用常量或确定有值的对象来调用 equals。 

    + 正例：`"test".equal(object);`
    + 反例：`object.equals("test"); `
    + 说明：**推荐使用 java.util.Objects#equals(JDK7引入的工具类)。 **

13. **【强制】**所有的相同类型的包装类对象之间值的比较，全部使用 equals 方法比较。 

    说明：对于 Integer var = ? 在-128 至 127 范围内的赋值， Integer对象是在 IntegerCache.cache产生，会复用已有对象， 这个区间内的 Integer 值可以直接使用==进行判断，但是这个区间之外的所有数据，都会在堆上产生，并不会复用已有对象， 这是一个大坑，推荐使用 equals 方法进行判断。 

14. 关于基本数据类型与包装数据类型的使用标准如下: 

    1. **【强制】**所有的 POJO 类属性必须使用包装数据类型。 
    2. **【强制】** RPC 方法的返回值和参数必须使用包装数据类型。 
    3. **【推荐】** 所有的局部变量使用基本数据类型。 

    说明：POJO 类属性没有初值是提醒使用者在需要使用时，必须 自己显式地进行赋值，任何 NPE 问题，或者入库检查，都由使 用者来保证。 

    正例:数据库的查询结果可能是 null，因为自动拆箱，用基本数据类型接收有 NPE 风险。 

    反例:比如显示成交总额涨跌情况，即正负 x%，x 为基本数据 类型，调用的 RPC 服务，调用不成功时，返回的是默认值，页 面显示为 0%，这是不合理的，应该显示成中划线。所以包装数 据类型的 null 值，能够表示额外的信息，如:远程调用失败，异 常退出。 

15. **【强制】**定义 DO/DTO/VO 等 POJO 类时，不要设定任何属性默认值。

    反例：POJO 类的 gmtCreate 默认值为 new Date();但是这个 属性在数据提取时并没有置入具体值，在更新其它字段时又附带 更新了此字段，导致创建时间被修改成当前时间。 

16. **【强制】**序列化类新增属性时， 请 不 要 修 改 serialVersionUID 字段，避免反序列失败;如果完全不兼容升级， 避免反序列化混乱，那么请修改 serialVersionUID 值。 

    说明：注意 serialVersionUID 不一致会抛出序列化运行时异常。 

17. 【强制】构造方法里面禁止加入任何业务逻辑，如果有初 始化逻辑，请放在 init 方法中。

18. 【强制】POJO 类必须写 toString 方法。使用 IDE 中的工 具:source> generate toString 时，如果继承了另一个 POJO 类，注意在前面加一下 super.toString。 说明:在方法执行抛出异常时，可以直接调用 POJO 的 toString() 方法打印其属性值，便于排查问题。 

19. 【推荐】使用索引访问用 String 的 split 方法得到的数组 时，需做最后一个分隔符后有无内容的检查，否则会有抛 IndexOutOfBoundsException 的风险。 

    说明：

    ````java
    String str = "a,b,c,,"; 
    String[] ary = str.split(",");
    // 预期大于 3，结果是 3
    System.out.println(ary.length);
    ````

    

20. 【推荐】类内方法定义顺序依次是:公有方法或保护方法 > 私有方法 > getter/setter 方法。

    说明:公有方法是类的调用者和维护者最关心的方法，首屏展示 最好;保护方法虽然只是子类关心，也可能是“模板设计模式” 下的核心方法;而私有方法外部一般不需要特别关心，是一个黑 盒实现;因为承载的信息价值较低，所有 Service 和 DAO 的 getter/setter 方法放在类体最后 

21. 【推荐】final 可以声明类、成员变量、方法、以及本地变 量，下列情况使用 final 关键字: 

    1)不允许被继承的类，如:String 类。 2)不允许修改引用的域对象，如:POJO 类的域变量。 3)不允许被重写的方法，如:POJO 类的 setter 方法。 

    4)不允许运行过程中重新赋值的局部变量。 5)避免上下文重复使用一个变量，使用 final 描述可以强 制重新定义一个变量，方便更好地进行重构

22. 【推荐】慎用 Object 的 clone 方法来拷贝对象。 说明:对象的 clone 方法默认是浅拷贝，若想实现深拷贝需要重 写 clone 方法实现属性对象的拷贝。

23. 【强制】关于 hashCode 和 equals 的处理，遵循如下规则: 

    1. 只要重写 equals，就必须重写 hashCode。

    2. 因为 Set 存储的是不重复的对象，依据 hashCode 和 equals 进行判断，所以 Set 存储的对象必须重写这两个方 法。 

    3. 如果自定义对象做为 Map 的键，那么必须重写 

       hashCode 和 equals。 

    说明：String重写了hashCode 和 equals 方法，所以我们可以非常愉快地使用String对象作为key来使用。 

24.  【强制】 ArrayList 的 subList 结果不可强转成 ArrayList， 否 则 会 抛 出 ClassCastException 异 常 ， 即 java.util.RandomAccessSubList cannot be cast to java.util.ArrayList. 

    说明:subList 返回的是 ArrayList 的内部类 SubList，并不是 ArrayList ，而是 ArrayList 的一个视图，对于 SubList 子列表 的所有操作最终会反映到原列表上。

25. 【强制】在 subList 场景中，高度注意对原集合元素个数的 修改，会导致子列表的遍历、增加、删除均会产生 ConcurrentModificationException 异常。 

26. 【强制】使用集合转数组的方法，必须使用集合的 toArray(T[] array)，传入的是类型完全一样的数组，大小就是 list.size()。 

    说明：使用 toArray 带参方法，入参分配的数组空间不够大时， toArray 方法内部将重新分配内存空间，并返回新数组地址;如果数组元素大于实际所需，下标为[ list.size() ]的数组元素将被 置为 null，其它数组元素保持原值，因此最好将方法入参数组大 小定义与集合元素个数一致。
    正例：

    ````java
    List<String> list = new ArrayList<String>(2);
    list.add("guan");
    list.add("bao");
    String[] array = new String[list.size()]; 
    array = list.toArray(array);
    ````

    反例：

    直接使用 toArray 无参方法存在问题，此方法返回值只能 是 Object[]类，若强转其它类型数组将出现 ClassCastException 错误

27. 【强制】使用工具类 Arrays.asList()把数组转换成集合时， 不能使用其修改集合相关的方法，它的 add/remove/clear 方法 会抛出 UnsupportedOperationException 异常。 

    说明:asList 的返回对象是一个 Arrays 内部类，并没有实现集 合的修改方法。Arrays.asList 体现的是适配器模式，只是转换接 口，后台的数据仍是数组。 

28. 

    

     

    