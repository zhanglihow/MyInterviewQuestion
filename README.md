# 面试题总结
### 1，HTTPS和HTTP有什么区别，到底安全在哪里？
##### https://www.jianshu.com/p/be7a20cc8468  

### 2，Tcp三次握手
##### https://github.com/jawil/blog/issues/14  

### 3，Android View 的分发机制
##### https://blog.csdn.net/carson_ho/article/details/54136311
##### https://www.jianshu.com/p/e99b5e8bd67b

### 4，线性布局和相对布局特点？哪个高效？
##### https://www.jianshu.com/p/8a7d059da746

### 5，一个整数转换为二进制后，1的个数
``` 
public int countA(int n){  
   int res = 0;  
   while(n != 0){  
       n &= (n - 1);  
       res++;  
   }  
   return res;
} 
```

### 6，删除链表指定节点
##### https://blog.csdn.net/u012572955/article/details/51279439

### 7，Handler机制
##### https://blog.csdn.net/garyhu1/article/details/54573548/

### 8，Java 浮点数的实际应用场景
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
### 9，字符串
问：下面两行语句分别输出什么？  
String str1 = 'a' + 3 + "Hello";  
String str2 = "Hello" + 'a' + 3;  

str1 为 100Hello，str2 为 Helloa3 因为 java 中 char 字符型存放字符常量，底层使用 16 位无符号整型表示，所以对于 str1 运算时 'a' + 3 会被转换成 int 运算，然后进行字符串拼接；而 str2 两次都进行字符串拼接操作。  

### 10，Http Get 和 Post 这两者有什么区别？
传输形式的区别：  
1，通过Get方法发起请求时，会将请求参数拼接在request-url尾部，格式是url?param1=xxx&param2=xxx&[…]。  
2，http协议并没有对url长度做限制，但是一些浏览器和服务器可能会有限制，所以通过GET方法发起的请求参数不能够太长。而通过POST方法发起的请求是将参数放在请求体中的，所以不会有GET参数的这些问题。  
方法本身的语义：  
GET方法通常是指从服务器获取某个URL资源，其行为可以看作是一个读操作，对同一个URL进行多次GET并不会对服务器产生什么影响。而POST方法通常是对某个URL进行添加、修改，例如一个表单提交，通常会往服务器插入一条记录。多次POST请求可能导致服务器的数据库中添加了多条记录。    

##### https://sunshinevvv.coding.me/blog/2017/02/09/HttpGETv.s.POST/  
  
### 11，OkHttp缓存大致的流程  
1，从接收到的请求中，解析出Url和各个首部。  
2，查询本地是否有缓存副本可以使用。  
3，如果有缓存，则进行新鲜度检测，如果缓存足够新鲜，则使用缓存作为响应返回，如果不够新鲜了，则构造条件请求，发往服务器再验证。如果没有缓存，就直接将请求发往服务器。  
4，把从服务器返回的响应，更新或是新增到缓存中。  
  
### 12，简单说说 Java 中垃圾回收的方式有哪些？
##### https://mp.weixin.qq.com/s/Cb51NSvXs6lx31V2Q-9p5w
##### https://blog.csdn.net/bushanyantanzhe/article/details/79381148  
  
### 13，数据库中的事务
##### https://blog.csdn.net/liduolp/article/details/48579155  

### 14，try catch finally 执行顺序
###### https://www.cnblogs.com/superFish2016/p/6687549.html  

### 15,简单说说 Java 中 sleep() 与 wait() 方法的区别？
sleep() 方法使当前线程进入停滞状态（阻塞当前线程），让出 CUP 的使用，目的是不让当前线程独自霸占该进程所获的 CPU 资源。该方法是 Thread 类的静态方法，当在一个 synchronized 块中调用 sleep() 方法时，线程虽然休眠了，但是其占用的锁并没有被释放；当 sleep() 休眠时间期满后，该线程不一定会立即执行，因为其它线程可能正在运行而且没有被调度为放弃执行，除非此线程具有更高的优先级。

wait() 方法是 Object 类的，当一个线程执行到 wait() 方法时就进入到一个和该对象相关的等待池中，同时释放对象的锁（对于 wait(long timeout) 方法来说是暂时释放锁，因为超时时间到后还需要返还对象锁），其他线程可以访问。wait() 使用 notify() 或 notifyAll() 或者指定睡眠时间来唤醒当前等待池中的线程。wait() 必须放在 synchronized 块中使用，否则会在运行时抛出 IllegalMonitorStateException 异常。  

