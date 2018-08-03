# Java 篇

### 1，删除链表指定节点

##### https://blog.csdn.net/u012572955/article/details/51279439

### 2，Java 浮点数的实际应用场景

问：请用 java 实现如下描述流程；你买了价值 1.1 元的东西，你给收银员 2.0 元钱，收银员找你 0.9 元？    

```
BigDecimal bd1 = new BigDecimal("2.0");  
BigDecimal bd2 = new BigDecimal("1.1");  
BigDecimal result=bd1.subtract(bd2);  

//BigDecimal  
BigDecimal b1 = new BigDecimal("1.34");//1.34   
BigDecimal b2 = BigDecimal.valueOf(1.34);//1.34   
BigDecimal one1 = new BigDecimal(1.34);//1.3400000000000000799360577730112709105014801025390625  
BigDecimal two1 = new BigDecimal("1.34");//1.34  

public BigDecimal add(BigDecimal value);//加法  
public BigDecimal subtract(BigDecimal value);//减法   
public BigDecimal multiply(BigDecimal value);//乘法  
public BigDecimal divide(BigDecimal value);//除法     

//compareTo方法  
//值相等但具有不同标度的两个BigDecimal对象（如，2.0 和 2.00）被认为是相等的。  
BigDecimal one = BigDecimal.valueOf(1);  
BigDecimal two = BigDecimal.valueOf(2);  
BigDecimal three = one.add(two);  
int i1 = one.compareTo(two);//-1  
int i2 = two.compareTo(two);//0  
int i3 = three.compareTo(two);//1
```

### 3，字符串

问：下面两行语句分别输出什么？  
String str1 = 'a' + 3 + "Hello";  
String str2 = "Hello" + 'a' + 3;  

str1 为 100Hello，str2 为 Helloa3 因为 java 中 char 字符型存放字符常量，底层使用 16 位无符号整型表示，所以对于 str1 运算时 'a' + 3 会被转换成 int 运算，然后进行字符串拼接；而 str2 两次都进行字符串拼接操作。  

### 4，简单说说 Java 中垃圾回收的方式有哪些？

##### https://mp.weixin.qq.com/s/Cb51NSvXs6lx31V2Q-9p5w

##### https://blog.csdn.net/bushanyantanzhe/article/details/79381148

### 5，数据库中的事务

##### https://blog.csdn.net/liduolp/article/details/48579155

### 6，try catch finally 执行顺序

###### https://www.cnblogs.com/superFish2016/p/6687549.html

### 7,简单说说 Java 中 sleep() 与 wait() 方法的区别？

sleep() 方法使当前线程进入停滞状态（阻塞当前线程），让出 CUP 的使用，目的是不让当前线程独自霸占该进程所获的 CPU 资源。该方法是 Thread 类的静态方法，当在一个 synchronized 块中调用 sleep() 方法时，线程虽然休眠了，但是其占用的锁并没有被释放；当 sleep() 休眠时间期满后，该线程不一定会立即执行，因为其它线程可能正在运行而且没有被调度为放弃执行，除非此线程具有更高的优先级。

wait() 方法是 Object 类的，当一个线程执行到 wait() 方法时就进入到一个和该对象相关的等待池中，同时释放对象的锁（对于 wait(long timeout) 方法来说是暂时释放锁，因为超时时间到后还需要返还对象锁），其他线程可以访问。wait() 使用 notify() 或 notifyAll() 或者指定睡眠时间来唤醒当前等待池中的线程。wait() 必须放在 synchronized 块中使用，否则会在运行时抛出 IllegalMonitorStateException 异常。  

由此可以看出它们之间的区别如下：  
1,sleep() 不释放同步锁，wait() 释放同步锁。  
2,sleep(milliseconds) 可以用时间指定来使他自动醒过来，如果时间没到则只能调用 interreput() 方法来强行打断（不建议，会抛出 InterruptedException），而 wait() 可以用 notify() 直接唤起。  
3,sleep() 是 Thread 的静态方法，而 wait() 是 Object 的方法。  
4,wait()、notify()、notifyAll() 方法只能在同步控制方法或者同步控制块里面使用，而 sleep() 方法可以在任何地方使用。  

### 8,简单说说 Java 中内存泄漏与内存溢出的区别？

这内存溢出（OutOfMemory）是指程序在申请内存时没有足够的内存空间供其使用。内存泄露（MemoryLeak）是指程序在申请内存后无法释放已申请的内存空间，一次内存泄露危害可以忽略，但内存泄露堆积后果很严重，无论多少内存迟早会被消耗尽，所以内存泄漏最终可能会导致内存溢出。

内存泄漏本身一般对业务逻辑不会产生什么危害，作为一般的用户在频次不高的情况下根本感觉不到内存泄漏的存在，真正有危害的是内存泄漏的堆积，这会最终消耗尽系统所有的内存，所以频次不高和占用内存不大的泄露一般都比较难以发现定位，如果需要定位分析内存泄漏可以采用一些第三方工具辅助，譬如 MAT 等。

内存溢出出现的原因一般比较多，譬如内存中一次加载的数据量过于庞大，启动参数内存值设定的过小，内存持续泄漏导致内存用光等。解决内存溢出可以通过修改 JVM 启动参数(-Xms/-Xmx 等，不过一般不建议)，检查分析代码找出庞大数据或者泄漏点。  

### 9，GC机制
[JVM GC 机制与性能优化](https://blog.csdn.net/antony9118/article/details/51375662)
### 10，Java反射
[Java反射](https://blog.csdn.net/feather_wch/article/details/78719833)
### 11，Java泛型
[java 泛型详解](https://blog.csdn.net/s10461/article/details/53941091/)
### 12，类加载机制，加载过程 
[类加载机制－类加载的时机、过程](https://blog.csdn.net/u012834750/article/details/70834735)
### 13，单链表添加具体实现
[java中单项链表实现方法:增加、删除、插入数据](https://blog.csdn.net/gg543012991/article/details/51030329)
### 14，进程与线程 
[进程与线程的一个简单解释](https://www.cnblogs.com/dreamroute/p/5207813.html)
### 15，Java并发面试题
[Java并发面试题](https://blog.csdn.net/u010796790/article/details/52194646)
### 16，为什么应该在循环中检查线程的等待条件
[wait必须放在while循环里面的原因探析](https://blog.csdn.net/qq_35181209/article/details/77362297)






