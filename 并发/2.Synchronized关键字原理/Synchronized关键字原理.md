# Synchronized关键字原理

````java
/**
	叫号的代码
**/
public class TicketRobot implements Runnable {

    private static int index = 1;

    private static  final int max = 500;

    @Override
    public void run() {
        synchronized (this) {
            while (index <= max) {
                System.out.println(Thread.currentThread().getName() + "叫号：" + (index++));
            }
        }
    }

    public static void main(String[] args) {
        Thread t1 = new Thread(new TicketRobot());
        Thread t2 = new Thread(new TicketRobot());
        Thread t3 = new Thread(new TicketRobot());
        Thread t4 = new Thread(new TicketRobot());

        t1.start();
        t2.start();
        t3.start();
        t4.start();
    }
}
````

## 一、概念

是利用锁的机制来实现同步的。

锁机制有如下两种特性：

+ **互斥性**：即在同一时间只允许一个线程持有某个对象锁，通过这种特性来实现多线程中的协调机制，这样在同一时间只有一个线程对需同步的代码块（复合操作）进行访问。互斥性我们也往往称为操作的原子性。
+ **可见性**：必须确保在锁被释放之前，对共享变量所做的修改，对于随后获得该锁的另一个线程是可见的（即在获得锁时应获得最新共享变量的值），否则另一个线程可能是在本地缓存的某个副本上继续操作从而引起不一致。

## 二、synchronized的用法

````java
public class SysDemo1 {
    public static void main(String[] args) {
        SysDemo1 sysDemo1 = new SysDemo1();
        for (int i = 0; i < 5; i++) {
            new Thread(sysDemo1::accessResources1).start();
        }
    }

    /**
     * 修饰静态方法
     */
    public static synchronized void accessResources() {
        try {
            // 停留两秒钟
            TimeUnit.SECONDS.sleep(2);
            System.out.println(Thread.currentThread().getName() + "is Running");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    /**
     * 修饰非静态方法
     */
    public  synchronized void accessResources1() {
        try {
            TimeUnit.SECONDS.sleep(2);
            System.out.println(Thread.currentThread().getName() + "is Running");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    // 代码块1（对象） this指的是当前的对象
    public void accessResources2() {
        synchronized (this) {
            try {
                TimeUnit.SECONDS.sleep(2);
                System.out.println(Thread.currentThread().getName() + "is Running");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    // 代码块(修饰对象的是class类)
    public void accessResources3() {
        synchronized (SysDemo1.class) {
            // 有Class对应的所有的对象都共同使用这一个锁
            try {
                TimeUnit.SECONDS.sleep(2);
                System.out.println(Thread.currentThread().getName() + "is Running");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
````

根据修饰对象分类：

1. 同步方法

   + 同步非静态方法

     `Pubulic synchronized void methodName() {}`

   + 同步静态方法

     `Pubulic synchronized static void methodName() {}`

2. 同步代码块

   `synchronized(this | object) {}`

   `synchronized(类.class) {}`

   根据获取的锁分类

   + 获取对象锁

     synchronized(this | object) {}

     修饰非静态方法

     在Java中，每个对象都会有一个monitor对象，这个对象其实就是Java对象的锁，通常会被称为“内置锁” 或 “对象锁”。类的对象可以有多个，所以每个独享有其独立的对象锁，互不干扰。

   + 获取类锁

     synchronized(类.class){}

     修饰静态方法

     在Java中，针对每个类也有一个锁，可以称为“类锁”，类锁实际上是通过对象锁实现的，即类的Class对象锁，每个类只有一个Class对象，所以每一个类只有一个类锁。

   在Java中，每个对象都会有一个monitor对象，监视器

   + 某一个线程占有这个对象的时候，先查看monitor的计数器是不是0，如果是0还没有线程占有，这个时候线程占有这个对象，并且对这个对象的monitor+1，如果不为0，表示这个线程已经被其他线程占有，这个线程等待。当线程释放占有权的时候，monitor-1；