由此可以看出它们之间的区别如下：  
1,sleep() 不释放同步锁，wait() 释放同步锁。  
2,sleep(milliseconds) 可以用时间指定来使他自动醒过来，如果时间没到则只能调用 interreput() 方法来强行打断（不建议，会抛出 InterruptedException），而 wait() 可以用 notify() 直接唤起。  
3,sleep() 是 Thread 的静态方法，而 wait() 是 Object 的方法。  
4,wait()、notify()、notifyAll() 方法只能在同步控制方法或者同步控制块里面使用，而 sleep() 方法可以在任何地方使用。  

### 16,简单说说 Java 中内存泄漏与内存溢出的区别？
这内存溢出（OutOfMemory）是指程序在申请内存时没有足够的内存空间供其使用。内存泄露（MemoryLeak）是指程序在申请内存后无法释放已申请的内存空间，一次内存泄露危害可以忽略，但内存泄露堆积后果很严重，无论多少内存迟早会被消耗尽，所以内存泄漏最终可能会导致内存溢出。

内存泄漏本身一般对业务逻辑不会产生什么危害，作为一般的用户在频次不高的情况下根本感觉不到内存泄漏的存在，真正有危害的是内存泄漏的堆积，这会最终消耗尽系统所有的内存，所以频次不高和占用内存不大的泄露一般都比较难以发现定位，如果需要定位分析内存泄漏可以采用一些第三方工具辅助，譬如 MAT 等。

内存溢出出现的原因一般比较多，譬如内存中一次加载的数据量过于庞大，启动参数内存值设定的过小，内存持续泄漏导致内存用光等。解决内存溢出可以通过修改 JVM 启动参数(-Xms/-Xmx 等，不过一般不建议)，检查分析代码找出庞大数据或者泄漏点。  
    
### 17,给定一个整数，请写一个函数判断该整数的奇偶性
二进制中如果 一个数是偶数那么最后一个一定是 0 如果一个数是奇数那么最后一位一定是 1；而十进制 1 在 8 位二进制中表示为 0000 0001，我们只需将一个数个 1相与（&） 得到的结果如果是 1 则表示该数为奇数，否知为偶数。
```
public boolean isOdd(int num){
    return num & 1 != 0;
}
```
### 18,同样给定一个整数，请写一个函数判断该整数是不是2的整数次幂
一个二进制如果表示为 0..0100…0，那么它减去1得到的数二进制表示肯定是 0..0011..1 的形式。那么这个数与自自己减一后的数相与得到结果肯定为0。
```
8   0000 1000      7   0000 0111
7 & 0000 0111      6 & 0000 0110
-------------      -------------
0   0000 0000      6   0000 0110

public boolean log2(int num){
   return (num & (num - 1)) == 0;
}
```
### 19,在其他数都出现两次的数组中找到只出现一次的那个数  
首先我们应该知道二进制异或操作，异或结果是二进制中两个位相同为0，相异为1。因此可以有个规律：  
```
任何整数 n 与 0 异或总等于其本身 n，一个数与其本身异或那么结果肯定是 0。
```
假设有这么一个序列： C B D A A B C 其中只有 D 出现一次，那么因为异或满足交换律和结合律，所以我们遍历异或此序列的过程等价于  
```
eO ^ (A ^ A ^ B ^ B ^ C ^ C ) ^ D = eO ^ 0 ^ D = D
```
所以对于任何排列的数组，如果只有一个数只出现了奇数次，其他的数都出现了欧数次，那么最终异或的结果肯定为出现奇数次的那个数。  
```
public int oddTimesNum(int[] arr) {
   int eO = 0;
   for (int cur : arr) {
       eO = eO ^ cur;
   }

   return eO;
}
```
### 20,在其他数都出现两次的数组中找到只出现一次的那两个数
```
public void printOddTimesNum(int[] arr) {
   int eO = 0;
   int eOhasOne = 0;

   for (int cur : arr) {
       eO = eO ^ cur;
   }

   int rightOne = eO & (~eO + 1);
   for (int cur : arr) {
       if ((rightOne & cur) != 0) {
           eOhasOne = eOhasOne ^ cur;
       }
   }

   System.out.println("eOhasOne = " + eOhasOne + "  " + (eOhasOne ^ eO));
}
```





