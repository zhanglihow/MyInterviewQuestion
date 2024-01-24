# Android 篇

### 1，Android 事件的分发机制

https://blog.csdn.net/carson_ho/article/details/54136311

https://www.jianshu.com/p/e99b5e8bd67b

事件分发从Action_Down开始，最初由Activity的dispatchTouchEvent()方法接收，不拦截不中断的正常分发流程：Activity的disPatchTouchEvent()方法到PhoneWindow的superDispatchTouchEvent方法，再到DecorView的superDispatchTouchEvent方法，再到ViewGroup的dispatchTouchEvent方法，在ViewGroup的dispatchTouchEvent方法中判断是否拦截，若拦截调用ViewGroup的onTouchEvent方法，该ViewGroup消费掉；若不拦截，该ViewGroup遍历子View根据点击的位置等条件判断是否为接收事件的子View，是，则分发给该子View的dispatchTouchEvent()方法，然后会调用View的onTouchEvent方法，在onTouchEvent方法中会判断该子View是否可点击，是，则事件最终传递到View的onClick方法消费；否则，事件返回向上传递，直到消费或者终止。

在dispatchTouchEvent()方法中返回true或者false，事件不向下传递，只用调用super.dispatchTouchEvent方法，事件才会向下传递。
在onTouchEvent()方法中返回true，事件在该方法中消费，不会向下或者向上传递；返回super.onTouchEvent方法，将会调用ViewonTouchEvent方法，判断长按事件和点击事件的执行条件存不存在，存在则会在点击事件中消费。
在onInterceptTouchEvent()方法中返回true表示拦截事件，事件可能会在该ViewGroup中消费掉；返回false表示事件继续往下传递

当某个View的onTouchEvent()返回true，那么事件不会向下或者向上传递，而Action_MOVE和Action_UP事件将会在该View的onTouchEvent方法中处理

### 2，线性布局和相对布局特点？哪个高效？

https://www.jianshu.com/p/8a7d059da746

### 3，Handler机制

