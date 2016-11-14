title: Java竞赛赛前复习(三)(基础语法篇下)
date: 2014-04-24 10:22
tags: [Java,竞赛前复习]
categories: 辅助攻击技能
description: Java有什么基础语法的呢？看本文就知道啦～
---


<b>运算符：</b>

![注意那些不常用的](/images/java3/图片1.png)


---

<b>数组初始化：</b>
对：
```
int[] i =new int[3];  //数组是对象  
int[] i2 = new int[]{1,3,5}; //给了初值
int[] i3 = {3,3,3,2};
int[] i4 = new int[2];
```
不对：
```
int[] i4 = new int[2]{3,5}; //后面给了初值，那中括号中的长度不给写  
int[2] i4 = new int[]; //长度要写后面
```

---

<b>访问权限：</b>

![记住权限](/images/java3/图片2.png)

</br>
![](/images/java3/图片3.png)

答案：C

---

<b>I/O流：</b>

![](/images/java3/图片4.png)

>Input – read
>Output – write

</br>
</br>

<b>字节流：</b>
FileInputStream  FileOutputStream
</br>
</br>
<b>字符流：</b>
FileReader      FileWriter 
不够好用，改成了包装类：
</br>
BufferedReader 
![](/images/java3/图片5.png)
BufferedWriter ：
![](/images/java3/图片6.png)
![](/images/java3/图片7.png)

</br>
</br>

<b>I / O例题：</b>

1：
![](/images/java3/图片8.png)

Separator：看OS
答案：AB

2.
![](/images/java3/图片10.png) 

可以查它们的父类，看共同的方法
ABC都有
D没有：
	在输入流里面才有mark，输出流都没有
![](/images/java3/图片11.png)
选E

---

<b>序列化</b>

![](/images/java3/图片12.png)

>ObjectOutputStream （处理流）将 Java 对象的基本数据类型和图形写入 OutputStream（输出流）。
>只能将支持 java.io.Serializable 接口的对象写入流中。
>必须使用与写入对象时相同的类型和顺序从相应 ObjectInputstream 中读回对象。
>一个类序列化：类里面的所有属性（对象），都要序列化

![](/images/java3/图片13.png)
选B

</BR>
>序列化（也有叫串行化）：
>	序列化就是一种用来处理对象流的机制，所谓对象流也就是将对象的内容进行流化。可以对流化后的对象进行读写操作，也可将流化后的对象传输于网络之间。序列化是为了解决在对对象流进行读写操作时所引发的问题。
>序列化的实现：将需要被序列化的类实现Serializable接口，然后使用一个输出流(如：FileOutputStream)来构造一个ObjectOutputStream(对象流)对象，接着，使用ObjectOutputStream对象的writeObject(Object obj)方法就可以将参数为obj的对象写出(即保存其状态)，要恢复的话则用输入流。

</BR>

>串行化的特点：

 >   （1）如果某个类能够被串行化，其子类也可以被串行化。如果该类有父类，则分两种情况来考虑，如果该父类已经实现了可串行化接口。则其父类的相应字段及属性的处理和该类相同；如果该类的父类没有实现可串行化接口，则该类的父类所有的字段属性将不会串行化。
如果父类没有实现串行化接口，则其必须有默认的构造函数（即没有参数的构造函数）。否则编译的时候就会报错。在反串行化的时候，默认构造函数会被调用。但是若把父类标记为可以串行化，则在反串行化的时候，其默认构造函数不会被调用。这是为什么呢？这是因为Java 对串行化的对象进行反串行化的时候，直接从流里获取其对象数据来生成一个对象实例，而不是通过其构造函数来完成。

>  （2）声明为static和transient类型的成员数据不能被串行化。因为static代表类的状态， transient代表对象的临时数据；

>  （3）相关的类和接口：在java.io包中提供的涉及对象的串行化的类与接口有ObjectOutput接口、ObjectOutputStream类、ObjectInput接口、ObjectInputStream类。


参考博文：http://blog.csdn.net/yakihappy/article/details/3979373


---

输入输出：
![](/images/java3/图片14.png)

用法：
![](/images/java3/图片15.png)
![](/images/java3/图片16.png)

%.1f 是会四舍五入的

![](/images/java3/图片17.png)