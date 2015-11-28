title: Java竞赛赛前复习(四)(多线程)
date: 2014-04-24 10:23
tags: [Java,竞赛前复习]
categories: 辅助攻击技能 #文章文类
---

用一个表格描述完需要描述的区别：

单线程 | 多线程
------------ | ------------- 
同步（等待） | 异步、同时，ajax（异步javascript以及xml）（如输入和验证是异步的）
不同时 | 同时
同一时间做一件事|同一时间做多件事
线程不安全（独享资源）|线程安全（资源同时被访问不会出现问题，共享资源）

---

<b>一、实现多线程</b>

-方法一：继承Thread类，重写run方法
![](/images/java4/1.png)
 
>会看到主线程、runner1交替输出，每次运行的结果都可能不一样，随机的交替的，看CPU时间片正在给谁。
Start()改了run()，也可以正常执行，但是是用独占的方式占用，不会交替。和顺序差不多了……

![](/images/java4/2.png)



-方法二：类A实现Runnable接口，A的实例做为Thread的构造方法参数，new Thread
![](/images/java4/3.png)

例题：
![](/images/java4/4.png)

-方法三：调用start()方法启动线程(这个都懂就不写了)

---

<b>二、Deamon线程（也叫：守护线程）</b>
![](/images/java4/5.png)

Thread类的方法，进行设置：
![](/images/java4/6.png)




比如一个main线程，输出3次，一个deamon线程，死循环输出
结果main三次后，deamon也停止了


---

<b>三、线程状态转换</b>
![](/images/java4/7.png)
不是说start()就立刻执行的，可能CPU在执行其他线程
要等待调度
有情况发生了，还会阻塞

---

<b>四、线程控制基本方法</b>
![不记得盗图自哪里的](/images/java4/8.png)


下面主要讲这三种方法：

![](/images/java4/9.png)

<b>（4.1）sleep方法：</b>

![](/images/java4/10.png)

注意：是静态方法！直接类名.方法名
![](/images/java4/11.png)
<br>

<b>（4.2）join方法：</b>
![](/images/java4/12.png)
![](/images/java4/13.png)
线程跑完了~再跑main（线程run合并到main中）

<br>
<b>（4.3）yield方法：</b>
![](/images/java4/14.png)

---

<b>五、线程的优先级</b>
![](/images/java4/15.png)
![](/images/java4/16.png)

---

<b>六、线程同步（类似我们OS中说的互斥）</b>

-发现问题：
![](/images/java4/17.png)
![](/images/java4/18.png)
 
第一个++后休息，回来变成了第二个
Num是静态的变量，本不应该有这种情况出现

-解决问题：第一个执行的时候，锁住当前对象
![](/images/java4/19.png)
或者：
![](/images/java4/20.png)






容易死锁!
->把锁的粒度加粗



![](/images/java4/21.png)





最后了！终于

= =，遇到这种题。。就算了吧
记得wait是要处理A那个异常的，notify不用处理异常
就算是处理完的，执行会报错：java.lang.IllegalMonitorStateException