https://blog.csdn.net/garyhu1/article/details/54573548
### 4，SurfaceView与View 
[surfaceView和View的区别](https://www.cnblogs.com/dubo-/p/6638094.html)
### 5，Application生命周期 
[玩转Android Application的生命周期](https://www.jianshu.com/p/11654f7f0c4a)
### 6，自定义View里，onDraw详细优化 
[view ondraw性能优化](http://blog.sina.com.cn/s/blog_972577b30102vrp4.html)
### 7，SurfaceView替换方案 
[建议使用TextureView替代SurfaceView](https://blog.csdn.net/oDongFangZhiZi/article/details/73867785)
### 8，详细描述应用从点击桌面图标到首页Activity展示的流程
[一篇文章看明白 Android 从点击应用图标到界面显示的过程](https://blog.csdn.net/freekiteyu/article/details/79318031)
### 9，Fragment的懒加载实现，参数传递与保存 
[Fragment的懒加载实现](https://blog.csdn.net/ljcitworld/article/details/77528585)
### 10，ViewPager的缓存实现 
[ViewPager的缓存机制](http://www.cnblogs.com/Joanna-Yan/p/4824434.html)
### 11，子线程访问UI的验证与后果 
[难道子线程真的不能更新UI吗？能或不能，那又是为什么呢？](https://blog.csdn.net/u012534831/article/details/80124510)
### 12，主线程Looper.loop为什么不会造成死循环 
[Android中为什么主线程不会因为Looper.loop()里的死循环卡死？](https://www.zhihu.com/question/34652589)
### 13，Android内存优化与分析 
[Android Studio下的应用性能优化总结-内存优化](https://blog.csdn.net/y1258429182/article/details/51176424)
### 14，Glide加载长图，图片背景变色 
[解决使用Glide加载图片背景出现浅绿色](https://blog.csdn.net/sheilazxx/article/details/54584096)  
### 15，Activity的启动流程
[Android Activity的启动流程源码解析(8.0)](https://blog.csdn.net/pihailailou/article/details/78545391)
### 16，Android 从点击应用图标到界面显示的过程

![](https://img-blog.csdn.net/20180212172050357?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZnJlZWtpdGV5dQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

[Android 从点击应用图标到界面显示的过程](https://blog.csdn.net/freekiteyu/article/details/79318031)

### 17，RecyclerView与ListView的异同
[Android控件RecyclerView与ListView的异同](http://www.cnblogs.com/littlepanpc/p/4497290.html)
### 18，类的加载机制
[从Java到android：类的加载机制](https://blog.csdn.net/tubby_ting/article/details/54093475)

### 19，主线程中的Looper.loop()一直无限循环为什么不会造成ANR？
https://www.jianshu.com/p/cfe50b8b0a41
### 20，Activity四种启动模式
https://www.cnblogs.com/wanghaoyuhappy/p/5292419.html

### 21，Android种涉及到的设计模式
##### 1、适配器模式：ListView或GridView的Adapter
简介：不同的数据提供者使用一个适配器来向一个相同的客户提供服务。
##### 2、建造者模式：AlertDialog.Builder
简介：可以分步地构造每一部分。
##### 3、命令模式：Handler.post后Handler.handleMessage
简介：把请求封装成一个对象发送出去，方便定制、排队、取消。
##### 4、享元模式：Message.obtainMessage通过重用Message对象来避免大量的Message对象被频繁的创建和销毁。
简介：运用共享技术有效地支持大量细粒度的对象。
##### 5、迭代器模式：如通过Hashtable.elements方法可以得到一个Enumeration，然后通过这个Enumeration访问Hashtable中的数据，而不用关心Hashtable中的数据存放方式。
简介：提供一个方法顺序访问数据集合中的所有数据而又不暴露对象的内部表示。
##### 6、备忘录模式：Activity的onSaveInstanceState和onRestoreInstanceState就是通过Bundle这种序列化的数据结构来存储Activity的状态，至于其中存储的数据结构，这两个方法不用关心
简介：不需要了解对象的内部结构的情况下备份对象的状态，方便以后恢复。
##### 7、观察者模式：我们可以通过BaseAdapter.registerDataSetObserver和BaseAdapter.unregisterDataSetObserver两方法来向BaseAdater注册、注销一个DataSetObserver。这个过程中，DataSetObserver就是一个观察者，它一旦发现BaseAdapter内部数据有变量，就会通过回调方法DataSetObserver.onChanged和DataSetObserver.onInvalidated来通知DataSetObserver的实现类。事件通知也是观察者模式
简介：一个对象发生改变时，所有信赖于它的对象自动做相应改变。
##### 8、原型模式：比如我们需要一张Bitmap的几种不同格式：ARGB_8888、RGB_565、ARGB_4444、ALAPHA_8等。那我们就可以先创建一个ARGB_8888的Bitmap作为原型，在它的基础上，通过调用Bitmap.copy(Config)来创建出其它几种格式的Bitmap。另外一个例子就是Java中所有对象都有的一个名字叫clone的方法，已经原型模式的代名词了
简介：在系统中要创建大量的对象，这些对象之间具有几乎完全相同的功能，只是在细节上有一点儿差别。
##### 9、代理模式：类似于ios开发的delegate委托模式，所有的AIDL都一个代理模式的例子。假设一个Activity A去绑定一个Service S，那么A调用S中的每一个方法其实都是通过系统的Binder机制的中转，然后调用S中的对应方法来做到的。Binder机制就起到了代理的作用。
简介：为其他对象提供一种代理以控制对这个对象的访问。
##### 10、状态模式：View.onVisibilityChanged方法，就是提供了一个状态模式的实现，允许在View的visibility发生改变时，引发执行onVisibilityChanged方法中的动作。
简介：状态发生改变时，行为改变。
##### 11、策略模式：
举例：Java.util.List就是定义了一个增（add）、删（remove）、改（set）、查（indexOf）策略，至于实现这个策略的ArrayList、LinkedList等类，只是在具体实现时采用了不同的算法。但因为它们策略一样，不考虑速度的情况下，使用时完全可以互相替换使用。
简介：定义了一系列封装了算法、行为的对象，他们可以相互替换。
##### 12、调解者模式
简介：一个对象的某个操作需要调用N个对象的M个方法来完成时，把这些调用过程封装起来，就成了一个调解者
举例：如Resource.getDrawable方法的实现逻辑是这样的：创建一个缓存来存放所有已经加载过的，如果getDrawable中传入的id所对应的Drawable以前没有被加载过，那么它就会根据id所对应的资源类型，分别调用XML解析器生成，或者通过读取包中的图片资源文件来创建Drawable。
而Resource.getDrawable把涉及到多个对象、多个逻辑的操作封装成一个方法，就实现了一个调解者的角色。
##### 13、抽象工厂模式
DAO与Service的使用

### 22，Android中的线程和线程池

##### FixedThreadPool 
只有核心线程，没有非核心线程，线程数固定，即使线程处于闲置状态，也不会被回收，除非线程池被关闭。

##### CachedThreadPool
线程数目不固定，只有非核心线程，没有核心线程，线程池中有超时机制。
适合处理大量且耗时较少的任务。

##### ScheduleThreadPool
核心线程固定，非核心线程不固定，非核心线程处于闲置状态就会被回收。
适合执行定时任务和固定周期的重复任务。

##### SingleThreadExecutor
只有一个核心线程，不需要考虑线程同步问题。

https://www.cnblogs.com/huangjialin/p/8546513.html

 

### 23，Android各版本大致的差异

https://blog.csdn.net/s13383754499/article/details/82736912

### 24，自定义View及View的绘制流程

https://www.cnblogs.com/CVstyle/p/6399188.html

### 25 JetPack 有哪些
https://www.jianshu.com/p/4f3e0ed71fb6

