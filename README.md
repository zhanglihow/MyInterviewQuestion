# 我的面试题总结
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
##### https://blog.csdn.net/guoxiaojie_415/article/details/49226045

### 6，删除链表指定节点
##### https://blog.csdn.net/u012572955/article/details/51279439

### 7，Handler机制
##### https://blog.csdn.net/garyhu1/article/details/54573548/

### 8，Java 浮点数在实际应用场景中踩坑题目解析
问：请用 java 实现如下描述流程；你买了价值 1.1 元的东西，你给收银员 2.0 元钱，收银员找你 0.9 元？    

BigDecimal bd1 = new BigDecimal("2.0");  
BigDecimal bd2 = new BigDecimal("1.1");  
BigDecimal result=bd1.subtract(bd2);  

#### BigDecimal  
BigDecimal b1 = new BigDecimal("1.34");//1.34   
BigDecimal b2 = BigDecimal.valueOf(1.34);//1.34   
BigDecimal one1 = new BigDecimal(1.34);//1.3400000000000000799360577730112709105014801025390625  
BigDecimal two1 = new BigDecimal("1.34");//1.34  

public BigDecimal add(BigDecimal value);//加法  
public BigDecimal subtract(BigDecimal value);//减法   
public BigDecimal multiply(BigDecimal value);//乘法  
public BigDecimal divide(BigDecimal value);//除法     

compareTo方法  
值相等但具有不同标度的两个BigDecimal对象（如，2.0 和 2.00）被认为是相等的。  
BigDecimal one = BigDecimal.valueOf(1);  
BigDecimal two = BigDecimal.valueOf(2);  
BigDecimal three = one.add(two);  
int i1 = one.compareTo(two);//-1  
int i2 = two.compareTo(two);//0  
int i3 = three.compareTo(two);//1

### 9，字符串
问：下面两行语句分别输出什么？  
String str1 = 'a' + 3 + "Hello";  
String str2 = "Hello" + 'a' + 3;  

str1 为 100Hello，str2 为 Helloa3 因为 java 中 char 字符型存放字符常量，底层使用 16 位无符号整型表示，所以对于 str1 运算时 'a' + 3 会被转换成 int 运算，然后进行字符串拼接；而 str2 两次都进行字符串拼接操作。


